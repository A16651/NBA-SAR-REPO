# 06 — AI-Assisted Mapping

## Purpose
This diagram describes the compilation system used to associate the target fields of the official **NBA SAR Template** with column schemas inside the **Vidyanvesha ERP**. By running this process offline, mappings are generated, reviewed, and published prior to execution.

---

## Component Responsibilities

### 1. Analysis Tiers
* **Schema Analyzer:** Inspects ERP columns, data types, and logical relationships to create a structural schema map.
* **Template Analyzer:** Parses target NBA guidelines to structure expected input parameters.

### 2. Rule Mapping & Generation
* **Mapping LLM:** Proposes draft associations linking ERP metadata properties to NBA variables.
* **Rule Generator:** Converts LLM suggestions into executable query code or formula instructions.

### 3. Verification & Version Control
* **Rule Validator:** Evaluates draft rules for mathematical syntax errors or data type mismatches.
* **Rule Verification Service:** The administrative portal where human experts review and approve candidate rules.
* **Rule Version Manager:** Tracks and indexes active and legacy rules inside the repository.
* **Rule Repository:** Relational database storing verified and version-controlled active rules.

### 4. Continuous Improvement
* **Runtime Knowledge Feedback:** Reports runtime failures or dynamic rule edits back to the Mapping LLM to refine compilation accuracy for future iterations.

---

## Process Flow

1. **Intake:** The **ERP Schema Metadata** and the **NBA SAR Template** are parsed by their respective analyzer services.
2. **AI Proposal:** The **Mapping LLM** receives the analyzed schemas and proposes mappings, which the **Rule Generator** writes as code structures.
3. **Verify:** The proposed rules are structurally tested by the **Rule Validator** and sent to the **Rule Verification Service** for human audit and review.
4. **Publish:** The approved rules are versioned by the **Rule Version Manager** and stored in the **Rule Repository** for runtime use.
5. **Learn:** High-level metrics and runtime adjustment feedback loop back into the **Mapping LLM** to improve future generation cycles.

---

**Next Step:** Learn how databases and file repositories are architected: [07 — Repository Architecture](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/07-repository-architecture.md)
