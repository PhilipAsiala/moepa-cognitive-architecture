# The MOEPA Cognitive Architecture — Technical Specification

Leaders start at the [repository primer](../README.md). This file is the builder specification.

Version: 3.0 — Three-Tier Model (Thesis / Data Substrate / Agents)

Author: Philip Asiala

Last Updated: October 18, 2026

Status: Draft for Review — Feedback Welcome

Repository: [philosophical-ai-architecture](https://github.com/PhilipAsiala/philosophical-ai-architecture) (GitHub) — canonical home of the MOEPA Cognitive Architecture

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

- Internally managed knowledge graphs (Neo4j, Amazon Neptune).
- Custom entity resolution and schema management.
- Version-controlled semantic models.

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

```json
{
  "triple": {"s": "IncomeVerification:TX12345", "p": "hasAmount", "o": 85000},
  "epistemic_metadata": {"confidence": 0.98, "justification": "ThirdPartyStudy_2025_n=125000", "status": "HighReliability"}
}
```

A federation layer (for example, a workflow router or Trino) supports cross-layer queries such as: "find all high-confidence income facts that satisfy axiological fairness and support praxeological auto-approval."

**End state vs. evolution.** The SPO/quad hypergraph + lakehouse described here is the **imperative end state** — every substrate must converge on owned triples with layer metadata envelopes and federated cross-layer query. Organizations **evolve** toward that target incrementally (e.g. Iceberg/Parquet with SPO-compatible schemas first, pilot triple store, then enterprise graph + federation). Interim storage is valid when ownership, open formats, provenance, and a documented migration path to the SPO/quad end state are in place.

This substrate scales from lightweight edge deployments (JSON triples + SQLite) to enterprise deployments (full graph + Iceberg). It is sovereignty-aligned with the Owned-Brain strategy: self-hosted graph control, open formats, PROV-O lineage compatibility, and one owned base triple that remains queryable as a single auditable whole.

**Provenance three-way split** (to avoid double-claiming):
- Data Substrate: structural lineage (for example, this table came from that source via this join).
- Metrology: observational provenance (who measured it, against what standard, with what error bounds).
- Epistemology: justificatory provenance (confidence, warrant, and belief revision over claims).

### 5.1 Per-Layer Storage Mapping

Each MOEPA layer has a natural representation for its knowledge artifacts. The shared substrate stores the **base triple once**; each layer attaches a **metadata envelope** (or a linked sub-graph) without duplicating the base fact.

| Layer | Natural Representation | Storage on Shared Substrate |
| :--- | :--- | :--- |
| **Metrology** | Observations with units, error bounds, calibration standards, quality-gate results, drift status, observational lineage | Base triples and tabular records in the open lakehouse (`DS1`: Apache Iceberg / Polaris, Parquet) with a measurement-trust envelope and provenance stamp (`DS2`) |
| **Ontology** | Entities, categories, hierarchies, typed relations; graphs, taxonomies, semantic networks | Native graph DBs (Neo4j, property graphs) or RDF-style triples (`DS3`); nodes = entities, edges = relations; registry entries for governed assets (`DS6`) |
| **Epistemology** | Justified beliefs, evidence trails, confidence weights, provenance chains, uncertainty models (Bayesian networks, Dempster-Shafer, argumentation frameworks) | Enriched SPO triples with epistemic metadata (confidence, source reliability, evidence-graph links, revision history); owned vector index entries bound to entity and provenance IDs (`DS4`); versioned facts with W3C PROV-O lineage |
| **Praxeology** | Plans, decision procedures, action sequences, outcome telemetry, production rules, goal hierarchies, MDPs / PDDL planning domains | Workflow state snapshots and action logs as time-series or versioned triples in the decision ledger (`DS5`); procedural attachments to graph nodes (HAS_PROCEDURE edges → state machines / scripts) |
| **Axiology** | Value hierarchies, utility/preference functions, ethical constraints, priority rankings, multi-criteria decision models (weighted sums, lexicographic ordering, deontological rules) | Versioned Policy-as-Code bundles and the Golden Master baseline (`DS7`); value nodes + weighted relation graphs (PREFERS / CONSTRAINS edges); policy-check outcomes written to the ledger (`DS5`) |

**Unification principle.** All five layers write to and read from the same SPO-centric hypergraph + lakehouse. A federation layer (workflow router or Trino) enables cross-layer queries such as: *"find all high-confidence (epistemic) income facts that satisfy axiological fairness and support praxeological auto-approval."* Each layer's knowledge keeps its own envelope while belief, action, and value revision can run across the stack.

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

## 6. Implementation Playbook
### 6.1 Recommended Technology Stack by Layer (Ownership-Focused)

**Cross-cutting — MCP integration layer:** Expose every layer capability as an
MCP server or MCP facade. Orchestrators (Bedrock Agents, LangGraph routers,
policy-governed agent runtimes) discover and invoke tools only through MCP — never
through direct RAG or data-layer API calls.

- Metrology (Data Foundation): Self-hosted open lakehouse (MinIO + Iceberg under an
  Apache Polaris table catalog), Great Expectations or Monte Carlo for quality,
  OpenLineage / PROV-O for lineage — avoiding a vendor-owned store as the only
  record of lineage. Semantic document parsing via Docling,
  Unstructured, or equivalent; ingestion outputs Proto-SPOs with provenance
  envelopes, exposed through an MCP ingestion server.
- Ontology: Neo4j or Amazon Neptune (self-managed), internal schema governance;
  entity resolution and graph queries exposed as MCP tools.
- Epistemology: Self-hosted retrieval (PGVector/Chroma) + Guardrails AI +
  cryptographic validation in CI/CD; RAG and verification exposed as MCP
  servers — not called directly from orchestration glue.
- Praxeology: Deterministic workflow engines (LangGraph, Temporal, Camunda)
  with human-in-the-loop approval queues; workflow steps and state transitions
  exposed as MCP tools.
- Axiology: OPA/Gatekeeper for policy-as-code, OS- or infrastructure-level write
  locks on the Golden Master baseline; policy checks exposed as MCP tools for
  pre-action gating.

### 6.2 Quick-Start Checklist for New Projects
- Define Metrology boundary and data quality baseline (internal control, not vendor-owned).
- Implement semantic ingestion producing Proto-SPOs with provenance, structure, and semantic metadata (no chainsaw chunking).
- Expose ingestion, retrieval, workflow, and policy capabilities as MCP servers or facades.
- Create or extend domain ontology / knowledge graph schema (internal ownership).
- Implement RAG with citation + grounding verification pipeline against owned data (via MCP, not direct API calls).
- Design deterministic workflow (state machine or auditable step sequence) with MCP-governed tool invocation.
- Create the Golden Master policy baseline and apply OS- or infrastructure-level write locks.
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
