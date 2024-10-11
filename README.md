# Manticore Search 中文文档

## 官方介绍

### Manticore Search —— 易于使用的开源快速数据库用于搜索

### 性能

性能是 Manticore Search 开发的驱动力。我们致力于实现**低响应时间**，这对于分析大型数据集至关重要。**吞吐量也是一个关键考虑因素**，使 Manticore 能够处理每秒大量查询。Manticore Search 是针对大数据和向量搜索的**最快开源搜索引擎**。

- 在[大型数据集基准测试](https://db-benchmarks.com/test-taxi/#manticore-search-vs-elasticsearch)（17亿文档）中，Manticore Search 的速度比 Elasticsearch 快 **4 倍**。
- 在[日志分析基准测试](https://db-benchmarks.com/test-logs10m/#elasticsearch-with-no-tuning-vs-manticore-search-default-row-wise-storage)（1000万个 Nginx 日志记录）中，Manticore Search 的速度比 Elasticsearch 快 **29 倍**。
- 在[中等规模的数据集（1亿条 Hackernews 评论）基准测试](https://db-benchmarks.com/test-hn/#manticore-search-columnar-storage-vs-elasticsearch)中，Manticore Search 的速度比 Elasticsearch **快 5 倍**。
- 在[小规模的数据集（100万条 Hackernews 评论）基准测试](https://db-benchmarks.com/test-hn-small/#manticore-search-vs-elasticsearch)中，Manticore Search 的速度比 Elasticsearch **快 15 倍**。

### 具有成本效益的搜索引擎

Manticore Search 是最用户友好、易于访问且**具有成本效益的搜索数据库**。即使在仅有 **1 个核心和 1GB 内存**的小型 VM/容器环境中，我们也能[保持出色的速度和效率](https://db-benchmarks.com/?cache=slowest&engines=clickhouse_1_core_21.8.11.4%2Celasticsearch_1_core_7.15.2%2Cmanticoresearch_1_core_6.0.2%2Cmeilisearch_1_core_1.1.1%2Cmysql_1_core_8.0.28%2Cmysql_percona_1_core_8.0.28-19%2Cpostgres_1_core_15.2+%28Debian+15.2-1.pgdg110%2B1%29&tests=hn_small&memory=1024&queries=0%2C1%2C2%2C3%2C5%2C6%2C7%2C8%2C16%2C17%2C18%2C19%2C20%2C21%2C22%2C25%2C26%2C27)。Manticore Search 旨在支持广泛的用例，并在各种规模的操作中提供强大的性能与资源效率。欲了解更多信息，请查看我们的[基准测试](https://db-benchmarks.com/)，以查看 Manticore 如何在各种场景中超越其他解决方案。

### 向量搜索

发现 Manticore Search 强大的语义和向量搜索功能。通过阅读我们关于 Manticore 中的[向量搜索](https://manticoresearch.com/blog/vector-search/)和将[向量搜索集成到 GitHub 的文章](https://manticoresearch.com/blog/github-semantic-search/)，了解更多信息。

### Elasticsearch 替代方案

Manticore Search 提供了比 Elasticsearch 更优的替代方案。将 Manticore 搜索引擎[与 Logstash 和 Beats 搭配使用](https://manticoresearch.com/blog/integration-of-manticore-with-logstash-filebeat/)，处理 1000 万条 Nginx 日志数据集时，可实现高达 [29 倍的性能提升](https://db-benchmarks.com/test-logs10m/#3-competitors-with-no-tuning-at-once)。了解更多关于我们在[不同用例](https://manticoresearch.com/blog/manticore-alternative-to-elasticsearch/#search-speed)中提高搜索速度的信息。

### 专业服务

尽管 Manticore 是 100% 开源的，但我们在这里帮助您充分利用它！

✓ 咨询：节省团队的时间和资源，加快构建速度
✓ 精细调优：确保您的实例以最佳性能运行
✓ 功能开发：获得量身定制的自定义功能，以满足您的业务需求

了解更多关于我们全面服务的信息。

### 真正的开源

我们热爱开源。Manticore Search 和其他公开可用的 Manticore 产品均可免费使用，并以 [OSI 批准的开源许可证发布](https://opensource.org/licenses)。欢迎在 [GitHub](https://github.com/manticoresoftware/manticoresearch) 上贡献您的力量。

---

## 文档目录


* [☝ 介绍](Introduction.md)
* [❗ 先看这里](Read_this_first.md)
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
* [2️⃣ Starting the server](Starting_the_server.md)
    * [• In Linux](Starting_the_server/Linux.md)
    * [• Manually](Starting_the_server/Manually.md)
    * [• In Docker](Starting_the_server/Docker.md)
    * [• In Windows](Starting_the_server/Windows.md)
    * [• In MacOS](Starting_the_server/MacOS.md)
* [3️⃣ 创建表](Creating_a_table.md)
    * [⪢ 数据类型](Creating_a_table/Data_types.md)
        * [• 行式和列式属性存储](Creating_a_table/Data_types.md#Row-wise-and-columnar-attribute-storages)
    * [⪢ 创建本地表](Creating_a_table/Local_tables.md)
        * [✔ 实时表](Creating_a_table/Local_tables/Real-time_table.md)
        * [• 普通表](Creating_a_table/Local_tables/Plain_table.md)
        * [• 普通表和实时表设置](Creating_a_table/Local_tables/Plain_and_real-time_table_settings.md)
        * [• 渗透表](Creating_a_table/Local_tables/Percolate_table.md)
        * [• 模板表](Creating_a_table/Local_tables/Template_table.md)
    * [⪢ 自然语言处理（NLP）和分词]
        * [• 数据分词](Creating_a_table/NLP_and_tokenization/Data_tokenization.md)
        * [• 支持的语言](Creating_a_table/NLP_and_tokenization/Supported_languages.md)
        * [• 连续书写的语言](Creating_a_table/NLP_and_tokenization/Languages_with_continuous_scripts.md)
        * [• 低级分词](Creating_a_table/NLP_and_tokenization/Low-level_tokenization.md)
        * [• 通配符搜索设置](Creating_a_table/NLP_and_tokenization/Wildcard_searching_settings.md)
        * [• 忽略停用词](Creating_a_table/NLP_and_tokenization/Ignoring_stop-words.md)
        * [• 词形](Creating_a_table/NLP_and_tokenization/Wordforms.md)
        * [• 例外](Creating_a_table/NLP_and_tokenization/Exceptions.md)
        * [• Morphology](Creating_a_table/NLP_and_tokenization/Morphology.md)
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
        * [Mirroring](Creating_a_cluster/Remote_nodes/Mirroring.md)
        * [Load balancing](Creating_a_cluster/Remote_nodes/Load_balancing.md)
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
        * [• 旋转表](Data_creation_and_modification/Adding_data_from_external_storages/Rotating_a_table.md)
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
    * [• 子选择](Searching/Sub-selects.md)
    * [• 分组](Searching/Grouping.md)
    * [• 分面搜索](Searching/Faceted_search.md)
    * [• 地理（Geo）搜索](Searching/Geo_search.md)
    * [• 检索查询](Searching/Percolate_query.md)
    * [• 自动补全](Searching/Autocomplete.md)
    * [• 拼写纠正](Searching/Spell_correction.md)
        * [• 模糊搜索](Searching/Spell_correction.md#Fuzzy-Search)
    * [• 查询缓存](Searching/Query_cache.md)
    * [• 排序规则](Searching/Collations.md)
    * [• 基于成本的优化器](Searching/Cost_based_optimizer.md)
    * [• K-最近邻向量搜索](Searching/KNN.md)
* [• 更新表结构和设置](Updating_table_schema_and_settings.md)
    * [• 在实时模式下更新表模式](Updating_table_schema_and_settings.md#Updating-table-schema-in-RT-mode)
    * [• 在实时模式下更新表的全文搜索（FT）设置](Updating_table_schema_and_settings.md#Updating-table-FT-settings-in-RT-mode)
    * [• 重命名实时表](Updating_table_schema_and_settings.md#Renaming-a-real-time-table)
    * [• 更新普通模式下的表全文搜索（FT）设置](Updating_table_schema_and_settings.md#Updating-table-FT-settings-in-plain-mode)
    * [• 重建辅助索引](Updating_table_schema_and_settings.md#Rebuilding-a-secondary-index)
    * [• 修改分布式表](Updating_table_schema_and_settings.md#Changing-a-distributed-table)
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
    * [• 关于实时表结构的简要说明](Securing_and_compacting_a_table/RT_table_structure.md)
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
        * [⪢ UDF](Extensions/UDFs_and_Plugins/UDF.md)
            * [创建函数](Extensions/UDFs_and_Plugins/UDF/Creating_a_function.md)
            * [删除函数](Extensions/UDFs_and_Plugins/UDF/Deleting_a_function.md)
        * [⪢ 插件]
            * [• 创建插件](Extensions/UDFs_and_Plugins/Plugins/Creating_a_plugin.md)
            * [• 删除插件](Extensions/UDFs_and_Plugins/Plugins/Deleting_a_plugin.md)
            * [• 启用和禁用 Buddy 插件](Extensions/UDFs_and_Plugins/Plugins/Enabling_and_disabling_buddy_plugins.md)
            * [• 重新加载插件](Extensions/UDFs_and_Plugins/Plugins/Reloading_plugins.md)
            * [• 排名插件](Extensions/UDFs_and_Plugins/Plugins/Ranker_plugins.md)
            * [• 令牌过滤器插件](Extensions/UDFs_and_Plugins/Plugins/Token_filter_plugins.md)
* [• 令牌过滤器插件](Miscellaneous_tools.md)
* [• OpenAPI 规范](Openapi.md)
* [• 远程监控](Telemetry.md)
* [• 更新日志](Changelog.md)
* [🐞 报告BUG](Reporting_bugs.md)
* [📖 参考文献](References.md)
    * [• 先前版本](References.md#Documentation-for-old-Manticore-versions)
    <!-- proofread -->