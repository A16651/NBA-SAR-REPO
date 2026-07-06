# 09 — Deployment Architecture

## Purpose
This diagram describes the physical deployment topology of the system, partitioning services into distinct physical clusters and detailing network integration boundaries.

---

## Infrastructure Layers

### 1. Client Layer
* **Faculty Browser:** Standard client web browser where coordinators access the portal over HTTPS.

### 2. Application Cluster
Hosts deployment containers of core platform services.
* **Services:** SAR Portal UI (Next.js), Report Orchestrator FastAPI API, Context Builder, Rule Execution Engine, Narrative Engine, and Document Assembler.

### 3. Private AI Cluster
Dedicated self-hosted GPUs hosting deep-learning model servers.
* **Services:** Mapping LLM and Narrative LLM models, running inside the private institutional zone to enforce security.

### 4. Data Layer
Persistent databases, caching nodes, and file repositories.
* **Services:** Rule Repository (PostgreSQL), Knowledge Repository (PostgreSQL), Prompt Template Repository (PostgreSQL), Vector Database (Qdrant), Redis Cache, and Object Storage (MinIO).

### 5. Enterprise Systems (External)
Legacy university infrastructure the platform integrates with.
* **Services:** Vidyanvesha ERP database, and external static NBA SAR templates.

---

## Network Connection Pathways

* **Access:** The **Faculty Browser** communicates with the **Application Cluster** (Next.js portal) via HTTPS.
* **Process Flow:** The **Application Cluster** orchestrates reports by writing/reading details to/from the **Data Layer** databases and fetching raw academic information from **Enterprise Systems** (ERP).
* **AI Flow:** The **Application Cluster** calls model containers in the **Private AI Cluster** via internal REST API endpoints. The **Private AI Cluster** retrieves embedded contextual guidelines and vectors directly from the **Data Layer**.

---

**Next Step:** Learn about governance, access, and logging: [10 — Security Design](file:///C:/Aniket%20Personal/EkamVistar%20Tasks/Group%20Task/NBA%20SAR%20ARCH/docs/10-security-design.md)
