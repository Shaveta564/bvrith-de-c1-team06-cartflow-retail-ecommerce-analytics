# Dashboard Insights

**Week:** 9  
**Project:** P06 CartFlow  
**Purpose:** Document the Power BI dashboard pages, evidence-based observations, filter behavior, Gold-table traceability, reconciliation results, and limitations.

---

## 1. Dashboard Pages

| Page | Purpose | Main Visuals |
|---|---|---|
| Page 1: Commerce Overview | Provide a high-level summary of CartFlow commerce performance and operational health | KPI cards, GMV Trend, Orders Trend, GMV by Category, Sales Date slicer, On-Time Delivery Rate, Payment Reconciliation Rate |
| Page 2: Seller and Category Analysis | Show seller performance, category sales, and review-quality patterns | GMV by Category, Top Sellers by Order Count, Top Sellers by GMV, Seller Average Review Score |
| Page 3: Fulfilment and Payment | Show delivery performance and payment/review quality metrics | Average Delivery Delay Trend, On-Time Delivery Rate, Payment Reconciliation Rate, Reviewed Order Coverage |

---

## 2. Key Insights

### Page 1 — Commerce Overview

1. **Overall Order Volume:**  
   For the full available sales-date range, the Power BI Commerce Overview displays approximately **98K total orders**. The owning Gold table reconciliation returned **98,150 orders**, which is displayed as 98K in Power BI because compact number formatting is enabled.

2. **Overall GMV:**  
   The Commerce Overview displays approximately **$148.32M total GMV** for the full available sales-date range.

3. **Average Order Value:**  
   The dashboard displays an **Average Order Value of approximately $1.51K** for the full available sales-date range.

4. **Cancellation Rate:**  
   The dashboard displays a **Cancellation Rate of 4.82%** for the full available sales-date range.

5. **Sales Date Filter Behavior:**  
   When the Sales Date slicer was changed from the full period to **01-06-2025 through 01-12-2025**, Total Orders changed from approximately **98K to 54K**, Total GMV changed from approximately **$148.32M to $82.05M**, and Average Order Value changed from approximately **$1.51K to $1.52K**.

6. **Filtered Order Reconciliation:**  
   For the filtered period **01-06-2025 through 01-12-2025**, the Gold validation query returned **54,055 orders**. Power BI displayed the corresponding value as approximately **54K** because compact number formatting was enabled.

7. **Independent Gold Table Filter Behavior:**  
   The Sales Date slicer affected visuals based on `agg_sales_daily`, including the Total Orders, Total GMV, Average Order Value and sales trends. Visuals based on independent Gold tables such as `agg_category_sales`, `agg_delivery_delay`, and `agg_payment_review` did not change. This behavior is consistent with the approved independent Gold-table model.

---

### Page 2 — Seller and Category Analysis

8. **Top Sellers by Order Count:**  
   The Top Sellers by Order Count visual shows the highest seller order counts in the approved `agg_seller_performance` Gold table. Gold validation returned the following top sellers:

   - `SLR002740` — 64 orders
   - `SLR002880` — 64 orders
   - `SLR001569` — 63 orders
   - `SLR000895` — 61 orders
   - `SLR001051` — 60 orders
   - `SLR000147` — 60 orders
   - `SLR002066` — 59 orders
   - `SLR000763` — 59 orders
   - `SLR001282` — 59 orders
   - `SLR000903` — 58 orders

9. **Category Sales:**  
   The GMV by Category visual compares GMV across category codes using the approved `agg_category_sales` Gold table. The visual is descriptive and does not establish reasons for differences between categories.

10. **Seller GMV:**  
    The Top Sellers by GMV visual compares seller-level GMV using the `gmv` field from `agg_seller_performance`.

11. **Seller Review Quality:**  
    The Seller Average Review Score visual compares seller-level average review scores using `average_review_score` from `agg_seller_performance`.

---

### Page 3 — Fulfilment and Payment

12. **On-Time Delivery Rate:**  
    The Fulfilment and Payment page displays an **On-Time Delivery Rate of 36.36%**, using the approved delivery Gold data and the existing On-Time Delivery Rate measure.

13. **Payment Reconciliation:**  
    The page displays a **Payment Reconciliation Rate of 99.96%**. Gold validation returned **93,808 reconciled orders** out of **93,841 complete-coverage orders**, producing a reconciliation rate of approximately **99.9648%**, which matches the Power BI value after percentage formatting.

14. **Reviewed Order Coverage:**  
    The page displays **90.36% Reviewed Order Coverage** using the approved `reviewed_order_coverage` field from `agg_payment_review`.

15. **Average Delivery Delay Trend:**  
    The Average Delivery Delay Trend visual shows the `average_delay_days` field over `purchase_date` from `agg_delivery_delay`. The displayed series contains negative values in the supplied Gold data. No causal or operational conclusion is made from those values; the dashboard visualizes the approved Gold field as provided.

---

## 3. How the Dashboard Uses Gold Tables

| Dashboard Page | Gold Table Used | Important Fields / Measures |
|---|---|---|
| Commerce Overview | `agg_sales_daily` | `sales_date`, `total_orders`, GMV and order measures |
| Commerce Overview | `agg_category_sales` | `category_code`, `gmv` |
| Commerce Overview | `agg_delivery_delay` | `on_time_orders`, `delivery_eligible_orders`, On-Time Delivery Rate |
| Commerce Overview | `agg_payment_review` | Payment reconciliation fields |
| Seller and Category Analysis | `agg_seller_performance` | `seller_id`, `order_count`, `gmv`, `average_review_score` |
| Seller and Category Analysis | `agg_category_sales` | `category_code`, `gmv`, `order_count`, `average_order_value` |
| Fulfilment and Payment | `agg_delivery_delay` | `purchase_date`, `average_delay_days`, `on_time_orders`, `delivery_eligible_orders` |
| Fulfilment and Payment | `agg_payment_review` | `payment_reconciliation_rate`, `reviewed_order_coverage`, `reconciled_orders`, `complete_coverage_orders` |

---

## 4. Power BI Validation

- [x] Dashboard uses the approved Gold outputs only.
- [x] Power BI model retains the approved independent Gold-table structure.
- [x] No unsafe relationships were added to force cross-filtering.
- [x] Page 1 Sales Date slicer was tested.
- [x] Sales-related KPI values changed when the Sales Date slicer was applied.
- [x] GMV Trend and Orders Trend responded to the Sales Date filter.
- [x] Independent Gold-table visuals were checked for expected filter behavior.
- [x] Filtered Total Orders was reconciled with `agg_sales_daily`.
- [x] Filtered Gold validation returned **54,055 orders**.
- [x] Power BI displayed the filtered value as approximately **54K** because of compact formatting.
- [x] Page 2 Top Sellers by Order Count was reconciled with `agg_seller_performance`.
- [x] Top seller values in Gold matched the Page 2 Top Sellers by Order Count visual.
- [x] Page 3 Payment Reconciliation Rate was reconciled with `agg_payment_review`.
- [x] Gold validation returned **93,808 reconciled orders** and **93,841 complete-coverage orders**.
- [x] Gold Payment Reconciliation Rate was approximately **99.96%**, matching Power BI.
- [x] Page 1 full-period Total Orders was reconciled with `agg_sales_daily`.
- [x] Gold returned **98,150 total orders**, displayed as approximately **98K** in Power BI.
- [x] Dashboard pages were reviewed for visual readability, labels, spacing and number formatting.
- [x] Week 9 Power BI refinement and validation evidence was captured.

---

## 5. Scope and Limitations

- The dashboard uses the approved Gold outputs carried forward from Week 8.
- No raw, Bronze, or Silver tables are used as direct Power BI sources.
- The approved independent Gold-table structure was retained.
- The Sales Date slicer primarily affects visuals based on `agg_sales_daily`.
- Independent Gold tables are not artificially connected through unsafe relationships.
- Power BI compact formatting displays **98,150** total orders as approximately **98K**.
- Power BI compact formatting displays **54,055** filtered orders as approximately **54K**.
- Dashboard observations describe patterns visible in the available Gold data and do not establish business causation.
- The Average Delivery Delay Trend contains negative values in the supplied `average_delay_days` Gold field. The dashboard does not alter or reinterpret those values.
- Payment metrics are sourced from `agg_payment_review`, whose grain is currency-level rather than sales-date-level.
- Streaming or live-event functionality is not included in this Week 9 dashboard refinement and belongs to Week 10.

---

## 6. Traceability

The dashboard follows the traceability chain:

**Power BI Visual → Measure / Field → Owning Gold Table → Gold Validation**

### Example 1 — Total Orders

**Total Orders KPI → `total_orders` → `agg_sales_daily` → Gold SQL reconciliation**

Full-period Gold result:

```sql
SELECT
    SUM(total_orders) AS gold_total_orders
FROM agg_sales_daily;
