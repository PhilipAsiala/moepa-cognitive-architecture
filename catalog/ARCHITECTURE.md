# The MOEPA Cognitive Architecture — Technical Specification

Leaders start at the [repository primer](../README.md). This file is the builder specification.

Version: 3.1 — Three-Tier Model (Thesis / Data Substrate / Agents); record shape, system-of-record, and gateway rules aligned to the first running implementation

Author: Philip Asiala

Last Updated: October 18, 2026

Status: Draft for Review — Feedback Welcome

Repository: [moepa-cognitive-architecture](https://github.com/PhilipAsiala/moepa-cognitive-architecture) (GitHub) — canonical home of the MOEPA Cognitive Architecture

> **Core terms.** The **MOEPA Cognitive Architecture** is the thesis (the five layers and the intake scorecard). The **Data Substrate** is how owned knowledge is stored. **Agents** are the engine that consumes the Data Substrate across the layers. For the executive business briefs, see [primer/](../primer/). For the enterprise capability catalog, see [catalog/README.md](README.md).

## Executive Summary: The Owned-Brain Strategy

This specification is for architects and engineers implementing a decision leaders have already framed: what the organization owns, and what it rents.

The MOEPA Cognitive Architecture (**Metrology**, measurement; **Ontology**, shared definitions; **Epistemology**, verification; **Praxeology**, action; **Axiology**, value constraints) turns that decision into five scored layers.

- **Rent the muscles (compute).** Hardware execution (VPC, clusters, GPUs) is treated as interchangeable, variable-cost capacity, with exit terms.
- **Own the brain (intellectual property).** Knowledge graphs, validation models, ethical guardrails, and mission rules stay portable and access-controlled. They are core intellectual property when the organization can export and audit them. A vendor-hosted copy of the same assets does not meet that test.

Predictive components (scores, confidence, quality gates) and generative components (retrieved answers, summaries, recommendations) both write to the owned substrate and pass the same policy checks.

Key principle: this document is the implementation layer for environments that need sovereignty, explainability, and governance that can be measured. It is a draft specification, not a deployed system.

## 1. The Owned-Brain Strategy — Core Principles
### 1.1 Why This Matters Now
Agentic AI, multimodal models, and open-weight ecosystems add both capability and risk. Organizations that do not keep ownership of data, definitions, verification, workflows, and policy face:

- Vendor lock-in that becomes expensive to unwind, and operating cost that rises with use.
- Uncontrolled data exfiltration and compliance violations.
- Inability to audit or explain high-stakes decisions.
- Erosion of institutional knowledge as models drift.

### 1.2 The Decoupling Imperative
MOEPA enforces a clean separation between rented, interchangeable compute and the owned, versioned, auditable Data Substrate. This mirrors successful patterns in cloud-native architecture while extending them to the domain of reasoning itself.

Core Principle: We rent commodity compute. We own the brain. Ownership means internal control of data (Metrology), semantics (Ontology), validation (Epistemology), workflows (Praxeology), and values (Axiology), held on the Data Substrate so the same record can be found again.

## 2. MOEPA Layer Definitions — Philosophical Grounding & Practical Translation
Each layer is named after a classical philosophical discipline and grounded in a specific mathematical formalization. This ensures the framework is both intellectually coherent and technically implementable.

### Layer 1 — Metrology (Science of Measurement) — The Data Foundation Layer
Philosophical Definition: The study of measurement, standards, and the conditions under which reliable observation is possible.

Mathematical Grounding: Measure theory, statistics, calibration theory, and boundary conditions.

Enterprise Translation: Establishing the foundational data layer—ensuring all data is measured, quality-assured, observable, and traceable before it enters higher cognitive layers. This is the bedrock that prevents "garbage in, garbage out" across the entire architecture.

Key Artifacts:

- Self-hosted open-format data substrate containers (Iceberg, Parquet) that Metrology qualifies through ingress quality controls (see §5).
- Internal data quality frameworks (Great Expectations, Monte Carlo, or custom).
- Comprehensive quality gates plus observational lineage/provenance over what enters the substrate.
- Observability for drift, anomaly detection, and statistical profiling.
- Encrypted, air-gappable datasets with strict egress controls.

Explicitly avoid: Architectures where third-party platforms own the data foundation, quality rules, and lineage in stores the organization cannot export.

### Layer 2 — Ontology (Study of Being / Reality)
Philosophical Definition: The study of what exists, the categories of being, and the relationships between entities.

Mathematical Grounding: Graph theory, formal ontologies, description logics.

Enterprise Translation: Modeling domain reality as structured, queryable knowledge rather than flat text.

Key Artifacts:

- Internally managed knowledge graphs (Apache Jena Fuseki, self-managed Neo4j), rebuilt from the lakehouse system of record rather than holding truth of their own.
- Custom entity resolution and schema management.
- Version-controlled semantic models and an organization-owned JSON-LD context.

Explicitly avoid: External platforms that own the core semantic model and entity truth layer.

### Layer 3 — Epistemology (Study of Knowledge & Truth)
Philosophical Definition: The study of how we know what we know, justification, and the distinction between belief and justified true belief.

Mathematical Grounding: Formal logic, probability theory, Bayesian inference, cryptographic verification.

Enterprise Translation: Separating probabilistic model output from verified facts; building chains of custody for information.

Key Artifacts:

- Cryptographic (SHA-256) fingerprinting of source artifacts and verification pipeline configurations.
- Grounded retrieval with source citation + verification against owned data.
- Deterministic fact-verification gates before any execution.

### Layer 4 — Praxeology (Study of Purposeful Action)
Philosophical Definition: The study of human action, intentionality, and the logical structure of goal-directed behavior.

Mathematical Grounding: Game theory, decision theory, planning algorithms, workflow formalisms.

Enterprise Translation: Governing how agents act—what tools they may call, in what sequence, and under what human oversight.

Key Artifacts:

- Deterministic workflow lifecycles (intake → plan → execute).
- Per-record action scopes (allowed and denied action classes) enforced as policy before any tool call.
- LangGraph state machines.
- Mandatory human-in-the-loop checkpoints.
- Immutable audit trails at every milestone.

### Layer 5 — Axiology (Study of Value & Ethics)
Philosophical Definition: The study of value, worth, and ethical principles—what ought to be preserved or optimized.

Mathematical Grounding: Optimization theory, multi-objective decision making, constitutional AI approaches.

Enterprise Translation: Hard-coding organizational values, regulatory constraints, and mission alignment so they cannot be easily overridden.

Key Artifacts:

- "Golden Master" policy baseline with OS- or infrastructure-level write locks.
- Preferred/forbidden verb enforcement (allowed vs. prohibited agent actions).
- Zero Trust policy blocks.
- Constitutional guardrails that survive prompt injection.

## 3. The MOEPA Stack Specification
The five layers are interdependent. Weakness in any layer undermines the integrity of the whole system. Layers are numbered bottom-up (1 = foundation, 5 = highest governance). All layers must score ≥3 to avoid an automatic NO-GO; an unconditional GO requires every layer to score ≥4, and a layer at exactly 3 yields a CONDITIONAL GO.

### Strategic Evaluation Matrix

| Layer | The Econometric & Risk Lens (Program Evaluation / Risk Analysis) | The Systems Engineering & Zero Trust Lens (Enterprise IT) |
| --- | --- | --- |
| 5. Axiology | Minimizes compliance costs and legal liabilities by hardcoding mandatory operational boundaries. | Enforces policy-as-code at the OS/Infrastructure level, eliminating client-side manipulation. |
| 4. Praxeology | Lowers operational risk by replacing erratic manual loops with highly predictable, auditable processes. | Implements deterministic state-machines and strict agentic action boundaries. |
| 3. Epistemology | Protects the statistical validity of decision models by preventing data pollution and hallucinations. | Deploys deterministic verification gates with cryptographic (SHA-256) artifact integrity checks. |
| 2. Ontology | Models complex mission-domain relational networks (e.g., entity ownership, program eligibility, and dependency tracking) into clean, queryable realities. | Maintains the canonical entity registry, semantic knowledge graph, and controlled vocabularies. |
| 1. Metrology | Establishes baseline data integrity, ensuring that econometric profiling relies on uncorrupted metrics. | Enforces ingress quality gates, provenance stamping, and egress controls on the owned open-format lakehouse. |

## 4. MOEPA Intake & Scoring Framework
### 4.1 Purpose
Every AI procurement request, vendor pitch, internal use-case, or model deployment must be audited against the five MOEPA layers before funding or infrastructure provisioning is approved.

### 4.2 Scoring Rubric (1–5 Scale)
Decision Bands: Each layer is scored 1–5, and the lowest layer score sets the overall recommendation.

- NO-GO: any layer scores 1 or 2 (automatic NO-GO with required remediation).
- CONDITIONAL GO: every layer scores ≥3 and at least one layer scores exactly 3 — approved only if that layer's named controls and oversight are demonstrably active.
- GO: every layer scores ≥4.

Minimum Threshold: A score of 3 is the minimum acceptable standard for a layer and does not trigger a NO-GO, but a project is not an unconditional GO until every layer scores ≥4.

Score Definitions:

- 1: Completely Missing or Free-Form Prompt Dependent — High Risk
- 2: Partial / Ad-Hoc Controls — Elevated Risk
- 3: Defined & Contained — Minimum Acceptable Standard (Conditional)
- 4: Strongly Enforced & Measurable — Good Practice
- 5: Immutable / Cryptographically Proven & Fully Decoupled — Gold Standard

### 4.3 Layer-by-Layer Evaluation Criteria
#### Layer 1 — Metrology Evaluation (Data Foundation)
Risk: Poor data quality, uncontrolled lineage, vendor lock-in on the data layer, loss of sovereignty over organizational truth.

Audit Question: How is data quality measured, assured, and made observable? Is the data foundation internally controlled or owned by an outside vendor?

Scoring Guidance:

- Score 1: No data quality measurement; complete reliance on vendor-managed proprietary data platforms.
- Score 3: Basic internal data quality rules and lineage tracking exist within standard data lakes.
- Score 5: Comprehensive internal data observability, statistical profiling, provenance tracking, and self-hosted open-format data lake with full sovereignty.

#### Layer 2 — Ontology Evaluation (Structured Reality)
Risk: Context collapse, poor reasoning quality, inability to maintain consistent world model.

Audit Question: How does the system represent and maintain structured knowledge of your domain? Is the semantic model internally owned or controlled by an outside vendor?

Scoring Guidance:

- Score 1: Raw pre-trained weights only; no domain structuring or custom schema constraints.
- Score 3: Core domain entities, relationships, and code sets are documented in an organization-owned, governed dictionary with effective dates. Open industry standards (for example schema.org, FIBO, NIEM) may be adopted as the basis; entities defined only inside a vendor's proprietary schema do not qualify.
- Score 5: Live, internally managed semantic knowledge graph and SPO/quad store that evolves with your business rules, with point-in-time effective dates and steward-approved vocabulary changes.

#### Layer 3 — Epistemology Evaluation (Truth & Verification)
Risk: Hallucination amplification, unverified code execution, lack of operational traceability, and blind reliance on probabilistic outputs.

Audit Question: How does the system differentiate between a statistically generated guess and an immutable, verified enterprise fact? Are validation gates centralized or hidden inside a vendor's black-box pipeline?

Scoring Guidance:

- Score 1: Prompt-dependent validation only; model outputs are served directly to users or APIs with zero deterministic cross-checking.
- Score 3: Basic automated checks exist (e.g., flat retrieval checks). Retrieval surfaces source citations, but lacks cryptographic pipeline validation.
- Score 5: Advanced cryptographic verification is standard. Pipeline integration validates model and verification configurations using SHA-256 hashes before execution. Every fact is verified against your sovereign, owned Metrology asset, and verification metadata is stored with that fact on the Data Substrate.

#### Layer 4 — Praxeology Evaluation (Agentic Workflow Boundaries)
Risk: Uncontrolled agentic loops, destructive autonomous API actions, and untraceable multi-step execution paths.

Audit Question: What deterministic framework governs the sequence of execution when an AI calls a tool or generates a system artifact? How is human oversight structurally guaranteed?

Scoring Guidance:

- Score 1: Free-form, autonomous execution loops with zero state-machine tracking; tools are exposed to the LLM via open-ended prompts.
- Score 3: Agentic logic is bounded by basic sequential code, but lacks a centralized state machine. Human-in-the-loop checkpoints exist but are bypassable.
- Score 5: The workflow is driven by immutable, deterministic state machines. Execution follows strict, auditable lifecycles (intake → plan → execute) generating permanent audit trails. State parameters are versioned on the Data Substrate.

#### Layer 5 — Axiology Evaluation (Governance & Value Alignment)
Risk: Prompt injection vulnerabilities, alignment drift, and client-side manipulation of organizational guardrails by developers or end-users.

Audit Question: How are the ethical boundaries, compliance mandates, and organizational value guardrails permanently locked down against intentional or accidental modification?

**Enterprise-Scale Weighting (for 1,000+ use-case intake environments):** In high-volume enterprise and public-sector intake processes, Axiology scores are weighted heavily by two factors: (1) documented **Business ROI** (quantified mission impact, risk reduction, cost avoidance, equity improvements, or throughput gains with traceable assumptions and sensitivity analysis) and (2) the presence of a formal, auditable **Chargeback/Showback model** that attributes platform, compute, data, and governance costs back to business owners. Proposals lacking credible ROI quantification or a viable cost attribution model cannot achieve a score of 4 or higher regardless of other governance controls.

Scoring Guidance:

- Score 1: Soft constraints only; guidelines are embedded within the system prompt and easily bypassed by sophisticated prompt injections.
- Score 3: Compliance rules are centralized, but security configuration settings are modifiable by local client environments or developers at the edge.
- Score 5: Core organizational values, preferred/forbidden verb lists, and security policies are hardcoded into a "Golden Master" policy baseline ([DS7](data-substrate.md#ds7--policy-as-code-and-constitutional-baseline)) locked via OS- or infrastructure-level write constraints. Policy code is cryptographically protected and versioned. In addition, a quantified Business ROI model and approved chargeback/showback mechanism are in place and reviewed at the executive level.

### 4.4 Executive Governance & Architecture Review Chain

To support enterprise-scale intake (1,000+ requests) while maintaining sovereignty and preventing uncontrolled proliferation, MOEPA mandates a formal executive governance gate and a strict Architecture Review Chain for all proposals.

**Executive Approval Gate:** Any use case that receives an overall MOEPA score of 4 or higher (or any proposal requesting production funding or enterprise platform resources) must pass an explicit executive-level approval gate before scaling. This gate is separate from technical scoring and is triggered by the weighted Axiology score (incorporating Business ROI and chargeback justification). The executive gate reviews mission alignment, quantified ROI, cost attribution model, and residual risk.

**Mandatory Architecture Review Chain:** Before executive sign-off, every proposal must traverse the following strict, sequential review chain. Each step must provide documented sign-off; no step may be bypassed. Role titles are illustrative — organizations map each step to their own governance bodies (architecture review board, data platform office, business program office, etc.):

1. **Deduplication Check** — The proposer searches the enterprise asset registry ([DS6](data-substrate.md#ds6--enterprise-capability-and-asset-registry)) and documents that the dataset, schema, or agent does not already exist. No scoring begins until this is recorded.
2. **Enterprise Architecture Review** — Technical architecture review for alignment with enterprise standards, security patterns, and MOEPA layer controls.
3. **Data Platform — ingestion and lineage review** — Data platform engineering validates ingestion approach, lineage, and quality controls (see Metrology data availability requirements).
4. **Data Platform — capacity and cost review** — Platform owners confirm capacity, cost model integration, and platform-level governance.
5. **Business program office** — Owning program confirms operational readiness, ROI assumptions, and acceptance of chargeback/showback obligations.
6. **Executive Sign-off** — Formal approval by designated executive authority (or governance board) confirming the weighted ROI case, approved cost model, and completion of the preceding chain.

This chain ensures that non-duplication, technical feasibility, data reality, platform economics, business ownership, and executive accountability are all explicitly addressed. Prior decisions recorded on the Data Substrate ([DS5](data-substrate.md#ds5--cross-layer-audit-and-decision-ledger)) support the deduplication check at step 1.

## 5. The Data Substrate
The Data Substrate is the storage tier, not a sixth scored layer. The five disciplines remain the five scored layers (Metrology, Ontology, Epistemology, Praxeology, Axiology), and the 1–5 per-layer scoring model is unchanged. The enterprise capabilities that make up the substrate are specified in [Data Substrate Capabilities](data-substrate.md) (`DS1`–`DS7`); this section defines the representation they converge on.

The substrate provides a single SPO/quad backbone (Subject-Predicate-Object, quads with context) plus lakehouse storage where the base triple lives once. Each MOEPA layer attaches layer-specific metadata envelopes (epistemic, praxeological, axiological, etc.) without duplicating the base fact.

### 5.0 The MOEPA Record

The unit of storage is one **MOEPA record**: the Ontology triple plus one envelope for each of the other four layers, carried on the same row. Implementations may call it a *quintuple* (five parts). The five parts answer five separate questions and are never collapsed into one another:

| Part | Question it answers | Required fields on every write | Optional fields |
| :--- | :--- | :--- | :--- |
| **Ontology** | What is this? | `subject`, `predicate`, `object` | — |
| **Epistemology** | Why believe it? | generating agent or activity (`prov:wasGeneratedBy`), generation time (`prov:generatedAtTime`), SHA-256 fingerprint of this version | source/producer trust level |
| **Metrology** | How good is it right now? | measurement confidence (0–1, after quality rules), validity window (`validUntil`) | decay label, quality-gate results, snapshot statistics |
| **Axiology** | What is it allowed to mean for people? | classification marking | PII flag, mission alignment, value weight |
| **Praxeology** | What may be done with it? | allowed action classes, denied action classes | execution trigger |

```json
{
  "@type": "moepa:CognitiveQuintuple",
  "@id": "urn:uuid:84a5b2c9-1738-4e1a-9f5b-6d7e8a9b0c1d",
  "moepa:Ontology":     {"moepa:Subject": "urn:user:phil_a", "moepa:Predicate": "moepa:requestedInferenceOn", "moepa:Object": "urn:dataset:financial_q3_report"},
  "moepa:Epistemology": {"prov:wasGeneratedBy": "urn:service:assembly", "prov:generatedAtTime": "2026-10-08T12:57:00Z", "moepa:sensorTrustLevel": 0.99, "moepa:cryptographicHash": "sha256-a7c9f8e2"},
  "moepa:Metrology":    {"moepa:confidenceScore": 0.98, "moepa:decayRate": "High", "moepa:validUntil": "2026-10-09T12:57:00Z"},
  "moepa:Axiology":     {"moepa:classificationLevel": "CUI", "moepa:containsPII": false, "moepa:missionAlignment": "Data Auditing", "moepa:valueWeight": 85},
  "moepa:Praxeology":   {"moepa:allowedActions": ["Read", "Encrypt", "RouteToModel"], "moepa:deniedActions": ["ExportToPublicStorage", "UnencryptedTransmission"]}
}
```

The record is JSON-LD against an organization-owned context document, so the same record is a row in the lakehouse, a set of triples in the graph projection, and a payload for the policy engine without translation. A write that is missing any required field is rejected before it reaches the substrate; the rejection is itself a Metrology quality gate (`AG1`).

**Append-only supersession.** A record is never updated in place. A change is a new row with the same `@id` and a new Epistemology fingerprint and generation time; the newest row for an `@id` is the current assertion and older rows remain readable for audit. A write whose `@id` and fingerprint both match the latest row is not appended. Downstream projections and embeddings are keyed to the fingerprint, so a superseding row is re-projected and re-embedded while an unchanged row is reused.

**Keep the parts separate.** A table name is Ontology. The snapshot statistics of that table are Metrology. An audit-log table is still an Iceberg table (Ontology) whose rows happen to be about provenance (Epistemology). A prompt that asks for an action still has to pass marking, freshness, and source checks before anything runs.

Because all five envelopes are columns on the same record, the basic cross-layer query — "find all high-confidence income facts that satisfy axiological fairness and support praxeological auto-approval" — is a filter over the record table itself. A federation layer (for example, a workflow router or Trino) is added when that query must join the record table to its projections, to other catalogs, or to tables at a scale where a single engine is no longer enough.

### 5.0.1 System of Record and Projections

The open-format lakehouse under its table catalog (`DS1`) is the **only system of record**. Every other engine that serves a layer — the graph store for Ontology, the vector index for Epistemology, the policy engine's loaded bundle for Axiology and Praxeology — is a **projection**: a rebuildable copy that exists because its query shape (SPARQL, nearest-neighbour, Rego) is not a Parquet scan. Projections are never a second source of truth.

- Embedding vectors are durably stored in a lakehouse table keyed to the record `@id` and fingerprint; the live vector index is loaded from that table.
- The policy engine loads its bundle from the versioned policy repository (`DS7`); the hash of the bundle in force is written to the decision ledger (`DS5`) with every decision. The policy engine does not scan the lakehouse on the request path.
- A rebuild job must be able to empty every projection and reload it from the lakehouse. **That rebuild is an acceptance test, not an operational afterthought.** A service whose last projection rebuild failed reports unhealthy so callers know search and graph results may be stale before relying on them.

**End state vs. evolution.** The SPO/quad hypergraph + lakehouse described here is the **imperative end state** — every substrate must converge on owned records with layer metadata envelopes, a single system of record with rebuildable projections, and federated cross-layer query. Organizations **evolve** toward that target incrementally (e.g. Iceberg/Parquet with SPO-compatible schemas first, pilot triple store, then enterprise graph + federation). Interim storage is valid when ownership, open formats, provenance, and a documented migration path to the SPO/quad end state are in place.

This substrate scales from lightweight edge deployments (JSON triples + SQLite) to enterprise deployments (full graph + Iceberg). It is sovereignty-aligned with the Owned-Brain strategy: self-hosted graph control, open formats, PROV-O lineage compatibility, and one owned base triple that remains queryable as a single auditable whole.

**Provenance three-way split** (to avoid double-claiming):
- Data Substrate: structural lineage (for example, this table came from that source via this join; which snapshot of which catalog).
- Metrology: measurement quality of the assertion right now — error bounds, calibration standard, quality-gate results, **measurement confidence after quality rules**, freshness, decay, validity window, and (for table-valued objects) snapshot statistics such as row counts, null counts, and commit age.
- Epistemology: chain of custody and warrant for the claim — which agent or activity generated it, when, the SHA-256 fingerprint of this version, the trust level of the producer, corroborating sources, and belief revision over time.

**Two confidences.** *Measurement confidence* (Metrology) is how well this assertion survived the quality rules at ingest and how fresh it still is. *Producer trust* (Epistemology) is how much the source is believed before any quality rule runs. *Claim confidence* produced by verification agents (`AG3`) — source count, corroboration, conflict — is also Epistemology. They are different numbers and are stored under different envelopes; a policy or routing rule names which one it reads.

### 5.1 Per-Layer Storage Mapping

Each MOEPA layer has a natural representation for its knowledge artifacts. The shared substrate stores the **base triple once**; each layer attaches a **metadata envelope** (or a linked sub-graph) without duplicating the base fact.

| Layer | Natural Representation | Storage on Shared Substrate |
| :--- | :--- | :--- |
| **Metrology** | Observations with units, error bounds, calibration standards, quality-gate results, measurement confidence, freshness and decay, validity windows, drift status | Metrology envelope on each record (`confidenceScore`, `validUntil`, decay label) in the open lakehouse (`DS1`: Apache Iceberg / Polaris, Parquet) with a provenance stamp (`DS2`). When the Ontology object is itself a lakehouse table, the table's snapshot and manifest metrics (row counts, null counts, commit age) are the metrology source; no separate store is needed |
| **Ontology** | Entities, categories, hierarchies, typed relations; graphs, taxonomies, semantic networks | SPO columns on each record in the lakehouse (`DS3`), projected into an RDF/SPARQL store (Apache Jena Fuseki) or self-managed property graph (Neo4j) for graph walk and query; nodes = entities, edges = relations; registry entries for governed assets (`DS6`). The graph store is a rebuildable projection of the lakehouse |
| **Epistemology** | Justified beliefs, chains of custody, evidence trails, producer trust, claim confidence, uncertainty models (Bayesian networks, Dempster-Shafer, argumentation frameworks) | Epistemology envelope on each record (W3C PROV-O generating agent and time, SHA-256 fingerprint, producer trust); verification results and corroboration written by `AG3`; embedding vectors stored durably in a lakehouse table keyed to record `@id` and fingerprint, projected into the owned vector index (`DS4`) |
| **Praxeology** | Plans, decision procedures, action sequences, per-record action scopes, outcome telemetry, production rules, goal hierarchies, MDPs / PDDL planning domains | Praxeology envelope on each record (allowed and denied action classes, execution trigger), evaluated as a policy package before any tool call; workflow state snapshots and action logs as time-series or versioned triples in the decision ledger (`DS5`); procedural attachments to graph nodes (HAS_PROCEDURE edges → state machines / scripts) |
| **Axiology** | Value hierarchies, utility/preference functions, ethical constraints, classification markings, priority rankings, multi-criteria decision models (weighted sums, lexicographic ordering, deontological rules) | Axiology envelope on each record (classification marking, PII flag, mission alignment, value weight); versioned Policy-as-Code bundles and the Golden Master baseline (`DS7`) that hold the rules — including the clearance-versus-marking rule — evaluated against that envelope; value nodes + weighted relation graphs (PREFERS / CONSTRAINS edges); policy-check outcomes, allow and deny, written to the ledger (`DS5`) with the policy bundle hash |

**Unification principle.** All five layers write to and read from the same SPO-centric hypergraph + lakehouse. A federation layer (workflow router or Trino) enables cross-layer queries such as: *"find all high-confidence (epistemic) income facts that satisfy axiological fairness and support praxeological auto-approval."* Each layer's knowledge keeps its own envelope while belief, action, and value revision can run across the stack.

**Where "who may see it" lives.** The Epistemology layer asks the question at retrieval time, but it does not own the answer. The classification marking is an Axiology attribute of the record, the clearance rule is Policy-as-Code in `DS7`, and the Policy Gate (`AG5`) evaluates caller clearance against the marking. Verification and retrieval agents (`AG3`, `DS4`) apply that decision as pre-retrieval filtering; they consume the marking, they do not define it. This keeps disclosure rules outside both the model and the retrieval code.

**Scale range.** From edge devices (lightweight JSON triples + SQLite) to enterprise deployments (full graph + Iceberg).

### 5.2 Architectural Evolution Principles

All implementations adopting the MOEPA Cognitive Architecture must follow the
evolution principles below:

**Governance over abstraction.** Avoid vendor-locked orchestration — native
Bedrock-only tooling, LangChain glue-code, or equivalent framework coupling
that cannot be ported. Use the Model Context Protocol (MCP) as the standardized
interface for all data and tool access. New capabilities are defined as MCP
servers so logic remains portable across hosts (Bedrock, self-hosted
orchestrators, or equivalent runtimes).

**From fragments to semantic objects.** No chainsaw chunking. Ingestion uses
document-aware semantic parsing (Docling, Unstructured, or equivalent). Every
data object carries provenance, structure, and semantic metadata. Chunks are
Proto-SPOs — provenance-stamped semantic segments not yet normalized into
Subject-Predicate-Object triples — that preserve semantic intent end-to-end
before converging to owned SPO/quad records on the substrate.

**MCP-first pattern.** Orchestrators do not call data or RAG layers directly.
Service logic lives inside MCP-compliant services. Legacy APIs required for
throughput are wrapped in MCP facades so capabilities remain visible and
governable for AI orchestrators.

**One gateway, no side doors.** MCP is the discovery and invocation contract;
it is not by itself a veto. Every model endpoint, MCP server, and tool facade
sits behind a single policy-enforcing gateway that holds each request until
the Policy Gate (`AG5`) and the action-scope gate (`AG4`) return allow. The
gateway pattern is external authorization (for example Envoy `ext_authz`): the
proxy stays a proxy, the authorizer loads the governing record, asks the policy
engine, writes the decision — allow or deny — to the ledger (`DS5`), and only
then lets the proxy route upstream. A denied request never reaches the model
or the tool. A model or tool endpoint reachable by any path that skips this
gateway is a side door. A side door scores below 3 on Axiology and Praxeology
— an automatic NO-GO — regardless of what the gated path does, unless it is
covered by a time-boxed, recorded exception under §9 with a named date by
which it closes.

## 6. Implementation Playbook
### 6.1 Recommended Technology Stack by Layer (Ownership-Focused)

**Cross-cutting — MCP integration layer:** Expose every layer capability as an
MCP server or MCP facade. Orchestrators (Bedrock Agents, LangGraph routers,
policy-governed agent runtimes) discover and invoke tools only through MCP — never
through direct RAG or data-layer API calls.

**Cross-cutting — policy-enforcing gateway and model translation:** One
gateway (Envoy or equivalent with external authorization) is the only entry
point for callers; it delegates allow/deny to the policy engine and routes
only allowed requests upstream. Behind it, a model translation proxy (LiteLLM
or equivalent) turns an allowed inference call into a call to whichever model
host is in use — local open-weight models on owned GPUs, or a cloud model
later — so the model is swappable "muscle" and never sees a request the
gateway denied. Pin gateway, catalog, graph, and proxy images to digests so
the running control plane is the reviewed control plane.

- Metrology (Data Foundation): Self-hosted open lakehouse (MinIO or any
  S3-compatible object store + Iceberg under an Apache Polaris table catalog),
  Great Expectations or Monte Carlo for quality, OpenLineage / PROV-O for
  lineage — avoiding a vendor-owned store as the only record of lineage.
  Iceberg snapshot and manifest metrics serve as metrology for table-valued
  objects. Semantic document parsing via Docling, Unstructured, or equivalent;
  ingestion outputs Proto-SPOs with provenance envelopes, exposed through an
  MCP ingestion server.
- Ontology: Apache Jena Fuseki (RDF / SPARQL, runs unchanged on a laptop and on
  any Kubernetes) or self-managed Neo4j, loaded as a projection from the
  lakehouse; internal schema governance; entity resolution and graph queries
  exposed as MCP tools. Managed cloud graph services (Amazon Neptune, Azure
  Cosmos Gremlin, Spanner Graph) are conditional rent at best: the query
  dialect and operations lock to the provider, so they are not a home for the
  canonical semantic model.
- Epistemology: Self-hosted retrieval (Qdrant / pgvector / Chroma) loaded as a
  projection from a lakehouse embeddings table + Guardrails AI +
  cryptographic validation in CI/CD; RAG and verification exposed as MCP
  servers — not called directly from orchestration glue.
- Praxeology: Per-record action scopes evaluated as a policy package in the
  same engine as Axiology (one decision, two packages) for the tool-call gate;
  deterministic workflow engines (LangGraph, Temporal, Camunda) with
  human-in-the-loop approval queues for sequencing and checkpoints; workflow
  steps and state transitions exposed as MCP tools.
- Axiology: OPA/Gatekeeper for policy-as-code, OS- or infrastructure-level write
  locks on the Golden Master baseline; policy bundle hash recorded on every
  ledger decision; policy checks exposed as MCP tools for pre-action gating and
  invoked by the gateway authorizer.

### 6.2 Quick-Start Checklist for New Projects
- Define Metrology boundary and data quality baseline (internal control, not vendor-owned).
- Adopt the MOEPA record shape (§5.0): one triple plus four envelopes, JSON-LD against an owned context, required fields rejected at write, append-only supersession by `@id` and fingerprint.
- Stand up the lakehouse and catalog as the only system of record; prove every projection (graph, vector, policy bundle) can be emptied and rebuilt from it (§5.0.1).
- Implement semantic ingestion producing Proto-SPOs with provenance, structure, and semantic metadata (no chainsaw chunking).
- Expose ingestion, retrieval, workflow, and policy capabilities as MCP servers or facades.
- Put one policy-enforcing gateway in front of every model and tool endpoint; prove a denied request returns a refusal at the gateway and never reaches the model (§5.2).
- Create or extend domain ontology / knowledge graph schema (internal ownership).
- Implement RAG with citation + grounding verification pipeline against owned data (via MCP, not direct API calls).
- Design deterministic workflow (state machine or auditable step sequence) with MCP-governed tool invocation.
- Create the Golden Master policy baseline and apply OS- or infrastructure-level write locks; write the bundle hash to the ledger on every decision.
- Pin control-plane images to digests.
- Map all five layers to the MOEPA scorecard and obtain review board sign-off.

## 7. Success Metrics & Key Performance Indicators
### Governance Health
- % of AI projects that pass initial MOEPA intake on first submission (target: >70%).
- Average time from intake submission to GO/NO-GO decision (target: <5 business days).

### Risk Reduction
- Reduction in vendor-owned layer dependencies (target: significant reduction in external vendor control of Metrology/Ontology layers).
- Reduction in security findings related to AI systems.
- Mean time to detect policy drift or configuration bypass.

### Operational Excellence
- Infrastructure cost predictability.
- Model performance consistency before vs. after MOEPA controls.
- Developer velocity on approved patterns.

## 8. Alignment with Industry Standards & Frameworks
MOEPA is designed to be complementary to major AI governance frameworks:

- NIST AI RMF 1.0
- ISO/IEC 42001:2023
- MITRE ATLAS
- OWASP LLM Top 10

## 9. Governance of the MOEPA Cognitive Architecture
The practices below describe how an organization adopting the MOEPA Cognitive Architecture should govern its own instance. Architectural evolution rules (MCP-first integration, semantic ingestion, Proto-SPOs, five-layer PR gate) are defined in §5.2 above. To propose changes to this repository itself, see [CONTRIBUTING.md](../CONTRIBUTING.md).

- Semantic versioning (MAJOR.MINOR.PATCH).
- Quarterly review by Architecture Review Board.
- Time-boxed exception process for high-value innovation pilots.
- Open internal RFC process for proposed changes.
