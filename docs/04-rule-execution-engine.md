# 04 — Rule Execution Engine

## Purpose
This diagram details the architecture of the **Rule Execution Engine**, the component responsible for computing all quantitative metrics required for the NBA SAR report. It enforces deterministic mathematical execution and handles rule exceptions dynamically via an AI fallback recovery flow.

---

## Component Responsibilities

### 1. Rule Loading
* **Rule Repository:** Relational database holding all approved, versioned database mapping and calculation formulas.
* **Rule Loader:** Dynamically selects and retrieves active rule definitions for the current report context.
* **Rule Runtime Cache:** An in-memory cache (Redis) that keeps active rules hot to reduce database queries.

### 2. Rule Execution
* **Rule Dispatcher:** Orchestrates calculations by scheduling which formulas to run and passing the **ERP Snapshot** data down.
* **Mapping Engine:** Directs how ERP columns associate with target NBA fields.
* **Formula Engine:** Computes complex mathematical ratios (e.g., student-faculty ratio, enrollment ratios, placement averages).
* **Validation Engine:** Checks calculated values against structural boundaries and flags abnormal anomalies.

### 3. Runtime AI Recovery (Fallback)
* **Runtime Mapping Agent:** Initiates when the engine detects a missing mapping rule for a needed field.
* **Mapping LLM:** Infers a candidate query structure or field association based on ERP schema descriptions and returns a temporary rule to allow the engine to complete.

### 4. Output
* **Immutable FactBook:** The final computed collection of mathematical facts. Once compiled, it is read-only.
* **Knowledge Repository:** Stores the FactBook alongside a complete calculation trace.

---

## Detailed Data Flow

1. **Load:** The **Rule Loader** grabs rules from the **Rule Repository** and caches them in the **Rule Cache**.
2. **Dispatch:** The **Rule Dispatcher** receives the **ERP Snapshot** and cached rules, invoking downstream engines.
3. **Compute:** The **Mapping**, **Formula**, and **Validation** engines evaluate data to produce the final **FactBook**.
4. **AI Fallback (If needed):** If a mapping rule is missing during execution:
   * The **Mapping Engine** notifies the **Runtime Mapping Agent**.
   * The agent asks the **Mapping LLM** to infer a mapping rule.
   * The LLM responds with a **Temporary Runtime Rule** which is fed back into the mapping pipeline to compile the FactBook.
5. **Persist:** The finished **FactBook** is stored permanently in the **Knowledge Repository**.

---

**Next Step:** See how qualitative narratives are generated: [05 — Narrative Generation Engine](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/05-narrative-generation-engine.md)
