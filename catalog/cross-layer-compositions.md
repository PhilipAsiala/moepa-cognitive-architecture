# End-to-End Business Compositions

Individual capabilities do not deliver business outcomes in isolation. An enterprise AI workflow is a composition of **[Data Substrate capabilities](data-substrate.md) (`DS1`–`DS7`)** and **[Enterprise Agent capabilities](agents.md) (`AG1`–`AG6`)** operating across the five layers of the **MOEPA Cognitive Architecture**.

This page provides six repeatable blueprints for common high-stakes enterprise and public-sector workflows.

---

## 1. End-to-End Decision Auditability

- **Business problem:** A customer, regulator, or inspector general challenges an AI-assisted decision six months later, and the organization must reconstruct the exact data, definitions, sources, human approvals, and policy rules that produced it.
- **Capabilities composed:** `DS2` (Provenance) + `DS3` (Entity Version) + `AG3` (Verification & Citations) + `AG4` (Workflow & Human Checkpoint) + `AG5` (Policy Gate over `DS7`) → written to `DS5` (Cross-Layer Audit Ledger).

```
AG5 — Policy Gate Agent (Axiology)        Records DS7 policy bundle version & pass/refusal
  ↑
AG4 — Workflow Agent (Praxeology)         Records state transitions & human approver ID
  ↑
AG3 — Verification Agent (Epistemology)   Records retrieved source IDs & confidence breakdown
  ↑
AG2 — Entity Agent (Ontology)             Records canonical entity & schema effective date
  ↑
AG1 — Telemetry Agent (Metrology)         Records raw input hash, timestamp & quality status
  ↑
DS5 — Cross-Layer Audit Ledger            Single immutable trace linking all five layers
```

---

## 2. High-Volume Triage with Deterministic Escalation

- **Business problem:** Processing thousands of routine filings, claims, or verifications per day without letting edge cases, low-quality inputs, or low-confidence guesses slip through unreviewed.
- **Capabilities composed:** `AG1` (Telemetry Gate) + `AG2` (Entity Resolution) + `AG3` (Verification Gate) + `AG4` (State Machine & Escalation) + `AG5` (Policy Gate).

```
1. AG1 (Metrology)     → Input quality sufficient?
                           NO  → Quarantine & escalate immediately
                           YES → Proceed to entity resolution (AG2)
2. AG3 (Epistemology)  → Evidence supports high-confidence verified answer?
                           HIGH (≥90%, corroborated) → Automated path (pre-approved, non-consequential action classes only)
                           MEDIUM (70–89%)           → Mandatory human review queue
                           LOW (<70% or conflict)    → Specialist escalation queue
3. AG4 (Praxeology)    → Execute state machine path; every consequential action pauses at the human checkpoint regardless of confidence
4. AG5 (Axiology)      → Enforce Policy-as-Code before any external notice or record update
```

---

## 3. Grounded Enterprise Research & Analyst Copilot

- **Business problem:** Analysts, examiners, or caseworkers need an AI assistant to synthesize complex policies and case files without hallucinating rules or surfacing records the user is not cleared to see.
- **Capabilities composed:** `DS3` (Knowledge Graph) + `DS4` (Owned Vector Index) + `AG3` (Verification & Citation Agent) + `AG5` (Policy & PII Filter).

```
Analyst Query
  ↓
AG2 + DS3 (Ontology)      → Resolve entities and traverse graph relationships
  ↓
AG3 + DS4 (Epistemology)  → Retrieve clearance-filtered passages (`Proto-SPO`s);
                            verify every claim cites an owned record; score confidence
  ↓
AG5 (Axiology)            → Enforce disclosure, privacy, and prompt-injection rules
  ↓
Delivered Response        → Cited substrate IDs + decomposed confidence + policy pass stamp
```

---

## 4. Sovereign AI Project Intake and Portfolio Scoring

- **Business problem:** Evaluating dozens or hundreds of AI proposals consistently, preventing duplicate builds, and blocking vendor lock-in before contracts are signed.
- **Capabilities composed:** `AG4` (Intake Workflow) searching `DS6` (Asset Registry) + `AG5` (ROI & Chargeback Gate) + `DS5` (Governance Ledger).

| Step | Capability | Action |
| :--- | :--- | :--- |
| **1. Deduplicate** | `AG4` over `DS6` + `DS3` | Search the asset registry and canonical entity registry to prove the dataset or agent does not already exist |
| **2. Qualify Data** | `DS1` + `AG1` | Verify whether required source data is already governed on the enterprise platform |
| **3. Score 5 Layers** | [Enterprise Capability Matrix](capability-matrix.md) | Score Metrology through Axiology (1–5); any layer `< 3` triggers an automatic `NO-GO` |
| **4. Validate ROI** | `AG5` | Verify quantified business ROI and chargeback/showback attribution |
| **5. Record Decision** | `DS5` | Write scores, compensating controls, and executive sign-off to the governance ledger |

---

## 5. Continuous Post-Launch Compliance and Drift Monitoring

- **Business problem:** An AI system passes initial intake, but six months later its input data drifts, its escalation rate spikes, or its outcomes skew across demographic groups.
- **Capabilities composed:** `AG1` (Drift & KPI Monitor) + `AG4` (Workflow Telemetry) + `AG5` (Bias, Equity & Policy Monitor).

```
AG1 (Metrology)   → Monitors input distributions & post-launch KPIs vs. pre-launch baseline
AG4 (Praxeology)  → Monitors state transitions, loop rates, and human override frequency
AG5 (Axiology)    → Monitors policy-gate refusals and demographic equity thresholds
  ↓
Automated Governance Alert → Triggers workflow throttle, rollback, or mandatory re-review
```

---

## 6. Portable Multi-Model Orchestration via MCP

- **Business problem:** Swapping an underlying LLM (for example, moving from a cloud frontier model to a local open-weight model) without rewriting data integrations, RAG pipelines, or policy checks.
- **Capabilities composed:** `AG6` (MCP Capability Bus) wrapping `DS1`–`DS7` and `AG1`–`AG5`.

```
Model / Orchestrator Host (Cloud LLM, Local Open-Weight Model, State Machine)
  ↓  invokes capabilities exclusively via MCP contracts
AG6 — MCP Capability Bus
  ├── Metrology MCP Server     → DS1/DS2 ingestion, quality & provenance checks (AG1)
  ├── Ontology MCP Server      → DS3/DS6 entity resolution, graph & registry queries (AG2)
  ├── Epistemology MCP Server  → DS4 grounded retrieval & citation verification (AG3)
  ├── Praxeology MCP Server    → workflow state transitions & human approval queues (AG4)
  └── Axiology MCP Server      → DS7 policy evaluation & guardrail checks (AG5)
```

---

## Related Documents

- **[Enterprise Capability Catalog Overview](README.md)**
- **[Data Substrate Capabilities](data-substrate.md)** (`DS1`–`DS7`)
- **[Enterprise Agent Capabilities](agents.md)** (`AG1`–`AG6`)
- **[Enterprise Capability Matrix](capability-matrix.md)**
- **[Technical Specification](ARCHITECTURE.md)**
