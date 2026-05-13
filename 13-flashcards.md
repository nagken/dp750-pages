# DP-750 Flashcards

> Click each card to flip.

<section class="fc-section" data-fc-title="Setup">

<div class="flashcard"><div class="fc-q">Cluster type for a workflow task?<div class="fc-a"><strong>Job cluster</strong> - ephemeral, cheaper than all-purpose.</div></div></div>

<div class="flashcard"><div class="fc-q">Access mode that supports all languages and Scala UDFs?<div class="fc-a"><strong>Single User (Assigned).</strong> Shared mode has Scala restrictions.</div></div></div>

<div class="flashcard"><div class="fc-q">Recommended automation identity?<div class="fc-a"><strong>Service principal</strong> with OAuth M2M (PATs are deprecated for prod).</div></div></div>

<div class="flashcard"><div class="fc-q">Central secret store recommendation?<div class="fc-a"><strong>Azure Key Vault-backed secret scope.</strong></div></div></div>

<div class="flashcard"><div class="fc-q">How do you sync Entra users + groups to Databricks?<div class="fc-a"><strong>SCIM provisioning</strong> at the account level.</div></div></div>

</section>

<section class="fc-section" data-fc-title="Unity Catalog">

<div class="flashcard"><div class="fc-q">3-level namespace?<div class="fc-a"><strong>catalog.schema.table</strong></div></div></div>

<div class="flashcard"><div class="fc-q">Mask SSN for non-HR users?<div class="fc-a"><strong>Column mask function</strong> using <code>is_member('hr_admins')</code>.</div></div></div>

<div class="flashcard"><div class="fc-q">Filter rows by region per user?<div class="fc-a"><strong>Row filter function</strong>.</div></div></div>

<div class="flashcard"><div class="fc-q">Share data with another company?<div class="fc-a"><strong>Delta Sharing</strong>. Provider creates a Share; recipient sees it as a catalog.</div></div></div>

<div class="flashcard"><div class="fc-q">Query Postgres without copying data?<div class="fc-a"><strong>Lakehouse Federation</strong>.</div></div></div>

<div class="flashcard"><div class="fc-q">UC object that abstracts ADLS path + identity?<div class="fc-a"><strong>External location</strong> (with a Storage credential).</div></div></div>

</section>

<section class="fc-section" data-fc-title="Process">

<div class="flashcard"><div class="fc-q">Incremental file ingestion at scale?<div class="fc-a"><strong>Auto Loader</strong> (<code>cloudFiles</code>).</div></div></div>

<div class="flashcard"><div class="fc-q">One-shot SQL batch load with skip-already-loaded?<div class="fc-a"><strong>COPY INTO.</strong></div></div></div>

<div class="flashcard"><div class="fc-q">New default clustering for Delta tables?<div class="fc-a"><strong>Liquid clustering</strong> - replaces partitioning + ZORDER.</div></div></div>

<div class="flashcard"><div class="fc-q">Auto-run OPTIMIZE + VACUUM?<div class="fc-a"><strong>Predictive Optimization.</strong></div></div></div>

<div class="flashcard"><div class="fc-q">Stream row-level changes from a Delta table?<div class="fc-a"><strong>Change Data Feed (CDF)</strong> - <code>readChangeFeed</code>.</div></div></div>

<div class="flashcard"><div class="fc-q">Drop bad rows declaratively in a Lakeflow pipeline?<div class="fc-a"><strong><code>@dlt.expect_or_drop</code></strong>.</div></div></div>

</section>

<section class="fc-section" data-fc-title="Deploy">

<div class="flashcard"><div class="fc-q">Trigger a job when a file arrives?<div class="fc-a"><strong>File-arrival trigger.</strong></div></div></div>

<div class="flashcard"><div class="fc-q">Package job + pipeline + notebook for CI/CD?<div class="fc-a"><strong>Databricks Asset Bundles</strong> - databricks.yml + targets.</div></div></div>

<div class="flashcard"><div class="fc-q">Where to query audit events?<div class="fc-a"><strong><code>system.access.audit</code></strong> system table.</div></div></div>

<div class="flashcard"><div class="fc-q">Detect data drift on a Gold table?<div class="fc-a"><strong>Lakehouse Monitoring</strong> (TimeSeries or InferenceLog profile).</div></div></div>

<div class="flashcard"><div class="fc-q">Mode for Lakeflow pipeline to keep cluster running between updates?<div class="fc-a"><strong>Development mode</strong> (Production mode is ephemeral).</div></div></div>

</section>

---

[Master Index](00-MASTER-INDEX.md)
