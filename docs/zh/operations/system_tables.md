# 系统表

系统表被用作实现一些系统的工程以及提供访问系统如何工作的一些相关信息。你不可以删除系统表(但是可以执行DETACH).系统表没有数据或者元数据文件存储在磁盘上，而是在服务器启动时候创建的。系统表是只读的，可以在system数据库下面找到。

## system.asynchronous_metrics {#system_tables-asynchronous_metrics}
包含一些在后台周期性计算的相关指标。例如，使用的RAM大小。

Columns:

- `metric` ([String](../data_types/string.md)) — 指标名字.
- `value` ([Float64](../data_types/float.md)) — 指标值.

**例如**

```sql
SELECT * FROM system.asynchronous_metrics LIMIT 10
```

```text
┌─metric──────────────────────────────────┬──────value─┐
│ jemalloc.background_thread.run_interval │          0 │
│ jemalloc.background_thread.num_runs     │          0 │
│ jemalloc.background_thread.num_threads  │          0 │
│ jemalloc.retained                       │  422551552 │
│ jemalloc.mapped                         │ 1682989056 │
│ jemalloc.resident                       │ 1656446976 │
│ jemalloc.metadata_thp                   │          0 │
│ jemalloc.metadata                       │   10226856 │
│ UncompressedCacheCells                  │          0 │
│ MarkCacheFiles                          │          0 │
└─────────────────────────────────────────┴────────────┘
```

**See Also**

- [Monitoring](monitoring.md) — Clickhouse有关监控的基础概念.
- [system.metrics](#system_tables-metrics) — 包含即时计算指标.
- [system.events](#system_tables-events) — 包含一些发生的events.

## system.clusters

包含有关集群可用性的信息以及服务器节点信息。
Columns:

```
cluster String      — 集群名字.
shard_num UInt32 — 集群的shard数量，从1开始计数.
shard_weight UInt32 — 写数据时候shard的权重.
replica_num UInt32 — shard的副本数目, 从1开始计数.
host_name String — 主机名字，从配置文件中获取的.
String host_address — 主机IP地址，从DNS中解析获取.
port UInt16 — 连接到该服务器的端口号.
user String — 连接到服务器的用户名字.
```

## system.columns
关于所有表的信息的列信息，你可以使用该表查询一些类似于[DESCRIBE TABLE](../query_language/misc.md#misc-describe-table) 名命令获取的信息，但是该表一次可以获取多张表的列信息.

表`system.columns`包含如下列（对应列的类型在括号中）:

- `database` (String) — 数据库名字.
- `table` (String) — 表明.
- `name` (String) — 列明.
- `type` (String) — 列类型.
- `default_kind` (String) — 列类型对应的默认值，如果不指定则为一个空字符串.
- `default_expression` (String) — Expression for the default value, or an empty string if it is not defined.
- `data_compressed_bytes` (UInt64) — The size of compressed data, in bytes.
- `data_uncompressed_bytes` (UInt64) — The size of decompressed data, in bytes.
- `marks_bytes` (UInt64) — The size of marks, in bytes.
- `comment` (String) — The comment about column, or an empty string if it is not defined.
- `is_in_partition_key` (UInt8) — Flag that indicates whether the column is in partition expression.
- `is_in_sorting_key` (UInt8) — Flag that indicates whether the column is in sorting key expression.
- `is_in_primary_key` (UInt8) — Flag that indicates whether the column is in primary key expression.
- `is_in_sampling_key` (UInt8) — Flag that indicates whether the column is in sampling key expression.



