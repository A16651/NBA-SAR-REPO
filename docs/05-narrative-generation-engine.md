# 05 — Narrative Generation Engine

## Purpose
This diagram outlines the **Narrative Generation Engine**, which produces qualitative narrative descriptions for the NBA SAR. It uses a Retrieval-Augmented Generation (RAG) structure to ensure all AI-generated text remains grounded in deterministic mathematical results and official institutional data.

---

## Component Responsibilities

### 1. Prompt Construction (RAG Pipeline)
* **Prompt Builder:** Accepts the computed FactBook numbers and schedules prompts for needed narrative sections.
* **Context Retriever:** Performs semantic vector searches to fetch institutional files associated with the target section.
* **Vector Database:** Stores embedded policies, handbooks, guidelines, and previous SAR answers.
* **Prompt Template Repository:** Stores pre-structured templates detailing how paragraphs should be formatted.
* **Prompt Composer:** Merges raw facts, retrieved context, and templates into a clean prompt package.

### 2. AI Generation
* **Narrative LLM:** Private inference instance that receives structured prompts and generates narrative responses.

### 3. Quality Assurance & Output
* **Narrative Validator:** Ensures the generated text is structured correctly, does not contain hallucinated calculations, and references actual FactBook numbers.
* **Knowledge Repository:** Stores validated narratives alongside the FactBook.

---

## Detailed Data Flow

1. **Trigger:** The **Prompt Builder** receives the **Immutable FactBook** and starts the narrative generation pipeline.
2. **Context Lookup:** The builder directs the **Context Retriever** to search the **Vector Database** for relevant institutional text.
3. **Compose:** The **Prompt Composer** combines the numeric facts (from prompt builder), semantic context (from vector database), and formatting layouts (from **Prompt Template Repository**).
4. **Generate:** The compiled prompt goes to the **Narrative LLM** for qualitative text composition.
5. **Verify:** The LLM's response is parsed and checked by the **Narrative Validator** to ensure it remains factual and grounded.
6. **Save:** Approved text is saved directly to the **Knowledge Repository**.

---

**Next Step:** See how mapping rules are initialized and improved: [06 — AI-Assisted Mapping](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/06-ai-assisted-mapping.md)
