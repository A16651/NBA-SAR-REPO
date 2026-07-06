# 08 — Report Generation Sequence

## Purpose
This sequence diagram shows the runtime chronological execution pathway of a report request, mapping the step-by-step messaging flow between client components, engines, databases, and LLMs.

---

## Participant Roles

* **Faculty:** The user initiating the report from the browser.
* **SAR Portal:** Next.js frontend handling user interaction.
* **Report Orchestrator:** FastAPI backend scheduling background workers.
* **Context Builder:** Snaps academic, criteria, and ERP parameters together.
* **Rule Execution Engine:** Deterministic calculation unit.
* **Runtime Mapping Agent & Mapping LLM:** AI fallback recovery system if a rule is missing.
* **Knowledge Repository:** relational database storing metrics and narratives.
* **Narrative Engine & Narrative LLM:** Textual generation components.
* **Document Assembler:** Layout engine compiling raw sections into PDF format.
* **Object Storage:** Flat-file server storing finalized reports.

---

## Detailed Sequence Steps

1. **Initiate:** The **Faculty** requests SAR generation via the **SAR Portal**.
2. **Orchestrate:** The portal sends a REST API request to the **Report Orchestrator**.
3. **Build Context:** The orchestrator instructs the **Context Builder** to snap parameters and retrieve the ERP snapshot.
4. **Calculate:** The Context Builder invokes the **Rule Execution Engine** to execute approved calculation rules.
5. **Write Facts:** The Rule Execution Engine outputs calculated metrics to the **Knowledge Repository** as an **Immutable FactBook**.
   * *Optional Fallback Flow:* If the engine discovers a missing mapping rule, it signals the **Runtime Mapping Agent** -> calls **Mapping LLM** to infer query structures -> returns a **Temporary Rule** to rule engine -> updates **FactBook** in **Knowledge Repository**.
6. **Compose Narratives:** The orchestrator triggers the **Narrative Engine**. The engine reads metrics from the **Knowledge Repository**, queries the **Narrative LLM** to write text, and stores generated narratives back in the **Knowledge Repository**.
7. **Assemble PDF:** The orchestrator instructs the **Document Assembler** to compile the document. The assembler reads numbers and narratives from the **Knowledge Repository** and pushes the compiled PDF into **Object Storage**.
8. **Deliver:** The **SAR Portal** retrieves the PDF download link from **Object Storage** to deliver it to the **Faculty** member.

---

**Next Step:** Review the infrastructure layout: [09 — Deployment Architecture](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/09-deployment-architecture.md)
