# Week 06 Log — CartFlow Data Quality, Trusted & Quarantine

**Week:** 6  
**Date range:** 14 August 2026 – 20 August 2026  
**Team:** P06 – CartFlow  
**Project:** CartFlow – Retail & E-commerce Analytics

---

## 1. Sprint Goal

The goal of Week 6 was to apply the approved CartFlow Data Quality rules to the Silver Candidate tables. Failed records were identified and routed to the appropriate Quarantine tables, while valid records were routed to Trusted Silver with complete DQ status, failure and lineage metadata.

---

## 2. Work Completed

| Task | Status | Evidence |
|---|---|---|
| Read the Silver Candidate tables produced in Week 5 | Done | `week06_01_candidate_readiness.png` |
| Implemented the approved CartFlow DQ rules for Orders, Order Items, Payments, Sellers and Reviews | Done | Notebook |
| Evaluated each approved rule using PASS/FAIL results | Done | `week06_02_dq_rule_results.png` |
| Routed valid records to Trusted Silver and failed records to Quarantine | Done | `week06_03_trusted_quarantine.png` |
| Added DQ status, failed rule IDs, failure reasons, severity, affected fields and lineage metadata | Done | `week06_04_dq_metadata.png` |
| Validated Trusted + Quarantine reconciliation and zero intersection | Done | `week06_05_reconciliation_replay.png` |
| Documented the correction/replay approach for quarantined records | Done | Notebook |

---

## 3. Key Decisions

- Used the Silver Candidate tables as the only inputs for Week 6 Data Quality processing.
- Applied the approved CartFlow DQ rule IDs and their defined severities.
- Routed each physical Candidate record to either Trusted Silver or Quarantine.
- Preserved failed records in Quarantine rather than deleting or silently correcting them.
- Added DQ metadata to make failures traceable to the applicable rule and source record.
- Applied the approved dependency order: Orders → Sellers → Order Items → Payments → Reviews.
- Used independent item and payment aggregation when performing payment/item reconciliation to avoid join fan-out.
- Used reconciliation to verify that Trusted and Quarantine records account for the Candidate records without overlap.
- Corrections and replay were treated as a controlled process; existing Quarantine records were not directly edited.

---

## 4. Blockers / Risks

| Blocker / Risk | Impact | Resolution / Help Needed |
|---|---|---|
| Some Candidate records may fail multiple DQ rules | Can make failure reasons and routing difficult to interpret | Recorded all applicable failed rule IDs and failure reasons for each affected record |
| Payment and item totals can be affected by join multiplication | Can produce incorrect reconciliation results | Aggregated payments and items independently before reconciliation |
| Invalid or unresolved reference records can affect dependent entities | Can affect downstream DQ processing | Applied the approved dependency order and reference checks |

---

## 5. Evidence Added to GitHub

### Notebook

- `notebooks/04_data_quality_checks.ipynb`

### Screenshots

- `screenshots/week06_01_candidate_readiness.png`
- `screenshots/week06_02_dq_rule_results.png`
- `screenshots/week06_03_trusted_quarantine.png`
- `screenshots/week06_04_dq_metadata.png`
- `screenshots/week06_05_reconciliation_replay.png`

### Documentation

- `docs/data_quality_summary.md`

### Weekly Log

- `weekly_logs/week06_log.md`

---

## 6. AI Transparency Note

| Question | Response |
|---|---|
| Where AI helped | AI was used to explain DQ rule implementation, PASS/FAIL evaluation, quarantine routing, DQ metadata, reconciliation and correction/replay concepts. |
| What we changed after AI suggestion | Updated the rule conditions, rule IDs, entity names, table names, dependency order and routing logic to match the approved CartFlow DQ rulebook. |
| What we verified manually | Reviewed the Candidate inputs, DQ rule results, Trusted and Quarantine routing, failure metadata, reconciliation results and replay logic in the Databricks notebook. |
| What we can explain without AI | We can explain how each DQ rule is evaluated, why records are routed to Trusted or Quarantine, how failure metadata is recorded, how Trusted and Quarantine reconciliation works, and why quarantined records must be corrected upstream and replayed. |

---

## 7. Next Week Preparation

- Use only the Trusted Silver outputs as inputs for Week 7 Gold processing.
- Review the approved Gold dimensions, facts, summary tables and KPI definitions.
- Define the required Gold table grains and business keys.
- Validate Gold aggregations against the Trusted Silver data.
