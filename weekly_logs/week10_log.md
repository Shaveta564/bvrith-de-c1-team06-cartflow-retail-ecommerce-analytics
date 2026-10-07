# Week 10 Log — CartFlow Structured Streaming Simulation

**Week:** 10  
**Date range:** 11 September 2026 – 17 September 2026  
**Team:** P06 – CartFlow  
**Project:** CartFlow – Retail & E-commerce Analytics

---

## 1. Sprint Goal

The goal of Week 10 was to implement and validate a controlled streaming simulation for CartFlow using Databricks Auto Loader and Structured Streaming.

The work focused on processing the two approved order-status JSON drops incrementally, applying an explicit event schema, event-time watermarking, deduplication, deterministic quality routing, Trusted/Quarantine handling, audit and ledger validation, and proving recovery and idempotency through a no-new-file rerun.

---

## 2. Work Completed

| Task | Owner | Status | Evidence |
|---|---|---|---|
| Reviewed the Week 10 streaming requirements and existing CartFlow architecture | Shaveta | Done | `notebooks/07_streaming_simulation.ipynb` |
| Configured the Week 10 streaming input path | Shaveta | Done | `/Volumes/p06/default/cartflow/week10/input` |
| Prepared and validated the approved Drop 01 and Drop 02 JSON inputs | Manasa | Done | `data_sample/streaming/order_status_drop_01.json`, `data_sample/streaming/order_status_drop_02.json` |
| Implemented explicit event schema for order-status events | Nandini | Done | `notebooks/07_streaming_simulation.ipynb` |
| Implemented Databricks Auto Loader ingestion | Shaveta | Done | `notebooks/07_streaming_simulation.ipynb` |
| Implemented stable streaming checkpoints | Manasa | Done | `notebooks/07_streaming_simulation.ipynb` |
| Implemented 30-minute event-time watermarking | Nandini | Done | `notebooks/07_streaming_simulation.ipynb` |
| Implemented event deduplication and physical line-level identity handling | Shaveta | Done | `notebooks/07_streaming_simulation.ipynb` |
| Implemented quality validation and Trusted/Quarantine routing | Manasa | Done | `notebooks/07_streaming_simulation.ipynb` |
| Implemented malformed/schema-error, late, duplicate, orphan and invalid-event handling | Nandini | Done | `notebooks/07_streaming_simulation.ipynb` |
| Implemented invalid status-transition and business-rule validation | Shaveta | Done | `notebooks/07_streaming_simulation.ipynb` |
| Validated Drop 01 processing | Manasa | Done | `screenshots/week10_01_source_drops.png`, `screenshots/week10_02_quality_routing.png` |
| Validated Drop 02 incremental processing | Nandini | Done | `screenshots/week10_03_drop02_incremental.png` |
| Validated cross-drop event-ID and business-key deduplication | Shaveta | Done | `screenshots/week10_04_dedup_reconciliation.png` |
| Validated final Bronze/Trusted/Quarantine reconciliation | Shaveta, Manasa, Nandini | Done | `screenshots/week10_04_dedup_reconciliation.png` |
| Performed no-new-file recovery and idempotency validation | Shaveta, Manasa, Nandini | Done | `screenshots/week10_05_no_new_file_recovery.png` |
| Validated final source-file counts, quality routing, watermark state and run audit | Shaveta, Manasa, Nandini | Done | `screenshots/week10_06_final_validation.png` |
| Updated Structured Streaming design documentation | Shaveta, Manasa, Nandini | Done | `streaming/structured_streaming_design.md` |
| Preserved Kafka production architecture-awareness documentation | Shaveta, Manasa, Nandini | Done | `streaming/kafka_event_schema.json` |
| Completed final Week 10 validation checklist | Shaveta, Manasa, Nandini | Done | `screenshots/week10_06_final_validation.png` |

---

## 3. Key Decisions

- Continued from the existing CartFlow architecture and kept Week 10 focused on streaming rather than modifying the validated Week 8 Gold/Power BI implementation or Week 9 dashboard.
- Used Databricks Auto Loader and Structured Streaming for the controlled JSON-file streaming simulation.
- Used the actual Week 10 streaming input path:
  `/Volumes/p06/default/cartflow/week10/input`
- Used the two approved order-status JSON drops:
  - `order_status_drop_01.json`
  - `order_status_drop_02.json`
- Used an explicit 14-field schema for the order-status events.
- Used a 30-minute event-time watermark for late-event handling.
- Used the required stable Bronze checkpoint:
  `stable/checkpoints/cartflow_order_status_v1`
- Used separate downstream quality checkpointing and schema-location state.
- Used physical source filename, physical line number and stable line identity so that every input line could be traced through the pipeline.
- Used event-level deduplication and order/status/sequence business-key deduplication.
- Routed invalid or poor-quality records to Quarantine rather than allowing them into the Trusted output.
- Included validation for malformed/schema-error records, duplicate events, late events, orphaned references, invalid event types, invalid status transitions, invalid or missing sequence values and future-dated events.
- Used the existing Trusted Silver entities for reference validation:
  `p06.default.trusted_silver_orders`,
  `p06.default.trusted_silver_order_items`,
  `p06.default.trusted_silver_sellers`.
- Used stable event and business ledgers to validate repeatability and idempotency.
- Used `.trigger(availableNow=True)` for the Databricks Serverless-compatible controlled execution.
- Kept Kafka as production architecture awareness only. Kafka implementation was not required for the internship.
- Preserved the existing `streaming/kafka_event_schema.json` because it documents the design-only Kafka architecture and is separate from the actual Databricks streaming implementation.
- Completed a no-new-file rerun using the same governed checkpoints and confirmed that previously processed data did not create additional Bronze, Trusted, Quarantine, Audit or ledger records.

---

## 4. Validation Results

The completed Week 10 run processed **200 physical Bronze lines** across the two approved drops.

| Validation | Result |
|---|---:|
| Drop 01 physical lines | 100 |
| Drop 02 physical lines | 100 |
| Total Bronze physical lines | 200 |
| Trusted outcomes | 185 |
| Quarantine outcomes | 15 |
| Trusted + Quarantine | 200 |
| Duplicate Bronze line identities | 0 |
| Duplicate Trusted line identities | 0 |
| Duplicate Quarantine line identities | 0 |

The final reconciliation therefore confirms:

**Trusted + Quarantine = Bronze**

and every governed physical source line has a unique downstream outcome.

### No-New-File Recovery Validation

The no-new-file recovery validation confirmed that the governed counts remained unchanged after restarting the streaming processing with the same checkpoints:

| Metric | Before | After | Stable |
|---|---:|---:|---|
| Bronze | 200 | 200 | `true` |
| Trusted | 185 | 185 | `true` |
| Quarantine | 15 | 15 | `true` |
| Audit | 2 | 2 | `true` |
| Event ledger | 197 | 197 | `true` |
| Business ledger | 200 | 200 | `true` |

All recovery checks returned `true`.

---

## 5. Blockers / Risks

| Blocker / Risk | Impact | Resolution |
|---|---|---|
| Databricks Serverless did not support the default continuous ProcessingTime trigger used by the initial streaming approach | The streaming execution required a compatible trigger configuration | Resolved by using `.trigger(availableNow=True)` |
| Streaming quality issues were intentionally present in the approved input data | Invalid records needed to be separated from trusted records without losing evidence | Resolved through deterministic quality routing and Quarantine handling |
| Duplicate and repeated processing could affect streaming counts | Could cause incorrect results during recovery or reruns | Resolved using stable checkpoints, deduplication and event/business ledger validation |
| Late and future-dated events require event-time controls | Incorrect event timing could affect trusted processing | Addressed through event-time validation and the 30-minute watermark |
| Some streaming events intentionally reference non-existing orders, items or sellers | Such records cannot safely enter the Trusted output | Resolved through reference checks against the existing Trusted Silver tables |
| Week 10 is a controlled file-based simulation rather than a production event platform | Does not represent a continuously running production Kafka environment | Documented as a controlled student streaming simulation; Kafka remains architecture awareness only |

---

## 6. Evidence Added to GitHub

### Streaming Notebook

- `notebooks/07_streaming_simulation.ipynb`

The notebook contains the completed Week 10 streaming implementation, including:

- Explicit event schema
- Auto Loader ingestion
- Stable checkpoints
- Structured Streaming processing
- 30-minute event-time watermark
- Event and business-key deduplication
- Physical source line identity
- Quality routing
- Trusted and Quarantine handling
- Reference validation
- Audit and ledger validation
- Drop 01 processing
- Drop 02 processing
- No-new-file recovery and idempotency validation
- Final validation checklist

### Streaming Input Samples

- `data_sample/streaming/order_status_drop_01.json`
- `data_sample/streaming/order_status_drop_02.json`

### Streaming Design Documentation

- `streaming/structured_streaming_design.md`

### Kafka Architecture Awareness

- `streaming/kafka_event_schema.json`

This file documents Kafka-style production architecture awareness only. Kafka implementation is not mandatory for the internship.

### Weekly Log

- `weekly_logs/week10_log.md`

### Week 10 Screenshots / Validation Evidence

The final Week 10 evidence set contains six screenshots:

- `screenshots/week10_01_source_drops.png` — Drop 01 and Drop 02 source-file counts and physical-line identity evidence.
- `screenshots/week10_02_quality_routing.png` — Drop 01 quality routing and quarantined physical line identities.
- `screenshots/week10_03_drop02_incremental.png` — Drop 02 incremental processing and schema-error evidence.
- `screenshots/week10_04_dedup_reconciliation.png` — Cross-drop deduplication and final Bronze/Trusted/Quarantine reconciliation.
- `screenshots/week10_05_no_new_file_recovery.png` — No-new-file recovery showing governed counts unchanged before and after restart.
- `screenshots/week10_06_final_validation.png` — Final source, quality, watermark/audit and validation results showing all required checks passed.

---

## 7. Final Validation Checklist

The final Week 10 validation confirmed:

- Drop 01 physical lines = 100
- Drop 02 physical lines = 100
- Trusted + Quarantine = Bronze
- Bronze line identities are unique
- Trusted line identities are unique
- Quarantine line identities are unique
- No-new-file Bronze count remains stable
- No-new-file Trusted count remains stable
- No-new-file Quarantine count remains stable
- No-new-file Audit count remains stable
- Event ledger remains stable on no-new-file rerun
- Business ledger remains stable on no-new-file rerun

**Final result: All final Week-10 validation checks passed.**

---

## 8. AI Transparency Note

| Question | Response |
|---|---|
| Where AI helped | AI was used to assist with reviewing the Week 10 streaming requirements, checking the streaming design against the earlier CartFlow weeks, identifying potential implementation issues, improving the notebook structure, preparing validation logic and preparing supporting documentation. |
| What we changed after AI suggestion | The streaming implementation was refined to use explicit schema handling, stable checkpoints, line-level source identity, deduplication, event-time watermarking, deterministic quality routing, reference validation, audit/ledger checks and recovery/idempotency validation. The Serverless-compatible `availableNow=True` trigger was used for the completed simulation. |
| What we verified manually | The team manually executed the notebook in Databricks, processed both approved JSON drops, reviewed the streaming outputs, checked the validation results and confirmed that all final Week 10 validation checks returned `true`. |
| What we can explain without AI | We can explain the order-status JSON event source, Auto Loader ingestion, Structured Streaming flow, explicit schema, Bronze processing, quality routing, Trusted/Quarantine handling, deduplication, watermarking, checkpoints, reference validation, recovery testing and final validation results. |

---

## 9. Next Week Preparation

- Preserve the completed and validated Week 10 streaming notebook as the final streaming implementation.
- Ensure all Week 10 files, documentation and six final screenshots are organized in the project repository.
- Review the final CartFlow repository structure and confirm that Weeks 1–10 are represented correctly.
- Preserve the validated Week 8 Gold and Power BI implementation and Week 9 dashboard refinement as the baseline project outputs.
- Verify that Week 10 streaming remains separate from the Week 8/9 Gold and Power BI source boundary.
- Prepare the complete CartFlow project for final review and submission.
- Be prepared to explain the complete project flow from source data and Trusted Silver through Gold, Power BI dashboard refinement and the Week 10 streaming simulation.
