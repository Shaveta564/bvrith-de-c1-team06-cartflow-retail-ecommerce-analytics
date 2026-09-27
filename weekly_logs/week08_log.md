# Week 08 Log — CartFlow Power BI Dashboard

**Week:** 8  
**Date range:** 28 August 2026 – 03 September 2026  
**Team:** P06 – CartFlow  
**Project:** CartFlow – Retail & E-commerce Analytics

---

## 1. Sprint Goal

The goal of Week 8 was to hand off the approved CartFlow Gold outputs to Power BI and build the first working Commerce Overview dashboard. The work focused on connecting only approved Gold tables, validating field types and model relationships, creating business-focused KPIs and visuals, reconciling selected dashboard values with Gold outputs, and preserving the required dashboard and evidence artifacts.

---

## 2. Work Completed

| Task | Owner | Status | Evidence |
|---|---|---|---|
| Reviewed and verified the approved Week 7 Gold tables for Power BI use | Shaveta | Done | Gold source register |
| Connected the approved Gold summary tables to Power BI | Nandini | Done | Power BI model |
| Verified Power BI field data types for the Gold tables | Manasa | Done | Power BI Data/Model view |
| Removed automatically created unsafe relationships between independent Gold summary tables | Nandini | Done | Power BI model |
| Created the Commerce Overview KPI cards | Manasa | Done | `week08_powerbi_draft.png` |
| Created GMV Trend, Orders Trend and GMV by Category visuals | Manasa | Done | `week08_powerbi_draft.png` |
| Created and validated the On-Time Delivery Rate measure | Nandini | Done | Power BI dashboard |
| Created the final Commerce Overview dashboard layout | Shaveta | Done | `week08_powerbi_draft.png` |
| Reconciled Total Orders with the `agg_sales_daily` Gold table | Nandini | Done | `week08_06_measure_reconciliation.png` |
| Saved the working Power BI dashboard | Shaveta | Done | `dashboard/powerbi_dashboard.pbix` |
| Updated the Power BI dashboard README | Team | Done | `dashboard/README.md` |

---

## 3. Key Decisions

- Used only the approved CartFlow Gold outputs as Power BI sources.
- Imported the required Gold batch-summary tables:
  `agg_sales_daily`, `agg_seller_performance`, `agg_category_sales`,
  `agg_delivery_delay` and `agg_payment_review`.
- Kept the five Gold summary tables independent because their declared
  business grains are different.
- Removed automatically created relationships that were not required and
  could affect the declared Gold grain.
- Verified Power BI data types for dates, text fields, whole-number measures
  and decimal measures.
- Built the first dashboard around commerce, order, delivery and payment
  health rather than creating one visual for every Gold table.
- Used the approved Gold measures and business definitions rather than
  inventing new KPI logic.
- Reconciled the Total Orders dashboard value against its owning Gold table.
- Kept Week 9 visual refinement and insight development outside the Week 8
  scope.

---

## 4. Blockers / Risks

| Blocker / Risk | Impact | Resolution / Help Needed |
|---|---|---|
| Initial Power BI authentication/connection issue | Delayed the initial Gold-to-Power BI connection | Resolved by using the available Personal Access Token connection |
| Power BI automatically created relationships between independent Gold summary tables | Could affect the intended Gold grain and cross-table behaviour | Removed the automatically created relationships and kept the Gold tables independent |
| Dashboard KPI values need to remain consistent with Gold definitions | Incorrect measure logic could produce misleading dashboard values | Used the owning Gold tables and reconciled the Total Orders KPI against `agg_sales_daily` |
| Dashboard layout needed to present several KPIs and visuals clearly | Poor placement could reduce readability | Arranged the dashboard into KPI, trend, category and operational-health sections |

---

## 5. Evidence Added to GitHub

### Power BI Dashboard

- `dashboard/powerbi_dashboard.pbix`
- `dashboard/README.md`

### Screenshots

- Week 8 Gold source/connection evidence
- Week 8 Power BI model evidence
- Week 8 Commerce Overview dashboard screenshot
- `screenshots/week08_06_measure_reconciliation.png`

### Weekly Log

- `weekly_logs/week08_log.md`

---

## 6. AI Transparency Note

| Question | Response |
|---|---|
| Where AI helped | AI was used to explain the Week 8 Power BI requirements, guide the Gold-to-Power BI connection, explain data-type and relationship checks, assist with dashboard visual selection and layout, and help prepare the README and weekly log. |
| What we changed after AI suggestion | The team manually reviewed and applied the suggestions, including selecting the approved Gold tables, removing automatically created relationships, creating dashboard measures and visuals, arranging the dashboard, and updating the project documentation. |
| What we verified manually | Verified the approved Gold tables, declared grains, Power BI field data types, relationships, dashboard KPI values, PBIX file, README content and Total Orders reconciliation against `agg_sales_daily`. |
| What we can explain without AI | We can explain why Power BI uses only approved Gold outputs, why the Gold summary tables remain independent, what each dashboard KPI represents, how the dashboard visuals are connected to their owning Gold tables, and how the Total Orders reconciliation was performed. |

---

## 7. Next Week Preparation

- Continue using the completed Week 8 PBIX as the starting point for Week 9.
- Review and refine dashboard visual hierarchy, labels, layout and usability.
- Test slicers, filters and visual interactions where appropriate.
- Reconcile important final presentation values under the relevant filter
  state.
- Prepare evidence-backed dashboard insights and limitations for Week 9.
- Keep the existing Gold-only Power BI model stable while refining the
  dashboard.
