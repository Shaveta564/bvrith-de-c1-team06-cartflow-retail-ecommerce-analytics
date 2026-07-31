# Week 03 Log — CartFlow Data Exploration

**Week:** 3  
**Date range:** 24 July 2026 – 30 July 2026  
**Team:** Individual  
**Project:** CartFlow – Retail & E-commerce Analytics

---

## 1. Sprint Goal

The goal of this sprint was to explore the CartFlow source data, understand the relationships between datasets, identify data quality issues, and demonstrate join multiplication before building the Bronze layer.

---

## 2. Work Completed

| Task | Owner | Status | Evidence |
|---|---|---|---|
| Uploaded CartFlow source files to Databricks Volume | Pavan | Done | week03_volume_and_source.png |
| Created Spark DataFrames and SQL Views | Pavan | Done | Notebook |
| Inspected schemas and table contents | Pavan | Done | week03_schema.png |
| Executed SQL exploration queries | Pavan | Done | week03_sql_output.png |
| Verified source files and Volume path | Pavan | Done | week-3_assigined volume path.png |
| Explored source data and relationships | Pavan | Done | week03_event_locations.png |

---

## 3. Key Decisions

- Used Spark SQL temporary views for data exploration.
- Kept the Bronze layer limited to a demonstration table as required for Week 3.

---

## 4. Blockers / Risks

| Blocker | Impact | Help Needed |
|---|---|---|
| Understanding join multiplication | Delayed analysis initially | Reviewed notebook examples and SQL queries |

---

## 5. Evidence Added to GitHub

- week-3_assigined volume path.png
- week03_volume_and_source.png
- week03_schema.png
- week03_sql_output.png
- week03_event_locations.png
- Updated Week 03 Notebook

---

## 6. AI Transparency Note

| Question | Response |
|---|---|
| Where AI helped | Explained Spark SQL concepts, schema inspection, joins, and GitHub documentation. |
| What we changed after AI suggestion | Improved screenshot organization and documentation. |
| What we verified manually | SQL query outputs, schemas, DataFrame creation, and Volume path. |
| What we can explain without AI | Data loading, schema inspection, SQL queries, joins, and Week 3 workflow. |

---

## 7. Next Week Preparation

- Begin building the official Bronze tables.
- Implement data ingestion and validation for Week 4.
