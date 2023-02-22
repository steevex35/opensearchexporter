[comment]: <> (Code generated by mdatagen. DO NOT EDIT.)

# sqlserverreceiver

## Default Metrics

The following metrics are emitted by default. Each of them can be disabled by applying the following configuration:

```yaml
metrics:
  <metric_name>:
    enabled: false
```

### sqlserver.batch.request.rate

Number of batch requests received by SQL Server.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| {requests}/s | Gauge | Double |

### sqlserver.batch.sql_compilation.rate

Number of SQL compilations needed.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| {compilations}/s | Gauge | Double |

### sqlserver.batch.sql_recompilation.rate

Number of SQL recompilations needed.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| {compilations}/s | Gauge | Double |

### sqlserver.lock.wait.rate

Number of lock requests resulting in a wait.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| {requests}/s | Gauge | Double |

### sqlserver.lock.wait_time.avg

Average wait time for all lock requests that had to wait.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| ms | Gauge | Double |

### sqlserver.page.buffer_cache.hit_ratio

Pages found in the buffer pool without having to read from disk.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| % | Gauge | Double |

### sqlserver.page.checkpoint.flush.rate

Number of pages flushed by operations requiring dirty pages to be flushed.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| {pages}/s | Gauge | Double |

### sqlserver.page.lazy_write.rate

Number of lazy writes moving dirty pages to disk.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| {writes}/s | Gauge | Double |

### sqlserver.page.life_expectancy

Time a page will stay in the buffer pool.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| s | Gauge | Int |

### sqlserver.page.operation.rate

Number of physical database page operations issued.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| {operations}/s | Gauge | Double |

#### Attributes

| Name | Description | Values |
| ---- | ----------- | ------ |
| type | The page operation types. | Str: ``read``, ``write`` |

### sqlserver.page.split.rate

Number of pages split as a result of overflowing index pages.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| {pages}/s | Gauge | Double |

### sqlserver.transaction.rate

Number of transactions started for the database (not including XTP-only transactions).

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| {transactions}/s | Gauge | Double |

### sqlserver.transaction.write.rate

Number of transactions that wrote to the database and committed.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| {transactions}/s | Gauge | Double |

### sqlserver.transaction_log.flush.data.rate

Total number of log bytes flushed.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| By/s | Gauge | Double |

### sqlserver.transaction_log.flush.rate

Number of log flushes.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| {flushes}/s | Gauge | Double |

### sqlserver.transaction_log.flush.wait.rate

Number of commits waiting for a transaction log flush.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| {commits}/s | Gauge | Double |

### sqlserver.transaction_log.growth.count

Total number of transaction log expansions for a database.

| Unit | Metric Type | Value Type | Aggregation Temporality | Monotonic |
| ---- | ----------- | ---------- | ----------------------- | --------- |
| {growths} | Sum | Int | Cumulative | true |

### sqlserver.transaction_log.shrink.count

Total number of transaction log shrinks for a database.

| Unit | Metric Type | Value Type | Aggregation Temporality | Monotonic |
| ---- | ----------- | ---------- | ----------------------- | --------- |
| {shrinks} | Sum | Int | Cumulative | true |

### sqlserver.transaction_log.usage

Percent of transaction log space used.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| % | Gauge | Int |

### sqlserver.user.connection.count

Number of users connected to the SQL Server.

| Unit | Metric Type | Value Type |
| ---- | ----------- | ---------- |
| {connections} | Gauge | Int |

## Resource Attributes

| Name | Description | Values | Enabled |
| ---- | ----------- | ------ | ------- |
| sqlserver.database.name | The name of the SQL Server database. | Any Str | true |