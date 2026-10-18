# 5-Layer AI Evaluation Checklist

> For program managers and governance reviewers scoring a proposal before funding, procurement, or scale-up. Completing it changes the decision from a feature review to **GO**, **CONDITIONAL GO**, or **NO-GO**, with the gaps named.

A proposal that cannot be mapped to all five layers does not pass intake. A proposal must score at least 3 on every layer for conditional approval, and at least 4 on every layer for full approval.

On first use: **Metrology** is measurement and telemetry; **Ontology** is shared definitions; **Epistemology** is verification; **Praxeology** is action and human checkpoints; **Axiology** is value and priority constraints. Score predictive outputs (risk scores, forecasts, match confidence) and generative outputs (summaries, explanations, recommendations) against the same layers. A score still needs a source. A written recommendation on a consequential case still needs a human checkpoint.

---

## How to Use This Checklist

1. **For each of the five layers**, review the scoring criteria and assign a score of 1–5
2. **Record evidence** for each score — a score without supporting evidence is not auditable
3. **Calculate the overall recommendation** using the decision band rules below
4. **Document gaps** at any layer scoring 1–3 and define required remediation
5. **Present to governance reviewers** before any funding or deployment decision

---

## Decision Bands

| Overall Score | Recommendation | Condition |
|---|---|---|
| Any layer scores 1–2 | **NO-GO** | Automatic rejection — remediation required before re-evaluation |
| All layers ≥ 3, at least one layer = 3 | **CONDITIONAL GO** | Approved only if named remediation controls are active and documented |
| All layers ≥ 4 | **GO** | Approved for funding and deployment |

> **Important:** The lowest-scoring layer determines the overall recommendation. A proposal scoring 5-5-5-5-2 is an automatic NO-GO, not an average.

---

## Layer 1 — Metrology: Data Foundation

**Core question:** Do we control and trust the data this system uses?

| Score | Description | Indicators |
|---|---|---|
| **1** | No data quality controls; complete vendor dependency | No data quality measurement; vendor owns all data and lineage; agency cannot export or audit source data |
| **2** | Partial controls; significant gaps | Some quality checks exist but are ad hoc; lineage is incomplete; data cannot be reproduced without vendor cooperation |
| **3** | Defined controls; minimum acceptable standard | Basic internal quality rules; lineage tracked at ingestion; data is exportable in standard formats |
| **4** | Strong controls; measurable quality | Automated quality monitoring; full provenance records; open-format storage; regular quality audits |
| **5** | Comprehensive sovereignty; gold standard | Self-hosted open-format lakehouse; cryptographic provenance; real-time quality observability; zero vendor dependency on data foundation |

**Evaluation questions:**
- [ ] Where does the raw data live, and who controls it?
- [ ] Can the agency export a complete, usable copy of all input data at any time?
- [ ] Is there a documented lineage trail from source to model input?
- [ ] What happens to data access if this vendor's contract ends?
- [ ] Are data quality standards defined by the agency or the vendor?

**Score: _____ / 5**
**Evidence / Notes:**
> *(Record what evidence was reviewed and why the score was assigned)*

---

## Layer 2 — Ontology: Structured Knowledge and Meaning

**Core question:** Do we own the definitions and relationships this system relies on?

| Score | Description | Indicators |
|---|---|---|
| **1** | No domain model; raw model weights only | System uses generic pre-trained understanding; no agency-defined entity model; definitions inconsistent across systems |
| **2** | Basic schemas exist but agency does not own them | Standardized external schemas used; no internal knowledge graph; vendor controls entity definitions |
| **3** | Agency-defined schemas; basic structured knowledge | Internal data dictionaries or schemas exist; core entities are defined; basic consistency across systems |
| **4** | Governed knowledge model; version-controlled | Agency-maintained knowledge graph or entity model; versioned definitions; relationships documented and consistent |
| **5** | Live, sovereign semantic model; full ownership | Internally managed knowledge graph evolving with policy; all entity relationships owned and auditable; AST-level domain understanding |

**Evaluation questions:**
- [ ] Who defines the meaning of core domain terms (e.g., "applicant," "income," "household unit")?
- [ ] Are there documented relationships between entities that the system uses?
- [ ] If the vendor changed their entity model, how would it affect the agency's operations?
- [ ] Can the agency reproduce its domain knowledge model independently of the vendor?
- [ ] Are schema changes version-controlled and auditable?

**Score: _____ / 5**
**Evidence / Notes:**
> *(Record what evidence was reviewed and why the score was assigned)*

---

## Layer 3 — Epistemology: Truth, Verification, and Accountability

**Core question:** Can we verify outputs and trace recommendations to evidence?

| Score | Description | Indicators |
|---|---|---|
| **1** | No verification; outputs used directly | Model outputs accepted without any checking; no source citations; no distinction between facts and inferences |
| **2** | Basic checks; significant gaps | Some validation exists but is inconsistent; limited source citation; verification depends on vendor-provided confidence scores |
| **3** | Defined verification; source citations present | RAG with source citations; basic fact-checking against owned data; confidence levels reported |
| **4** | Strong verification; auditable chains | Automated verification gates; every output traces to specific records; confidence levels tied to evidence; audit logs exist |
| **5** | Cryptographic verification; full chain of custody | SHA-256 or equivalent validation; every fact verified against sovereign data; complete audit trail; hallucination detection active |

**Evaluation questions:**
- [ ] When the system produces a recommendation, what evidence supports it?
- [ ] Can the agency independently verify a system output without relying on the vendor?
- [ ] Is there a distinction between a verified fact and a model prediction?
- [ ] What happens when the system is wrong — how would the error be detected and traced?
- [ ] Can the agency produce a chain of evidence for any decision to a Congressional inquiry?

**Score: _____ / 5**
**Evidence / Notes:**
> *(Record what evidence was reviewed and why the score was assigned)*

---

## Layer 4 — Praxeology: Decision Workflows and Human Oversight

**Core question:** Do we control how the system acts and who approves consequential decisions?

| Score | Description | Indicators |
|---|---|---|
| **1** | No workflow governance; autonomous action | System can take consequential actions without approval; no state machine; audit logs absent or incomplete |
| **2** | Basic controls; bypassable checkpoints | Approval steps exist but can be skipped; workflow logic not inspectable; incomplete audit trails |
| **3** | Defined workflows; human oversight required | Documented approval workflows; human-in-the-loop checkpoints enforced; basic audit logging |
| **4** | Governed workflows; immutable logs | Workflow logic documented and auditable; human override always available; audit logs tamper-evident |
| **5** | Deterministic state machine; cryptographic audit trail | Immutable workflow state machine; every action logged with approver and timestamp; no action possible outside defined scope |

**Evaluation questions:**
- [ ] What is the most consequential action this system can take, and what approval is required?
- [ ] Can the system take actions outside its defined workflow without being detected?
- [ ] Is there an immutable audit log of every action and its approver?
- [ ] Who can override the system at any point, and how?
- [ ] Is the workflow logic inspectable by the agency's own team?

**Score: _____ / 5**
**Evidence / Notes:**
> *(Record what evidence was reviewed and why the score was assigned)*

---

## Layer 5 — Axiology: Values, Ethics, and Mission Alignment

**Core question:** Does this system enforce agency values and compliance requirements — and can we prove it?

| Score | Description | Indicators |
|---|---|---|
| **1** | Soft guidelines only; easily bypassed | Values embedded in prompts only; no infrastructure-level enforcement; no testing of guardrail effectiveness |
| **2** | Partial enforcement; significant gaps | Some hard rules exist but many constraints are soft; compliance coverage incomplete; no regular testing |
| **3** | Defined guardrails; documented constraints | Key prohibited actions blocked at application level; compliance requirements documented; basic testing |
| **4** | Strong enforcement; regularly tested | Guardrails enforced at infrastructure level for high-risk actions; regular compliance testing; version-controlled policy config |
| **5** | Immutable enforcement; cryptographically proven | OS/infrastructure-level policy locks; constitutional guardrails survive prompt injection; automated compliance verification; zero soft constraints for statutory requirements |

**Evaluation questions:**
- [ ] What are the most important things this system must never do? How are those prevented?
- [ ] Can a sophisticated user or developer circumvent the system's guardrails?
- [ ] How is the system tested to verify that compliance constraints are working?
- [ ] Are the values and constraints defined by the agency or by the vendor?
- [ ] When policy changes (new regulation, court ruling), how quickly can the system be updated?

**Score: _____ / 5**
**Evidence / Notes:**
> *(Record what evidence was reviewed and why the score was assigned)*

---

## Scoring Summary

| Layer | Score (1–5) | GO / Conditional / NO-GO |
|---|---|---|
| Layer 1 — Metrology | | |
| Layer 2 — Ontology | | |
| Layer 3 — Epistemology | | |
| Layer 4 — Praxeology | | |
| Layer 5 — Axiology | | |
| **Overall (lowest layer score)** | | |

**Overall Recommendation:** ☐ GO  ☐ CONDITIONAL GO  ☐ NO-GO

---

## Remediation Requirements

*For any layer scoring 1–3, document the specific gap and required remediation:*

| Layer | Gap Description | Required Control | Owner | Target Date |
|---|---|---|---|---|
| | | | | |
| | | | | |
| | | | | |

---

## Conditional GO Requirements

*If the overall recommendation is CONDITIONAL GO, the following controls must be active before deployment:*

| Condition | Verification Method | Status |
|---|---|---|
| | | |
| | | |

---

## Review and Approval

| Role | Name | Date | Signature |
|---|---|---|---|
| Evaluator | | | |
| Technical Lead | | | |
| Program Manager | | | |
| Governance Reviewer | | | |

---

## Notes for Evaluators

**On scoring 3 vs. 4:** A score of 3 means the minimum standard is met — the proposal can proceed conditionally. A score of 4 means good governance practice is in place. The goal is to move every layer toward 4 or 5 over time. A comfortable 3 that never improves is a governance risk that accumulates quietly.

**On vendor-provided evidence:** When a vendor provides documentation as evidence for a score, independently verify at least one key claim before accepting it. Common patterns: vendors describe security and governance features in sales materials that are not actually enabled in the proposed configuration.

**On scoring consistency:** Use the same rubric across all proposals reviewed in a given cycle. Inconsistent scoring undermines the usefulness of the framework as a comparative tool.

**On the "any layer" rule:** The lowest layer sets the overall score deliberately. A system with excellent values governance (Layer 5 = 5) but uncontrolled data (Layer 1 = 2) is not a 3.5 — it is a NO-GO. The layers are interdependent. Weakness in one undermines all.

---

## Supplement: Technical Review Gate (For Architects)

*Leaders score business outcomes using the layer sections above. Architecture reviewers apply this supplement before unconditional GO on implementations.*

In addition to per-layer scores, technical reviewers verify the proposal satisfies the
[Architectural Governance and Evolution Guidelines](MOEPA-Architectural-Governance-and-Evolution-Guidelines.md).

| Gate | Pass criteria | Score impact if failed |
|---|---|---|
| **Governed capability access** | Data, retrieval, workflow, and policy capabilities are inspectable and governable — not hidden in vendor glue code | Cap Praxeology and Epistemology at 3; CONDITIONAL GO minimum |
| **Semantic ingestion** | Document ingress preserves structure and provenance — not naive text splitting | Cap Metrology at 3; CONDITIONAL GO minimum |
| **Citation behavior** | Generated outputs return exact citations to owned substrate records | Cap Epistemology at 3; CONDITIONAL GO minimum |
| **Five-layer impact documentation** | Proposal documents Metrology through Axiology impact and any exceptions with compensating controls | Cannot achieve unconditional GO without documentation |

---

## Related Documents

- [MOEPA Cognitive Architecture for Leaders](MOEPA-5-Layer-Framework.md) — detailed per-layer leadership questions
- [Architectural Governance Guidelines](MOEPA-Architectural-Governance-and-Evolution-Guidelines.md) — technical supplement for architects
- [Owned vs. Rented Strategy](Owned-vs-Rented-AI-Strategy.md) — ownership decision framework
- [Architecture Specification](../catalog/ARCHITECTURE.md) — technical specification of scoring criteria
