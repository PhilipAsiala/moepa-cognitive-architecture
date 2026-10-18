# Enterprise Capability Matrix

This matrix is the single governance view of the **Enterprise Capability Catalog**. Rather than organizing capabilities as abstract philosophical checklists, it groups them into the two capability pillars the enterprise actually builds, funds, and owns:

1. **[Data Substrate Capabilities](data-substrate.md) (`DS1`–`DS6`)** — the organization-owned storage and semantic foundation.
2. **[Enterprise Agent Capabilities](agents.md) (`AG1`–`AG6`)** — the execution engine and deterministic control gates that run on top of the Data Substrate.

Every capability is mapped to the **MOEPA Cognitive Architecture** layer it serves and bound to the existing **1–5 intake rubric (`GO` / `CONDITIONAL GO` / `NO-GO`)** defined in [ARCHITECTURE.md](ARCHITECTURE.md) (§4.2) and the [5-Layer Evaluation Checklist](../docs/5-Layer-Evaluation-Checklist.md):

- **Minimum set (Score 3 — Defined & Contained):** Required to avoid an automatic `NO-GO`. Missing any minimum-set capability means the proposal scores below 3 on that layer.
- **Score 4 (Managed & Measured) and Score 5 (Optimized & Sovereign):** Capabilities that lift a proposal from `CONDITIONAL GO` to an unconditional `GO` and compound value across the enterprise.

---

## Part 1: Data Substrate Capabilities (The Storage)

See full specifications in [Data Substrate Capabilities](data-substrate.md).

| ID | Enterprise Capability | MOEPA Layer | Minimum Set (Score 3 Baseline) | Maturity Progression (Score 4 → Score 5) | Accountable Owner |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **DS1** | **Open-Format Lakehouse & Table Catalog** | 1. Metrology / Substrate | Core data stored in exportable open formats (Parquet/CSV/JSON) with RBAC, egress logs, and platform availability check prior to building new pipelines | **4:** Native Apache Iceberg + Parquet tables in an open catalog (Polaris) with replay<br>**5:** Self-hosted, air-gappable lakehouse with zero-trust egress alerting | Data Platform Owner |
| **DS2** | **Semantic Ingestion & Provenance Ledger** | 1. Metrology | Source origin, collection timestamp, and basic quality validation recorded per batch; governed documents parsed along structural boundaries (no fixed-token chainsaw chunking) | **4:** Automated semantic parsing into `Proto-SPO` objects with versioned configs<br>**5:** Cryptographic (SHA-256) source fingerprinting and end-to-end PROV-O / OpenLineage graphs | Data Quality & Governance Owner |
| **DS3** | **Canonical Entity Registry & Knowledge Graph** | 2. Ontology | Core domain entities (customer, case, asset, policy), relationships, and controlled vocabularies documented with schema effective dates | **4:** Internally managed knowledge graph and governed vocabulary service<br>**5:** SPO/quad backbone storing each base fact once with point-in-time historical queryability | Domain Ontology Owner |
| **DS4** | **Owned Vector & Grounded Retrieval Index** | 2. Ontology / 3. Epistemology | Vector and retrieval index hosted inside organization-controlled infrastructure, returning source citations for every passage | **4:** Embeddings bound to canonical entity IDs (`DS3`) and provenance (`DS2`); auto-updated on source change<br>**5:** Pre-retrieval clearance filtering and cryptographic index verification | Knowledge Assurance Owner |
| **DS5** | **Cross-Layer Audit & Decision Ledger** | 3. Epistemology / 4. Praxeology / 5. Axiology | Tamper-evident logs of inputs, cited sources, confidence scores, workflow approvals, and policy checks, plus a versioned policy baseline | **4:** Cross-referenced audit chain linking Metrology through Axiology on every decision<br>**5:** Append-only signed ledger with cross-layer metadata envelopes and OS-locked Golden Master policy | Compliance & Operations Owner |
| **DS6** | **AI Demand Management & Asset Deduplication** | 2. Ontology / Portfolio | Proposers search an inventory of existing datasets, schemas, and agents by domain before intake scoring proceeds | **4:** Mandatory semantic search over the knowledge graph and catalog at intake<br>**5:** Formal non-duplication proof required before any new capability is funded | Enterprise Architecture & Catalog Steward |

---

## Part 2: Enterprise Agent Capabilities (The Engine)

See full specifications in [Enterprise Agent Capabilities](agents.md).

| ID | Enterprise Capability | MOEPA Layer | Minimum Set (Score 3 Baseline) | Maturity Progression (Score 4 → Score 5) | Accountable Owner |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **AG1** | **Telemetry & Quality Gate Agents** | 1. Metrology | Automated ingress validation rules on core fields; failed records quarantined and escalated; post-launch outcome KPIs defined | **4:** Continuous statistical profiling, drift alerting, and pre-launch KPI baselining<br>**5:** Automatic pipeline quarantine on drift and scheduled post-launch ROI/KPI verification loops | Data Platform + Business Owner |
| **AG2** | **Entity Resolution & Semantic Mapping Agents** | 2. Ontology | Deterministic/hybrid mapping of raw inputs to canonical entity definitions (`DS3`) and official code sets; ambiguous matches flagged for review | **4:** Graph-backed entity resolution across heterogeneous datasets<br>**5:** Dynamic relationship updates with point-in-time policy awareness and steward approval gates | Domain Integration Owner |
| **AG3** | **Verification, Grounding & Citation Agents** | 3. Epistemology | Grounded RAG over `DS4` with source citations; primary-source verification gate on consequential claims; documented confidence scoring; hallucination checks | **4:** Automated verification and hallucination gates block ungrounded claims; decomposed confidence scores<br>**5:** Multi-source corroboration, consistency checks, and SHA-256 pipeline integrity verification | Decision Assurance Owner |
| **AG4** | **Workflow & Execution Agents** | 4. Praxeology | Explicit workflow sequence; allow-listed agent tool scopes; mandatory human-in-the-loop checkpoints before consequential actions; defined escalation paths | **4:** Formal state-machine execution (LangGraph/Temporal) routing routine tasks to code/small models<br>**5:** Infrastructure-enforced checkpoints and tool scopes that cannot be bypassed by prompts | Workflow & Operations Owner |
| **AG5** | **Policy & Compliance Gate Agents** | 5. Axiology | Key legal, privacy, and compliance rules encoded as machine checks outside the model; prompt-injection sanitization; periodic bias audits; qualitative ROI and cost attribution | **4:** Infrastructure Policy-as-Code (OPA), continuous equity monitoring, quantified ROI & chargeback models<br>**5:** Inviolable constitutional guardrails verified by scheduled adversarial red-teaming | Policy, Responsible AI & Finance Owners |
| **AG6** | **MCP Capability Bus** | Cross-Cutting | Explicit, versioned tool contracts between orchestrators and enterprise data/services with centralized invocation logging | **4:** All new substrate and agent capabilities exposed as Model Context Protocol (MCP) servers or facades<br>**5:** Full host portability — models and orchestrators can be swapped with zero integration rewrites | Platform Architecture Owner |

---

## How to Use This Matrix in Project Intake

1. **Check the Data Substrate first (`DS1`–`DS6`):** Does the proposal reuse existing governed tables, entity definitions, and indexes (`DS6`), or is it standing up a shadow silo?
2. **Check the Agent Engine (`AG1`–`AG6`):** Which agents are probabilistic proposers (`AG4` planning), and which are deterministic gates (`AG1` quality, `AG3` verification, `AG5` policy refusal)?
3. **Score the five layers:** Use the [5-Layer Evaluation Checklist](../docs/5-Layer-Evaluation-Checklist.md). Any layer missing its **Minimum Set (Score 3)** capabilities receives a score `< 3`, resulting in an automatic **NO-GO** until remediated.
