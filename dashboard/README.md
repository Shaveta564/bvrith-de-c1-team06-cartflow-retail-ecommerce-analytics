# CartFlow Power BI Dashboard

## Week 9 — Dashboard Refinement, Interactions and Insights

This folder contains the refined Power BI dashboard for the CartFlow
Week 9 Gold-to-Power BI dashboard refinement.

Expected file:

`dashboard/powerbi_dashboard.pbix`

## Power BI Source Rule

Power BI uses approved Gold outputs only.

The dashboard is not connected directly to raw, Bronze, Silver Candidate,
Trusted Silver detail, or Quarantine data.

## Gold Sources

The Power BI model uses the following approved Gold batch-summary tables:

| Gold Table | Grain |
|---|---|
| `agg_sales_daily` | One row per sales date |
| `agg_seller_performance` | One row per seller |
| `agg_category_sales` | One row per month + category |
| `agg_delivery_delay` | One row per purchase date + customer state |
| `agg_payment_review` | One row per currency |

## Model and Relationships

The five Gold summary tables are kept as independent tables.

No relationships were created between the summary tables merely because
some field names are similar. This preserves the declared Gold grain of
each table and avoids unsafe cross-table joins.

The Week 9 refinement did not change the approved Gold model structure.

## Dashboard Pages

### Page 1 — Commerce Overview

The page provides a high-level view of CartFlow commerce performance.

Visuals include:

- Total Orders
- Total GMV
- Average Order Value
- Non-Cancelled Orders
- Cancellation Rate
- GMV Trend
- Orders Trend
- GMV by Category
- On-Time Delivery Rate
- Payment Reconciliation Rate
- Sales Date slicer

The Sales Date slicer was tested using the full period and a filtered
period. Sales-related visuals responded to the filter as expected.

### Page 2 — Seller and Category Analysis

The page focuses on seller performance, category sales and review quality.

Visuals include:

- GMV by Category
- Top Sellers by Order Count
- Top Sellers by GMV
- Seller Average Review Score

The Top Sellers by Order Count visual was reconciled against
`agg_seller_performance`.

### Page 3 — Fulfilment and Payment

The page focuses on delivery performance and payment/review quality.

Visuals include:

- Average Delivery Delay Trend
- On-Time Delivery Rate
- Payment Reconciliation Rate
- Reviewed Order Coverage

The payment reconciliation value was reconciled against
`agg_payment_review`.

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

## Interaction and Filter Behavior

The Page 1 Sales Date slicer was tested using:

**01-01-2025 → 01-12-2025**

and the filtered period:

**01-06-2025 → 01-12-2025**

During testing:

- Total Orders changed from approximately 98K to 54K.
- Total GMV changed from approximately $148.32M to $82.05M.
- Average Order Value changed from approximately $1.51K to $1.52K.
- GMV Trend responded to the filter.
- Orders Trend responded to the filter.
- Visuals based on independent Gold tables remained unchanged.

The independent behavior is intentional and avoids unsafe relationships
between Gold summary tables.

The final dashboard was returned to the full date range before completion.

## Validation and Reconciliation

Selected dashboard values were reconciled against their owning Gold
sources.

### Total Orders

Gold validation:

```sql
SELECT
    SUM(total_orders) AS gold_total_orders
FROM agg_sales_daily;
