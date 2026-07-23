# Data Dictionary

**Project:** CartFlow – Retail & E-Commerce Analytics  
**Week:** 2  
**Purpose:** Define the structure of raw, reference, Silver, and streaming datasets used in the CartFlow project.

---

## 1. Source File Catalog

| File Name | Grain | Purpose | Approx. Rows | Notes |
|---|---|---|---:|---|
| orders.csv | One row per order | Stores order header and lifecycle information | ~35,000 | Main transactional dataset |
| order_items.parquet | One row per order item | Stores products purchased in each order | ~120,000 | Multiple items per order |
| sellers.json | One row per seller | Stores seller reference information | ~1,500 | Reference dataset |
| payments.csv | One row per payment | Stores payment information | ~40,000 | Linked using `order_id` |
| reviews.csv | One row per review | Stores customer review information | ~30,000 | Linked using `order_id` |
| order_status_drop_01.json / order_status_drop_02.json | One row per event | Streaming order status events | Variable | Used for streaming simulation |

---

## 2. Raw File Schema: orders.csv

| Field Name | Data Type | Required? | Description |
|---|---|---|---|
| source_record_id | string | Yes | Stable physical source row key |
| order_id | string | Yes | Fictional order business key |
| customer_region | string | Yes | Customer region |
| customer_state | string | Yes | Customer state |
| customer_city_code | string | Yes | Fictional city code |
| customer_segment | string | Yes | Customer segment |
| order_status | string | Yes | Current order status |
| purchase_ts | timestamp | No | Order purchase timestamp |
| approval_ts | timestamp | No | Payment approval timestamp |
| carrier_handoff_ts | timestamp | No | Carrier handoff timestamp |
| delivered_ts | timestamp | No | Delivery timestamp |
| estimated_delivery_ts | timestamp | Yes | Estimated delivery timestamp |
| return_ts | timestamp | No | Return completion timestamp |
| currency_code | string | Yes | Currency code |

---

## 3. Raw File Schema: order_items.parquet

| Field Name | Data Type | Required? | Description |
|---|---|---|---|
| source_record_id | string | Yes | Stable physical source row key |
| order_item_id | string | Yes | Order item identifier |
| order_id | string | Yes | Parent order identifier |
| order_item_seq | integer | Yes | Order item sequence |
| product_id | string | Yes | Product identifier |
| category_code | string | Yes | Product category |
| seller_id | string | Yes | Seller identifier |
| item_price | decimal | Yes | Product price |
| freight_value | decimal | Yes | Freight amount |
| quantity | integer | Yes | Quantity ordered |
| item_created_ts | timestamp | Yes | Item creation timestamp |

---

## 4. Reference File Schema: sellers.json

| Field Name | Data Type | Required? | Description |
|---|---|---|---|
| source_record_id | string | Yes | Stable physical source row key |
| seller_id | string | Yes | Seller identifier |
| seller_region | string | Yes | Seller region |
| seller_state | string | Yes | Seller state |
| seller_type | string | Yes | Seller category |
| service_band | string | Yes | Service level |
| active_from | date | Yes | Active start date |
| active_to | date | Yes | Active end date |
| seller_status | string | Yes | Current seller status |

---

## 5. Canonical Silver Table Design

Final Silver table name:

```text
silver_order_summary
```

| Silver Field | Data Type | Source Mapping | Business Meaning |
|---|---|---|---|
| order_id | string | orders.order_id | Canonical order identifier |
| order_item_id | string | order_items.order_item_id | Order item identifier |
| seller_id | string | order_items.seller_id | Seller identifier |
| customer_region | string | orders.customer_region | Customer region |
| customer_segment | string | orders.customer_segment | Customer segment |
| category_code | string | order_items.category_code | Product category |
| order_status | string | orders.order_status | Latest order status |
| payment_value | decimal | payments.payment_value | Payment amount |
| review_score | integer | reviews.review_score | Customer rating |
| purchase_ts | timestamp | orders.purchase_ts | Purchase timestamp |

---

## 6. Streaming Event Schema

| Field Name | Data Type | Required? | Description |
|---|---|---|---|
| event_id | string | Yes | Event identifier |
| schema_version | integer | Yes | Event schema version |
| event_ts | timestamp | Yes | Event timestamp |
| event_type | string | Yes | Event type |
| order_id | string | Yes | Order identifier |
| seller_id | string | Yes | Seller identifier |
| order_item_id | string | No | Order item identifier |
| previous_status | string | Yes | Previous order status |
| new_status | string | Yes | Updated order status |
| status_reason | string | Yes | Reason for status update |
| promised_delivery_ts | timestamp | Yes | Promised delivery timestamp |
| location_code | string | Yes | Event location code |
| event_sequence_no | integer | Yes | Event sequence number |
| producer_run_id | string | Yes | Producer run identifier |
