# Scenario: AI Project Intake Scoring

**Agency context:** A government agency receives dozens of AI proposals annually from internal teams and vendors. Leadership needs a consistent, defensible way to evaluate these proposals — comparing them fairly, identifying governance gaps early, and building a historical record of investment decisions.

**The goal:** A MOEPA-governed intake workflow that scores every proposal against all five layers, produces a GO / CONDITIONAL GO / NO-GO recommendation, and maintains a durable governance record that leadership can reference in future budget reviews or oversight inquiries.

---

## The Problem This Solves

Without a consistent framework, AI proposal evaluation tends to be:
- **Inconsistent** — different reviewers apply different standards
- **Vendor-biased** — vendors control the presentation; leadership has no neutral reference
- **Undocumented** — decisions are made in meetings, not in records
- **Ungovernable** — approved projects drift from their original scope with no accountability trail

The MOEPA intake workflow turns proposal evaluation into a governed, auditable process.

---

## The Intake Workflow

```
Proposal Submitted
        ↓
[METROLOGY]   Data quality review — is the proposal complete and verifiable?
        ↓
[ONTOLOGY]    Entity resolution — what systems, data, and processes are involved?
        ↓
[EPISTEMOLOGY] Claim verification — are the vendor's factual claims accurate?
        ↓
[PRAXEOLOGY]  Scoring workflow — five-layer scoring with human review gates
        ↓
[AXIOLOGY]    Mission alignment check — does this proposal align to agency priorities?
        ↓
GO / CONDITIONAL GO / NO-GO + Documentation Record
```

---

## How MOEPA Layers Apply

### Layer 1 — Metrology: Validate the Proposal Submission

**What happens:**  
The intake system checks that the proposal submission is complete and meets minimum standards before scoring begins.

**Specific controls:**
- Required fields validated: project name, sponsoring office, proposed use case, estimated cost, data sources identified, compliance considerations noted
- Factual claims flagged for verification in Layer 3 (e.g., "our AI achieves 97% accuracy on similar tasks")
- Incomplete submissions returned to submitter with specific gaps identified — not silently scored as low

**Outcome:** Every proposal that enters scoring is complete by a defined standard. Incomplete proposals are not scored — they are returned. This prevents the common failure mode where a polished vendor deck gets scored despite missing critical information.

---

### Layer 2 — Ontology: Map to the Agency's Domain Model

**What happens:**  
The system resolves the entities in the proposal against the agency's canonical model of its systems, data assets, and business processes.

**Specific controls:**
- "Customer data" in the proposal is resolved to: which specific data systems, which data classifications (PII? FISMA-controlled?), what current governance status
- "Integration with case management system" is resolved to: which system (COTS or custom), what API capability, what security classification, what existing data flows
- Proposed use case is mapped to existing business process definitions in the agency's process inventory

**Outcome:** The scoring team works from a common understanding of what the proposal actually touches — not the vendor's framing of it. Dependencies and risks that the proposal glosses over become visible.

---

### Layer 3 — Epistemology: Verify the Proposal's Claims

**What happens:**  
Any factual claims in the proposal are checked against the agency's owned reference data before they influence the score.

**Claims verified in a sample proposal:**

| Claim in Proposal | Verification Result |
|---|---|
| "97% accuracy on income verification tasks" | Checked against agency's internal benchmark dataset — actual tested accuracy: 91.3% on agency data vs. 97% on vendor's test set (different distribution) |
| "Compliant with applicable federal safeguarding standards" | Agency CISO reviewed — vendor's proposed architecture does not meet FedRAMP Moderate requirements |
| "Similar deployment at Agency X reduced processing time by 40%" | Agency X contacted — actual reduction was 22%; 40% figure included implementation period efficiencies that did not persist |

**Outcome:** The scoring team knows which vendor claims are verified, which are overstated, and which cannot be confirmed. This is documented in the proposal record — not just shared verbally.

---

### Layer 4 — Praxeology: Execute the Scoring Workflow

**What happens:**  
The five-layer scoring workflow runs as a defined state machine with mandatory review gates.

**Workflow states:**
```
SUBMITTED → COMPLETENESS_CHECK → ENTITY_RESOLUTION → CLAIM_VERIFICATION 
         → LAYER_SCORING → HUMAN_REVIEW → RECOMMENDATION_ISSUED → ARCHIVED
```

**Layer scoring (using the 5-Layer Evaluation Checklist):**

| Layer | Score | Rationale |
|---|---|---|
| Metrology | 2 | Vendor's data platform holds all ingestion history; no export capability confirmed |
| Ontology | 3 | Vendor uses agency-provided entity IDs but schema is vendor-controlled |
| Epistemology | 3 | Source citations available but verification is through vendor API only |
| Praxeology | 4 | Workflow logic is documented; human review gates present and enforced |
| Axiology | 3 | Guardrails documented but enforced at application layer only |

**Overall score: 2 (lowest layer score = Metrology)**  
**Recommendation: NO-GO — Metrology score of 2 is an automatic NO-GO**

**Human review gate:** Before issuing the recommendation, the scoring team lead reviews the scores and evidence, confirms the Metrology assessment with the agency's data architect, and signs off.

**Outcome record:**
```
Proposal: INTAKE-2025-0147
Title: Automated income match scoring — VendorCo proposal
Recommendation: NO-GO
Determining factor: Metrology score 2/5
Rationale: Vendor's platform owns all data lineage and quality records.
           Agency cannot independently audit match history or reproduce
           quality results without vendor cooperation.
Required remediation: Vendor must demonstrate open-format data export
           with complete provenance records before re-evaluation.
Scored by: [Reviewer A, Reviewer B]
Approved by: [Program Director]
Date: 2025-04-03
Record ID: INTAKE-2025-0147-REC
```

---

### Layer 5 — Axiology: Mission and Compliance Alignment

**What happens:**  
Before issuing the recommendation, the proposal is checked against agency mission priorities and compliance requirements.

**Checks performed:**
- **Mission alignment:** Does this proposal advance the agency's stated AI strategic priorities? — PARTIAL (addresses efficiency goal but not equity goal)
- **Privacy Act compliance:** Does the proposed data use comply with the agency's Privacy Act system of records? — RISK FLAGGED (vendor data processing environment not covered by current SORN)
- **FISMA compliance:** Does the system meet the security baseline for the data it will process? — GAP (FedRAMP authorization not in place)
- **Equity review:** Has the vendor provided disaggregated accuracy metrics across demographic groups? — NOT PROVIDED

**Outcome:** Two compliance gaps flagged (Privacy Act SORN coverage, FedRAMP authorization) are added to the NO-GO documentation as required remediation items.

---

### Data Substrate: The Governance Record

The Data Substrate now holds:

| Record | Contents |
|---|---|
| Proposal record | Full submission, completeness validation results |
| Entity map | All systems, data assets, and processes identified |
| Claim verification | Each vendor claim with verification result and evidence |
| Scoring record | Layer-by-layer scores with evidence and rationale |
| Decision record | Recommendation, determining factor, human sign-off |
| Compliance record | Mission alignment assessment, compliance gap findings |

This record is retrievable in five years when the vendor re-submits a revised proposal — or when leadership wants to understand why a proposal was rejected.

---

## What Leadership Gets from This Process

**Consistent, comparable decisions:** Every proposal is scored on the same rubric by the same criteria.

**Vendor accountability:** Vendor claims are verified before they influence scores. Overstated metrics are documented.

**Auditable governance:** Every NO-GO, CONDITIONAL GO, and GO decision has a documented rationale that can be reviewed by oversight bodies.

**Institutional memory:** The proposal record persists. Future evaluations can reference what was previously scored and why.

**Remediation clarity:** NO-GO decisions come with specific remediation requirements — not vague "needs improvement" feedback.

---

## What Would Go Wrong Without This Process

| Failure Mode | Consequence |
|---|---|
| Vendor accuracy claims accepted unchallenged | Agency approves a system that performs significantly worse on agency data than vendor benchmarks suggest |
| Metrology ownership gap not caught | Agency discovers two years later that it cannot export its own data from the vendor's platform |
| No audit record | When an oversight inquiry asks why a proposal was approved, no documentation exists |
| Inconsistent scoring | One program scores vendors generously; another scores conservatively; cross-program comparisons are meaningless |

---

## Related Documents

- [5-Layer Evaluation Checklist](../docs/5-Layer-Evaluation-Checklist.md) — the scoring rubric used in this example
- [Owned vs. Rented AI Strategy](../docs/Owned-vs-Rented-AI-Strategy.md) — why Metrology ownership is the critical gate
