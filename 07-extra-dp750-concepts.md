# DP-750 Extra Concepts

> Subtle distinctions and nuances exam wording loves.

## Liquid clustering vs partitioning vs ZORDER

| Approach | When |
|---|---|
| **Partition** | Old default; coarse-grained, low cardinality columns (e.g. date) |
| **ZORDER BY** | Multi-dimensional clustering for filter columns (used with OPTIMIZE) |
| **Liquid clustering** | New default; replaces both for new tables; auto-rebalances |

## Photon

- Vectorized execution engine in C++.
- Costs more DBUs but often faster overall (cheaper per job).
- Best for SQL aggregations and large scans; less benefit for row-by-row Python UDFs.

## Cluster access modes - limitations

| Mode | Scala | UDFs | Init scripts | Mounts | Spark conf overrides |
|---|---|---|---|---|---|
| **Single User** | y | y all | y | y | y |
| **Shared** | ! limited | Python/SQL only (Scala UDFs limited) | Restricted | Restricted | Restricted |

## Default catalog and schema

- Workspace default catalog set in admin settings.
- Reduce 3-part names with `USE CATALOG` and `USE SCHEMA`.

## DBFS root vs Volumes

- **DBFS root** - legacy; sensitive data should not live there.
- **Volumes** (Unity Catalog) - managed or external; preferred for new code.

## Parquet vs Delta

| Capability | Parquet | Delta |
|---|---|---|
| ACID | n | y |
| Time travel | n | y |
| Schema evolution | manual | built-in |
| MERGE | n | y |
| CDF | n | y |

## Auto Loader notification mode vs directory listing

- **Notification (file events)** - uses Azure Event Grid + Storage Queue; better for high file count.
- **Directory listing** - periodic listing; simpler, less infra.

## Data quality with DLT/Lakeflow expectations

| Action | Effect |
|---|---|
| `expect` | Track failure but keep row |
| `expect_or_drop` | Drop bad row |
| `expect_or_fail` | Fail entire pipeline run |

## Materialized views vs streaming tables

- **Streaming table** - append-only; reads from streaming source.
- **Materialized view** - recomputed; depends on incrementality of source.
- Both supported in Lakeflow / DLT.

## Lakehouse Monitoring profiles

| Profile | Use |
|---|---|
| **Snapshot** | Daily quality on full table |
| **TimeSeries** | Trends over time |
| **InferenceLog** | ML model output drift |

## Workflows: notebooks vs jobs vs pipelines

| Concept | What |
|---|---|
| **Notebook** | Interactive code surface |
| **Job (Workflow)** | One or more tasks orchestrated |
| **Lakeflow pipeline** | Declarative ETL surface (can be a task in a job) |

## Asset Bundles: validate vs deploy vs run

```bash
databricks bundle validate
databricks bundle deploy -t prod
databricks bundle run my_job -t prod
```

---

[Master Index](00-MASTER-INDEX.md)
