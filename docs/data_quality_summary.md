# Data Quality Summary

**Week:** 6  
**Purpose:** Summarize data quality rules, failures and business impact.

---

## 1. Quality Rule Results
| Rule ID | Rule Name             | Severity | Passed Count | Failed Count | Business Impact                                                                 |
| ------- | --------------------- | -------: | -----------: | -----------: | ------------------------------------------------------------------------------- |
| DQ-01   | Required ID not null  |     High |   **99,800** |      **200** | Records without IDs cannot be uniquely identified and should not be trusted.    |
| DQ-02   | Duplicate key check   |     High |   **99,801** |      **199** | Duplicate keys can inflate KPIs and lead to incorrect dashboard metrics.        |
| DQ-03   | Valid reference key   |   Medium |  **109,479** |      **521** | Invalid foreign keys break joins between tables and produce incomplete reports. |
| DQ-04   | Valid timestamp order |   Medium |   **99,602** |      **398** | Incorrect event sequence affects delivery time, SLA, and operational metrics.   |


---

## 2. Failed Record Examples
| Rule ID | Sample Record ID                 | Failure Reason                             | Action / Handling                                       |
| ------- | -------------------------------- | ------------------------------------------ | ------------------------------------------------------- |
| DQ-01   | NULL Order ID                    | Required identifier is missing             | Exclude record and send to source system for correction |
| DQ-02   | Duplicate Order ID               | Same Order ID appears more than once       | Remove duplicate after business validation              |
| DQ-03   | Invalid Order ID Reference       | Payment references a non-existent Order ID | Reject or quarantine until reference is corrected       |
| DQ-04   | Order ID with invalid timestamps | Approval time occurs before purchase time  | Flag record and correct timestamp before Gold layer     |


---

## 3. What Should Block Gold Metrics?

The following rules should block or flag Gold table generation:

DQ-01 – Required ID not null: Gold tables should not contain records without primary keys.
DQ-02 – Duplicate key check: Duplicate business keys can produce incorrect counts, revenue, and customer metrics.
DQ-03 – Valid reference key: Invalid foreign keys should be flagged because they lead to failed joins and incomplete analytics.
DQ-04 – Valid timestamp order: Records with inconsistent timestamps should be excluded from time-based KPIs until corrected.

---

## 4. Quality Summary

The dataset is generally in good condition, with most records passing all quality checks. The largest number of failures occurred in the reference key validation (521 records), followed by timestamp validation (398 records). Missing IDs and duplicate keys are fewer in number but have the highest business impact because they directly affect data integrity and dashboard accuracy. Invalid reference keys can cause incomplete joins, while incorrect timestamps impact delivery and SLA reporting. High-severity issues should be excluded from the Gold layer, whereas medium-severity issues should be flagged for review. The mentor should carefully review primary key integrity, duplicate handling, and foreign key validation before approving the final Gold datasets
