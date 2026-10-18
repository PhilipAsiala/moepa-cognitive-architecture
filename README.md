# The MOEPA Cognitive Architecture
### Deterministic, Sovereign Enterprise AI

Modern enterprise AI has an architecture problem. Organizations plug probabilistic large language models directly into sensitive data and enterprise APIs, hoping that prompt wording and thin guardrails will prevent hallucinations, compliance violations, and vendor lock-in.

In high-stakes environments — defense, finance, healthcare, and critical infrastructure — **"mostly accurate" is an operational failure.**

This repository defines a three-part architecture for enterprise AI that separates what the organization **must own** from the commodity compute it **can rent**:

| Tier | What It Is | Business Role |
| :--- | :--- | :--- |
| **1. MOEPA Cognitive Architecture** *(The Thesis)* | Five non-negotiable governance layers (**M**etrology, **O**ntology, **E**pistemology, **P**raxeology, **A**xiology) and a project intake scorecard (**GO** / **CONDITIONAL GO** / **NO-GO**). | Separates AI concerns so every failure mode has a named owner and a deterministic control. |
| **2. Data Substrate** *(The Storage)* | The organization-owned knowledge library (`DS1`–`DS7`) where raw measurements, entity definitions, verified claims, audit logs, and policy rules live in open, portable formats. | Prevents vendor lock-in. You can swap models or clouds without losing institutional memory. |
| **3. Agents** *(The Engine)* | The specialized workflows and control gates (`AG1`–`AG6`) that consume the Data Substrate — using probabilistic models to plan, bounded by deterministic code to verify and govern. | Runs the business safely without letting a black-box model police itself. |

> **Own the brain. Rent the muscles.** Own the Data Substrate and the governance rules across the five MOEPA layers. Rent GPU capacity and commercial models for the Agents that consume them.

---

## 1. The Thesis: The Five Layers of MOEPA

When vendors bundle ingestion, search, model guessing, and API execution into a single black box ("Agentic AI"), you lose auditability and sovereignty. MOEPA separates the lifecycle into five layers. Each layer answers one plain-English question before an AI system is allowed to act:

| MOEPA Layer | The Plain-English Question | Stored in the Data Substrate (`DS`) | Executed by Enterprise Agents (`AG`) | What Fails Without It |
| :--- | :--- | :--- | :--- | :--- |
| **1. Metrology** | *"What did we actually measure?"* | **[DS1](catalog/data-substrate.md#ds1--open-format-lakehouse-and-table-catalog)** Open Lakehouse<br>**[DS2](catalog/data-substrate.md#ds2--semantic-ingestion-and-provenance-ledger)** Provenance Ledger | **[AG1](catalog/agents.md#ag1--telemetry-and-quality-gate-agents-metrology)** Telemetry & Quality Gate Agents | **Garbage-In at Scale:** Uncalibrated feeds and broken document chunks poison downstream decisions. |
| **2. Ontology** | *"What do these things mean, and how do they relate?"* | **[DS3](catalog/data-substrate.md#ds3--canonical-entity-registry-and-knowledge-graph)** Canonical Entity Registry & Graph<br>**[DS6](catalog/data-substrate.md#ds6--enterprise-capability-and-asset-registry)** Capability & Asset Registry | **[AG2](catalog/agents.md#ag2--entity-resolution-and-semantic-mapping-agents-ontology)** Entity Resolution Agents | **Vendor Lock-In & Silos:** Every team or SaaS tool defines "customer," "case," or "asset" differently. |
| **3. Epistemology** | *"How do we know this is true, and who may see it?"* | **[DS4](catalog/data-substrate.md#ds4--owned-vector-and-grounded-retrieval-index)** Owned Vector & Retrieval Index | **[AG3](catalog/agents.md#ag3--verification-grounding-and-citation-agents-epistemology)** Verification & Citation Agents | **Hallucinations & Leaks:** The AI states unverified claims as fact or exposes restricted data. |
| **4. Praxeology** | *"What purposeful action are we taking?"* | **[DS5](catalog/data-substrate.md#ds5--cross-layer-audit-and-decision-ledger)** Cross-Layer Audit Ledger | **[AG4](catalog/agents.md#ag4--workflow-and-execution-agents-praxeology)** Workflow & Execution Agents | **Rogue Automation:** Agents loop, call unauthorized APIs, or skip human review on consequential actions. |
| **5. Axiology** | *"Should we do this under our rules?"* | **[DS7](catalog/data-substrate.md#ds7--policy-as-code-and-constitutional-baseline)** Policy-as-Code Baseline | **[AG5](catalog/agents.md#ag5--policy-and-compliance-gate-agents-axiology)** Policy & Compliance Gate Agents | **Compliance Failure:** Relying on an LLM's system prompt to enforce law, policy, or spending limits. |

*Cross-cutting:* the **[AG6](catalog/agents.md#ag6--mcp-capability-bus-cross-cutting) MCP Capability Bus** is the single contract through which every agent reaches every substrate capability, so models and orchestrators can be swapped without rewiring the layers.

---

## 2. The Storage: The Data Substrate

The **Data Substrate** is the physical manifestation of what the organization owns. Instead of scattering institutional knowledge across vendor-hosted vector databases and SaaS silos, all five MOEPA layers read from and write to one open, portable foundation:

- **Open formats first (`DS1`, `DS2`):** Tables and structured document segments (`Proto-SPO`s) live in open lakehouse formats (Apache Iceberg, Parquet, Polaris) with cryptographic provenance.
- **Shared enterprise meaning (`DS3`, `DS6`):** Entities, relationships, and controlled vocabularies live in an organization-owned knowledge graph, and every governed dataset and agent is listed in an asset registry, so every agent speaks the same language and duplicate projects are visible at intake.
- **Owned retrieval, audit history, and policy (`DS4`, `DS5`, `DS7`):** Embeddings and citations live in an in-house index; workflow approvals and policy checks are written to an immutable cross-layer ledger; the Policy-as-Code rules themselves are versioned and owned.

---

## 3. The Engine: Enterprise Agents

Large language models are **probabilistic** — they predict the next token. Enterprise governance is **deterministic** — a rule is either followed or broken.

In this architecture an **Agent** is any governed service that acts on the Data Substrate: the probabilistic planners that draft and propose, *and* the deterministic gates that bound them. The **Agents** tier separates the two:

| Role | Nature | How Agents Operate on the Data Substrate |
| :--- | :--- | :--- |
| **Propose & Plan** | Probabilistic | **Workflow Agents (`AG4`)** route routine tasks to deterministic code or small local models, and use frontier LLMs only when synthesis is needed. |
| **Qualify & Map** | Deterministic / Hybrid | **Telemetry (`AG1`)** and **Entity Agents (`AG2`)** validate raw inputs and bind them to canonical enterprise entities before reasoning begins. |
| **Verify & Govern** | Deterministic Gate | **Verification (`AG3`)** blocks claims that lack a substrate citation or user clearance. **Policy Gate Agents (`AG5`)** enforce Policy-as-Code (OPA) *outside* the model, refusing any non-compliant action. |
| **Connect** | Deterministic Contract | **The MCP Capability Bus (`AG6`)** exposes every substrate and agent tool via the Model Context Protocol, so models can be swapped without rewriting integrations. |

---

## Repository Structure

This repository is organized into three parts, plus supporting diagrams:

1. **`README.md` (This Executive Primer)** — How the **MOEPA Cognitive Architecture**, the **Data Substrate**, and **Agents** fit together.
2. **[`primer/` (Executive Briefs)](primer/)** — Short playbooks applying the three tiers to boardroom decisions:
   - [Data Sovereignty](primer/data-sovereignty.md) — Owning the Data Substrate so you can switch models or vendors at will.
   - [Zero-Trust Governance](primer/zero-trust-governance.md) — Using Verification and Policy Gate Agents to stop hallucinations and compliance violations.
   - [Investment & ROI](primer/roi.md) — Funding reusable substrate and agent capabilities instead of disposable SaaS subscriptions.
3. **[`catalog/` (Enterprise Capability Catalog)](catalog/)** — Concrete specifications for builders and intake reviewers:
   - [Data Substrate Capabilities (`DS1`–`DS7`)](catalog/data-substrate.md)
   - [Enterprise Agent Capabilities (`AG1`–`AG6`)](catalog/agents.md)
   - [Enterprise Capability Matrix (`GO` / `CONDITIONAL GO` / `NO-GO`)](catalog/capability-matrix.md)
   - [End-to-End Business Compositions](catalog/cross-layer-compositions.md)
   - [Technical Specification (`ARCHITECTURE.md`)](catalog/ARCHITECTURE.md)
4. **[`diagrams/`](diagrams/)** — Mermaid diagrams of the stack, information flow, and owned-vs-rented comparison.

---

## Feedback and License

Feedback and proposals are welcome via [GitHub Issues](https://github.com/PhilipAsiala/philosophical-ai-architecture/issues/new?template=feedback.yml) — see [CONTRIBUTING.md](CONTRIBUTING.md). Licensed under the [MIT License](LICENSE) (see [TRADEMARK_POLICY.md](TRADEMARK_POLICY.md)).
