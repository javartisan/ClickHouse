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
