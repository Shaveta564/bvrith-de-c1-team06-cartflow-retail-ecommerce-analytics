# Week 09 Log — CartFlow Power BI Dashboard Refinement

**Week:** 9  
**Date range:** 04 September 2026 – 10 September 2026  
**Team:** P06 – CartFlow  
**Project:** CartFlow – Retail & E-commerce Analytics

---

## 1. Sprint Goal

The goal of Week 9 was to continue from the validated Week 8 Power BI
dashboard and complete the dashboard refinement, seller and category
analysis, supported interactions, validation and evidence-based insight
documentation.

The work focused on refining the Commerce Performance page, developing
the Seller and Category Performance page, testing supported filter
behaviour, reconciling representative dashboard values against their
owning Gold tables, improving readability and presentation, and
documenting evidence-based insights and limitations without changing the
approved Gold source boundary.

---

## 2. Work Completed

| Task | Owner | Status | Evidence |
|---|---|---|---|
| Continued from the validated Week 8 Power BI dashboard | Shaveta | Done | `dashboard/powerbi_dashboard.pbix` |
| Reviewed the existing Power BI model and confirmed the approved Gold model structure | Manasa | Done | `screenshots/week09_01_final_model.png` |
| Refined the Page 1 Commerce Performance dashboard | Shaveta | Done | `dashboard/powerbi_dashboard.pbix` |
| Added and tested the Sales Date slicer on the Commerce Performance page | Shaveta | Done | `screenshots/week09_04_filter_interaction.png` |
| Tested the Sales Date slicer using full-range and filtered date selections | Shaveta | Done | `screenshots/week09_04_filter_interaction.png` |
| Reconciled filtered Total Orders against `agg_sales_daily` Gold data | Nandini | Done | `screenshots/week09_05_filtered_gold_reconciliation.png` |
| Refined Page 2 — Seller and Category Performance | Manasa | Done | `dashboard/powerbi_dashboard.pbix` |
| Created/refined GMV by Category visual | Manasa | Done | Page 2 in PBIX |
| Created/refined Top Sellers by Order Count visual | Manasa | Done | Page 2 in PBIX |
| Created/refined Top Sellers by GMV visual | Manasa | Done | Page 2 in PBIX |
| Created/refined Seller Average Review Score visual | Manasa | Done | Page 2 in PBIX |
| Reconciled Payment Reconciliation Rate with `agg_payment_review` | Nandini | Done | `screenshots/week09_06_payment_reconciliation.png` |
| Reconciled Top Seller Order Count values with `agg_seller_performance` | Nandini | Done | `screenshots/week09_07_top_seller_validation.png` |
| Reconciled Total Orders against `agg_sales_daily` | Nandini | Done | `screenshots/week09_05_filtered_gold_reconciliation.png` |
| Reviewed dashboard readability, labels, spacing and number formatting | Shaveta | Done | Final Power BI dashboard |
| Documented dashboard insights, evidence and limitations | Team | Done | `docs/dashboard_insights.md` |
| Updated dashboard documentation and traceability | Team | Done | `dashboard/README.md` |
| Preserved Week 9 dashboard and validation evidence | Team | Done | `screenshots/week09_*` |

---

## 3. Key Decisions

- Continued using the validated Week 8 Power BI PBIX as the starting point
  for Week 9 instead of rebuilding the dashboard.
- Kept the Power BI model restricted to the five approved Gold tables:
  `agg_sales_daily`, `agg_seller_performance`, `agg_category_sales`,
  `agg_delivery_delay` and `agg_payment_review`.
- Preserved the declared business grain of each Gold summary table.
- Used the existing `DimDate` table for valid date-based filtering.
- Preserved the approved date relationships:
  `DimDate[Date]` to `agg_sales_daily[sales_date]` and
  `DimDate[Date]` to `agg_delivery_delay[purchase_date]`.
- Did not introduce unsafe relationships between independent Gold tables
  simply to force slicer cross-filtering.
- Refined Page 1 as the Commerce Performance page.
- Added and tested the Sales Date slicer using the approved date-filtering
  path.
- Developed Page 2 for seller and category performance using the approved
  seller and category Gold tables.
- Retained the existing Top Sellers by GMV visual because it provided a
  clear seller-performance view.
- Used approved Gold fields and measures rather than introducing
  unsupported KPI definitions.
- Reconciled representative dashboard values against their owning Gold
  tables.
- Verified that the filtered Total Orders value of 54,055 is displayed as
  approximately 54K in Power BI because of compact number formatting.
- Verified the Payment Reconciliation Rate of approximately 99.96% against
  the `agg_payment_review` Gold table.
- Verified the Top 10 seller order-count values against
  `agg_seller_performance`.
- Preserved the negative values present in the Gold `average_delay_days`
  field where applicable and documented the data limitation rather than
  altering the source data.
- Completed readability and presentation checks for the final two
  dashboard pages.
- Documented evidence-based insights and limitations in
  `docs/dashboard_insights.md`.
- Kept Week 10 streaming/live-data implementation outside the Week 9
  scope.

---

## 4. Blockers / Risks

| Blocker / Risk | Impact | Resolution / Help Needed |
|---|---|---|
| Gold summary tables have different business grains and do not all share a common safe filtering path | Sales Date filtering does not cross-filter every visual on the dashboard | Preserved the approved model structure and documented the expected filter behaviour |
| Power BI compact number formatting displays large values in abbreviated form | Exact reconciliation values are not directly visible on KPI cards | Verified exact values against Gold SQL results and documented the reconciliation |
| `average_delay_days` contains negative values in the supplied Gold data | Delivery-delay values require careful interpretation | Preserved the approved Gold values and documented the limitation rather than changing the source |
| Dashboard contains multiple analysis areas across two pages | Required clear visual hierarchy and readable presentation | Refined page layouts, titles, labels, spacing and visual formatting |
| Representative dashboard values required validation after refinement | Incorrect presentation or measure configuration could produce inconsistent results | Reconciled Total Orders, Payment Reconciliation Rate and Top Seller values against Gold data |

---

## 5. Evidence Added to GitHub

### Power BI Dashboard

- `dashboard/powerbi_dashboard.pbix`
- `dashboard/README.md`

The final PBIX contains:

- Page 1 — Commerce Performance
- Page 2 — Seller and Category Performance

### Dashboard Insights

- `docs/dashboard_insights.md`

### Screenshots

- `screenshots/week09_01_final_model.png`
- `screenshots/week09_02_page1_commerce_overview.png`
- `screenshots/week09_03_page2_seller_category.png`
- `screenshots/week09_04_filter_interaction.png`
- `screenshots/week09_05_filtered_gold_reconciliation.png`
- `screenshots/week09_06_payment_reconciliation.png`
- `screenshots/week09_07_top_seller_validation.png`

### Weekly Log

- `weekly_logs/week09_log.md`

### Notebook

- `notebooks/06_powerbi_export.ipynb` — reused as the existing
  Gold-to-Power BI hand-off and validation notebook. No separate Week 9
  Power BI export notebook was created.

---

## 6. AI Transparency Note

| Question | Response |
|---|---|
| Where AI helped | AI was used to assist with Week 9 Power BI dashboard refinement, page structure, visual presentation, DAX guidance, filter-interaction testing, reconciliation-query preparation, documentation and interpretation of dashboard results. |
| What we changed after AI suggestion | The team manually reviewed and adapted the suggestions to the actual Gold tables, declared grains, Power BI model, dashboard requirements and observed results. Page layouts, visual selections, filtering behaviour and documentation were adjusted based on the actual project data. |
| What we verified manually | Verified the Power BI model, approved Gold tables, `DimDate` relationships, Sales Date slicer behaviour, Total Orders reconciliation, Top Seller values, Payment Reconciliation Rate, dashboard visual values, readability, presentation and documented Gold-data limitations. |
| What we can explain without AI | We can explain the purpose and contents of both dashboard pages, the five approved Gold sources, why the Gold tables retain their declared grains, how the `DimDate` filtering path works, how representative dashboard values were reconciled against Gold data, and why the documented data limitations were preserved. |

---

## 7. Next Week Preparation

- Preserve the completed and validated Week 9 Power BI dashboard as the
  baseline for the next sprint.
- Ensure the final Week 9 PBIX, README, dashboard insights, screenshots and
  weekly log are consistent with the final two-page dashboard.
- Preserve the Gold-only Power BI source boundary and existing Gold
  definitions.
- Prepare for the Week 10 streaming/live-data work.
- Keep the validated Week 9 dashboard and documentation available as the
  reference point for Week 10.
- Do not modify the approved Gold batch-summary definitions unless required
  by the next sprint's scope.
