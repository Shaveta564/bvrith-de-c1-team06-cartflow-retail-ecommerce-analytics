# Synthetic Data Assumptions

**Week:** 2  
**Purpose:** Document how synthetic data is created for the CartFlow project.

---

## 1. Synthetic Data Boundary

This project uses synthetic educational e-commerce data only. It must not be presented as real company, customer, seller, employee, merchant, government, or online marketplace data.

The dataset is generated only for learning data engineering concepts such as data ingestion, transformation, data quality validation, streaming, and analytics. All customer IDs, seller IDs, products, payments, reviews, and events are fictional.

---

## 2. Domain Assumptions

| Area | Assumption |
|------|------------|
| Geography / Scope | India (multiple states and cities) |
| Time Period | January 2026 – March 2026 |
| Business Domain | Retail & E-Commerce Marketplace |
| Source Systems | Order Management System, Seller Management System, Payment System, Customer Review System |
| Event Types | Order Created, Order Approved, Order Shipped, Order Delivered, Order Cancelled, Order Returned |
| Reference Data | Sellers, Product Categories, Payment Methods |

---

## 3. Data Volume Assumptions

| File | Approximate Rows | Reason |
|------|-----------------:|--------|
| `orders.csv` | 35,000 | Simulates customer orders |
| `order_items.parquet` | 120,000 | Simulates multiple products per order |
| `sellers.json` | 1,500 | Seller reference data |
| `payments.csv` | 40,000 | Payment transactions |
| `reviews.csv` | 30,000 | Customer review records |
| `order_status_event.json` | 150,000 | Simulated streaming order status events |

---

## 4. Controlled Data Quality Issues

| Issue Type | Approx. Share | Why Include It |
|------------|--------------:|----------------|
| Duplicate Order IDs | 0.2%–0.5% | Test duplicate detection |
| Missing Values | 1%–3% | Test completeness checks |
| Invalid Foreign Keys | 0.5%–1% | Test referential integrity |
| Payment Amount Mismatch | 0.5%–1% | Test payment validation |
| Invalid Delivery Dates | 0.1%–0.3% | Test chronological validation |
| Conflicting Order Status | 0.2%–0.5% | Test business rule validation |

---

## 5. Manual Verification

Before using the generated data, the team should verify that:

- Row counts are within the expected range.
- Primary key fields are unique and not null.
- Foreign key relationships are valid between orders, order items, sellers, payments, and reviews.
- Date and timestamp values follow realistic business sequences.
- Payment values are reasonable and correspond to order values.
- Controlled data quality issues are intentionally present but limited.
- Source files are available in CSV, Parquet, and JSON formats for ETL processing.
- The dataset is suitable for Bronze, Silver, Gold, and Streaming pipeline implementation in Databricks.
