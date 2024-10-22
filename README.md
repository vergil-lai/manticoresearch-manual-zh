# Manticore Search 中文文档

## 介绍

- [官网](https://manticoresearch.com/)
- [Github](https://github.com/manticoresoftware/manticoresearch)

**❗阅读最新的 [Manticore 与 Elasticsearch 对比](https://manticoresearch.com/blog/manticore-alternative-to-elasticsearch/) 博文❗**

Manticore Search 是一个易于使用的开源快速搜索数据库，是 Elasticsearch 的一个很好的替代方案。它与其他解决方案的区别在于：

- 它非常快速，因此比其他替代方案更具成本效益。例如，Manticore 比其他解决方案更具优势：
  - 对于[小数据](https://db-benchmarks.com/test-hn-small/#mysql-vs-manticore-search) Manticore 比 MySQL **快 182 倍** ([可复现](https://github.com/db-benchmarks/db-benchmarks#get-started)❗)
  - 对于[日志分析](https://db-benchmarks.com/test-logs10m/#elasticsearch-with-no-tuning-vs-manticore-search-default-row-wise-storage) Manticore 比 Elasticsearch **快 29 倍** ([可复现](https://github.com/db-benchmarks/db-benchmarks#get-started)❗)
  - 对于[小型数据集](https://db-benchmarks.com/test-hn-small/#manticore-search-vs-elasticsearch) Manticore 比 Elasticsearch **快 15 倍** ([可复现](https://github.com/db-benchmarks/db-benchmarks#get-started)❗)
  - 对于[中等规模数据](https://db-benchmarks.com/test-hn/#manticore-search-columnar-storage-vs-elasticsearch) Manticore 比 Elasticsearch **快 5 倍** ([可复现](https://github.com/db-benchmarks/db-benchmarks#get-started)❗)
  - 对于[大数据](https://db-benchmarks.com/test-taxi/#manticore-search-vs-elasticsearch) Manticore 比 Elasticsearch **快 4 倍** ([可复现](https://github.com/db-benchmarks/db-benchmarks#get-started)❗)
  - 在单台服务器上，Manticore 的最大吞吐量可比 Elasticsearch 高出 **2 倍** ([可复现](https://manticoresearch.com/blog/manticore-alternative-to-elasticsearch/#data-ingestion-performance)❗)
- 由于其现代的多线程架构和高效的查询并行化能力，Manticore 能够充分利用所有 CPU 核心，实现最快的响应时间。
- 强大且快速的全文搜索可无缝处理小型和大型数据集。
- 针对小型、中型和大型数据集的行式存储。
- 对于更大的数据集，Manticore 通过 [Manticore Columnar Library](https://github.com/manticoresoftware/columnar/) 提供列式存储支持，能够处理无法放入内存的数据集。
- 自动创建高效的二级索引，节省时间和精力。
- 基于成本的查询优化器优化查询，以实现最佳性能。
- Manticore 以 SQL 为主，使用 SQL 作为其原生语法，并提供与 MySQL 协议的兼容性，允许您使用您喜欢的 MySQL 客户端。
- 提供 [PHP](https://github.com/manticoresoftware/manticoresearch-php)、[Python](https://github.com/manticoresoftware/manticoresearch-python)、[JavaScript](https://github.com/manticoresoftware/manticoresearch-javascript)、[Typescript](https://github.com/manticoresoftware/manticoresearch-typescript)、[Java](https://github.com/manticoresoftware/manticoresearch-java)、[Elixir](https://github.com/manticoresoftware/manticoresearch-elixir) 和 [Go](https://github.com/manticoresoftware/manticoresearch-go) 客户端，集成变得更加轻松。
- Manticore 还提供了一个程序化的 HTTP JSON 协议，用于更灵活的数据和架构管理。
- 由 C++ 构建的 Manticore Search 启动快速，内存占用极少，底层优化使其性能表现出色。
- 支持实时插入，新增文档可以立即访问。
- 通过 [互动课程](https://play.manticoresearch.com/) 提供的互动教程，让学习变得轻松。
- Manticore 还提供内置的复制和负载均衡功能，增强了可靠性。
- 数据可以轻松同步自 MySQL、PostgreSQL、ODBC、xml 和 csv 等来源。
- 尽管不完全符合 ACID，但 Manticore 仍支持事务和二进制日志，以确保写入的安全性。
- 通过内置工具和 SQL 命令轻松进行数据备份和恢复。

[Craigslist](https://www.craigslist.org/)、[Socialgist](https://socialgist.com/)、[PubChem](https://pubchem.ncbi.nlm.nih.gov/)、[Rozetka](https://rozetka.com.ua/) 以及许多其他公司使用 Manticore 来实现高效搜索和流式过滤。

Manticore Search 是从 [Sphinx 2.3.2](https://github.com/sphinxsearch/sphinx) 于 2017 年分叉而来。



## 更多功能

全文搜索和相关性：

- 超过 20 种[全文搜索运算符](https://play.manticoresearch.com/fulltextintro/)和超过 20 种排名因素
- 自定义排名

其他搜索功能：

- [丰富的过滤功能](https://manual.manticoresearch.com/Searching/Full_text_matching/Operators)
- [分面搜索](https://play.manticoresearch.com/faceting/)
- [地理空间搜索](https://play.manticoresearch.com/geosearch/)
- [向量搜索](https://manual.manticoresearch.com/Searching/KNN)
- [表连接](https://manual.manticoresearch.com/Searching/Joining)
- [拼写纠正](https://play.manticoresearch.com/didyoumean/)
- [自动补全](https://play.manticoresearch.com/simpleautocomplete/)
- 用于过滤和数据操作的广泛函数

自然语言处理 (NLP)：

- [词干分析](https://manual.manticoresearch.com/Creating_a_table/NLP_and_tokenization/Morphology)
- [词形还原](https://manual.manticoresearch.com/Creating_a_table/NLP_and_tokenization/Morphology)
- [停用词](https://manual.manticoresearch.com/Creating_a_table/NLP_and_tokenization/Ignoring_stop-words#stopwords)
- [同义词](https://manual.manticoresearch.com/Creating_a_table/NLP_and_tokenization/Exceptions)
- [词形转换](https://manual.manticoresearch.com/Creating_a_table/NLP_and_tokenization/Wordforms#wordforms)
- [字符和词级别的高级分词](https://manual.manticoresearch.com/Creating_a_table/NLP_and_tokenization/Low-level_tokenization#charset_table)
- [中文分词](https://play.manticoresearch.com/icu-chinese/)
- [文本高亮](https://play.manticoresearch.com/highlighting/)

通过“渗透”表进行流过滤 [使用 "percolate" 表](https://play.manticoresearch.com/pq/)

高可用性：

- 数据可以跨服务器和数据中心分布
- [同步复制](https://play.manticoresearch.com/replication/)
- 内置负载均衡

安全性：

- [支持 https](https://play.manticoresearch.com/https/)
- [只读模式](https://manual.manticoresearch.com/Security/Read_only)

数据安全性：

- 通过 [manticore-backup 工具和 SQL 命令 BACKUP](https://manual.manticoresearch.com/Securing_and_compacting_a_table/Backup_and_restore) 来备份和恢复数据

数据存储：

- 行式存储——需要更多内存，提供更快的性能
- 列式存储——需要更少的内存，仍提供不错的性能，但对于某些查询性能略低于行式存储
- 文档存储——不需要内存，但只允许获取原始值，不能进行排序/分组/过滤

性能优化：

- [二级索引](https://manual.manticoresearch.com/Server_settings/Searchd#secondary_indexes)
- 基于成本的优化器确定查询的最有效执行计划

数据类型：

- 全文字段——倒排索引
- 行式和列式存储的 int、bigint 和 float 数字字段
- 多值属性（数组）
- 字符串和 JSON
- 用于键值用途的磁盘上 “[存储](https://play.manticoresearch.com/docstore/)”

集成：

- [与 MySQL 和 PostgreSQL 同步](https://manual.manticoresearch.com/Creating_a_table/Local_tables/Plain_table#Plain-table)
- [与 XML 同步](https://manual.manticoresearch.com/Adding_data_from_external_storages/Fetching_from_XML_streams#XML-file-format)
- [与 CSV 同步](https://manual.manticoresearch.com/Adding_data_from_external_storages/Fetching_from_CSV,TSV#Fetching-from-TSV,CSV)
- [作为 MySQL 的存储引擎](https://manual.manticoresearch.com/Extensions/SphinxSE#Using-SphinxSE)
- [通过 FEDERATED 引擎与 MySQL 连接](https://manual.manticoresearch.com/Extensions/FEDERATED)
- [ProxySQL](https://manticoresearch.com/2018/06/18/using-proxysql-to-route-inserts-in-a-distributed-realtime-index/)
- [Apache Superset](https://manticoresearch.com/blog/manticoresearch-apache-superset-integration/)
- [Grafana](https://manticoresearch.com/blog/manticoresearch-grafana-integration/)
- [Fluentbit](https://manticoresearch.com/blog/integration-of-manticore-with-fluentbit/)
- [Logstash/Filebeat](https://manticoresearch.com/blog/integration-of-manticore-with-logstash-filebeat/)
- [Vector.dev](https://manticoresearch.com/blog/integration-of-manticore-with-vectordev/)
- [Mysqldump](https://manual.manticoresearch.com/Securing_and_compacting_a_table/Backup_and_restore#Backup-and-restore-with-mysqldump)
- [Manticore Columnar Library](https://github.com/manticoresoftware/columnar)



---

## 文档目录


* [☝ 介绍](Introduction.md)
* [❗ 首先阅读](Read_this_first.md)
* [1️⃣ 安装](Installation/Installation.md)
    * [• Docker](Installation/Docker.md)
    * [• RedHat和CentOS](Installation/RHEL_and_Centos.md)
    * [• Debian和Ubuntu](Installation/Debian_and_Ubuntu.md)
    * [• MacOS](Installation/MacOS.md)
    * [• Windows](Installation/Windows.md)
    * [• 从源码编译](Installation/Compiling_from_sources.md)
    * [• Manticore Buddy](Installation/Manticore_Buddy.md)
    * [• 从Sphinx迁移](Installation/Migration_from_Sphinx.md)
* [🔰 快速入门指南](Quick_start_guide.md)
* [2️⃣ 启动服务器](Starting_the_server.md)
    * [• In Linux](Starting_the_server/Linux.md)
    * [• Manually](Starting_the_server/Manually.md)
    * [• In Docker](Starting_the_server/Docker.md)
    * [• In Windows](Starting_the_server/Windows.md)
    * [• In MacOS](Starting_the_server/MacOS.md)
* [3️⃣ 创建表](Creating_a_table.md)
    * [⪢ 数据类型](Creating_a_table/Data_types.md)
        * [• 行存储和列存储属性](Creating_a_table/Data_types.md#行存储和列存储属性)
    * [⪢ 创建本地表](Creating_a_table/Local_tables.md)
        * [✔ 实时表](Creating_a_table/Local_tables/Real-time_table.md)
        * [• 普通表](Creating_a_table/Local_tables/Plain_table.md)
        * [• 普通表和实时表设置](Creating_a_table/Local_tables/Plain_and_real-time_table_settings.md)
        * [• 渗透表](Creating_a_table/Local_tables/Percolate_table.md)
        * [• 模板表](Creating_a_table/Local_tables/Template_table.md)
    * [⪢ 自然语言处理（NLP）和分词]
        * [• 数据分词](Creating_a_table/NLP_and_tokenization/Data_tokenization.md)
        * [• 支持的语言](Creating_a_table/NLP_and_tokenization/Supported_languages.md)
        * [• 中文、日文、韩文（CJK）和泰语语言](Creating_a_table/NLP_and_tokenization/Languages_with_continuous_scripts.md)
        * [• 低级分词](Creating_a_table/NLP_and_tokenization/Low-level_tokenization.md)
        * [• 通配符搜索设置](Creating_a_table/NLP_and_tokenization/Wildcard_searching_settings.md)
        * [• 忽略停用词](Creating_a_table/NLP_and_tokenization/Ignoring_stop-words.md)
        * [• 词形](Creating_a_table/NLP_and_tokenization/Wordforms.md)
        * [• 异常处理](Creating_a_table/NLP_and_tokenization/Exceptions.md)
        * [• 词法](Creating_a_table/NLP_and_tokenization/Morphology.md)
        * [• 高级 HTML 分词](Creating_a_table/NLP_and_tokenization/Advanced_HTML_tokenization.md)
    * [⪢ 创建分布式表](Creating_a_table/Creating_a_distributed_table/Creating_a_distributed_table.md)
        * [• 创建本地分布式表](Creating_a_table/Creating_a_distributed_table/Creating_a_local_distributed_table.md)
        * [• 远程表](Creating_a_table/Creating_a_distributed_table/Remote_tables.md)
* [• 列出表](Listing_tables.md)
* [• 删除表](Deleting_a_table.md)
* [• 清空表](Emptying_a_table.md)
* [⪢ 创建集群](Creating_a_cluster/Creating_a_cluster.md)
    * [添加新节点](Creating_a_cluster/Adding_a_new_node.md)
    * [⪢ 删除节点](Creating_a_cluster/Remote_nodes.md)
        * [镜像](Creating_a_cluster/Remote_nodes/Mirroring.md)
        * [负载均衡](Creating_a_cluster/Remote_nodes/Load_balancing.md)
    * [⪢ 设置复制](Creating_a_cluster/Setting_up_replication/Setting_up_replication.md)
        * [创建复制集群](Creating_a_cluster/Setting_up_replication/Creating_a_replication_cluster.md)
        * [加入复制集群](Creating_a_cluster/Setting_up_replication/Joining_a_replication_cluster.md)
        * [删除复制集群](Creating_a_cluster/Setting_up_replication/Deleting_a_replication_cluster.md)
        * [在复制集群中添加和删除表](Creating_a_cluster/Setting_up_replication/Adding_and_removing_a_table_from_a_replication_cluster.md)
        * [管理复制节点](Creating_a_cluster/Setting_up_replication/Managing_replication_nodes.md)
        * [复制集群状态](Creating_a_cluster/Setting_up_replication/Replication_cluster_status.md)
        * [重启集群](Creating_a_cluster/Setting_up_replication/Restarting_a_cluster.md)
        * [集群恢复](Creating_a_cluster/Setting_up_replication/Cluster_recovery.md)
* [4️⃣ 连接服务器](Connecting_to_the_server.md)
    * [MySQL协议](Connecting_to_the_server/MySQL_protocol.md)
    * [HTTP](Connecting_to_the_server/HTTP.md)
    * [通过 HTTP 的 SQL](Connecting_to_the_server/HTTP.md#SQL-over-HTTP)
* [⪢ 数据创建和修改](Data_creation_and_modification/Data_creation_and_modification.md)
    * [⪢ 向表中添加文档]
        * [✔ 向实时表添加文档](Data_creation_and_modification/Adding_documents_to_a_table/Adding_documents_to_a_real-time_table.md)
        * [向渗透表添加规则](Data_creation_and_modification/Adding_documents_to_a_table/Adding_rules_to_a_percolate_table.md)
    * [⪢ 从外部存储添加数据]
        * [创建普通表](Data_creation_and_modification/Adding_data_from_external_storages/Plain_tables_creation.md)
        * [⪢ 从数据库获取数据]
            * [介绍](Data_creation_and_modification/Adding_data_from_external_storages/Fetching_from_databases/Introduction.md)
            * [数据库连接](Data_creation_and_modification/Adding_data_from_external_storages/Fetching_from_databases/Database_connection.md)
            * [执行获取查询](Data_creation_and_modification/Adding_data_from_external_storages/Fetching_from_databases/Execution_of_fetch_queries.md)
            * [处理获取的数据](Data_creation_and_modification/Adding_data_from_external_storages/Fetching_from_databases/Processing_fetched_data.md)
            * [范围查询](Data_creation_and_modification/Adding_data_from_external_storages/Fetching_from_databases/Ranged_queries.md)
        * [从 XML 流获取数据](Data_creation_and_modification/Adding_data_from_external_storages/Fetching_from_XML_streams.md)
        * [• 从 CSV、TSV 获取数据](Data_creation_and_modification/Adding_data_from_external_storages/Fetching_from_CSV,TSV.md)
        * [• 主+增量模式查询](Data_creation_and_modification/Adding_data_from_external_storages/Main_delta.md)
        * [⪢ 从表中添加数据]
            * [• 合并表](Data_creation_and_modification/Adding_data_from_external_storages/Adding_data_to_tables/Merging_tables.md)
            * [• 在普通表中使用杀死列表](Data_creation_and_modification/Adding_data_from_external_storages/Adding_data_to_tables/Killlist_in_plain_tables.md)
            * [• 将一张表附加到另一张表](Data_creation_and_modification/Adding_data_from_external_storages/Adding_data_to_tables/Attaching_one_table_to_another.md)
            * [• 导入实时表](Data_creation_and_modification/Adding_data_from_external_storages/Adding_data_to_tables/Importing_table.md)
        * [• 轮换表](Data_creation_and_modification/Adding_data_from_external_storages/Rotating_a_table.md)
    * [⪢ 更新文档]
        * [• 替换 VS 更新](Data_creation_and_modification/Updating_documents/REPLACE_vs_UPDATE.md)
        * [• 替换](Data_creation_and_modification/Updating_documents/REPLACE.md)
        * [• 更新](Data_creation_and_modification/Updating_documents/UPDATE.md)
    * [• 删除文档](Data_creation_and_modification/Deleting_documents.md)
    * [• 事务](Data_creation_and_modification/Transactions.md)
* [5️⃣ 搜索]
    * [• 简介](Searching/Intro.md)
    * [⪢ 全文匹配]
        * [• 基本用法](Searching/Full_text_matching/Basic_usage.md)
        * [• 操作符](Searching/Full_text_matching/Operators.md)
        * [• 转义](Searching/Full_text_matching/Escaping.md)
        * [• 查询分析](Searching/Full_text_matching/Profiling.md)
        * [• 布尔优化](Searching/Full_text_matching/Boolean_optimization.md)
    * [• 搜索结果](Searching/Search_results.md)
    * [• 过滤器](Searching/Filters.md)
    * [• 连接](Searching/Joining.md)
    * [• 表达式](Searching/Expressions.md)
    * [• 搜索选项](Searching/Options.md)
    * [• 高亮显示](Searching/Highlighting.md)
    * [• 排序与排名](Searching/Sorting_and_ranking.md)
    * [• 分页](Searching/Pagination.md)
    * [• 分布式搜索](Searching/Distributed_searching.md)
    * [• 多查询](Searching/Multi-queries.md)
    * [• 子查询](Searching/Sub-selects.md)
    * [• 分组](Searching/Grouping.md)
    * [• 分面搜索](Searching/Faceted_search.md)
    * [• 地理（Geo）搜索](Searching/Geo_search.md)
    * [• 渗透查询](Searching/Percolate_query.md)
    * [• 自动补全](Searching/Autocomplete.md)
    * [• 拼写校正](Searching/Spell_correction.md)
        * [• 模糊搜索](Searching/Spell_correction.md#模糊搜索)
    * [• 查询缓存](Searching/Query_cache.md)
    * [• 排序规则](Searching/Collations.md)
    * [• 基于成本的优化器](Searching/Cost_based_optimizer.md)
    * [• K-最近邻向量搜索](Searching/KNN.md)
* [• 更新表结构和设置](Updating_table_schema_and_settings.md)
    * [• 在实时模式下更新表模式](Updating_table_schema_and_settings.md#在实时模式下更新表的全文设置)
    * [• 在实时模式下更新表的全文搜索设置](Updating_table_schema_and_settings.md#在实时模式下更新表的全文搜索设置)
    * [• 重命名实时表](Updating_table_schema_and_settings.md#重命名实时表)
    * [• 更新普通表的全文搜索设置](Updating_table_schema_and_settings.md#更新普通表的全文搜索设置)
    * [• 重建二级索引](Updating_table_schema_and_settings.md#重建二级索引)
    * [• 修改分布式表](Updating_table_schema_and_settings.md#修改分布式表)
* [⪢ 函数](Functions.md)
    * [• 数学函数](Functions/Mathematical_functions.md)
    * [• 搜索与排名函数](Functions/Searching_and_ranking_functions.md)
    * [• 类型转换函数](Functions/Type_casting_functions.md)
    * [• 数组与条件处理函数](Functions/Arrays_and_conditions_functions.md)
    * [• 日期和时间函数](Functions/Date_and_time_functions.md)
    * [• 地理空间函数](Functions/Geo_spatial_functions.md)
    * [• 字符串函数](Functions/String_functions.md)
    * [• 其他函数](Functions/Other_functions.md)
* [⪢ 表的安全性与压缩]
    * [• 备份与恢复](Securing_and_compacting_a_table/Backup_and_restore.md)
    * [• 实时表的结构](Securing_and_compacting_a_table/RT_table_structure.md)
    * [• 将RAM块刷新到新磁盘块](Securing_and_compacting_a_table/Flushing_RAM_chunk_to_a_new_disk_chunk.md)
    * [• 将实时表刷新到磁盘](Securing_and_compacting_a_table/Flushing_RAM_chunk_to_disk.md)
    * [• 压缩表](Securing_and_compacting_a_table/Compacting_a_table.md)
    * [• 刷新与合并期间的隔离](Securing_and_compacting_a_table/Isolation_during_flushing_and_merging.md)
    * [• 冻结表](Securing_and_compacting_a_table/Freezing_a_table.md)
    * [• 刷新属性](Securing_and_compacting_a_table/Flushing_attributes.md)
    * [• 刷新hostnames](Securing_and_compacting_a_table/Flushing_hostnames.md)
* [⪢ 安全]
    * [• SSL](Security/SSL.md)
    * [• 只读](Security/Read_only.md)
* [⪢ 日志]
    * [• 查询日志](Logging/Query_logging.md)
    * [• 服务器日志](Logging/Server_logging.md)
    * [• 二进制日志](Logging/Binary_logging.md)
    * [• Docker日志](Logging/Docker_logging.md)
    * [• 轮转查询和服务器日志](Logging/Rotating_query_and_server_logs.md)
* [⪢ 节点信息与管理]
    * [• 节点状态](Node_info_and_management/Node_status.md)
    * [• SHOW META](Node_info_and_management/SHOW_META.md)
    * [• SHOW THREADS](Node_info_and_management/SHOW_THREADS.md)
    * [• SHOW QUERIES](Node_info_and_management/SHOW_QUERIES.md)
    * [• SHOW VERSION](Node_info_and_management/SHOW_VERSION.md)
    * [• KILL](Node_info_and_management/KILL.md)
    * [• SHOW WARNINGS](Node_info_and_management/SHOW_WARNINGS.md)
    * [• SHOW VARIABLES](Node_info_and_management/SHOW_VARIABLES.md)
    * [⪢ 性能分析]
        * [• 查询分析](Node_info_and_management/Profiling/Query_profile.md)
        * [• 查询计划](Node_info_and_management/Profiling/Query_plan.md)
    * [⪢ 表设置和状态]
        * [• SHOW TABLE STATUS](Node_info_and_management/Table_settings_and_status/SHOW_TABLE_STATUS.md)
        * [• SHOW TABLE SETTINGS](Node_info_and_management/Table_settings_and_status/SHOW_TABLE_SETTINGS.md)
* [⪢ 服务器设置]
    * [• Searchd](Server_settings/Searchd.md)
    * [• 通用设置](Server_settings/Common.md)
    * [• 特殊后缀](Server_settings/Special_suffixes.md)
    * [• 脚本化配置](Server_settings/Scripted_configuration.md)
    * [• 注释](Server_settings/Comments.md)
    * [• 表和源声明的继承](Server_settings/Inheritance_of_index_and_source_declarations.md)
    * [• 在线设置变量](Server_settings/Setting_variables_online.md)
* [⪢ 集成]
    * [Logstash](Integration/Logstash.md)
    * [Filebeat](Integration/Filebeat.md)
    * [DBeaver](Integration/DBeaver.md)
    * [Apache Superset](Integration/Apache_Superset.md)
* [⪢ 扩展]
    * [SphinxSE](Extensions/SphinxSE.md)
    * [FEDERATED](Extensions/FEDERATED.md)
    * [⪢ UDFs 和插件](Extensions/UDFs_and_Plugins/UDFs_and_Plugins.md)
        * [列出插件](Extensions/UDFs_and_Plugins/Listing_plugins.md)
        * [⪢ 用户自定义函数 (UDF)](Extensions/UDFs_and_Plugins/UDF.md)
            * [创建函数](Extensions/UDFs_and_Plugins/UDF/Creating_a_function.md)
            * [删除函数](Extensions/UDFs_and_Plugins/UDF/Deleting_a_function.md)
        * [⪢ 插件]
            * [• 创建插件](Extensions/UDFs_and_Plugins/Plugins/Creating_a_plugin.md)
            * [• 删除插件](Extensions/UDFs_and_Plugins/Plugins/Deleting_a_plugin.md)
            * [• 启用和禁用 Buddy 插件](Extensions/UDFs_and_Plugins/Plugins/Enabling_and_disabling_buddy_plugins.md)
            * [• 重新加载插件](Extensions/UDFs_and_Plugins/Plugins/Reloading_plugins.md)
            * [• 排名插件](Extensions/UDFs_and_Plugins/Plugins/Ranker_plugins.md)
            * [• 令牌过滤器插件](Extensions/UDFs_and_Plugins/Plugins/Token_filter_plugins.md)
* [• 杂项工具](Miscellaneous_tools.md)
* [• OpenAPI 规范](Openapi.md)
* [• 远程监控](Telemetry.md)
* [• 更新日志](Changelog.md)
* [🐞 报告BUG](Reporting_bugs.md)
* [📖 参考文献](References.md)
    * [• 先前版本](References.md#旧版本 Manticore 的文档)
