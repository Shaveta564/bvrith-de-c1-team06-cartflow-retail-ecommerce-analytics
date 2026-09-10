# Week 04 Log — CartFlow Bronze Ingestion

**Week:** 4  
**Date range:** 31 July 2026 – 06 August 2026  
**Team:** P06 – CartFlow  
**Project:** CartFlow – Retail & E-commerce Analytics

---

## 1. Sprint Goal

The goal of Week 4 was to ingest the five approved CartFlow batch source datasets from the Databricks Volume into persistent Bronze Delta tables. The Bronze layer preserves the source data while adding technical metadata and lineage information required for traceability, reconciliation, and controlled reruns.

---

## 2. Work Completed

| Task | Status | Evidence |
|---|---|---|
| Confirmed access to the approved CartFlow source files in the Databricks Volume | Done | `week04_01_source_inventory.png` |
| Created source views for orders, payments, reviews, sellers and order items | Done | Notebook |
| Applied appropriate source-format handling for CSV, JSON and Parquet files | Done | Notebook |
| Added Bronze ingestion metadata and record-hash fields | Done | `week04_02_bronze_metadata.png` |
| Created persistent Bronze Delta tables for all five approved sources | Done | `week04_03_bronze_tables.png` |
| Reconciled source record counts with Bronze record counts | Done | `week04_04_reconciliation.png` |
| Verified controlled rerun and Delta table history | Done | `week04_05_rerun_history.png` |

---

## 3. Key Decisions

- Created one persistent Bronze Delta table for each approved CartFlow source dataset.
- Preserved source business values in the Bronze layer without applying Silver-level cleaning or standardization.
- Used format-appropriate ingestion handling for CSV, JSON and Parquet sources.
- Added consistent technical metadata for source traceability and ingestion auditing.
- Added a record hash to support record-level identification and reconciliation.
- Used a controlled full-refresh approach for rerunning the Bronze ingestion notebook.
- Used source-to-Bronze reconciliation and Delta history as evidence of the ingestion and rerun process.

---

## 4. Blockers / Risks

| Blocker / Risk | Impact | Resolution / Help Needed |
|---|---|---|
| No major blockers encountered during Bronze ingestion | No significant impact on the planned Week 4 work | None |

---

## 5. Evidence Added to GitHub

### Notebook

- `notebooks/02_bronze_ingestion.ipynb`

### Screenshots

- `screenshots/week04_01_source_inventory.png`
- `screenshots/week04_02_bronze_metadata.png`
- `screenshots/week04_03_bronze_tables.png`
- `screenshots/week04_04_reconciliation.png`
- `screenshots/week04_05_rerun_history.png`

### Weekly Log

- `weekly_logs/week04_log.md`

---

## 6. AI Transparency Note

| Question | Response |
|---|---|
| **Where AI helped** | AI was used to explain Bronze ingestion patterns, source-format handling, metadata, Delta tables, reconciliation, record hashing, and rerun validation. |
| **What we changed after AI suggestion** | Updated the source paths, table names, schema handling, metadata fields, and SQL statements to match the CartFlow project requirements. |
| **What we verified manually** | Reviewed the source files, schemas, Bronze table definitions, metadata columns, reconciliation queries, and rerun/Delta history evidence in the Databricks workspace. |
| **What we can explain without AI** | We can explain why the Bronze layer preserves raw business values, the purpose of ingestion metadata and record hashes, how source-to-Bronze reconciliation works, and how a controlled rerun is validated. |

---

## 7. Next Week Preparation

- Use the completed Bronze Delta tables as the inputs for Week 5.
- Apply approved type conversions and standardization rules in the Silver layer.
- Preserve source record identifiers and ingestion lineage during Silver transformations.
- Validate Silver counts, grain, keys and transformation results.
