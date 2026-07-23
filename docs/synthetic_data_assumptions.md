# Synthetic Data Assumptions

**Project:** CartFlow – Retail & E-Commerce Analytics  
**Week:** 2  
**Purpose:** Document the assumptions used for creating and validating synthetic educational datasets for the CartFlow project.

---

## 1. Synthetic Data Boundary

This project uses synthetic educational retail and e-commerce data only. The dataset must not be presented as real company, customer, seller, employee, merchant, government, or marketplace data.

All customer IDs, seller IDs, products, orders, payments, reviews, and streaming events are fictional and are created solely for learning data engineering concepts including data ingestion, data quality validation, ETL pipelines, streaming, and analytics.

---

## 2. Domain Assumptions

| Area | Assumption |
|------|------------|
| Geography / Scope | India (multiple regions, states, and cities) |
| Time Period | January 2026 – March 2026 |
| Business Domain | Retail & E-Commerce Marketplace |
| Source Systems | Order Management System, Seller Management System, Payment System, Customer Review System |
| Event Types | Order Created, Order Approved, Carrier Handoff, Order Delivered, Order Returned |
| Reference Data | Sellers, Product Categories, Customer Segments, Regions |

---

## 3. Data Volume Assumptions

| File | Approximate Rows | Reason |
|------|-----------------:|--------|
| `orders.csv` | ~35,000 | Simulates customer orders |
| `order_items.parquet` | ~120,000 | Simulates products purchased in each order |
| `sellers.json` | ~1,500 | Seller reference information |
| `payments.csv` | ~40,000 | Payment transaction records |
| `reviews.csv` | ~30,000 | Customer review records |
| `order_status_drop_01.json` | Variable | Streaming order status events |
| `order_status_drop_02.json` | Variable | Additional streaming order status events |

---

## 4. Controlled Data Quality Issues

| Issue Type | Approx. Share | Purpose |
|------------|--------------:|---------|
| Duplicate Records | 0.2%–0.5% | Test duplicate detection |
| Missing Values | 1%–3% | Test completeness validation |
| Invalid Foreign Keys | 0.5%–1% | Test referential integrity |
| Invalid Timestamp Sequence | 0.1%–0.3% | Test chronological validation |
| Invalid Reference Codes | 0.5%–1% | Test lookup validation |

---

## 5. Manual Verification

Before using the generated datasets, verify that:

- Row counts are within the expected range.
- Primary key fields are present, unique, and not null.
- Foreign key relationships are valid across orders, order items, sellers, payments, and reviews.
- Business keys, timestamps, and reference values are consistent across datasets.
- Controlled data quality issues are intentionally present but limited.
- Source files are available in CSV, Parquet, and JSON formats.
- The datasets are suitable for Bronze, Silver, Gold, and Streaming pipeline implementation in Databricks.
