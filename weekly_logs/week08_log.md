# Week 08 Log — CartFlow Power BI Dashboard

**Week:** 8  
**Date range:** 28 August 2026 – 03 September 2026  
**Team:** P06 – CartFlow  
**Project:** CartFlow – Retail & E-commerce Analytics

---

## 1. Sprint Goal

The goal of Week 8 was to hand off the approved CartFlow Gold outputs to Power BI and build the first working Commerce Overview dashboard.

The work focused on validating the approved Gold batch-summary tables, confirming their declared grains and required fields, completing the controlled Gold-to-Power BI hand-off, validating row counts and selected business measures, confirming repeat-run stability, connecting only approved Gold tables to Power BI, building the first working dashboard, reconciling selected dashboard values to their owning Gold tables, and preserving the required evidence and documentation.

---

## 2. Work Completed

| Task | Owner | Status | Evidence |
|---|---|---|---|
| Reviewed and verified the approved Week 7 Gold tables for Power BI use | Shaveta | Done | `week08_01_gold_inventory.png` |
| Validated the five approved Gold tables and their declared grains | Shaveta | Done | `week08_01_gold_inventory.png` |
| Validated required columns for all approved Gold tables | Shaveta | Done | `week08_02_column_validation.png` |
| Validated grain/key uniqueness and null/blank key checks | Shaveta | Done | `week08_03_grain_key_validation.png` |
| Reconciled Gold-to-hand-off row counts for all five Gold tables | Shaveta | Done | `week08_04_handoff_reconciliation.png` |
| Re-ran the Gold business fingerprint check and confirmed unchanged results | Shaveta | Done | `week08_05_repeat_run_fingerprint.png` |
| Connected the approved Gold summary tables to Power BI | Nandini | Done | `week08_06_powerbi_dashboard.png` |
| Verified Power BI field data types for the Gold tables | Manasa | Done | Power BI Data/Model view |
| Removed automatically created unsafe relationships between independent Gold summary tables | Nandini | Done | Power BI model |
| Created the Commerce Overview KPI cards | Manasa | Done | `week08_06_powerbi_dashboard.png` |
| Created GMV Trend, Orders Trend and GMV by Category visuals | Manasa | Done | `week08_06_powerbi_dashboard.png` |
| Created and validated the On-Time Delivery Rate measure | Nandini | Done | Power BI dashboard |
| Created the final Commerce Overview dashboard layout | Shaveta | Done | `week08_06_powerbi_dashboard.png` |
| Reconciled Total Orders with the `agg_sales_daily` Gold table | Nandini | Done | `week08_07_measure_reconciliation.png` |
| Saved the working Power BI dashboard | Shaveta | Done | `dashboard/powerbi_dashboard.pbix` |
| Updated the Power BI dashboard README | Team | Done | `dashboard/README.md` |
| Preserved Week 8 execution and dashboard evidence | Team | Done | `screenshots/week08_*` |

---

## 3. Key Decisions

- Used only the approved CartFlow Gold outputs as Power BI sources.
- Used the following five approved Gold batch-summary tables:
  `agg_sales_daily`, `agg_seller_performance`, `agg_category_sales`,
  `agg_delivery_delay` and `agg_payment_review`.
- Kept the five Gold summary tables independent because their declared
  business grains and keys are different.
- Removed automatically created relationships that were not required and
  could affect the declared Gold grain.
- Did not create a combined master Gold table.
- Verified required columns, grain/key uniqueness and null/blank key checks
  before treating the Gold hand-off as complete.
- Verified Gold-to-hand-off row-count reconciliation for all five tables.
- Confirmed repeat-run business fingerprints remained unchanged.
- Verified Power BI data types for dates, text fields, whole-number measures
  and decimal measures.
- Built the first dashboard around commerce, order, delivery and payment
  health rather than creating one visual for every Gold table.
- Used approved Gold measures and business definitions rather than
  introducing unsupported KPI logic.
- Reconciled the Total Orders dashboard value against its owning
  `agg_sales_daily` Gold table.
- Preserved the Gold-only Power BI source boundary.
- Kept Week 9 visual refinement and insight development outside the Week 8
  scope.

---

## 4. Blockers / Risks

| Blocker / Risk | Impact | Resolution / Help Needed |
|---|---|---|
| Initial Power BI authentication/connection issue | Delayed the initial Gold-to-Power BI connection | Resolved by using the available Personal Access Token connection |
| Power BI automatically created relationships between independent Gold summary tables | Could affect the intended Gold grain and cross-table behaviour | Removed the automatically created relationships and kept the Gold tables independent |
| Dashboard KPI values needed to remain consistent with Gold definitions | Incorrect measure logic could produce misleading dashboard values | Used the owning Gold tables and reconciled the Total Orders KPI against `agg_sales_daily` |
| Dashboard layout needed to present several KPIs and visuals clearly | Poor placement could reduce readability | Arranged the dashboard into KPI, trend, category and operational-health sections |
| Gold hand-off required repeat-run stability evidence | Without repeat-run evidence, reproducibility could not be demonstrated | Re-ran the business fingerprint check and confirmed unchanged row counts and fingerprints |

---

## 5. Evidence Added to GitHub

### Notebook

- `notebooks/06_powerbi_export.ipynb`

### Power BI Dashboard

- `dashboard/powerbi_dashboard.pbix`
- `dashboard/README.md`

### Screenshots

- `screenshots/week08_01_gold_inventory.png`
- `screenshots/week08_02_column_validation.png`
- `screenshots/week08_03_grain_key_validation.png`
- `screenshots/week08_04_handoff_reconciliation.png`
- `screenshots/week08_05_repeat_run_fingerprint.png`
- `screenshots/week08_06_powerbi_dashboard.png`
- `screenshots/week08_07_measure_reconciliation.png`

### Weekly Log

- `weekly_logs/week08_log.md`

---

## 6. AI Transparency Note

| Question | Response |
|---|---|
| Where AI helped | AI was used to explain the Week 8 Power BI requirements, guide the Gold-to-Power BI hand-off, explain data-type and relationship checks, assist with dashboard visual selection and layout, help with validation and reconciliation steps, and assist in preparing the README and weekly log. |
| What we changed after AI suggestion | The team manually reviewed and applied the suggestions, including selecting the approved Gold tables, validating Gold grains and keys, removing automatically created relationships, creating dashboard measures and visuals, arranging the dashboard, performing reconciliation checks, and updating the project documentation. |
| What we verified manually | Verified the approved Gold tables, declared grains, required columns, key uniqueness, null/blank key checks, row-count reconciliation, repeat-run fingerprints, Power BI field data types, relationships, dashboard KPI values, PBIX file, README content and Total Orders reconciliation against `agg_sales_daily`. |
| What we can explain without AI | We can explain why Power BI uses only approved Gold outputs, why the five Gold summary tables remain independent, what each dashboard KPI represents, how the dashboard visuals are connected to their owning Gold tables, how the Gold hand-off was validated, and how the Total Orders reconciliation was performed. |

---

## 7. Next Week Preparation

- Continue using the completed Week 8 PBIX as the starting point for Week 9.
- Review and refine dashboard visual hierarchy, labels, layout and usability.
- Test slicers, filters and visual interactions where appropriate.
- Reconcile important final presentation values under the relevant filter
  state.
- Prepare evidence-backed dashboard insights and limitations for Week 9.
- Create and maintain `docs/dashboard_insights.md` as part of the Week 9
  refinement and insight work.
- Keep the existing Gold-only Power BI model stable while refining the
  dashboard.
- Preserve the existing Gold source definitions and traceability while
  making Week 9 presentation changes.
