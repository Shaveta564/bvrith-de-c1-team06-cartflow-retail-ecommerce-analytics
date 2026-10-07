# CartFlow Power BI Dashboard

## Week 9 — Dashboard Refinement, Interactions and Insights

This folder contains the refined Power BI dashboard for the CartFlow
Week 9 Gold-to-Power BI dashboard refinement.

The Week 9 dashboard is the refined continuation of the Week 8
Gold-only Power BI hand-off.

Expected file:

`dashboard/powerbi_dashboard.pbix`

---

## Power BI Source Rule

Power BI uses approved Gold outputs only.

The dashboard is not connected directly to raw, Bronze, Silver Candidate,
Trusted Silver detail, or Quarantine data.

The approved Gold sources used by the dashboard are:

- `agg_sales_daily`
- `agg_seller_performance`
- `agg_category_sales`
- `agg_delivery_delay`
- `agg_payment_review`

---

## Gold Sources

The Power BI model uses the following approved Gold batch-summary tables:

| Gold Table | Grain | Main Dashboard Purpose |
|---|---|---|
| `agg_sales_daily` | One row per sales date | Orders, GMV, AOV, cancellation and sales trends |
| `agg_seller_performance` | One row per seller | Seller order count, seller GMV and review performance |
| `agg_category_sales` | One row per month + category | Category sales and GMV analysis |
| `agg_delivery_delay` | One row per purchase date + customer state | Delivery performance and on-time delivery |
| `agg_payment_review` | One row per currency | Payment reconciliation and review coverage |

The Gold tables retain their declared reporting grains.

---

## Model and Relationships

The five approved Gold summary tables retain their declared reporting
grains and are not directly joined to one another merely because some
field names are similar.

A shared `DimDate` table is used for valid date-based filtering.

The approved date relationships are:

- `DimDate[Date]` → `agg_sales_daily[sales_date]`
- `DimDate[Date]` → `agg_delivery_delay[purchase_date]`

The following Gold tables remain independent because no safe shared
filtering relationship was required for the dashboard:

- `agg_category_sales`
- `agg_seller_performance`
- `agg_payment_review`

This model preserves the declared Gold grains and avoids unsafe
cross-table joins.

The Week 9 refinement did not change the approved Gold business logic
or introduce unsafe relationships merely to force slicer behavior.

---

## Dashboard Pages

The final dashboard contains two pages.

### Page 1 — Commerce Performance

The page provides a high-level view of CartFlow commerce performance.

Visuals include:

- Total Orders
- Total GMV
- Average Order Value
- Non-Cancelled Orders
- Cancellation Rate
- On-Time Delivery Rate
- Payment Reconciliation Rate
- GMV Trend Over Time
- Monthly Order Volume
- Sales Date slicer

The page is designed to provide an overall view of orders, sales value,
cancellations, delivery performance and payment reconciliation.

The Sales Date slicer was tested using the full period and a filtered
period. Sales-related visuals responded to the filter as expected.

---

### Page 2 — Seller and Category Performance

The page focuses on seller performance, category sales and customer
review quality.

Visuals include:

- GMV by Category
- Top Sellers by Order Count
- Top Sellers by GMV
- Seller Average Review Score

The page provides a focused view of category contribution, seller
performance and seller review quality.

The Top Sellers by Order Count visual was reconciled against
`agg_seller_performance`.

---

## Main Measures and Fields

The dashboard uses approved Gold fields and existing measures.

Important measures and fields include:

- `total_orders`
- GMV
- Average Order Value
- Cancellation Rate
- `on_time_orders`
- `delivery_eligible_orders`
- On-Time Delivery Rate
- `reconciled_orders`
- `complete_coverage_orders`
- `payment_reconciliation_rate`
- `reviewed_order_coverage`
- `seller_id`
- `order_count`
- `average_review_score`

The On-Time Delivery Rate is calculated using on-time orders divided by
delivery-eligible orders.

The Power BI measure is:

```DAX
On-Time Delivery Rate =
DIVIDE(
    SUM(agg_delivery_delay[on_time_orders]),
    SUM(agg_delivery_delay[delivery_eligible_orders])
)
