# 07 — Repository Architecture

## Purpose
This diagram details the storage layout and database technologies used by the system, identifying exactly what data belongs to which repository component.

---

## Storage Components & Contents

### 1. Rule Repository (PostgreSQL)
Stores versioned instructions on how data is mapped and calculated.
* **Contents:** Mapping rules, formula rules, rule versions, and administrative rule metadata.

### 2. Knowledge Repository (PostgreSQL)
Stores execution-specific numeric results and text narratives.
* **Contents:** Immutable FactBooks, calculated metrics, narratives, audit trails, and data provenance.

### 3. Prompt Template Repository (PostgreSQL)
Maintains system-level formatting structures.
* **Contents:** Prompt templates, NBA section descriptions, and prompt version history.

### 4. Vector Database (Qdrant)
Stores text embeddings utilized during prompt retrieval.
* **Contents:** Institutional embeddings, previous SAR reports, NBA handbook documents, and university policy files.

### 5. Object Storage (MinIO / S3)
Stores large binary objects outside the SQL database.
* **Contents:** Generated final PDFs, uploaded evidence files (certificates, MOUs), and master templates.

### 6. Redis Runtime Cache (Redis)
Maintains high-speed transient data structures.
* **Contents:** Cached mapping rules, background Celery queue jobs, and active session cache.

---

## Architectural Principles
* **Separation of Concerns:** Relational metrics (Knowledge Repository), unstructured binary files (Object Storage), semantic embeddings (Vector Database), and setup data (Rule Repository) are stored in isolated systems optimized for their individual data models.
* **Immutability:** Runtime report outputs stored in the Knowledge Repository remain frozen once written, assuring historical compliance audits are reproducible.

---

**Next Step:** Trace calls sequentially at runtime: [08 — Report Generation Sequence](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/08-report-generation-sequence.md)
