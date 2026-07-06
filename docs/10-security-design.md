# 10 — Security Design

## Purpose
This diagram describes the security controls, access rules, data isolation boundaries, and audit mechanisms built into the platform to ensure generated reports remain secure and institutionally compliant.

---

## Security Domains

### 1. Identity & Access (User Controls)
* **Authentication:** Validates user credentials before granting system entrance.
* **Role-Based Access Control (RBAC):** Restricts portal actions based on roles (e.g., Only administrators/experts can manage templates and rule versions).

### 2. Runtime Governance (Computation Controls)
* **Rule Version Tracking:** Logs which rule template was active during execution.
* **Immutable FactBook:** Prevents mathematical calculation manipulation.
* **Execution Provenance:** Records calculation details so any number can be verified during external accreditation audits.

### 3. AI Governance (Model Controls)
* **Prompt Versioning:** Tracks exactly what instructions were sent to the LLM.
* **Model Versioning:** Identifies the active version of the privately-hosted model.
* **AI Output Validation:** Runs validation queries to ensure text responses are grounded.

### 4. Audit & Compliance (Verification Controls)
* **Immutable Audit Log:** Records administrative modifications.
* **SAR Version History:** Tracks revision steps for draft reports.
* **End-to-End Traceability:** Links raw ERP records, formulas, FactBook entries, narratives, and final PDF files in a single trace.

### 5. Security Controls (Infrastructure Controls)
* **TLS Encryption:** Encrypts data moving across system containers.
* **Encrypted Storage:** Protects databases and S3 object stores containing sensitive records.

---

## Governance & Security Flow

```
[Identity & Access]
  └─ Authentication -> RBAC Authorization
       └─ [Runtime Governance]
            ├─ Rule Versioning / FactBook Immutability / Execution Provenance
            └─ [AI Governance]
                 ├─ Prompt Versioning / Model Versioning / Output Validation
                 └─ [Audit & Compliance]
                      ├─ Immutable Audit Logs / SAR Versioning / Traceability Map
                      └─ [Security Controls]
                           └─ TLS Transport Encryption / Encrypted Storage
```

---

**Back to Start:** Return to overview roadmap: [00 — Architecture Map](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/00-architecture-map.md)
