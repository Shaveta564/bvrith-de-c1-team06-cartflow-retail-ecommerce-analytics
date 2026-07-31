# Week 04 Log — CartFlow Bronze Ingestion
**Week:** 4  
**Date range:** [31-07-2026 - 05-08-2026]  
**Team:** [P06-Cartflow / P06]  
**Project:** CartFlow (Project P06)
---
## 1. Sprint Goal
Ingest all five approved CartFlow batch sources (`orders`, `payments`, `reviews`, `sellers`, `order_items`) from the Volume into persistent Bronze Delta tables, following the Source-to-Bronze method from the Week 4 PageLoop worked example, with full technical metadata and reconciliation evidence.
---
## 2. Work Completed
| Task | Owner | Status | Evidence |
|---|---|---|---|
| Confirmed Volume access at `/Volumes/cartflow-06/default/cartflow-p06/` | [Student] | Done | Notebook Part 1 (`%fs ls`) |
| Built `orders_source` view (CSV, all-STRING schema, permissive mode) | [Student] | Done | Notebook Part 3 |
| Built `payments_source` view (CSV) | [Student] | Done | Notebook Part 4 |
| Built `reviews_source` view (CSV) | [Student] | Done | Notebook Part 5 |
| Built `sellers_source` view (JSON) | [Student] | Done | Notebook Part 6 |
| Built `order_items_source` view (Parquet, native schema) | [Student] | Done | Notebook Part 7 |
| Added `_source_file_name`, `_source_file_path`, `_ingested_at`, `_ingestion_run_id`, `_schema_version`, `_record_hash`, `_rescued_payload` to each bronze-ready view | [Student] | Done | Notebook Parts 3–7 |
| Created `bronze_cartflow_p06_orders/payments/reviews/sellers/order_items` as Delta tables | [Student] | Done | Notebook Parts 3–7, Catalog Explorer |
| Ran per-source and cross-source reconciliation (source count vs. Bronze count) | [Student] | Done | Notebook Part 8 |
| Ran controlled repeat-run test on all five tables | [Student] | Done | Notebook Part 9, `DESCRIBE HISTORY` |
---
## 3. Key Decisions
- Used `CREATE OR REPLACE TABLE ... USING DELTA` (controlled full refresh) for all five sources rather than `INSERT`/append, to avoid duplicate rows on rerun of these static batch files.
- Kept one Bronze table per source (no merging) to preserve source boundaries and simplify reconciliation, matching the PageLoop convention.
- Read `order_items.parquet` using its native Parquet schema directly, without a manual column-list or `_corrupt_record` handling, since Parquet is self-describing (unlike the CSV/JSON sources).
---
## 4. Blockers / Risks
| Blocker | Impact | Help Needed |
|---|---|---|
| [Blocker] | [Impact] | [Help needed] |
---
## 5. Evidence Added to GitHub
- `CartFlow_P06_Week04_Bronze_Ingestion.ipynb`
- [Screenshot of Catalog Explorer showing bronze_cartflow_p06_* tables]
- [Screenshot of reconciliation query results]
---
## 6. AI Transparency Note
| Question | Response |
|---|---|
| Where AI helped | Claude adapted the PageLoop Week 4 Source-to-Bronze notebook pattern to our CartFlow sources — inspecting our raw files to get exact column names, then generating matching source views, bronze-ready views with metadata/hash columns, table creation, and reconciliation cells for all five sources. |
| What we changed after AI suggestion | [Explain any table/column names, paths, or logic your team adjusted after review] |
| What we verified manually | [Explain: ran each cell ourselves, confirmed row counts reconciled, checked Catalog Explorer, confirmed the Volume path and catalog name were correct] |
| What we can explain without AI | [Explain: e.g., why we use full refresh instead of append, what the record hash is for, why Parquet doesn't need a manual schema] |
---
## 7. Next Week Preparation
- [Action]
- [Action]
