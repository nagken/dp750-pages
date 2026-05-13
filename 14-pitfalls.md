# DP-750 Pitfalls and Gotchas

## 1. Hive Metastore tables are NOT Unity Catalog

You must migrate (or use UC Sync). Hive Metastore is legacy.

## 2. Single User mode vs Shared mode

Shared mode has restrictions on Scala, init scripts, certain Spark conf overrides. Use Single User if you hit a wall.

## 3. PATs deprecated for production

Use service principals with OAuth M2M, not personal access tokens.

## 4. DBFS root for sensitive data is bad

Use Volumes or external locations with proper UC permissions instead.

## 5. MERGE without unique key = non-deterministic

Always identify a unique key (or use `WHEN NOT MATCHED BY SOURCE` carefully).

## 6. VACUUM with `RETAIN 0 HOURS` breaks time travel

Default 7-day floor exists for a reason. Override only if you understand consequences.

## 7. Photon costs more DBUs

Toggle ON when CPU-bound (SQL aggs / scans); leave OFF for tiny jobs / heavy Python UDFs.

## 8. Auto Loader checkpoint location is sacred

Don't share between streams; deleting the checkpoint loses ingestion state.

## 9. DLT/Lakeflow tables can only be modified by the pipeline

External SQL UPDATE/DELETE on a DLT-managed table will fail or be overwritten on next run.

## 10. Default catalog != workspace's default schema

Set both: `USE CATALOG prod; USE SCHEMA sales;` to drop 3-part names.

## 11. Cluster access mode sets feature limitations

For UDFs, mounts, init scripts - check access mode compatibility BEFORE building.

## 12. `mergeSchema=true` doesn't promote nullability changes

Adding NOT NULL to existing column requires explicit ALTER, not auto-evolve.

## 13. Streaming with stateful aggregations needs watermarks

Without watermark, state grows indefinitely -> OOM.

## 14. `OPTIMIZE` doesn't reorganize partitions automatically

Use Liquid clustering or `OPTIMIZE ZORDER BY`.

## 15. Asset Bundles need targets

Without `-t <target>` deploy uses the default target. Always be explicit.

## 16. Workflow file-arrival trigger requires UC volumes / external locations

Doesn't work on plain DBFS root.

## 17. Lakehouse Federation has read-only behavior

You cannot write to federated tables; treat them as virtual SELECT sources.

## 18. Delta Sharing recipient sees a Catalog, not a workspace

Permissions on the share are different from workspace ACLs.

## 19. Lakehouse Monitoring costs DBUs

Profiles run on a schedule; review metrics tables and dashboard refresh frequency.

## 20. Service principal OAuth requires admin onboarding

A user can't simply "add a service principal" without account-level admin rights.

---

[Master Index](00-MASTER-INDEX.md)
