# Automated NBA SAR Generation System
## Software Architecture

This repository contains the software architecture for the **Automated NBA Self-Assessment Report (SAR) Generation System**, designed as an extension to the existing **Vidyanvesha ERP**.

The objective of this system is to automate the generation of NBA accreditation reports by combining deterministic computation with AI-assisted narrative generation, while maintaining complete traceability, auditability, and compliance with NBA guidelines.

---

# Architecture Philosophy

The architecture is built around one simple principle:

> **AI may assist in writing the report, but it must never determine the facts.**

All numerical values are computed using deterministic algorithms. Artificial Intelligence is used only for tasks that benefit from natural language understanding, such as schema mapping and narrative generation.

This separation ensures that every generated report remains explainable, reproducible, and suitable for accreditation purposes.

---

# System Principles

The architecture follows these core principles:

- **Separation of Concerns:** Isolated modular components optimized for distinct functions.
- **Read-Only ERP Integration:** The system queries institutional data but never writes to the ERP.
- **Deterministic Before AI:** Numbers are calculated via code formulas before prompt generation.
- **Human-in-the-Loop Governance:** AI handles complex schema matching proposals but requires human confirmation.
- **Immutable Runtime Artifacts:** Executed report snapshots (FactBooks) are kept read-only.
- **Loose Coupling:** Services communicate using structured data payloads.
- **Security by Design:** Private model execution and partitioned database layers.
- **Complete Auditability:** Every computed cell has a calculation trace pointing to source databases.

---

# Core Architectural Artifacts

Throughout the architecture, several domain artifacts remain consistent across all components.

| Artifact | Description |
|-----------|-------------|
| **Report Context** | Metadata snap describing the target program, scope, and template parameters. |
| **ERP Snapshot** | Frozen read-only snapshot retrieved from the university ERP. |
| **FactBook** | Immutable collection of quantitative calculation metrics. |
| **Calculation Trace** | Complete validation trace containing formulas, inputs, and intermediate metrics. |
| **Narrative Package** | Validated, grounded qualitative content sections written by the LLM. |
| **Audit Response** | Formatted template objects ready for final report integration. |
| **Generated Report** | Final, verified submission-ready PDF document. |

---

# Architecture Views (Roadmap Sequence)

The architecture is structured as a sequential developer roadmap. Please read these viewpoints in order:

| Step | View / Diagram Name | Purpose | Documentation Link |
|:---:|---------------------|---------|--------------------|
| **00** | Architecture Overview | Introduces the roadmap sequence and high-level principles. | [00-architecture-map.md](docs/00-architecture-map.md) |
| **01** | System's Basic Overview | Outlines system boundaries, actors, and external system boundaries. | [01-systems-basic-overview.md](docs/01-systems-basic-overview.md) |
| **02** | Container Architecture | Exposes services, data stores, API endpoints, and internal container layouts. | [02-container-architecture.md](docs/02-container-architecture.md) |
| **03** | Compile & Runtime Workflow | Details compile-time rule creation versus live runtime generation. | [03-compile-runtime-workflow.md](docs/03-compile-runtime-workflow.md) |
| **04** | Rule Execution Engine | Describes formula processing engines and runtime mapping LLM fallback. | [04-rule-execution-engine.md](docs/04-rule-execution-engine.md) |
| **05** | Narrative Generation Engine | Illustrates prompt composer mechanics, vector RAG retriever, and validation. | [05-narrative-generation-engine.md](docs/05-narrative-generation-engine.md) |
| **06** | AI-Assisted Mapping | Explains how template rules are generated and approved prior to runtime. | [06-ai-assisted-mapping.md](docs/06-ai-assisted-mapping.md) |
| **07** | Repository Architecture | Maps system databases, cache, and object storage to their saved content types. | [07-repository-architecture.md](docs/07-repository-architecture.md) |
| **08** | Report Generation Sequence | Details runtime call sequencing between services from start request to download. | [08-report-generation-sequence.md](docs/08-report-generation-sequence.md) |
| **09** | Deployment Architecture | Displays application clusters, data storage segments, and AI model networks. | [09-deployment-architecture.md](docs/09-deployment-architecture.md) |
| **10** | Security Design | Describes RBAC rules, runtime data isolation, and end-to-end trace auditing. | [10-security-design.md](docs/10-security-design.md) |

---

# Repository Structure

```text
architecture/
├── README.md
├── diagrams/
│   ├── SVGs/                              # All diagrams in SVG format
│   ├── 00-architecture-map.d2
│   ├── 01 System's Basic Overview.d2
│   ├── 02 Container Architecture.d2
│   ├── 03 Compile & Runtime Workflow.d2
│   ├── 04 Rule Execution Engine.d2
│   ├── 05 narrative genration engine.d2
│   ├── 06 AI assited Maping.d2
│   ├── 07 Repository Architecture.d2
│   ├── 08  report genration sequence.d2
│   ├── 09 deployment architecture.d2
│   └── 10 security design.d2
└── docs/
    ├── 00-architecture-map.md
    ├── 01-systems-basic-overview.md
    ├── 02-container-architecture.md
    ├── 03-compile-runtime-workflow.md
    ├── 04-rule-execution-engine.md
    ├── 05-narrative-generation-engine.md
    ├── 06-ai-assisted-mapping.md
    ├── 07-repository-architecture.md
    ├── 08-report-generation-sequence.md
    ├── 09-deployment-architecture.md
    └── 10-security-design.md
```

---

# Reading Guide for Developers

If you are new to this repository:
1. Start with the **[Architecture Overview](docs/00-architecture-map.md)** to understand the overall philosophy.
2. Read the documentation files sequentially in numerical order (`01` through `10`).
3. Cross-reference each `.md` file in `docs/` with its source diagram in `diagrams/` to see components and connections clearly.

---

## Install D2 Compiler

To modify or compile the architecture diagrams, install Terrastruct's D2 compiler.

### 1. Download the D2 compiler

**Windows (PowerShell):**
```powershell
winget install Terrastruct.D2
```

**macOS (Homebrew):**
```bash
brew install d2
```

### 2. Add D2 to your system PATH

Ensure the directory containing the `d2` executable is added to your system's `PATH` environment variable.

Verify the installation by running:
```bash
d2 --version
```

### 3. Configure the VS Code extension

0. Install d2 Extenstion in VS Code 
1. Open **VS Code**.
2. Press **Ctrl/Cmd + Shift + P** and select **Preferences: Open Settings (UI)**.
3. Search for **`d2.execPath`**.
4. Set it to the full path of the D2 executable (e.g., `C:\Program Files\d2\d2.exe` on Windows or `/opt/homebrew/bin/d2` on macOS).