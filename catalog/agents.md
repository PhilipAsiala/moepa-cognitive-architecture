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
| **AG7** | [Policy-Enforcing Gateway](#ag7--policy-enforcing-gateway-cross-cutting) | Cross-Cutting | Deterministic Veto | The one door every caller uses; holds each request until the gates allow it and refuses the rest before any model or tool is reached |
| **AG8** | [Model Translation Proxy](#ag8--model-translation-proxy-cross-cutting) | Cross-Cutting | Rented Seam | Turn an allowed inference call into a call to whichever model host is in use, so models are swappable without touching records or gates |

---

## AG1 — Telemetry and Quality Gate Agents (Metrology)

- **What they do:** Inspect raw signals, documents, and batch/streaming feeds at ingress; enforce completeness, format, and range rules; attach confidence intervals; and monitor post-launch data drift and outcome KPIs against pre-launch baselines.
- **Failure mode they prevent:** Silent model degradation when an upstream data provider changes a schema or a sensor feed drifts out of calibration.
- **Minimum standard (Score 3 baseline):** Ingress validation rules run on core fields (a record missing a required envelope field, or with a confidence outside 0–1, is rejected before substrate write), failures are quarantined and escalated, and pre/post-launch outcome metrics are tracked. Each record carries a measurement envelope — confidence after quality rules, a validity window, and a decay label — so freshness is a stored fact, not an inference.
- **Target maturity (Score 4–5):** Continuous statistical profiling and drift alerting on every feed; automatic pipeline halt when quality thresholds break; a record whose validity window has passed is denied or re-qualified rather than served; lakehouse snapshot statistics (row counts, null counts, commit age) populate the measurement envelope for table-valued records; scheduled post-launch outcome KPI measurement published to the ledger (`DS5`) so `AG5` can judge whether the approved ROI case still holds.
- **Representative tools:** Great Expectations, Soda, Monte Carlo, OpenTelemetry, Iceberg snapshot/manifest metadata, Docling/Unstructured MCP ingestion servers.

---

## AG2 — Entity Resolution and Semantic Mapping Agents (Ontology)

- **What they do:** Resolve incoming records, names, accounts, and document mentions against the [Canonical Entity Registry and Knowledge Graph](data-substrate.md#ds3--canonical-entity-registry-and-knowledge-graph) (`DS3`), applying controlled taxonomies and linking relationships across datasets without inventing ad-hoc schemas.
- **Failure mode they prevent:** An AI assistant treating two records for the same legal entity as unrelated, or merging two distinct beneficiaries because of an unverified fuzzy match.
- **Minimum standard (Score 3 baseline):** Entity resolution rules map inputs to documented enterprise definitions and canonical code sets; ambiguous matches are flagged rather than auto-merged.
- **Target maturity (Score 4–5):** Graph-backed entity resolution agents with point-in-time schema awareness, confidence-scored relationship linking, and mandatory stewardship review for taxonomy changes.
- **Representative tools:** Graph resolution services over Apache Jena Fuseki (SPARQL) or Neo4j, RDF/SHACL validators, custom MCP entity-resolution servers.

---

## AG3 — Verification, Grounding, and Citation Agents (Epistemology)

- **What they do:** Sit between raw model generation and any downstream workflow. They retrieve grounded context from the [Owned Vector and Retrieval Index](data-substrate.md#ds4--owned-vector-and-grounded-retrieval-index) (`DS4`), verify that every factual claim in a proposed output cites an owned substrate record, check that the requesting user has clearance for those sources (applying the clearance-versus-marking rule defined in `DS7` before any evidence enters the context window), decompose confidence scores into evidence components, and reject ungrounded assertions.
- **Failure mode they prevent:** Hallucinations presented as official policy, opaque "94% confidence" scores that cannot be explained in an appeal, and unauthorized data leakage through RAG context windows.
- **Minimum standard (Score 3 baseline):** Responses cite owned source records; high-stakes claims are checked against a primary source before action; confidence methodology is documented; ungrounded outputs are flagged for review. A narrow deterministic form of this gate is a **citation allow-list**: the gate decision names the record IDs the model was authorized to use, and a completion that cites an ID outside that set, or names a denied action, is blocked post-call. This catches concrete leaks without a second model call; it does not establish that the rest of the answer is true, and it is idle if no decision packet is attached to the request.
- **Target maturity (Score 4–5):** Automated fact-verification and hallucination-detection gate blocks any ungrounded claim before it reaches a user or workflow; confidence scores break down source count, freshness, and conflict; pipeline artifacts are SHA-256 verified.
- **Representative tools:** Self-hosted RAG verification pipelines, Guardrails AI, Patronus / Ragas evaluation gates, cryptographic artifact signing.

---

## AG4 — Workflow and Execution Agents (Praxeology)

- **What they do:** Translate verified context into bounded business action. An orchestration agent may use a language model to decompose a goal or draft a plan, but execution is governed by a deterministic state machine that routes routine steps to ordinary code or small local models, reserves heavy frontier models for complex synthesis, enforces strict tool scopes, and pauses at mandatory human-in-the-loop checkpoints. Only pre-approved, non-consequential action classes may run end-to-end without a human approver; confidence scores route review effort but never waive the checkpoint on a consequential action.
- **Failure mode they prevent:** Rogue automation — agents calling unauthorized APIs, skipping required review steps, entering infinite loops, or burning frontier-model budget on routine lookups.
- **Minimum standard (Score 3 baseline):** Workflows follow a defined sequence of states; authorized agent tools are explicitly listed and out-of-scope calls are blocked; human approval is required and logged before any externally visible or consequential action; exception and escalation paths are defined. Praxeology has two halves that must agree: the **agent-side** allow-list of tools and states, and the **record-side** action envelope — the allowed and denied action classes carried on every substrate record ([ARCHITECTURE.md §5](ARCHITECTURE.md)). An action runs only when it is named, is in the record's allowed list, is not in its denied list, and is in the caller's scope. When the model is a leaf (it answers but never calls tools), there is no agentic loop to bound and the minimum reduces to that record-side check plus logging; the human checkpoint still applies to any consequential action class.
- **Target maturity (Score 4–5):** Infrastructure-enforced state machines (impossible to skip states or checkpoints via prompt manipulation); version-controlled adaptation rules; full state-transition audit logging to `DS5`.
- **Representative tools:** LangGraph, Temporal, Camunda, deterministic workflow routers, record-level action envelopes evaluated by the policy engine.

---

## AG5 — Policy and Compliance Gate Agents (Axiology)

- **What they do:** Enforce organizational law, regulatory mandates, ethics, and financial boundaries *outside* the probabilistic model. Every action proposed by `AG4` or response verified by `AG3` must pass through deterministic Policy-as-Code (loaded from the owned [Policy Baseline](data-substrate.md#ds7--policy-as-code-and-constitutional-baseline), `DS7`), constitutional guardrails, and prompt-injection defenses before execution. Also runs continuous bias/equity monitoring and enforces business ROI and chargeback/showback accountability, judging the outcome KPIs that `AG1` measures against the ROI case approved at intake.
- **Failure mode they prevent:** Relying on a system prompt ("please follow federal regulations and do not leak PII") to enforce statutory compliance, spending limits, or Rules of Engagement.
- **Minimum standard (Score 3 baseline):** Core statutory, privacy, and compliance rules are encoded as machine-enforceable checks that block violations; prompt-injection sanitization is active; periodic bias audits and red-team guardrail tests are conducted; proposal ROI and cost attribution are documented.
- **Target maturity (Score 4–5):** Infrastructure-level Policy-as-Code (Open Policy Agent / Gatekeeper) with veto power over every tool call and output; continuous demographic equity alerting; scheduled adversarial red-teaming; auditable ROI sensitivity and chargeback models integrated with finance. The strongest enforcement point is a **policy-enforcing gateway** in front of every model and data endpoint: the gateway holds the request on an external-authorization call, the authorizer loads the record and asks the policy engine, and a deny becomes an HTTP refusal that the model process never sees. Every door to a model must sit behind that gateway; a side door that reaches the model without the record check is an exception that must be time-boxed and recorded.
- **Representative tools:** Open Policy Agent (OPA / Rego), Cedar, Envoy `ext_authz` (or equivalent gateway external authorization), LLM Guard, NeMo Guardrails, fairness and telemetry monitors.

---

## AG6 — MCP Capability Bus (Cross-Cutting)

- **What it does:** Wraps every Data Substrate service (`DS1`–`DS8`) and Agent capability (`AG1`–`AG5`) behind standardized **Model Context Protocol (MCP)** servers or lightweight MCP facades for legacy APIs. Orchestrators discover and invoke tools exclusively through MCP. The bus sits *behind* the Policy-Enforcing Gateway (`AG7`): MCP is how a tool is found and called, the gateway is what decides whether the call may happen.
- **Failure mode they prevent:** Framework lock-in — where business logic is buried inside vendor-specific agent callbacks (e.g., proprietary cloud agent bindings or tightly coupled prompt chains) that cannot be audited or moved to a different model host.
- **Minimum standard (Score 3 baseline):** Tool interfaces between orchestrators and enterprise data/services use explicit, versioned contracts with central call logging. A versioned REST surface over a published JSON-LD record context, fronted by a gateway that logs every decision to `DS5`, meets this baseline; it is the integration point that later becomes an MCP facade.
- **Target maturity (Score 4–5):** Every ingestion, graph query, retrieval, workflow step, and policy gate is exposed as an MCP server or facade, allowing the enterprise to swap underlying LLMs or orchestrators without rewriting capability integrations. The MCP bus and the Policy-Enforcing Gateway (`AG7`) are complementary, not alternatives: MCP governs what an *agent* may reach; the gateway governs what any *caller* may reach. Model portability behind the gateway is delivered by the Model Translation Proxy (`AG8`).

---

## AG7 — Policy-Enforcing Gateway (Cross-Cutting)

- **What it does:** Is the only door a caller can use to reach a model, a tool, or the substrate. The gateway holds every request on an external-authorization call; an authorizer loads the governing substrate record, asks the Policy Gate (`AG5`) and the action-scope gate (`AG4`) for one decision, writes that decision — allow or deny — to the ledger (`DS5`) with the policy bundle hash, and only then lets the proxy route upstream. A deny is an HTTP refusal that the model process never sees. The gateway is also where caller identity and clearance are established, by consulting the identity registry (`DS8`) rather than trusting a header.
- **Failure mode they prevent:** A side door — any path to a model or tool that skips the record check — and gates that only advise because nothing in front of the model can refuse. This capability came out of deployment: the Policy Gate was correct from the start, but a denied prompt only stopped reaching the model once a gateway existed to hold the request.
- **Minimum standard (Score 3 baseline):** One gateway fronts every model and tool endpoint; it fails closed when the authorizer is unreachable; the authorizer logs every outcome; no other published route reaches a model. Any temporary side door is recorded as a time-boxed exception with a close date (ARCHITECTURE.md §9).
- **Target maturity (Score 4–5):** The gateway resolves identity, tenant, and clearance from `DS8` and passes them to the authorizer; the request body is forwarded so the authorizer can check what is being asked, not just who is asking; the gateway is the only ingress in production and all other service ports are unpublished; the decision is written before the upstream call is released (fail-closed ledger, see `DS5`).
- **Representative tools:** Envoy `ext_authz`, Envoy Gateway, Istio external authorization, Kong request-authorizer plugins — anything that can hold a request, call out, forward the body, and fail closed.

---

## AG8 — Model Translation Proxy (Cross-Cutting)

- **What it does:** Receives an inference call that the gateway (`AG7`) has already allowed and translates it to whichever model host is in use: open-weight models on owned GPUs, a cloud model API, or a managed inference endpoint. The record shape, the policy rules, the ledger, and the gateway contract do not change when the model does. It may also run a narrow post-call screen — the citation allow-list described under `AG3` — using a decision packet the gateway attached to the request.
- **Failure mode they prevent:** Model lock-in by integration: business logic that calls a specific vendor's API shape, so that changing models means changing every caller; and model calls that bypass the gate because the model endpoint was reachable directly.
- **Minimum standard (Score 3 baseline):** One OpenAI-compatible (or equivalent stable) interface for all callers; model hosts configured in one place; the proxy is reachable only through `AG7`; model list and routing are versioned configuration the organization owns.
- **Target maturity (Score 4–5):** Routing by task class (routine to small local models, synthesis to frontier models) driven by `AG4`; a post-call decision-packet screen on every routed call; the proxy's published ports removed in production; a model swap demonstrated with no change to any other unit's check.
- **Representative tools:** LiteLLM, vLLM routers, cloud model gateways (Bedrock, SageMaker, Vertex) behind the same `/v1` shape.
- **Ownership note:** This is the "rent the muscles" seam. The models behind it are rented; the proxy configuration — which models, which routes, which screen — is owned, which is why it is in the catalog.

---

## Related Catalog Pages

- **[Data Substrate Capabilities](data-substrate.md)** — the owned storage foundation these agents consume (`DS1`–`DS8`)
- **[Enterprise Capability Matrix](capability-matrix.md)** — Score 3 baseline requirements and ownership for `AG1`–`AG8`
- **[End-to-End Business Compositions](cross-layer-compositions.md)** — how `AG1`–`AG8` and `DS1`–`DS8` wire together in production workflows
- **[Technical Specification](ARCHITECTURE.md)** — §5.2 MCP-first and Proto-SPO evolution rules
