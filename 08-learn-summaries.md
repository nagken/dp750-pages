# DP-750 Learn Summaries

> Microsoft Learn summaries grouped by domain.

## Domain 1 - Set Up and Configure

**Workspaces, compute, networking, identity, secrets.** A Databricks account hosts one Unity Catalog metastore per region and multiple workspaces. Compute comes in three flavors: all-purpose interactive clusters (for notebooks), job clusters (ephemeral, cheaper, for Workflows), and SQL warehouses (Databricks SQL - serverless preferred for fast startup). Pools provide pre-warmed instances. Access modes are Single User (all languages, all features), Shared (multi-user, restricted Scala / init scripts), and No Isolation Shared (legacy, not recommended). Networking patterns include managed VNet (default), VNet injection, Private Link, and No Public IP. Identity is managed at the Databricks account level via SCIM provisioning from Microsoft Entra ID; service principals (OAuth M2M) are the recommended automation identity, with PATs deprecated for production. Secrets live in Databricks-backed scopes or Azure Key Vault-backed scopes (preferred). External locations + storage credentials replace DBFS for Unity-Catalog-managed external paths to ADLS.

## Domain 2 - Secure and Govern Unity Catalog Objects

**3-level namespace and fine-grained access.** Unity Catalog uses `catalog.schema.table`. Storage credentials wrap Azure managed identities (or service principals) with rights to ADLS; external locations bind a path to a credential. Managed tables let Unity Catalog own storage; external tables sit at user-specified paths. Grants required at every level (USE CATALOG -> USE SCHEMA -> SELECT/MODIFY/EXECUTE/READ VOLUME etc.). Fine-grained access uses row filters (SQL function returning boolean), column masks (function returning masked value, often combined with `is_member()`), and dynamic views. Lineage is automatic at table and column level for Delta tables, viewable in Catalog Explorer and queryable via system tables. Lakehouse Federation lets you query Postgres / MySQL / BigQuery / Snowflake as Unity Catalog tables. Delta Sharing is the open protocol for sharing data with other organizations; the provider creates a Share, the recipient sees it as a catalog.

## Domain 3 - Prepare and Process Data

**Spark SQL, PySpark, Delta, ingestion patterns.** The medallion architecture (Bronze -> Silver -> Gold) is canonical. Auto Loader (`cloudFiles`) is the scalable incremental file ingestion path with schema inference and evolution; COPY INTO is the one-shot SQL alternative with idempotency. Structured Streaming handles Kafka / Event Hubs. Delta Lake provides ACID, time travel, schema enforcement, MERGE (upsert + delete with a unique key), Change Data Feed, OPTIMIZE (compact), ZORDER (cluster by columns), Liquid clustering (replaces partitioning + ZORDER for new tables), VACUUM (clean tombstones, default 7-day floor), and Predictive Optimization (auto OPTIMIZE + VACUUM). Watermarks handle late streaming data. Lakeflow Declarative Pipelines (formerly Delta Live Tables / DLT) provides declarative ETL with expectations (`expect`, `expect_or_drop`, `expect_or_fail`), automatic checkpointing, and triggered or continuous modes.

## Domain 4 - Deploy and Maintain Pipelines and Workloads

**Workflows, Lakeflow pipelines, CI/CD, monitoring.** Workflows orchestrate notebooks, Python scripts, wheels, JARs, SQL, dbt, and Lakeflow pipelines as tasks; triggers include manual, schedule (cron), file arrival, and continuous. Lakeflow pipelines run in Triggered (one-shot) or Continuous mode; Development mode keeps the cluster around for iteration, Production mode tears it down. Databricks Asset Bundles package jobs, pipelines, and notebooks with environment-targeted YAML; `databricks bundle deploy -t prod` promotes via service principal OAuth. Source control via Databricks Repos integrates with Azure DevOps, GitHub, GitLab. Monitoring uses the Workflows UI, cluster event logs, Lakeflow event log (Delta table), system tables (`system.access.audit`, `system.billing.usage`), and Lakehouse Monitoring (Snapshot / TimeSeries / InferenceLog). Cost levers: job clusters over all-purpose, spot instances with on-demand fallback, autoscaling with sensible min, cluster policies, Photon when CPU-bound, Predictive Optimization, and tag-based chargeback.

---

[Master Index](00-MASTER-INDEX.md)
