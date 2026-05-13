# DP-750 Hands-On Labs

> Try in Azure Databricks Premium workspace with Unity Catalog enabled.

## Foundational

1. **Create workspace + attach UC metastore** - Premium tier; bind metastore.
2. **Configure SCIM** from Microsoft Entra ID at account level.
3. **Create a service principal** + OAuth M2M secret; use for CLI auth.
4. **Set up Azure Key Vault-backed secret scope**.

## Domain 1 - Set Up

5. **Create a cluster policy** that caps node sizes + enforces tags.
6. **Provision a serverless SQL warehouse**; query a sample table.
7. **Create a pool** + assign to a cluster; observe startup time.
8. **Compare Single User and Shared cluster behavior** for Scala UDFs.

## Domain 2 - Unity Catalog

9. **Create a storage credential** (managed identity to ADLS) + external location.
10. **Create catalogs `dev`, `prod`** with schemas for sales/finance/hr.
11. **Apply a row filter** restricting users to their region.
12. **Apply a column mask** to SSN for non-HR users.
13. **Browse lineage** in Catalog Explorer; trace a downstream Gold table.
14. **Set up Delta Sharing** between two metastores (or use sample share).
15. **Configure Lakehouse Federation** to a Postgres source.

## Domain 3 - Process Data

16. **Auto Loader notebook** - ingest JSON files from a Volume into a Bronze table.
17. **COPY INTO** - bulk-load CSV with header schema inference.
18. **MERGE** - upsert from Bronze into Silver with a unique key.
19. **OPTIMIZE + Liquid clustering** - convert a partitioned table to liquid clustering.
20. **Predictive Optimization** - enable on a hot table; observe.
21. **Change Data Feed** - `readChangeFeed` from Silver into a derived table.
22. **Lakeflow Declarative Pipeline** - write a 3-table pipeline with `expect_or_drop`.

## Domain 4 - Deploy

23. **Workflow with multiple tasks** - notebook -> pipeline -> SQL -> conditional + notification.
24. **File-arrival trigger** - kick off a job when a file lands in a Volume.
25. **Asset Bundle** - `databricks bundle init` template; deploy to dev + prod targets.
26. **Set up GitHub Actions** to deploy bundle on push.
27. **Lakehouse Monitoring** - enable TimeSeries profile on a Gold table; review dashboard.
28. **Query system tables** - `system.billing.usage` (cost by workspace), `system.access.audit` (recent grants).

---

[Master Index](00-MASTER-INDEX.md)
