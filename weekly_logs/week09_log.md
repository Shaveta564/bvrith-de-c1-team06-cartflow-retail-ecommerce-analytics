# Week 09 Log — CartFlow Power BI Dashboard Refinement

**Week:** 9  
**Date range:** 04 September 2026 – 10 September 2026  
**Team:** P06 – CartFlow  
**Project:** CartFlow – Retail & E-commerce Analytics

---

## 1. Sprint Goal

The goal of Week 9 was to continue from the validated Week 8 Power BI dashboard and complete the remaining dashboard analysis pages, interactions, validation and insight documentation.

The work focused on refining the Commerce Overview page, creating Seller and Category Analysis and Fulfilment and Payment pages, testing supported filter behaviour, reconciling representative dashboard values against the owning Gold tables, checking readability and accessibility, and documenting evidence-based insights and limitations without changing the approved Gold source boundary.

---

## 2. Work Completed

| Task | Owner | Status | Evidence |
|---|---|---|---|
| Continued from the validated Week 8 Power BI dashboard | Shaveta | Done | `dashboard/powerbi_dashboard.pbix` |
| Reviewed the existing Power BI model and confirmed the five approved Gold tables remained independent | Shaveta | Done | `screenshots/week09_01_final_model.png` |
| Refined the Page 1 Commerce Overview dashboard | Shaveta | Done | `dashboard/powerbi_dashboard.pbix` |
| Added and tested the Sales Date slicer on the Commerce Overview page | Shaveta | Done | `screenshots/week09_04_filter_interaction.png` |
| Tested the Sales Date slicer using full-range and filtered date selections | Shaveta | Done | `screenshots/week09_04_filter_interaction.png` |
| Reconciled filtered Total Orders against `agg_sales_daily` Gold data | Nandini | Done | Gold SQL reconciliation |
| Created Page 2 — Seller and Category Analysis | Manasa | Done | `dashboard/powerbi_dashboard.pbix` |
| Created GMV by Category visual | Manasa | Done | Page 2 in PBIX |
| Created Top Sellers by Order Count visual | Manasa | Done | Page 2 in PBIX |
| Created Top Sellers by GMV visual | Manasa | Done | Page 2 in PBIX |
| Created Seller Average Review Score visual | Manasa | Done | Page 2 in PBIX |
| Created Page 3 — Fulfilment and Payment | Manasa | Done | `dashboard/powerbi_dashboard.pbix` |
| Created Average Delivery Delay Trend visual | Manasa | Done | Page 3 in PBIX |
| Added On-Time Delivery Rate visual | Nandini | Done | Page 3 in PBIX |
| Added Payment Reconciliation Rate visual | Nandini | Done | Page 3 in PBIX |
| Added Reviewed Order Coverage visual | Nandini | Done | Page 3 in PBIX |
| Reconciled Payment Reconciliation Rate with `agg_payment_review` | Nandini | Done | Gold SQL reconciliation |
| Reconciled Top Seller Order Count values with `agg_seller_performance` | Nandini | Done | Gold SQL reconciliation |
| Reconciled Total Orders against `agg_sales_daily` | Nandini | Done | Gold SQL reconciliation |
| Reviewed dashboard readability and accessibility across all three pages | Shaveta | Done | Final Power BI dashboard |
| Documented dashboard insights, evidence and limitations | Team | Done | `docs/dashboard_insights.md` |
| Updated dashboard documentation and traceability | Team | Done | `dashboard/README.md` |
| Preserved Week 9 dashboard and validation evidence | Team | Done | `screenshots/week09_*` |

---

## 3. Key Decisions

- Continued using the validated Week 8 Power BI PBIX as the starting point for Week 9 instead of rebuilding the dashboard.
- Kept the Power BI model restricted to the five approved Gold tables:
  `agg_sales_daily`, `agg_seller_performance`, `agg_category_sales`,
  `agg_delivery_delay` and `agg_payment_review`.
- Kept the five Gold summary tables independent because their declared business grains and keys are different.
- Did not introduce unsafe relationships between the independent Gold tables simply to force slicer cross-filtering.
- Refined Page 1 and added a Sales Date slicer using `agg_sales_daily[sales_date]`.
- Verified that the Sales Date slicer changes the visuals supported by the `agg_sales_daily` source while independent Gold-table visuals remain unaffected.
- Created Page 2 for seller and category analysis using the approved seller and category Gold tables.
- Created Page 3 for fulfilment and payment analysis using the approved delivery and payment Gold tables.
- Used existing approved Gold fields and measures rather than introducing unsupported KPI definitions.
- Reconciled representative dashboard values against their owning Gold tables.
- Verified that the filtered Total Orders value of 54,055 is displayed as approximately 54K in Power BI because of compact number formatting.
- Verified the Payment Reconciliation Rate of approximately 99.96% against the `agg_payment_review` Gold table.
- Verified the Top 10 seller order-count values against `agg_seller_performance`.
- Preserved the negative values present in the Gold `average_delay_days` field and documented them as a data limitation rather than altering the source data.
- Completed readability and accessibility checks across all three dashboard pages.
- Documented evidence-based insights and limitations in `docs/dashboard_insights.md`.
- Kept Week 10 streaming/live-data implementation outside the Week 9 scope.

---

## 4. Blockers / Risks

| Blocker / Risk | Impact | Resolution / Help Needed |
|---|---|---|
| Five Gold summary tables have different business grains and no common safe relationship | Sales Date filtering does not cross-filter every visual on the dashboard | Kept the Gold tables independent and documented the expected filter behaviour |
| Power BI compact number formatting displays large values in abbreviated form | Exact reconciliation values are not directly visible on KPI cards | Verified the exact values against Gold SQL results and documented the reconciliation |
| `average_delay_days` contains negative values in the Gold data | Delivery-delay trend requires careful interpretation | Preserved the Gold values and documented the limitation; no source values were altered |
| Dashboard contains multiple analysis areas across three pages | Required clear visual hierarchy and readable presentation | Reviewed page layouts, labels, spacing and visual readability |
| Representative dashboard values required validation after refinement | Incorrect presentation or measure configuration could produce inconsistent results | Reconciled Total Orders, Payment Reconciliation Rate and Top Seller values against Gold data |

---

## 5. Evidence Added to GitHub

### Power BI Dashboard

- `dashboard/powerbi_dashboard.pbix`
- `dashboard/README.md`

The updated PBIX contains:

- Page 1 — Commerce Overview
- Page 2 — Seller and Category Analysis
- Page 3 — Fulfilment and Payment

### Dashboard Insights

- `docs/dashboard_insights.md`

### Screenshots

- `screenshots/week09_01_final_model.png`
- `screenshots/week09_02_page1_commerce_overview.png`
- `screenshots/week09_03_page2_seller_category.png`
- `screenshots/week09_04_filter_interaction.png`
- `screenshots/week09_05_page3_fulfilment_payment.png`
- `screenshots/week09_06_filtered_gold_reconciliation.png`
- `screenshots/week09_07_payment_reconciliation.png`
- `screenshots/week09_08_top_seller_validation.png`

### Weekly Log

- `weekly_logs/week09_log.md`

### Notebook

- `notebooks/06_powerbi_export.ipynb` — included if changes were made to the notebook during Week 9.

---

## 6. AI Transparency Note

| Question | Response |
|---|---|
| Where AI helped | AI was used to assist with Week 9 Power BI dashboard planning, page structure, visual selection, DAX guidance, filter-interaction testing, reconciliation-query preparation, documentation and interpretation of dashboard results. |
| What we changed after AI suggestion | The team manually reviewed and adapted the suggestions to the actual Gold tables, declared grains, Power BI model, dashboard requirements and observed results. Page layouts, visual selections, filtering behaviour and documentation were adjusted based on the actual project data. |
| What we verified manually | Verified the Power BI model, independent Gold tables, Sales Date slicer behaviour, Total Orders reconciliation, Top Seller values, Payment Reconciliation Rate, dashboard visual values, readability, accessibility and documented Gold-data limitations. |
| What we can explain without AI | We can explain the purpose and contents of all three dashboard pages, the five approved Gold sources, why the Gold tables remain independent, how the Sales Date slicer behaves, how representative dashboard values were reconciled against Gold data, and why the documented data limitations were preserved. |

---

## 7. Next Week Preparation

- Preserve the completed and validated Week 9 Power BI dashboard as the baseline for the next sprint.
- Review the Week 9 dashboard evidence and ensure all required files and screenshots are committed to GitHub.
- Preserve the Gold-only Power BI source boundary and existing Gold definitions.
- Prepare for the Week 10 streaming/live-data work.
- Keep the validated Week 9 dashboard and documentation available as the reference point for Week 10.
- Do not modify the approved Gold batch-summary definitions unless required by the next sprint's scope.
