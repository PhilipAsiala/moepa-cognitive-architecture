# Scenario: Third-Party Income Verification with 98% Confidence

**Agency context:** A federal agency administering income-based benefits or compliance programs uses AI to verify whether a constituent's self-reported income matches income reported by third parties — employers, banks, and other authorized reporters.

**The goal:** Process high volumes of cases automatically, flag discrepancies for human review, and produce an auditable confidence score that can be explained to the constituent and to oversight bodies.

---

## The Problem This Solves

Traditional income verification is largely manual: caseworkers compare self-reported data to third-party information documents by hand. This is slow, inconsistent, and does not scale.

AI-assisted verification could process millions of cases automatically — but only if the agency can:
1. Trust the data the system is using (its data, not a vendor's)
2. Explain *why* a confidence score is what it is
3. Guarantee that errors are caught before they affect citizens
4. Produce a complete audit trail for any challenged case

Without the MOEPA Cognitive Architecture, agencies often end up with a vendor-provided "match score" that nobody can explain.

---

## How MOEPA Layers Apply

### Layer 1 — Metrology: Validate the Income Data

**What happens:**  
Third-party information returns (employer wage reports, federal income reporting systems, bank interest statements) are ingested through the agency's quality gate.

**Specific controls:**
- Each record is validated: employer identifier present and format-valid, income amounts within expected range, program year matches reporting period, source reporter ID on authorized list
- Records failing validation are quarantined and flagged — they do not enter matching
- Each accepted record receives a provenance stamp: source system, collection date, validation results, and a content hash

**Outcome:** The agency can say "the third-party income data used in this match came from these specific sources, was validated on these dates, and has not been modified."

---

### Layer 2 — Ontology: Resolve Entities

**What happens:**  
The system resolves the constituent and employer entities in the case against the canonical entity registry.

**Specific controls:**
- The constituent identifier links to the canonical applicant entity in the knowledge graph, including all known associated IDs, case history, and prior-year verified income
- Each employer identifier links to the canonical employer entity, including all associated wage reports for this program year
- The knowledge graph query surfaces: "applicant X is associated with employer Y, who reported wages of $Z on date D for program year T"

**Outcome:** The system is working from the agency's own structured model of reality — not a vendor's interpretation of it.

---

### Layer 3 — Epistemology: Build the Confidence Score

**What happens:**  
The verification engine compares the constituent's reported income to the third-party evidence.

**Specific controls:**
- Four independent sources are retrieved for this applicant: employer wage report, third-party income report, bank interest statement, and prior-year case record
- Each source is weighted by source reliability and data freshness
- The system produces: a confidence score of 98.3%, a breakdown of that score by source, and a flag for one source showing a $400 discrepancy in the bank interest amount

**Confidence score output:**
```
Income Verification: Applicant ID ending 4471
Reported income: $87,400

Evidence summary:
  Employer wage report (filed 2025-01-31):     $85,000   ✓ CONFIRMED
  Third-party income report (filed 2025-02-15): $2,400  ✓ CONFIRMED
  Bank interest (direct data exchange):        $396      ✓ CONFIRMED (↕$4 from reported $400)
  Prior-year case comparison:                  CONSISTENT

Overall confidence: 98.3%
Note: $4 discrepancy in bank interest (within rounding threshold — auto-resolve)
Verification record: VER-2025-447183
```

**Outcome:** The confidence score is not a black box. It is a traceable calculation grounded in four specific, owned evidence sources with record IDs.

---

### Layer 4 — Praxeology: Route to the Right Workflow

**What happens:**  
The workflow engine receives the 98.3% confidence score and applies routing logic.

**Routing decision:**
- Score ≥ 95% AND no unresolved discrepancies → automated acceptance, logged
- Score 80–94% OR minor discrepancies within threshold → human spot-check sample
- Score < 80% OR discrepancy exceeds threshold → examiner review required

**For this case:** 98.3% score with a $4 discrepancy within the auto-resolve threshold → automated acceptance.

**Audit log entry:**
```
Workflow: INCOME_VERIFICATION
Case: CASE2025-447183
State transition: VERIFICATION_COMPLETE → ACCEPTED_AUTO
Confidence: 98.3%
Discrepancy: $4.00 (bank interest rounding — within auto-resolve threshold per policy v2.4)
Timestamp: 2025-03-15T14:32:07Z
Policy version: v2.4 (effective 2025-01-01)
Workflow ID: WF-2025-447183
```

**Outcome:** The case is processed automatically. The workflow state machine ensures no case can skip the confidence check or reach acceptance without passing through the verification gate.

---

### Layer 5 — Axiology: Policy and Compliance Guardrails

**What happens:**  
Before the case is closed, the axiology layer performs a final policy check.

**Specific checks:**
- Privacy Act: does the verification result contain any PII that must be masked in the audit log? ✓ Compliant — masked per policy
- Appeals rights: has the constituent been notified of their right to challenge? ✓ Compliant — notice scheduled
- Equitable treatment: does this constituent's confidence threshold align with the same standard applied to all applicants? ✓ Policy v2.4 applied uniformly
- Data retention: is this case subject to any retention hold? ✓ No hold — standard 7-year retention applied

**Outcome:** The case closes with a confirmed policy compliance record attached.

---

### Data Substrate: The Complete Record

The Data Substrate now holds an immutable record of this verification:

| Record Type | Contents |
|---|---|
| Metrology records | 4 third-party documents with provenance stamps and quality results |
| Ontology records | Applicant and employer entity linkages for this case |
| Epistemology records | Verification result, confidence score, source citations, discrepancy note |
| Praxeology records | Workflow log, state transition history, routing rationale, policy version |
| Axiology records | Policy compliance check results, retention classification |

---

## What the Leader Can Say to an Oversight Body

> "This constituent's income was verified at 98.3% confidence based on four independent third-party sources — an employer wage report, a third-party income report, a bank interest statement, and prior-year case history. A $4 rounding discrepancy in the bank interest figure was within our auto-resolve policy threshold. The case was processed under workflow policy version 2.4, effective January 1, 2025, and the complete evidence record is available as verification record VER-2025-447183."

This is only possible because the agency owns the data, the entity model, the verification logic, the workflow, and the compliance policy — none of it is inside a vendor's black box.

---

## What Would Go Wrong with a Rented Approach

With a typical vendor-provided income verification platform:

| MOEPA Layer | Rented Architecture Failure |
|---|---|
| Metrology | Third-party data ingested and validated by vendor — agency cannot reproduce quality results |
| Ontology | Applicant-employer matching done by vendor's entity model — agency cannot inspect match logic |
| Epistemology | Confidence score produced by vendor's algorithm — agency cannot decompose or explain it |
| Praxeology | Routing decisions made by vendor's workflow engine — no agency-owned audit log |
| Axiology | Policy compliance certified by vendor — agency cannot independently verify |

Result: When a constituent challenges the decision, or oversight demands documentation, the agency's honest answer is "the vendor's system said 98%" — with no way to independently verify or explain that score.

---

## Related Documents

- [MOEPA Cognitive Architecture for Leaders](../docs/MOEPA-5-Layer-Framework.md) — verification and workflow questions for this scenario
- [5-Layer Evaluation Checklist](../docs/5-Layer-Evaluation-Checklist.md) — how this scenario would score
