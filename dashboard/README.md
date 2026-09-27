# CartFlow Power BI Dashboard

## Week 8 — Commerce Overview

This folder contains the first working Power BI dashboard for the CartFlow
Week 8 Gold-to-Power BI hand-off.

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

## Main KPIs and Measures

The Commerce Overview dashboard contains:

- Total Orders
- Total GMV
- Average Order Value
- Non-Cancelled Orders
- Cancellation Rate
- On-Time Delivery Rate
- Payment Reconciliation Rate

The On-Time Delivery Rate measure is calculated using on-time orders
divided by delivery-eligible orders.

## Dashboard Page

### Page 1 — Commerce Overview

The page contains:

- KPI cards for commerce and order health
- GMV Trend
- Orders Trend
- GMV by Category
- On-Time Delivery Rate
- Payment Reconciliation Rate

The dashboard is organized around business questions rather than creating
one visual for each Gold table.

## Validation and Reconciliation

Selected dashboard values were reconciled against their owning Gold source.

For example:

- Total Orders on the dashboard was reconciled against
  `SUM(agg_sales_daily[total_orders])`.
- The reconciliation value matched the dashboard Total Orders value.

The reconciliation evidence is stored in:

`screenshots/`

## Refresh and Data Connection

The Power BI dashboard uses the approved Gold hand-off as its source.

Future refreshes should continue to use the governed Gold outputs and
should not introduce raw or Silver detail sources.

## Evidence

Week 8 evidence screenshots are stored under:

`screenshots/`

The evidence includes the Power BI model, dashboard page, and selected
measure reconciliation.

## Week 8 Boundary

This PBIX represents the first working Gold-only Power BI dashboard and
model for Week 8.

Further visual refinement, interaction testing, presentation improvements,
and evidence-backed dashboard insights belong to the Week 9 refinement
stage.
