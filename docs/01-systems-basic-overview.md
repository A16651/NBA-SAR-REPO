# 01 — System's Basic Overview

## Purpose
This diagram defines the high-level boundary of the **AI-Assisted NBA SAR Generation Platform**, detailing how it interacts with users, the existing ERP system, private AI components, and data storage.

---

## Core Entities

* **NBA Coordinator / Faculty:** The primary user who requests reports, reviews draft narratives, and downloads the finalized PDF.
* **AI-Assisted NBA SAR Generation Platform:** The main application system responsible for orchestrating report generation, running rules, and managing workflows.
* **Vidyanvesha ERP:** The institution's primary data store containing student, faculty, and academic records. Integration is strictly read-only.
* **Private AI Platform:** A self-hosted, secure LLM infrastructure used for mapping rules compilation and qualitative narrative text generation.
* **Knowledge & SAR Repository:** The persistent storage for finalized reports, mapping rules, generated FactBooks, and audit traces.

---

## Data Flow & Interactions

1. **User Action:** The **NBA Coordinator / Faculty** requests report generation or reviews progress on the **SAR Platform**.
2. **ERP Extraction:** The **SAR Platform** pulls student, faculty, and academic records from the **Vidyanvesha ERP** (read-only query).
3. **AI Reasoning:** The **SAR Platform** sends schema structures, prompts, and facts to the **Private AI Platform** to compile metadata mappings, run AI fallbacks, and generate qualitative narrative sections.
4. **Report Storage:** Once generated, the **SAR Platform** stores rules, metrics, narratives, and audit evidence in the **Knowledge & SAR Repository**.
5. **PDF Delivery:** The **NBA Coordinator / Faculty** downloads the finalized NBA SAR report directly from the **Knowledge & SAR Repository**.

---

## Key Architectural Decisions
* **ERP Integrity:** The platform has absolutely no write access to the Vidyanvesha ERP. The ERP remains the untouchable system of record.
* **Data Security:** The AI platform is hosted privately inside the organizational network to ensure student and faculty records never leak to public endpoints.

---

**Next Step:** Learn how these systems are structured internally: [02 — Container Architecture](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/02-container-architecture.md)
