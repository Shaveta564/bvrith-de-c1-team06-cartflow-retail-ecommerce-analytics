# Week 02 Log — Dataset Design & Data Dictionary

**Week:** 2  
**Date range:** 17 July 2026 – 23 July 2026  
**Team:** Team 06  
**Project:** CartFlow – Retail & E-Commerce Analytics

---

## 1. Sprint Goal

Design and document the project datasets by defining source files, schemas, keys, and assumptions. Prepare the project for the Bronze ingestion stage by documenting the data structure and organizing GitHub-safe sample datasets.

---

## 2. Work Completed

| Task | Owner | Status | Evidence |
|---|---|---|---|
| Prepared Data Dictionary for source datasets | Team | Done | `docs/data_dictionary.md` |
| Documented synthetic data assumptions | Team | Done | `docs/synthetic_data_assumptions.md` |
| Verified source datasets and relationships | Team | Done | Project documentation |
| Added GitHub-safe raw sample datasets | Team | Done | `data_sample/raw/` |
| Reviewed project folder structure | Team | Done | GitHub repository |

---

## 3. Key Decisions

- Used the official CartFlow source datasets as the basis for all documentation.
- Stored only GitHub-safe sample datasets instead of the complete dataset to keep the repository lightweight and compliant with project guidelines.

---

## 4. Blockers / Risks

| Blocker | Impact | Help Needed |
|---|---|---|
| No major blockers encountered during Week 2 | Low | None |

---

## 5. Evidence Added to GitHub

- Updated `docs/data_dictionary.md`
- Updated `docs/synthetic_data_assumptions.md`
- Added sample datasets under `data_sample/raw/`
- Updated `weekly_logs/week02_log.md`

---

## 6. AI Transparency Note

| Question | Response |
|---|---|
| Where AI helped | AI assisted in improving the structure, formatting, and completeness of the documentation. |
| What we changed after AI suggestion | Added clearer dataset descriptions, documented relationships, and refined assumptions to better align with the project documentation. |
| What we verified manually | Verified dataset names, schemas, keys, and project requirements against the official CartFlow Starter Brief and Project Playbook. |
| What we can explain without AI | The dataset structure, source files, relationships, documentation decisions, and the purpose of each dataset in the CartFlow pipeline. |

---

## 7. Next Week Preparation

- Load the source datasets into Databricks and perform initial data profiling.
- Verify schemas, row counts, null values, and relationships before starting the Bronze layer.
