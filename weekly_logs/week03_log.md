# Week 03 Log — CartFlow Data Exploration

**Week:** 3  
**Date range:** 24 July 2026 – 30 July 2026  
**Team:** 06  
**Project:** CartFlow – Retail & E-commerce Analytics

---

## 1. Sprint Goal

The goal of Week 3 was to explore and profile the approved CartFlow source datasets in Databricks, understand their schemas and business grains, identify initial data-quality signals, validate relationships between datasets, and demonstrate potential join multiplication before beginning Bronze ingestion.

---

## 2. Work Completed

| Task | Status | Evidence |
|---|---|---|
| Loaded and verified the approved CartFlow source files | Done | `week03_01_source_inventory.png` |
| Inspected schemas and business grains of the source datasets | Done | `week03_02_schemas_counts.png` |
| Calculated source row counts and distinct business-key counts | Done | `week03_02_schemas_counts.png` |
| Profiled NULL/blank values in important fields | Done | Notebook |
| Checked primary/business-key uniqueness and domain values | Done | `week03_03_key_uniqueness_domains.png` |
| Tested referential integrity using anti-joins | Done | `week03_04_referential_integrity.png` |
| Analysed child-record relationships by `order_id` | Done | Notebook |
| Demonstrated unsafe raw-join fan-out/multiplication | Done | `week03_05_fanout_safe_aggregation.png` |
| Demonstrated safe independent child aggregation before joining | Done | `week03_05_fanout_safe_aggregation.png` |

---

## 3. Key Decisions

- Used the approved CartFlow source files as the basis for Week 3 exploration.
- Kept the analysis focused on source-data profiling and relationship testing.
- Used `order_id` as the main parent grain for analysing child relationships.
- Tested item, payment and review relationships before performing combined analysis.
- Demonstrated that raw joining multiple child datasets can multiply records and distort measures.
- Used independent aggregation of child datasets before joining them at the `order_id` grain as the safe approach.
- Bronze ingestion, Silver transformations, Data Quality, Trusted/Quarantine and Gold processing were kept for their respective weeks.

---

## 4. Blockers / Risks

| Blocker / Risk | Impact | Resolution / Help Needed |
|---|---|---|
| Potential join multiplication when combining order items, payments and reviews | Can produce duplicated records and incorrect aggregated values | Tested fan-out explicitly and used independent child aggregation before joining |
| Possible unresolved references between parent and child datasets | Can affect relationship analysis and later transformations | Performed referential-integrity anti-join checks and recorded the results |

---

## 5. Evidence Added to GitHub

### Notebook

- `notebooks/01_data_exploration.ipynb`

### Screenshots

- `screenshots/week03_01_source_inventory.png`
- `screenshots/week03_02_schemas_counts.png`
- `screenshots/week03_03_key_uniqueness_domains.png`
- `screenshots/week03_04_referential_integrity.png`
- `screenshots/week03_05_fanout_safe_aggregation.png`

### Weekly Log

- `weekly_logs/week03_log.md`

---

## 6. AI Transparency Note

| Question | Response |
|---|---|
| Where AI helped | AI was used to explain Spark/PySpark concepts, data profiling approaches, relationship checks, anti-joins, and join fan-out analysis. |
| What we changed after AI suggestion | Reviewed and refined the exploration queries, relationship checks, and safe aggregation approach to match the CartFlow Week 3 requirements. |
| What we verified manually | Source availability, schemas, row counts, distinct keys, uniqueness checks, domain values, anti-join results, child-record relationships, and fan-out behaviour were reviewed manually in the Databricks notebook. |
| What we can explain without AI | We can explain the source dataset grains, business keys, referential-integrity checks, why raw child joins can multiply records, and why independent aggregation is safer before joining at order level. |

---

## 7. Next Week Preparation

- Use the approved source files and Week 3 findings as the basis for Week 4 Bronze ingestion.
- Build one Bronze Delta table for each approved source.
- Preserve raw source values during Bronze ingestion.
- Add the required ingestion metadata and lineage information.
- Validate source-to-Bronze reconciliation and rerun behaviour.
