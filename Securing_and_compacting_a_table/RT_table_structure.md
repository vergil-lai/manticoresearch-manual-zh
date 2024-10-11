# Real-time table structure

A plain table can be created from an external source using a special tool called `indexer`, which reads a "recipe" from the configuration, connects to the data sources, pulls documents, and builds table files. This is a lengthy process. If your data changes, the table becomes outdated, and you need to rebuild it from the refreshed sources. If your data changes incrementally, such as a blog or newsfeed where old documents never change and only new ones are added, the rebuild will take more and more time, as you will need to process the archive sources again and again with each pass.

One way to deal with this problem is by using several tables instead of one solid table. For example, you can process sources produced in previous years and save the table. Then, take only sources from the current year and put them into a separate table, rebuilding it as often as necessary. You can then place both tables as parts of a distributed table and use it for querying. The point here is that each time you rebuild, you only process data from the last 12 months at most, and the table with older data remains untouched without needing to be rebuilt. You can go further and divide the last 12 months table into monthly, weekly, or daily tables, and so on.

This approach works, but you need to maintain your distributed table manually. That is, add new chunks, delete old ones, and keep the overall number of partial tables not too large (with too many tables, searching can become slower, and the OS usually limits the number of simultaneously opened files). To deal with this, you can manually merge several tables together by running [indexer --merge](../Data_creation_and_modification/Adding_data_from_external_storages/Adding_data_to_tables/Merging_tables.md). However, that only solves the problem of having many tables, making maintenance more challenging. And even with 'per-hour' reindexing, you will most likely have a noticeable time gap between new data arriving in sources and rebuilding the table, which populates this data for searching.

A real-time table is designed to solve this problem. It consists of two parts:

1. A special RAM-based table (called RAM chunk) that contains portions of data arriving right now.
2. A collection of plain tables called disk chunks that were built in the past.

This is very similar to a standard [distributed table](../Creating_a_table/Creating_a_distributed_table/Creating_a_distributed_table.md), made from several local tables.

You don't need to build such a table by running `indexer`,  which reads a "recipe" from the config and tables data sources. Instead, the real-time table provides the ability to 'insert' new documents and 'replace' existing ones. When executing the 'insert' command, you push new documents to the server. It then builds a small table from the added documents and immediately brings it online. So, right after the 'insert' command completes, you can perform searches in all table parts, including the just-added documents.

The search server automatically maintains the table, so you don't have to worry about it. However, you might be interested in learning a few details about 'how it is maintained'.

**First, since indexed data is stored in RAM - what about emergency power-off?** Will I lose my table then? Well, before completion, the server saves new data into a special 'binlog'. This consists of one or several files, living on your persistent storage, which incrementally grows as you add more and more changes. You can adjust the behavior regarding how often new queries (or transactions) are stored in the binlog, and how often the 'sync' command is executed over the binlog file to force the OS to actually save the data on a safe storage. The most paranoid approach is to flush and sync after every transaction. This is the slowest but also the safest method. The least expensive way is to switch off the binlog entirely. This is the fastest method, but you risk losing your indexed data. Intermediate variants, like flush/sync every second, are also provided.

The binlog is designed specifically for sequential saving of newly arriving transactions; it is not a table and cannot be searched over. It is merely an insurance policy to ensure that the server will not lose your data. If a sudden disruption occurs and everything crashes due to a software or hardware problem, the server will load the freshest available dump of the RAM chunk and then replay the binlog, repeating stored transactions. Ultimately, it will achieve the same state as it was in at the moment of the last change.

**Second, what about limits?** What if I want to process, say, 10TB of data, but it just doesn't fit into RAM! RAM for a real-time table is limited and can be configured. When a certain amount of data is indexed, the server manages the RAM part of the table by merging together small transactions, keeping their number and overall size small. This process can sometimes cause delays during insertion, however. When merging no longer helps, and new insertions hit the [RAM limit](../Creating_a_table/Local_tables/Plain_and_real-time_table_settings.md#rt_mem_limit), the server converts the RAM-based table into a plain table stored on disk (called a disk chunk). This table is added to the collection of tables in the second part of the RT table and becomes accessible online. The RAM is then flushed, and the space is deallocated.

When the data from RAM is securely saved to disk, which occurs:

* when the server saves the collected data as a disk table
* or when it dumps the RAM part during a clean shutdown or by [manual flushing](../Securing_and_compacting_a_table/Flushing_RAM_chunk_to_disk.md#FLUSH-TABLE)

the binlog for that table is no longer necessary. So, it gets discarded. If all the tables are saved, the binlog will be deleted.

**Third, what about disk collection?**  If having many disk parts makes searching slower, what's the difference if I make them manually in the distributed table manner, or they're produced as disk parts (or, 'chunks') by an RT table? Well, in both cases, you can merge several tables into one. For example, you can merge hourly tables from yesterday and keep one 'daily' table for yesterday instead. With manual maintenance, you have to think about the schema and commands yourself. With an RT table, the server provides the [OPTIMIZE](../Securing_and_compacting_a_table/Compacting_a_table.md#OPTIMIZE-TABLE) command, which does the same, but keeps you away from unnecessary internal details.

**Fourth, if my "document" constitutes a 'mini-table' and I don't need it anymore, I can just throw it away. But if it is 'optimized', i.e. mixed together with tons of other documents, how can I undo or delete it?** Yes, indexed documents are 'mixed' together, and there is no easy way to delete one without rebuilding the whole table. And if for plain tables rebuilding or merging is just a normal way of maintenance, for a real-time table it keeps only the simplicity of manipulation, but not 'real-timeness'. To address the problem, Manticore uses a trick: when you delete a document, identified by document ID, the server just tracks the number. Together with other deleted documents, their IDs are saved in a so-called [kill-list](../Data_creation_and_modification/Adding_data_from_external_storages/Adding_data_to_tables/Killlist_in_plain_tables.md#Table-kill-list). When you search over the table, the server first retrieves all matching documents, and then throws out the documents that are found in the kill-list (that is the most basic description; in fact, internally it's more complex). The point is - for the sake of 'immediate' deletion, documents are not actually deleted, but are just marked as 'deleted'. They still occupy space in different table structures, being essentially garbage. Word statistics, which affect ranking, also aren't affected, meaning it works exactly as it is declared: we search among all documents, and then just hide ones marked as deleted from the final result. When a document is [replaced](../Data_creation_and_modification/Updating_documents/REPLACE.md), it means that it is killed in the old parts of the table and is inserted again in the freshest part. All consequences of 'hiding by killlist' are also in play in this case.

When a rebuild of some part of a table happens, e.g., when some transactions (segments) of a RAM chunk are merged, or when a RAM chunk is converted into a disk chunk, or when two disk chunks are merged together, the server performs a comprehensive iteration over the affected parts and physically excludes deleted documents from all of them. That is, if they were in document lists of some words - they are wiped away. If it was a unique word - it gets removed completely.

As a summary: the deletion works in two phases:
1. First, we mark documents as 'deleted' in real-time and suppress them in search results.
2. During some operation with an RT table chunk, we finally physically wipe the deleted documents for good.

**Fifth, if an RT table contains plain disk tables in its collection, can I just add my ready old disk table to it?** No. It's not possible to avoid unneeded complexity and prevent accidental corruption. However, if your RT table has just been created and contains no data, then you can [ATTACH TABLE](../Data_creation_and_modification/Adding_data_from_external_storages/Adding_data_to_tables/Attaching_one_table_to_another.md) your disk table to it. Your old table will be moved inside the RT table and will become its part.

As a summary about the RT table structure: it is a cleverly organized collection of plain disk tables with a fast in-memory table, intended for real-time insertions and semi-real-time deletions of documents. The RT table has a common schema, common settings, and can be easily maintained without deep digging into details. 
<!-- proofread -->