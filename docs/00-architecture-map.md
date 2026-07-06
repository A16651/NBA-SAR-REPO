# Architecture Overview

This document provides a sequential developer roadmap for the Automated NBA SAR Generation Platform. Rather than presenting the system as a single complex model, the architecture is broken down into a series of logical viewpoints designed to be read in order.

---

## Architectural Roadmap

### [01 — System's Basic Overview](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/01-systems-basic-overview.md)
* **Purpose:** High-level system context defining the boundaries, primary users, and external system integrations.
* **Focus:** Faculty/Coordinator interaction, read-only ERP connection, and private AI isolation.

### [02 — Container Architecture](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/02-container-architecture.md)
* **Purpose:** Exposes the major deployable services and data stores making up the platform.
* **Focus:** API gateway, rule execution engine, narrative agent, and databases.

### [03 — Compile & Runtime Workflow](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/03-compile-runtime-workflow.md)
* **Purpose:** Differentiates the offline rule compilation phase from the live report generation pipeline.
* **Focus:** Pre-compiling ERP mappings versus executing dynamic runtime tasks.

### [04 — Rule Execution Engine](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/04-rule-execution-engine.md)
* **Purpose:** Shows how metrics are calculated deterministically with automatic fallback logic.
* **Focus:** Domain processors, formula library, and runtime AI fallback rule inference.

### [05 — Narrative Generation Engine](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/05-narrative-generation-engine.md)
* **Purpose:** Illustrates the qualitative RAG workflow that generates textual responses.
* **Focus:** Context retrieval, prompt templates, and strict output validation.

### [06 — AI-Assisted Mapping](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/06-ai-assisted-mapping.md)
* **Purpose:** Details how ERP database schema and NBA templates are compiled into executable rules.
* **Focus:** Schema analyzer, AI mapping rule generator, and human-in-the-loop review.

### [07 — Repository Architecture](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/07-repository-architecture.md)
* **Purpose:** Visualizes the storage layout across relational database, vector database, object storage, and cache.
* **Focus:** Rules repository, factbooks, templates, and binary assets.

### [08 — Report Generation Sequence](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/08-report-generation-sequence.md)
* **Purpose:** Runtime call flow tracing messages between components from request to PDF download.
* **Focus:** Synchronous orchestration and asynchronous task coordination.

### [09 — Deployment Architecture](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/09-deployment-architecture.md)
* **Purpose:** Explains physical clustering, infrastructure zones, and server communication pathways.
* **Focus:** Web servers, worker processes, private AI hardware, and secure firewalls.

### [10 — Security Design](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/10-security-design.md)
* **Purpose:** Outlines access governance, data protection, trust boundaries, and auditing.
* **Focus:** Encryption, role permissions, factbook immutability, and compliance trails.

---

## Architectural Principles

* **Separation of Concerns:** Subsystems perform singular responsibilities to remain decoupled.
* **Deterministic Calculations First:** Numbers are computed before generating narrative text; AI never does math.
* **Strictly Read-Only Integration:** Vidyanvesha ERP data is queried but never written to or altered.
* **Auditability and Traceability:** Every calculated metric must maintain a complete calculation trace.
* **Human-in-the-Loop Governance:** AI simplifies administrative mapping work but requires explicit human approval.

---

**Next Step:** Review the first diagram: [01 — System's Basic Overview](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/01-systems-basic-overview.md)