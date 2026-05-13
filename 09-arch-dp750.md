# DP-750 Architectures

## 1. Workspace + account topology

```mermaid
flowchart TB
    Entra[Microsoft Entra ID]
    Entra -- SCIM --> Account[Databricks account]
    Account --> Meta[Unity Catalog metastore<br/>per region]
    Account --> WS1[Workspace dev]
    Account --> WS2[Workspace prod]
    Meta --> Cat1[Catalog dev]
    Meta --> Cat2[Catalog prod]
    Cat1 --> Sch1[Schema sales]
    Cat2 --> Sch2[Schema sales]
```

## 2. Storage credentials + external locations

```mermaid
flowchart LR
    MI[Azure Managed Identity]
    MI --> Cred[Storage credential]
    Cred --> Loc[External location:<br/>abfss://container@account.dfs.core.windows.net]
    Loc --> Tab[External tables / volumes]
    Loc --> AL[Auto Loader source]
```

## 3. Medallion + Lakeflow pipeline

```mermaid
flowchart LR
    Land[Landing<br/>Volume]
    Land --> AL[Auto Loader]
    AL --> Br[Bronze<br/>append]
    Br --> Si[Silver<br/>cleansed]
    Si --> Go[Gold<br/>aggregated]
    Br --> Exp1["Expectations: not null"]
    Si --> Exp2["Expectations: amount > 0"]
    Go --> BI[BI / ML / serving]
```

## 4. Workflows orchestration

```mermaid
flowchart LR
    Trigger[File-arrival trigger]
    Trigger --> Job[Workflow job]
    Job --> T1[Task 1: ingest notebook]
    T1 --> T2[Task 2: Lakeflow pipeline]
    T2 --> T3[Task 3: SQL aggregation]
    T3 --> T4[Task 4: dbt project]
    T4 --> Notif[Email + webhook]
```

## 5. CI/CD with Asset Bundles

```mermaid
flowchart LR
    Repo[GitHub repo:<br/>databricks.yml + src/]
    Repo --> CI[GitHub Actions]
    CI -- "validate + deploy -t dev" --> Dev[Dev workspace]
    CI -- "deploy -t prod" --> Prod[Prod workspace]
    SP[Service principal] -.-> CI
```

## 6. Row-level security pattern

```mermaid
flowchart LR
    User[User in HR group]
    User --> Q[SELECT * FROM employees]
    Q --> Filt[Row filter:<br/>region = current_user_region]
    Q --> Mask[Column mask on SSN]
    Filt --> Result[Filtered + masked rows]
    Mask --> Result
```

## 7. Lakehouse Monitoring + system tables

```mermaid
flowchart LR
    Tab[Gold table] --> LM[Lakehouse Monitoring]
    LM --> Profile[Profile: Snapshot / TimeSeries / InferenceLog]
    Profile --> Dash[Auto-generated dashboard]
    Sys[system.access.audit] --> Sec[Security audit]
    Sys2[system.billing.usage] --> Cost[Cost dashboard]
```

## 8. Multi-region DR

```mermaid
flowchart LR
    Reg1[Primary region]
    Reg1 --> WS1[Workspace + metastore]
    WS1 --> ADLS1[ADLS Gen2 RA-GRS]
    ADLS1 -. async replication .-> ADLS2[Secondary ADLS]
    Reg2[Secondary region]
    Reg2 --> WS2[Standby workspace]
    ADLS2 --> WS2
```

---

[Master Index](00-MASTER-INDEX.md)
