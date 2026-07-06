# 02 — Container Architecture

## Purpose
This diagram illustrates the container-level architecture (C4 Level 2) of the system, identifying individual deployable services, databases, external systems, and how runtime and configuration flows travel through them.

---

## Core Containers

### 1. Runtime Services
* **SAR Portal (Next.js):** The frontend web application where coordinators configure templates and monitor report generation.
* **Report Orchestrator (FastAPI):** The API Gateway that accepts client requests, starts workflows, and pushes background processing jobs to Redis.
* **Report Context Builder:** Formulates the starting parameters and metadata snapshot for a report run.
* **ERP Data Connector:** Intermediary layer executing read-only database queries to fetch raw institutional data.
* **Rule Execution Engine:** Runs pre-defined mathematical rules to compute numeric facts.
* **Runtime Mapping Agent:** Orchestrates quick AI schema inferences if a required rule is missing at runtime.
* **Narrative Generation Engine:** Coordinates context-retrieval and LLM calls to construct narrative sections.
* **Document Assembler:** Merges quantitative tables and qualitative text into a final formatted PDF.

### 2. Configuration Services (Rule Setup)
* **AI Mapping Compiler:** Translates new NBA template fields and raw ERP columns into candidate formulas.
* **Rule Validator & Verification Services:** Ensure proposed mappings match compiler structures and security regulations before publication.

### 3. Data Stores & Infrastructure
* **Redis:** Serves as the high-speed background job queue broker and session cache.
* **Rule Repository:** Holds approved, version-controlled mathematical rules and schema mappings.
* **Knowledge Repository:** Stores execution outputs including immutable FactBooks, audit trails, and narrative text.
* **Vector Database:** Stores embedded institutional documentation used for RAG query retrieval.
* **Object Storage:** Stores unstructured binary files like finalized PDFs and raw evidence documents.

### 4. External Dependencies
* **Vidyanvesha ERP:** External relational system of record containing student/faculty data.
* **Private AI Platform:** Contains the isolated **Mapping LLM** and **Narrative LLM**.

---

## Sequence of Flows

### Runtime Flow
1. **Request:** The **Faculty** triggers report generation in the **SAR Portal**. The request hits the **Report Orchestrator (FastAPI)**.
2. **Asynchronous Jobs:** The orchestrator submits task requests to **Redis**, which are handled asynchronously by background worker containers.
3. **Context Setup:** The **Report Context Builder** requests a snapshot from the **ERP Data Connector**, which reads data from the **Vidyanvesha ERP**.
4. **Deterministic Calculation:** The **Rule Execution Engine** loads approved formulas from the **Rule Repository** to compute metrics, storing the results in the **Knowledge Repository**.
   * *Fallback:* If a rule is missing, the **Runtime Mapping Agent** queries the **Mapping LLM** to infer a temporary rule, caches it in the **Rule Repository**, and executes.
5. **Narrative Generation:** The **Narrative Engine** fetches numerical facts from the **Knowledge Repository** and institutional text from the **Vector Database**, calling the **Narrative LLM** to produce qualitative reports.
6. **Assembly:** The **Document Assembler** pulls calculated facts and narratives from the **Knowledge Repository**, formats the final PDF, and places it in **Object Storage**.
7. **Download:** The user downloads the generated PDF from **Object Storage** via the **SAR Portal**.

### Configuration Flow (Rule Compilation)
1. **Input:** An updated **NBA SAR Template** or changes in **Vidyanvesha ERP** metadata trigger the **AI Mapping Compiler**.
2. **Drafting:** The compiler invokes **Mapping LLM** to draft candidate mapping rules.
3. **Validation & Publish:** Draft rules are run through the **Rule Validator** and **Verification Service** before being published as verified rules in the **Rule Repository**.

---

**Next Step:** See how compile-time matches runtime: [03 — Compile & Runtime Workflow](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/03-compile-runtime-workflow.md)
