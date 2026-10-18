# Enterprise Capability Catalog

An enterprise catalog should list what the organization actually builds, owns, and reuses to run the business — not repeat philosophical definitions across twenty files.

In the **MOEPA Cognitive Architecture**, every production capability belongs to one of two pillars:

1. **[Data Substrate Capabilities](data-substrate.md) (The Storage)** — the organization-owned knowledge library where measurements, canonical entity definitions, verified claims, workflow records, and policy rules are stored in open, portable formats (`DS1`–`DS6`).
2. **[Enterprise Agent Capabilities](agents.md) (The Engine)** — the governed agents and control services that consume the Data Substrate to ingest telemetry, resolve entities, verify truth, execute workflows, and enforce policy across the five MOEPA layers (`AG1`–`AG6`).

---

## How the Two Pillars Map to the Five MOEPA Layers

The five MOEPA layers are the governance questions. The Data Substrate and the Agents are the enterprise capabilities that answer them:

| MOEPA Layer | Governance Question | Data Substrate Capability (What We Store) | Enterprise Agent Capability (What Runs the Work) |
| :--- | :--- | :--- | :--- |
| **1. Metrology** | *What did we actually measure?* | **[DS1](data-substrate.md#ds1--open-format-lakehouse-and-table-catalog)** Open Lakehouse & Catalog<br>**[DS2](data-substrate.md#ds2--semantic-ingestion-and-provenance-ledger)** Semantic Ingestion & Provenance (`Proto-SPO`) | **[AG1](agents.md#ag1--telemetry-and-quality-gate-agents-metrology)** Telemetry & Quality Gate Agents |
| **2. Ontology** | *What do these things mean?* | **[DS3](data-substrate.md#ds3--canonical-entity-registry-and-knowledge-graph)** Canonical Entity Registry & Knowledge Graph<br>**[DS6](data-substrate.md#ds6--ai-demand-management-and-asset-deduplication)** Demand Management & Deduplication Index | **[AG2](agents.md#ag2--entity-resolution-and-semantic-mapping-agents-ontology)** Entity Resolution & Semantic Mapping Agents |
| **3. Epistemology** | *How do we know this is true, and who may see it?* | **[DS4](data-substrate.md#ds4--owned-vector-and-grounded-retrieval-index)** Owned Vector & Retrieval Index | **[AG3](agents.md#ag3--verification-grounding-and-citation-agents-epistemology)** Verification, Grounding & Citation Agents |
| **4. Praxeology** | *What purposeful action are we taking?* | **[DS5](data-substrate.md#ds5--cross-layer-audit-and-decision-ledger)** Cross-Layer Audit & Decision Ledger | **[AG4](agents.md#ag4--workflow-and-execution-agents-praxeology)** Workflow & Execution Agents<br>**[AG6](agents.md#ag6--mcp-capability-bus-cross-cutting)** MCP Capability Bus |
| **5. Axiology** | *Should we do this under our rules?* | **[DS5](data-substrate.md#ds5--cross-layer-audit-and-decision-ledger)** Versioned Policy & Constitutional Baseline | **[AG5](agents.md#ag5--policy-and-compliance-gate-agents-axiology)** Policy & Compliance Gate Agents |

---

## Catalog Contents

| Document | Purpose | Audience |
| :--- | :--- | :--- |
| **[Data Substrate Capabilities](data-substrate.md)** | The six core storage, semantic, and lineage capabilities (`DS1`–`DS6`) the organization must own so switching models or vendors never strands institutional memory | Enterprise architects, data platform owners, CDOs |
| **[Enterprise Agent Capabilities](agents.md)** | The six agent and control-plane capabilities (`AG1`–`AG6`) needed to run business workflows safely on top of the Data Substrate | AI/ML architects, platform engineers, security leads |
| **[Enterprise Capability Matrix](capability-matrix.md)** | Single governance table tying `DS1`–`DS6` and `AG1`–`AG6` to the **Score 3 minimum baseline** (`GO` / `CONDITIONAL GO` / `NO-GO`), maturity levels (3–5), and accountable owners | Portfolio boards, program managers, intake reviewers |
| **[End-to-End Business Compositions](cross-layer-compositions.md)** | Six repeatable blueprints showing how Agents and the Data Substrate combine for auditability, high-volume triage, grounded research, intake scoring, and continuous compliance | Solution architects, delivery teams |
| **[Technical Specification](ARCHITECTURE.md)** | Full builder specification for the MOEPA Cognitive Architecture (v2.3): SPO/quad representation, scoring rubric, and reference stack | Principal architects, engineering leads |

For the executive business case, start at the [repository primer](../README.md) and the two-page briefs in [primer/](../primer/).
