# Week 04 Log — CartFlow Bronze Ingestion

**Week:** 4  
**Date range:** 31-07-2026 – 06-08-2026  
**Team:** P06 – CartFlow  
**Project:** CartFlow (Project P06)

---

# 1. Sprint Goal

Ingest all five approved CartFlow batch sources (`orders`, `payments`, `reviews`, `sellers`, and `order_items`) from the Databricks Volume into persistent Bronze Delta tables following the Week 4 Source-to-Bronze architecture. Ensure every Bronze table contains technical metadata, supports reconciliation, and can be safely re-run without creating duplicate records.

---

# 2. Work Completed

| Task | Owner | Status | Evidence |
|------|-------|--------|----------|
| Confirmed Volume access at `/Volumes/cartflow-06/default/cartflow-p06/` | Shaveta |  Done | Notebook Part 1 (`%fs ls`) |
| Built `orders_source` view (CSV, STRING schema, permissive mode) | Manasa |  Done | Notebook Part 3 |
| Built `payments_source` view (CSV) | Nandini |  Done | Notebook Part 5 |
| Built `reviews_source` view (CSV) | Shaveta |  Done | Notebook Part 6 |
| Built `sellers_source` view (JSON) | Manasa |  Done | Notebook Part 7 |
| Built `order_items_source` view (Parquet, native schema) | Nandini |  Done | Notebook Part 4 |
| Added Bronze metadata columns (`_source_file_name`, `_source_file_path`, `_ingested_at`, `_ingestion_run_id`, `_schema_version`, `_record_hash`, `_rescued_payload`) | Shaveta |  Done | Notebook Parts 3–7 |
| Created Bronze Delta tables for all five datasets | Manasa |  Done | Catalog Explorer |
| Validated source vs Bronze row counts | Nandini |  Done | Notebook Part 8 |
| Verified repeat execution using `CREATE OR REPLACE TABLE` and `DESCRIBE HISTORY` | Shaveta |  Done | Notebook Part 9 |

---

# 3. Key Decisions

- Used `CREATE OR REPLACE TABLE ... USING DELTA` for all Bronze tables to support controlled full refreshes and prevent duplicate records during notebook reruns.
- Maintained one Bronze Delta table per source dataset to preserve source lineage and simplify reconciliation.
- Loaded the Parquet dataset (`order_items`) using its native schema because Parquet is self-describing, while CSV and JSON files required explicit ingestion handling.
- Added consistent ingestion metadata and record hashes to every Bronze table to improve traceability, auditing, and future incremental processing.

---

# 4. Blockers / Risks

| Blocker | Impact | Help Needed |
|----------|--------|-------------|
| No major blockers encountered | Bronze ingestion completed successfully | None |

---

# 5. Evidence Added to GitHub

- `02_bronze_ingestion.ipynb`
- Screenshot of Catalog Explorer showing all Bronze Delta tables
- Screenshot of reconciliation query results
- Screenshot of `DESCRIBE HISTORY` output demonstrating successful repeat-run execution

---

# 6. AI Transparency Note

| Question | Response |
|----------|----------|
| **Where AI helped** | Claude adapted the Week 4 PageLoop Source-to-Bronze notebook pattern for the CartFlow datasets by generating source views, Bronze-ready views with metadata columns, Delta table creation statements, reconciliation queries, and validation steps. |
| **What we changed after AI suggestion** | Updated the Volume path, catalog and schema names, Bronze table names, source file names, and dataset-specific column mappings to match the CartFlow project. Reviewed and adjusted the generated Spark SQL before execution. |
| **What we verified manually** | Executed every notebook cell, verified all Bronze Delta tables were created successfully, confirmed reconciliation counts matched, checked metadata columns, validated Catalog Explorer entries, and confirmed repeat-run behavior using `DESCRIBE HISTORY`. |
| **What we can explain without AI** | We understand the Bronze layer architecture, why full refresh is used for static batch data, the purpose of ingestion metadata and record hashes, how reconciliation validates successful ingestion, and why Parquet files do not require a manually defined schema. |

---

# 7. Next Week Preparation

- Implement Bronze-to-Silver transformations.
- Apply data quality validation rules and appropriate data types.
- Standardize and clean records before creating Silver Delta tables.
- Generate Silver reconciliation evidence and update project documentation.

---
