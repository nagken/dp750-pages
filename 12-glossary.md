# DP-750 Glossary

| Term | Meaning |
|---|---|
| **Account** | Databricks tenant-level container, hosts metastore + workspaces |
| **Asset Bundle** | YAML-based packaging of jobs/pipelines/notebooks for CI/CD |
| **Auto Loader** | `cloudFiles` source for incremental file ingestion |
| **Catalog** | Top-level Unity Catalog container |
| **Catalog Explorer** | UI for browsing catalogs/schemas/tables/lineage |
| **Change Data Feed (CDF)** | Read row-level changes between Delta versions |
| **Cluster** | Compute resources (driver + workers) |
| **Cluster policy** | Admin-defined constraints on cluster configuration |
| **Column mask** | Function returning masked value applied to a column |
| **COPY INTO** | SQL command for one-shot file load with idempotency |
| **Data Live Tables (DLT)** | Old name for Lakeflow Declarative Pipelines |
| **DBFS** | Databricks File System root (legacy) |
| **DBSQL / SQL warehouse** | Databricks SQL compute |
| **Delta Lake** | Default table format - ACID + time travel |
| **Delta Sharing** | Open protocol for sharing data |
| **External location** | Path + storage credential abstracting ADLS for UC |
| **Job cluster** | Ephemeral cluster scoped to one workflow run |
| **Lakeflow Declarative Pipelines** | Declarative ETL surface (formerly DLT) |
| **Lakehouse Federation** | Query external DBs as Unity Catalog tables |
| **Lakehouse Monitoring** | Auto data quality + drift on UC tables |
| **Liquid clustering** | New default cluster scheme; replaces partitioning + ZORDER |
| **Managed table** | Table where UC owns storage |
| **Materialized view** | Recomputed query result stored as a table |
| **MERGE** | Upsert + delete in one SQL statement |
| **Metastore** | Account-level UC catalog/schema/table registry |
| **OPTIMIZE** | Compact small files (and ZORDER) |
| **PAT** | Personal Access Token (deprecated for prod) |
| **Photon** | Vectorized C++ execution engine |
| **Pool** | Pre-warmed cluster instances |
| **Predictive Optimization** | Auto OPTIMIZE + VACUUM |
| **Repo** | Git-backed workspace folder |
| **Row filter** | Function returning boolean to filter rows per user |
| **Schema (database)** | UC second level container |
| **Service principal** | Automation identity (Entra app or Databricks-managed) |
| **Single User mode** | Cluster access mode supporting all features |
| **Shared mode** | Multi-user cluster mode with restrictions |
| **SCIM** | Provisioning protocol used to sync Entra users/groups |
| **Storage credential** | Wraps Azure managed identity with ADLS access |
| **Streaming table** | Append-only table fed by streaming source |
| **System tables** | UC-provided audit / billing / lineage tables |
| **Unity Catalog (UC)** | Cross-workspace data governance layer |
| **VACUUM** | Remove tombstoned Delta files |
| **Volume** | UC file container (managed or external) |
| **Watermark** | Late-data threshold in streaming |
| **Workflow / Job** | Orchestrated DAG of tasks |
| **ZORDER** | Multi-column clustering on top of OPTIMIZE |

---

[Master Index](00-MASTER-INDEX.md)
