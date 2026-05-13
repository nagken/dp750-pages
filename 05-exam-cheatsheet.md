# DP-750 Exam Cheatsheet

> Print-friendly. The 60-second reset.

## The 4 domains (25% each)

| Domain | Key topics |
|---|---|
| Set Up + Configure | Workspaces, clusters, SQL warehouses, networking, identity, secrets |
| Secure + Govern Unity Catalog | Catalog/schema/table, grants, row filters, column masks, lineage, Delta Sharing |
| Prepare + Process Data | Spark SQL, PySpark, Auto Loader, COPY INTO, Delta, OPTIMIZE/ZORDER, Liquid clustering, MERGE, DLT/Lakeflow |
| Deploy + Maintain | Workflows, Lakeflow pipelines, Asset Bundles CI/CD, monitoring, cost |

## Compute decision

| Need | Pick |
|---|---|
| Notebook iteration | All-purpose interactive |
| Workflow task | Job cluster (cheaper) |
| BI / SQL queries | SQL warehouse (serverless preferred) |
| Fast cluster startup | Pool or serverless |
| Per-user isolation + Scala UDFs | Single User access mode |
| Multi-user notebooks (SQL/Python) | Shared access mode |

## Unity Catalog mental model

- Account -> Metastore -> Catalog -> Schema -> Table / View / Volume / Function / Model.
- Storage credentials + external locations decouple cloud auth from per-table config.
- Grants required at every level: USE CATALOG, USE SCHEMA, then SELECT / MODIFY.

## Ingestion pattern picker

| Pattern | When |
|---|---|
| Auto Loader (cloudFiles) | Continuous file ingestion at scale |
| COPY INTO | One-shot SQL load with idempotency |
| Structured Streaming readStream | Kafka / Event Hubs |
| Lakehouse Federation | Query OLTP DB without moving data |

## Delta + table maintenance

- **OPTIMIZE** = compact small files.
- **OPTIMIZE ... ZORDER BY** = cluster by columns.
- **Liquid clustering** (preferred for new tables) replaces partitioning + ZORDER.
- **VACUUM** = delete old versions (default 7 day retention floor).
- **Predictive Optimization** = auto OPTIMIZE + VACUUM.
- **Change Data Feed** = read row-level changes between versions.
- **MERGE** = upsert + delete in one go (need unique key).

## Lakeflow / DLT essentials

- `@dlt.table` declares a table.
- Expectations: `expect`, `expect_or_drop`, `expect_or_fail`.
- Triggered vs Continuous mode.
- Development vs Production mode.
- Pipeline event log as Delta table.

## CI/CD

- **Databricks Asset Bundles** (databricks.yml) = bundle of jobs/pipelines/notebooks.
- Targets per env (dev/prod) override variables.
- Deploy with `databricks bundle deploy -t <env>`.
- Service principal auth (OAuth) for CI/CD.

## Question-pattern translator

| Wording | Answer |
|---|---|
| "incremental file ingestion at scale" | Auto Loader |
| "SQL one-shot batch load with skip-already-loaded" | COPY INTO |
| "row-level filter for non-HR users" | Row filter function |
| "mask SSN" | Column mask + `is_member` |
| "share Gold table with another company" | Delta Sharing |
| "query Postgres in place" | Lakehouse Federation |
| "cluster cluster cluster on column for filtering" | Liquid clustering (preferred) or ZORDER |
| "auto compact + vacuum" | Predictive Optimization |
| "package CI/CD" | Asset Bundles |
| "kick off job when file lands" | File-arrival trigger |
| "automation identity" | Service principal (OAuth) |
| "central secrets" | Azure Key Vault-backed secret scope |

## 60-second reset

1. Workspace + Account + Metastore + Catalog/Schema/Table.
2. Compute: All-purpose / Job / SQL warehouse / Pool. Access modes: Single User / Shared.
3. UC: storage credential + external location + grants + row/column security + lineage + Delta Sharing.
4. Ingestion: Auto Loader (default scale), COPY INTO (one-shot SQL), Structured Streaming (events), Lakehouse Federation (in place).
5. Delta: ACID, time travel, MERGE, OPTIMIZE, ZORDER, Liquid clustering, VACUUM, Predictive Optimization, CDF.
6. Lakeflow Declarative Pipelines (DLT): expectations, Triggered/Continuous, Dev/Prod.
7. Workflows: tasks, triggers (file arrival / continuous), notifications, alerts.
8. CI/CD: Asset Bundles + targets + service principal.
9. Monitoring: workflows UI + system tables + Lakehouse Monitoring.

---

[Master Index](00-MASTER-INDEX.md)
