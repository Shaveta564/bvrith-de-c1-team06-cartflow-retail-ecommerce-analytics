# Dashboard Insights

**Week:** 9  
**Project:** P06 CartFlow  
**Purpose:** Document the Power BI dashboard pages, evidence-based observations, filter behavior, Gold-table traceability, reconciliation results, and limitations.

---

## 1. Dashboard Pages

| Page | Purpose | Main Visuals |
|---|---|---|
| Page 1: Commerce Performance | Provide a high-level view of CartFlow commerce performance, sales trends, order volume, delivery performance and payment reconciliation | KPI cards, GMV Trend Over Time, Monthly Order Volume, GMV by Category, Sales Date slicer, On-Time Delivery Rate, Payment Reconciliation Rate |
| Page 2: Seller and Category Performance | Show seller performance, category sales and seller review-quality patterns | GMV by Category, Top Sellers by Order Count, Top Sellers by GMV, Seller Average Review Score |

The final Week 9 dashboard contains two pages.

The dashboard is the refined continuation of the Week 8 Gold-to-Power BI
hand-off.

---

## 2. Key Insights

### Page 1 — Commerce Performance

1. **Overall Order Volume:**  
   For the full available sales-date range, the Power BI Commerce Performance
   page displays approximately **98K total orders**. The owning Gold table
   reconciliation returned **98,150 orders**, which is displayed as 98K in
   Power BI because compact number formatting is enabled.

2. **Overall GMV:**  
   The Commerce Performance page displays approximately **$148.32M total GMV**
   for the full available sales-date range.

3. **Average Order Value:**  
   The dashboard displays an **Average Order Value of approximately $1.51K**
   for the full available sales-date range.

4. **Non-Cancelled Orders:**  
   The dashboard displays approximately **93K non-cancelled orders** for the
   full available sales-date range.

5. **Cancellation Rate:**  
   The dashboard displays a **Cancellation Rate of 4.82%** for the full
   available sales-date range.

6. **On-Time Delivery Rate:**  
   The dashboard displays an **On-Time Delivery Rate of 36.36%** using the
   approved delivery Gold data and the existing On-Time Delivery Rate
   measure.

7. **Payment Reconciliation:**  
   The dashboard displays a **Payment Reconciliation Rate of 99.96%**.
   Gold validation returned **93,808 reconciled orders** out of
   **93,841 complete-coverage orders**, producing a rate of approximately
   **99.9648%**.

8. **Sales Date Filter Behavior:**  
   When the Sales Date slicer was changed from the full period to
   **01-06-2025 through 01-12-2025**, Total Orders changed from approximately
   **98K to 54K**, Total GMV changed from approximately **$148.32M to
   $82.05M**, and Average Order Value changed from approximately
   **$1.51K to $1.52K**.

9. **Filtered Order Reconciliation:**  
   For the filtered period **01-06-2025 through 01-12-2025**, the Gold
   validation query returned **54,055 orders**. Power BI displayed the
   corresponding value as approximately **54K** because compact number
   formatting was enabled.

10. **Monthly Order Volume:**  
    The Monthly Order Volume visual presents order volume over the available
    sales-date range using the approved date-filter path. The visual is
    descriptive of the order-volume pattern and does not establish causal
    reasons for changes between periods.

11. **GMV Trend:**  
    The GMV Trend Over Time visual presents daily GMV using the approved
    `agg_sales_daily` Gold source. The visual describes the observed sales
    pattern over time without making causal claims about individual spikes
    or changes.

12. **Category GMV:**  
    The GMV by Category visual compares category-level GMV using the approved
    `agg_category_sales` Gold source. The visual is descriptive and does
    not establish reasons for differences between categories.

---

### Page 2 — Seller and Category Performance

13. **Top Sellers by Order Count:**  
    The Top Sellers by Order Count visual shows the highest seller order
    counts in the approved `agg_seller_performance` Gold table. Gold
    validation returned the following top sellers:

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

14. **Category Sales:**  
    The GMV by Category visual compares GMV across category codes using the
    approved `agg_category_sales` Gold table. The visual is descriptive and
    does not establish reasons for differences between categories.

15. **Seller GMV:**  
    The Top Sellers by GMV visual compares seller-level GMV using the `gmv`
    field from `agg_seller_performance`.

16. **Seller Review Quality:**  
    The Seller Average Review Score visual compares seller-level average
    review scores using `average_review_score` from
    `agg_seller_performance`.

---

## 3. How the Dashboard Uses Gold Tables

| Dashboard Page | Gold Table Used | Important Fields / Measures |
|---|---|---|
| Commerce Performance | `agg_sales_daily` | `sales_date`, `total_orders`, GMV, AOV, non-cancelled orders, cancellation rate |
| Commerce Performance | `agg_category_sales` | `category_code`, `gmv` |
| Commerce Performance | `agg_delivery_delay` | `on_time_orders`, `delivery_eligible_orders`, On-Time Delivery Rate |
| Commerce Performance | `agg_payment_review` | `reconciled_orders`, `complete_coverage_orders`, `payment_reconciliation_rate` |
| Seller and Category Performance | `agg_seller_performance` | `seller_id`, `order_count`, `gmv`, `average_review_score` |
| Seller and Category Performance | `agg_category_sales` | `category_code`, `gmv`, `order_count`, `average_order_value` |

The dashboard uses the approved Gold outputs only.

No raw, Bronze, Silver Candidate, Trusted Silver detail, or Quarantine
tables are used as direct Power BI sources.

---

## 4. Model and Filter Behavior

The Power BI model contains the five approved Gold summary tables and a
shared `DimDate` table.

The approved date relationships are:

- `DimDate[Date]` → `agg_sales_daily[sales_date]`
- `DimDate[Date]` → `agg_delivery_delay[purchase_date]`

The following Gold tables remain independent:

- `agg_category_sales`
- `agg_seller_performance`
- `agg_payment_review`

No direct relationships were created between independent Gold summary
tables merely because some field names are similar.

This preserves the declared Gold grains and avoids unsafe cross-table joins.

The Sales Date slicer was therefore evaluated according to the valid
filter paths in the approved model rather than by forcing all visuals to
respond to the slicer.

---

## 5. Power BI Validation

- [x] Dashboard uses the approved Gold outputs only.
- [x] Power BI model retains the approved Gold-table grains.
- [x] `DimDate` is used for valid date-based filtering.
- [x] `DimDate[Date]` is related to `agg_sales_daily[sales_date]`.
- [x] `DimDate[Date]` is related to `agg_delivery_delay[purchase_date]`.
- [x] No unsafe relationships were added to force cross-filtering.
- [x] Page 1 Sales Date slicer was tested.
- [x] Sales-related KPI values changed when the Sales Date slicer was applied.
- [x] GMV Trend responded to the Sales Date filter.
- [x] Monthly Order Volume responded to the Sales Date filter.
- [x] Independent Gold-table behavior was checked according to the approved model.
- [x] Filtered Total Orders was reconciled with `agg_sales_daily`.
- [x] Filtered Gold validation returned **54,055 orders**.
- [x] Power BI displayed the filtered value as approximately **54K** because of compact formatting.
- [x] Page 2 Top Sellers by Order Count was reconciled with `agg_seller_performance`.
- [x] Top seller values in Gold matched the Page 2 Top Sellers by Order Count visual.
- [x] Payment Reconciliation Rate was reconciled with `agg_payment_review`.
- [x] Gold validation returned **93,808 reconciled orders** and **93,841 complete-coverage orders**.
- [x] Gold Payment Reconciliation Rate was approximately **99.96%**, matching Power BI.
- [x] Full-period Total Orders was reconciled with `agg_sales_daily`.
- [x] Gold returned **98,150 total orders**, displayed as approximately **98K** in Power BI.
- [x] Dashboard pages were reviewed for visual readability, labels, spacing and number formatting.
- [x] Week 9 Power BI refinement and validation evidence was captured.

---

## 6. Scope and Limitations

- The dashboard uses the approved Gold outputs carried forward from Week 8.
- No raw, Bronze, or Silver tables are used as direct Power BI sources.
- The approved Gold-table grains are retained.
- `DimDate` provides valid date filtering through its approved relationships.
- Not every visual is expected to respond to every slicer when the approved
  model does not provide a valid filter path.
- Independent Gold tables are not artificially connected through unsafe
  relationships.
- Power BI compact formatting displays **98,150** total orders as
  approximately **98K**.
- Power BI compact formatting displays **54,055** filtered orders as
  approximately **54K**.
- Dashboard observations describe patterns visible in the available Gold
  data and do not establish business causation.
- The dashboard does not introduce new business logic that belongs in the
  Gold layer.
- Delivery metrics are sourced from the approved Gold data and are not
  manually altered in Power BI.
- Payment metrics are sourced from `agg_payment_review`, whose grain is
  currency-level rather than sales-date-level.
- The dashboard does not include streaming or live-event functionality.
  Streaming work belongs to Week 10.

---

## 7. Traceability

The dashboard follows the traceability chain:

**Power BI Visual → Measure / Field → Owning Gold Table → Gold Validation**

### Example 1 — Total Orders

**Total Orders KPI → `total_orders` → `agg_sales_daily` → Gold SQL reconciliation**

Full-period Gold result:

```sql
SELECT
    SUM(total_orders) AS gold_total_orders
FROM agg_sales_daily;
