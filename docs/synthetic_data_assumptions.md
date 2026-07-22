# Synthetic Data Assumptions

**Week:** 2  
**Purpose:** Document how educational data is created.

---

## 1. Synthetic Data Boundary

This project uses synthetic educational data only. It must not be presented as real company, customer, citizen, player, patient, government, or platform data.
This project uses synthetic educational e-commerce/order processing data created for learning purposes only. The data does not represent any real company, customer, employee, merchant, government agency, or online platform. All names, IDs, transactions, and events are fictional and are intended solely for practicing data engineering concepts.

---

## 2. Domain Assumptions

| Area              | Assumption                                                                           |
| ----------------- | ------------------------------------------------------------------------------------ |
| Geography / Scope | India (multiple cities and regions)                                                  |
| Time Period       | January 2026 – March 2026                                                            |
| Source Systems    | Order Management System, Customer Management System, Payment System, Delivery System |
| Event Types       | Order Created, Payment Completed, Order Shipped, Order Delivered, Order Cancelled    |
| Reference Data    | Products, Categories, Customers, Delivery Zones, Payment Methods                     |


---

## 3. Data Volume Assumptions

| File                | Approximate Rows | Reason                           |
| ------------------- | ---------------: | -------------------------------- |
| `orders.csv`        |          100,000 | Simulates customer orders        |
| `customers.csv`     |           20,000 | Customer master data             |
| `products.csv`      |            5,000 | Product reference information    |
| `order_events.json` |          300,000 | Simulates order lifecycle events |


---

## 4. Controlled Data Quality Issues
| Issue Type                   | Approx. Share | Why Include It                 |
| ---------------------------- | ------------: | ------------------------------ |
| Duplicate IDs                |     0.2%–0.5% | Tests uniqueness validation    |
| Missing values               |         1%–3% | Tests completeness rules       |
| Invalid reference keys       |       0.5%–1% | Tests referential integrity    |
| Negative / impossible values |     0.1%–0.5% | Tests range validation         |
| Timestamp inconsistencies    |     0.1%–0.3% | Tests chronological validation |


---

## 5. Manual Verification

Before using the generated data, the team should verify that:

Row counts are within the expected range.
Primary key fields are present and unique.
Date and timestamp values follow realistic business sequences.
Numeric fields (quantity, amount, price, etc.) contain reasonable values.
Controlled data quality defects are present but limited.
Source files contain different formats that require standardization during ETL.
Foreign key relationships between orders, customers, products, and events are valid.
The dataset is suitable for Bronze, Silver, and Gold layer processing in Databricks.
