# Week 07 Log — CartFlow Gold Aggregations

**Week:** 7  
**Date range:** 21 August 2026 – 27 August 2026  
**Team:** P06 – CartFlow  
**Project:** CartFlow – Retail & E-commerce Analytics

---

## 1. Sprint Goal

The goal of Week 7 was to build the CartFlow Gold layer using only Trusted Silver data. The work focused on creating approved dimensions, fact tables and batch aggregation tables with documented business grains, KPI definitions, validation checks and reconciliation evidence.

---

## 2. Work Completed

| Task | Owner | Status | Evidence |
|---|---|---|---|
| Read and verified the Week 6 Trusted Silver outputs | Shaveta | Done | `week07_01_trusted_input.png` |
| Created the approved Gold dimension tables | Nandini | Done | Notebook |
| Created the approved Gold fact tables | Manasa | Done | `week07_02_gold_dimensions_facts.png` |
| Built the approved batch Gold aggregation tables | Shaveta | Done | `week07_03_gold_aggregations.png` |
| Defined and validated the required Gold KPI calculations | Nandini | Done | `week07_04_kpi_validation.png` |
| Validated Gold grain, keys, measures and reconciliation | Manasa | Done | `week07_05_gold_validation_rerun.png` |
| Verified controlled rerun behaviour and Gold table stability | Shaveta | Done | `week07_05_gold_validation_rerun.png` |

---

## 3. Key Decisions

- Used only Trusted Silver data as the source for Gold processing.
- Did not use Candidate or Quarantine records for Gold aggregations.
- Created the approved CartFlow Gold dimensions, facts and batch summary tables.
- Defined each Gold table using an explicit business grain and key.
- Built the Gold layer around the approved KPI definitions and formulas.
- Used appropriate independent aggregation where required to prevent join multiplication.
- Validated Gold results using key, grain, measure and reconciliation checks.
- Kept Power BI dashboard development and streaming Gold outside the Week 7 scope.

---

## 4. Blockers / Risks

| Blocker / Risk | Impact | Resolution / Help Needed |
|---|---|---|
| Gold metrics depend on correct Trusted Silver inputs and table grain | Incorrect grain or joins can produce inaccurate KPIs | Validated Gold keys, grain and reconciliation |
| Multiple fact/child relationships can cause aggregation fan-out | Can inflate counts and monetary measures | Used appropriate aggregation and join-preservation checks |
| KPI calculations depend on clearly defined business rules | Ambiguous formulas can produce inconsistent metrics | Used the approved Gold KPI definitions and documented the calculations |

---

## 5. Evidence Added to GitHub

### Notebook

- `notebooks/05_gold_aggregations.ipynb`

### Documentation

- `docs/gold_metrics_definition.md`

### Screenshots

- `screenshots/week07_01_trusted_input.png`
- `screenshots/week07_02_gold_dimensions_facts.png`
- `screenshots/week07_03_gold_aggregations.png`
- `screenshots/week07_04_kpi_validation.png`
- `screenshots/week07_05_gold_validation_rerun.png`

### Weekly Log

- `weekly_logs/week07_log.md`

---

## 6. AI Transparency Note

| Question | Response |
|---|---|
| Where AI helped | AI was used to explain Gold table design, business grains, KPI aggregation, dimension/fact relationships, validation and reconciliation approaches. |
| What we changed after AI suggestion | Updated table names, source mappings, grains, KPI calculations and validation logic to match the approved CartFlow Gold model. |
| What we verified manually | Reviewed Trusted Silver inputs, Gold schemas, table grains, keys, KPI calculations, aggregation results, reconciliation checks and rerun behaviour in Databricks. |
| What we can explain without AI | We can explain why Gold reads only Trusted data, what each Gold table represents, how its grain and key are defined, how the KPIs are calculated, and how validation proves that the aggregations are reliable. |

---

## 7. Next Week Preparation

- Use the completed Gold outputs as the source for Week 8 Power BI development.
- Connect Power BI only to approved Gold tables and metrics.
- Prepare the required dashboard KPIs and visualizations.
- Verify that dashboard metrics reconcile with the validated Gold outputs.
