# Data Dictionary

**Project:** CartFlow – Retail & E-Commerce Analytics  
**Week:** 2  
**Purpose:** Define raw, reference, Silver, and streaming fields.

---

## 1. Source File Catalog

| File Name | Grain | Purpose | Approx. Rows | Notes |
|---|---|---|---:|---|
| orders.csv | One row per order | Stores order details and lifecycle timestamps | ~35,000 | Main transactional file |
| order_items.parquet | One row per order item | Stores products purchased in each order | ~120,000 | Multiple items per order |
| sellers.json | One row per seller | Stores seller information | ~1,500 | Reference dataset |
| payments.csv | One row per payment | Stores payment details | ~40,000 | Linked using order_id |
| reviews.csv | One row per review | Stores customer reviews | ~30,000 | Linked using order_id |
| order_status_event.json | One row per event | Streaming simulation | Variable | JSON streaming events |

---

## 2. Raw File Schema: orders.csv

| Field Name | Data Type | Required? | Example | Description |
|---|---|---|---|---|
| order_id | string | Yes | ORD100001 | Unique order identifier |
| customer_id | string | Yes | CUST001 | Customer identifier |
| order_status | string | Yes | Delivered | Current order status |
| purchase_timestamp | timestamp | Yes | 2026-07-01 09:30:00 | Order purchase time |
| approval_timestamp | timestamp | No | 2026-07-01 09:45:00 | Payment approval time |
| shipped_timestamp | timestamp | No | 2026-07-02 10:15:00 | Shipping time |
| delivered_timestamp | timestamp | No | 2026-07-05 16:20:00 | Delivery time |
| estimated_delivery_date | date | Yes | 2026-07-06 | Expected delivery date |

---

## 3. Raw File Schema: order_items.parquet

| Field Name | Data Type | Required? | Example | Description |
|---|---|---|---|---|
| order_id | string | Yes | ORD100001 | Order identifier |
| item_seq | integer | Yes | 1 | Item sequence number |
| product_id | string | Yes | PROD501 | Product identifier |
| category | string | Yes | Electronics | Product category |
| seller_id | string | Yes | SEL120 | Seller identifier |
| price | decimal | Yes | 1250.00 | Product price |
| freight_value | decimal | Yes | 75.00 | Shipping charge |

---

## 4. Reference File Schema: sellers.json

| Field Name | Data Type | Required? | Example | Description |
|---|---|---|---|---|
| seller_id | string | Yes | SEL120 | Unique seller ID |
| seller_city | string | Yes | Hyderabad | Seller city |
| seller_state | string | Yes | Telangana | Seller state |
| category_focus | string | Yes | Electronics | Main product category |

---

## 5. Canonical Silver Table Design

Final Silver table name:

```text
silver_order_summary
```

| Silver Field | Data Type | Source Mapping | Business Meaning |
|---|---|---|---|
| order_id | string | orders.order_id | Canonical order ID |
| customer_id | string | orders.customer_id | Customer identifier |
| seller_id | string | order_items.seller_id | Seller identifier |
| category | string | order_items.category | Product category |
| order_status | string | orders.order_status | Latest order status |
| total_price | decimal | order_items.price | Product revenue |
| freight_value | decimal | order_items.freight_value | Shipping charge |
| payment_value | decimal | payments.payment_value | Total payment |
| review_score | integer | reviews.review_score | Customer rating |
| purchase_date | date | orders.purchase_timestamp | Analytics date |

---

## 6. Streaming Event Schema

| Field Name | Data Type | Required? | Example | Description |
|---|---|---|---|---|
| event_id | string | Yes | EVT10001 | Unique event ID |
| event_timestamp | timestamp | Yes | 2026-07-03T10:15:00+05:30 | Event time |
| order_id | string | Yes | ORD100001 | Order identifier |
| event_type | string | Yes | Order Shipped | Event category |
| source_system | string | No | Marketplace | Event source |
| status | string | Yes | Delivered | Updated order status |
