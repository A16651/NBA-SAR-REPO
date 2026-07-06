# 03 — Compile & Runtime Workflow

## Purpose
This diagram outlines the complete lifecycle of rules and report generation, showing how offline setup (**Compile Phase**) feeds into the live execution pipeline (**Runtime Phase**).

---

## 1. Compile Phase (Offline Setup)
The compile phase is a preparation sequence executed when schema structures or accreditation guidelines change. It guarantees that the runtime rule engine is driven by pre-validated, deterministic instructions rather than ad-hoc runtime AI generation.

* **Analyze ERP Schema & NBA Template:** Analyzes the database layout and target report fields.
* **AI Generate Rules:** Employs LLM mapping to draft data association rules.
* **Validate Rules:** Validates structure and safety of candidate rules.
* **Publish Rule Set:** Publishes the verified rule package to the system's active storage, which is then loaded at runtime.

---

## 2. Runtime Phase (Live Execution)
The runtime phase runs whenever a user triggers a report generation request. It progresses step-by-step to compile raw data into a submission-ready PDF.

1. **Generate SAR Request:** Initiated by the user.
2. **Create Report Context:** Formulates target parameters (academic year, program, scope).
3. **Acquire ERP Snapshot:** Pulls a frozen read-only snapshot of institutional records.
4. **Load Approved Rules:** Ingests the latest compiled rules set from the repository.
5. **Execute Rule Engine:** Runs formulas against the ERP snapshot.
   * *Success:* Proceed directly to narrative generation.
   * *Rule Missing:* Enters the **AI Fallback** block to temporarily infer the missing association rule, then proceeds.
6. **Generate Narratives:** Combines calculated numbers with textual contextual lookup.
7. **Assemble Final Report:** Formats and merges quantitative tables and narratives.
8. **Store Report & Audit Artifacts:** Saves the output PDF and traces in object and database storage.
9. **Notify & Download:** Notifies the coordinator that the file is ready to download.

---

**Next Step:** Dive deeper into the math execution: [04 — Rule Execution Engine](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/04-rule-execution-engine.md)
