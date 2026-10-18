# Enterprise Agent Capabilities (The Engine)

**The business problem:** Vendors sell "Agentic AI" as a single black box that reads documents, guesses answers, and calls enterprise APIs. When that box hallucinates a policy, enters an infinite loop, or violates a regulation, leadership cannot tell whether the failure was bad input data, a broken definition, an unverified claim, a rogue workflow, or a missing compliance rule.

**The capability pillar:** In the **MOEPA Cognitive Architecture**, **Agents** are the execution engine that consumes the [Data Substrate](data-substrate.md). An Agent here is any governed service that acts on the substrate — the probabilistic planners that draft and propose, and the deterministic gates that bound them. Instead of one unconstrained agent, the enterprise deploys distinct agent and control capabilities mapped to the five MOEPA layers — separating **probabilistic planning** (where models draft, summarize, and propose) from **deterministic gates** (where code verifies sources, enforces workflows, and blocks policy violations).

---

## Capability Summary

| ID | Agent / Control Capability | MOEPA Layer | Mode | Business Function |
| :--- | :--- | :--- | :--- | :--- |
| **AG1** | [Telemetry and Quality Gate Agents](#ag1--telemetry-and-quality-gate-agents-metrology) | 1. Metrology | Deterministic + Statistical | Qualify incoming data, score uncertainty, detect drift, and quarantine bad feeds before substrate write |
| **AG2** | [Entity Resolution and Semantic Mapping Agents](#ag2--entity-resolution-and-semantic-mapping-agents-ontology) | 2. Ontology | Hybrid (Model + Graph Rules) | Map raw records to canonical enterprise entities and controlled vocabularies |
| **AG3** | [Verification, Grounding, and Citation Agents](#ag3--verification-grounding-and-citation-agents-epistemology) | 3. Epistemology | Deterministic Gate over Model Output | Verify claims against the Data Substrate, check user clearance, decompose confidence, and block hallucinations |
| **AG4** | [Workflow and Execution Agents](#ag4--workflow-and-execution-agents-praxeology) | 4. Praxeology | Probabilistic Plan / Deterministic State Machine | Route intent to the right model or tool, enforce step order, and pause at human checkpoints |
| **AG5** | [Policy and Compliance Gate Agents](#ag5--policy-and-compliance-gate-agents-axiology) | 5. Axiology | Deterministic Refusal | Enforce Policy-as-Code, constitutional guardrails, injection defense, and equity/ROI controls outside the LLM |
| **AG6** | [MCP Capability Bus](#ag6--mcp-capability-bus-cross-cutting) | Cross-Cutting | Deterministic Contract | Expose every substrate and agent tool through governed Model Context Protocol servers or facades |

---

## AG1 — Telemetry and Quality Gate Agents (Metrology)

- **What they do:** Inspect raw signals, documents, and batch/streaming feeds at ingress; enforce completeness, format, and range rules; attach confidence intervals; and monitor post-launch data drift and outcome KPIs against pre-launch baselines.
- **Failure mode they prevent:** Silent model degradation when an upstream data provider changes a schema or a sensor feed drifts out of calibration.
- **Minimum standard (Score 3 baseline):** Ingress validation rules run on core fields, failures are quarantined and escalated, and pre/post-launch outcome metrics are tracked.
- **Target maturity (Score 4–5):** Continuous statistical profiling and drift alerting on every feed; automatic pipeline halt when quality thresholds break; scheduled post-launch outcome KPI measurement published to the ledger (`DS5`) so `AG5` can judge whether the approved ROI case still holds.
- **Representative tools:** Great Expectations, Soda, Monte Carlo, OpenTelemetry, Docling/Unstructured MCP ingestion servers.

---

## AG2 — Entity Resolution and Semantic Mapping Agents (Ontology)

- **What they do:** Resolve incoming records, names, accounts, and document mentions against the [Canonical Entity Registry and Knowledge Graph](data-substrate.md#ds3--canonical-entity-registry-and-knowledge-graph) (`DS3`), applying controlled taxonomies and linking relationships across datasets without inventing ad-hoc schemas.
- **Failure mode they prevent:** An AI assistant treating two records for the same legal entity as unrelated, or merging two distinct beneficiaries because of an unverified fuzzy match.
- **Minimum standard (Score 3 baseline):** Entity resolution rules map inputs to documented enterprise definitions and canonical code sets; ambiguous matches are flagged rather than auto-merged.
- **Target maturity (Score 4–5):** Graph-backed entity resolution agents with point-in-time schema awareness, confidence-scored relationship linking, and mandatory stewardship review for taxonomy changes.
- **Representative tools:** Graph resolution services over Neo4j / Amazon Neptune, RDF/SHACL validators, custom MCP entity-resolution servers.

---

## AG3 — Verification, Grounding, and Citation Agents (Epistemology)

- **What they do:** Sit between raw model generation and any downstream workflow. They retrieve grounded context from the [Owned Vector and Retrieval Index](data-substrate.md#ds4--owned-vector-and-grounded-retrieval-index) (`DS4`), verify that every factual claim in a proposed output cites an owned substrate record, check that the requesting user has clearance for those sources, decompose confidence scores into evidence components, and reject ungrounded assertions.
- **Failure mode they prevent:** Hallucinations presented as official policy, opaque "94% confidence" scores that cannot be explained in an appeal, and unauthorized data leakage through RAG context windows.
- **Minimum standard (Score 3 baseline):** Responses cite owned source records; high-stakes claims are checked against a primary source before action; confidence methodology is documented; ungrounded outputs are flagged for review.
- **Target maturity (Score 4–5):** Automated fact-verification and hallucination-detection gate blocks any ungrounded claim before it reaches a user or workflow; confidence scores break down source count, freshness, and conflict; pipeline artifacts are SHA-256 verified.
- **Representative tools:** Self-hosted RAG verification pipelines, Guardrails AI, Patronus / Ragas evaluation gates, cryptographic artifact signing.

---

## AG4 — Workflow and Execution Agents (Praxeology)

- **What they do:** Translate verified context into bounded business action. An orchestration agent may use a language model to decompose a goal or draft a plan, but execution is governed by a deterministic state machine that routes routine steps to ordinary code or small local models, reserves heavy frontier models for complex synthesis, enforces strict tool scopes, and pauses at mandatory human-in-the-loop checkpoints. Only pre-approved, non-consequential action classes may run end-to-end without a human approver; confidence scores route review effort but never waive the checkpoint on a consequential action.
- **Failure mode they prevent:** Rogue automation — agents calling unauthorized APIs, skipping required review steps, entering infinite loops, or burning frontier-model budget on routine lookups.
- **Minimum standard (Score 3 baseline):** Workflows follow a defined sequence of states; authorized agent tools are explicitly listed and out-of-scope calls are blocked; human approval is required and logged before any externally visible or consequential action; exception and escalation paths are defined.
- **Target maturity (Score 4–5):** Infrastructure-enforced state machines (impossible to skip states or checkpoints via prompt manipulation); version-controlled adaptation rules; full state-transition audit logging to `DS5`.
- **Representative tools:** LangGraph, Temporal, Camunda, deterministic workflow routers.

---

## AG5 — Policy and Compliance Gate Agents (Axiology)

- **What they do:** Enforce organizational law, regulatory mandates, ethics, and financial boundaries *outside* the probabilistic model. Every action proposed by `AG4` or response verified by `AG3` must pass through deterministic Policy-as-Code (loaded from the owned [Policy Baseline](data-substrate.md#ds7--policy-as-code-and-constitutional-baseline), `DS7`), constitutional guardrails, and prompt-injection defenses before execution. Also runs continuous bias/equity monitoring and enforces business ROI and chargeback/showback accountability, judging the outcome KPIs that `AG1` measures against the ROI case approved at intake.
- **Failure mode they prevent:** Relying on a system prompt ("please follow federal regulations and do not leak PII") to enforce statutory compliance, spending limits, or Rules of Engagement.
- **Minimum standard (Score 3 baseline):** Core statutory, privacy, and compliance rules are encoded as machine-enforceable checks that block violations; prompt-injection sanitization is active; periodic bias audits and red-team guardrail tests are conducted; proposal ROI and cost attribution are documented.
- **Target maturity (Score 4–5):** Infrastructure-level Policy-as-Code (Open Policy Agent / Gatekeeper) with veto power over every tool call and output; continuous demographic equity alerting; scheduled adversarial red-teaming; auditable ROI sensitivity and chargeback models integrated with finance.
- **Representative tools:** Open Policy Agent (OPA / Rego), Cedar, LLM Guard, NeMo Guardrails, fairness and telemetry monitors.

---

## AG6 — MCP Capability Bus (Cross-Cutting)

- **What it does:** Wraps every Data Substrate service (`DS1`–`DS7`) and Agent capability (`AG1`–`AG5`) behind standardized **Model Context Protocol (MCP)** servers or lightweight MCP facades for legacy APIs. Orchestrators discover and invoke tools exclusively through MCP.
- **Failure mode they prevent:** Framework lock-in — where business logic is buried inside vendor-specific agent callbacks (e.g., proprietary cloud agent bindings or tightly coupled prompt chains) that cannot be audited or moved to a different model host.
- **Minimum standard (Score 3 baseline):** Tool interfaces between orchestrators and enterprise data/services use explicit, versioned contracts with central call logging.
- **Target maturity (Score 4–5):** Every ingestion, graph query, retrieval, workflow step, and policy gate is exposed as an MCP server or facade, allowing the enterprise to swap underlying LLMs or orchestrators without rewriting capability integrations.

---

## Related Catalog Pages

- **[Data Substrate Capabilities](data-substrate.md)** — the owned storage foundation these agents consume (`DS1`–`DS7`)
- **[Enterprise Capability Matrix](capability-matrix.md)** — Score 3 baseline requirements and ownership for `AG1`–`AG6`
- **[End-to-End Business Compositions](cross-layer-compositions.md)** — how `AG1`–`AG6` and `DS1`–`DS7` wire together in production workflows
- **[Technical Specification](ARCHITECTURE.md)** — §5.2 MCP-first and Proto-SPO evolution rules
