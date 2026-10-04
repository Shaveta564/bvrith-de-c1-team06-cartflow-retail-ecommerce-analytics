# Structured Streaming Design

**Week:** 10  
**Project:** CartFlow  
**Purpose:** Document the controlled Structured Streaming simulation implemented in Databricks using the approved order-status JSON drops.

---

## 1. Streaming Scenario

Week 10 simulates order-status events arriving as controlled JSON file drops.

Two approved event files are used:

- `order_status_drop_01.json`
- `order_status_drop_02.json`

Databricks Auto Loader detects the JSON files from the streaming input path. Structured Streaming processes the incoming records using an explicit event schema and a stable checkpoint.

The streaming flow is:

```text
Order Status JSON Drops
          ↓
Databricks Auto Loader
          ↓
Streaming Bronze
          ↓
Quality Validation and Routing
      ↙              ↘
   Trusted         Quarantine
      ↓                ↓
   Audit / Ledgers / Validation
          ↓
   Recovery and Idempotency Checks
