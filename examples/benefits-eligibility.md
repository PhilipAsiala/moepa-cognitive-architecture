# Scenario: Benefits Eligibility Determination

**Agency context:** A federal benefits-administering agency (e.g., Social Security Administration, Veterans Affairs, or a state Medicaid agency) uses AI to assess eligibility for benefits — income-tested, means-tested, or service-requirement-based programs.

**The goal:** AI-assisted eligibility determination that is fast and consistent, produces decisions that can be explained to applicants, supports the appeals process, and remains fully auditable for oversight and civil rights compliance.

---

## The Problem This Solves

Benefits eligibility determination is high-stakes: a wrong decision affects a citizen's income, healthcare, housing, or veterans' care. It is also high-volume: agencies process millions of applications annually.

The pressure to automate is real. But automation without governance creates new risks:
- Decisions that cannot be explained to the applicant
- Systematic errors affecting specific demographic groups that go undetected
- Appeals that cannot be supported because the decision trail is incomplete
- Legal liability when AI-assisted denials are challenged in court

The MOEPA Cognitive Architecture enables automation *with* accountability.

---

## Scenario: Income-Tested Benefits Eligibility

An applicant applies for a low-income benefits program. The eligibility rule requires that household income not exceed 200% of the federal poverty level (FPL) for the household size. The applicant reports household income of $38,000 for a family of four. The 200% FPL threshold for a family of four is $62,400.

---

## How MOEPA Layers Apply

### Layer 1 — Metrology: Validate Input Data Quality

**What happens:**  
The application triggers collection of available income evidence from authorized sources.

**Sources collected:**
- Federal wage records (prior year employer-reported data)
- State wage record system (quarterly employer-reported wages)
- Federal unearned income data (if shared under interagency data-sharing agreement)
- Prior-year benefits records (any existing income verification from prior enrollment)

**Quality validation:**
- Federal wage records for both adult household members found — quality status: VERIFIED
- State wage records for one adult — current quarter data available, prior quarters: VERIFIED
- No federal unearned income data (interagency data-sharing agreement not in place for this agency)
- Prior-year enrollment record — income verified at $36,800 (prior year) — status: HISTORICAL

**Provenance stamps issued:** Each data record enters the Data Substrate with source ID, collection date, quality results, and content hash.

**Outcome:** The system knows exactly what evidence it has and what it does not have — and marks the confidence assessment accordingly.

---

### Layer 2 — Ontology: Resolve the Household

**What happens:**  
The system resolves the household members and their relationships against the canonical entity model.

**Entity resolution results:**
- Adult 1: confirmed identity, linked to employment history and federal wage record
- Adult 2: confirmed identity, linked to employment history and state wage record
- Child 1 (age 7): confirmed as dependent — biological child per records
- Child 2 (age 4): confirmed as dependent — biological child per records
- No additional household members found in agency records

**Household composition:** 2 adults + 2 minor dependents = household of 4 ✓ (matches applicant's declaration)

**FPL threshold lookup:** 200% FPL for household of 4 (2025) = $62,400 — retrieved from agency's canonical policy reference, version 2025-01-01.

**Outcome:** The household model is resolved from the agency's own entity data — not from the vendor's interpretation of the application form.

---

### Layer 3 — Epistemology: Build the Income Verification and Confidence Score

**What happens:**  
The verification engine assembles and cross-checks all available income evidence.

**Income evidence summary:**

| Source | Adult 1 | Adult 2 | Notes |
|---|---|---|---|
| Federal wage report (prior year) | $24,800 | $12,400 | Prior year; may not reflect current |
| State wage records (Q3 current year, annualized) | $26,200 | $11,800 | Current; most recent quarter |
| Self-reported income | $24,000 | $14,000 | Application declaration |

**Verification analysis:**
- Adult 1: State wage record ($26,200 annualized) is most current; exceeds self-reported by $2,200
- Adult 2: State wage record ($11,800 annualized) is most current; below self-reported by $2,200
- Combined third-party verified income: $38,000 ($26,200 + $11,800)
- Self-reported combined income: $38,000
- **Match: ✓ CONFIRMED** — third-party and self-reported income align

**Confidence assessment:**
```
Household Income Verification
Applicant: Case 2025-H-44821
Total verified income: $38,000
FPL threshold: $62,400

Evidence strength:
  Adult 1: Current state wage record     CONFIRMED   ✓
  Adult 2: Current state wage record     CONFIRMED   ✓
  Self-reported income: MATCHES third-party verification ✓
  Unearned income: NOT AVAILABLE (no data sharing agreement)
                   — risk: potential unearned income not captured

Confidence: 91.4% (HIGH — human spot-check sample)
Note: Unearned income not verifiable from current data sources.
      Policy: applicant attestation accepted for unearned income
      below $500/month under regulation § 42.114(b).
Verification record: VER-2025-H-44821
```

**Outcome:** The confidence score is 91.4% — HIGH, but not at the automated acceptance threshold of 95%. This routes to the human spot-check sample per policy.

---

### Layer 4 — Praxeology: Route and Process

**What happens:**  
The workflow engine applies confidence-based routing.

**Routing decision:**
- Score 91.4% → Human spot-check sample (5% of cases in 90–94% band are reviewed)
- This case is selected for spot-check (by systematic sampling algorithm)

**Workflow state:**
```
APPLICATION_RECEIVED → DATA_COLLECTION → VERIFICATION_COMPLETE 
→ PENDING_SPOT_CHECK → [HUMAN_REVIEWED → APPROVED | ESCALATED]
```

**Human review outcome:**  
Eligibility specialist reviews the case. Confirms: third-party income matches self-reported. Notes the unearned income attestation falls under the regulatory de minimis provision. Approves.

**Approval record:**
```
Case: 2025-H-44821
State transition: PENDING_SPOT_CHECK → APPROVED
Reviewer: Eligibility Specialist ID 3847
Review action: Confirmed third-party income match; accepted unearned income
               attestation under § 42.114(b) de minimis provision
Timestamp: 2025-03-22T10:15:33Z
Workflow ID: WF-2025-H-44821
Policy version: 2025-01-01
```

**Outcome:** Decision reached with human review, full audit trail, and policy version recorded.

---

### Layer 5 — Axiology: Policy, Rights, and Equity

**What happens:**  
Before closing the case, the axiology layer performs final compliance checks.

**Checks:**
- **Due process:** Applicant notified of decision and right to appeal — ✓ Notice generated
- **Privacy compliance:** Decision letter contains only permitted disclosures — ✓ PII controls confirmed
- **Non-discrimination:** Income threshold applied uniformly across household types — ✓ Same rule, same threshold
- **Equity flag check:** Is this applicant's demographic group subject to any current equity monitoring alert? — No active alert
- **Policy version traceability:** Decision cites policy version 2025-01-01 — ✓ Recorded

**Outcome:** Case closes with full compliance record attached.

---

### Data Substrate: The Complete Decision Record

| Record | Contents |
|---|---|
| Income evidence records | 4 third-party records with provenance; quality results |
| Household entity records | 4 household members, their relationships, resolution sources |
| Verification record | Income comparison, evidence summary, confidence score |
| Spot-check workflow | Routing rationale, reviewer ID, approval, timestamp |
| Compliance record | Due process, privacy, equity, policy version |

---

## Supporting an Appeal

If the applicant later appeals, or if an oversight body requests documentation, the agency can produce:

1. **The exact data used** — with sources, collection dates, quality status
2. **The household determination** — how members were confirmed and what records were used
3. **The income verification** — which sources confirmed what amount, confidence score rationale
4. **The human review record** — who reviewed, what they saw, what they decided and why
5. **The policy version in effect** — which regulatory provisions governed the decision
6. **The equity monitoring status** — whether any demographic alert was active

This record is complete, owned, and independent of any vendor system.

---

## What Would Go Wrong Without MOEPA

| Layer | Failure Mode | Consequence for Applicant |
|---|---|---|
| Metrology | Data collected by vendor; agency cannot audit sources | Cannot verify whether correct data was used in appeal |
| Ontology | Household composition determined by vendor's model | Household count error not detectable or correctable |
| Epistemology | Confidence score from vendor algorithm | Cannot explain to applicant why 91% → cannot support appeal |
| Praxeology | Workflow logic in vendor system; audit log incomplete | Cannot show what human reviewed or when |
| Axiology | Rights notification managed by vendor | Cannot confirm due process obligations were met |

Result: A denied applicant who appeals hears "the system said you qualify/don't qualify" — with no explanation that a lawyer, judge, or oversight body can evaluate.

---

## Key Governance Principle This Demonstrates

Government agencies administering benefits programs are subject to the Due Process Clause, equal protection requirements, and program-specific regulations. Those legal obligations require that decisions be **explainable, documented, and reproducible**.

An AI system that cannot produce a complete, owned decision record is not just a governance risk — it is a legal liability.

---

## Related Documents

- [Income Verification Scenario](income-verification.md) — related pattern for income-based determinations
- [5-Layer Evaluation Checklist](../docs/5-Layer-Evaluation-Checklist.md) — how this use case would be scored before deployment
- [MOEPA Cognitive Architecture for Leaders](../docs/MOEPA-5-Layer-Framework.md) — due process and value constraints for this scenario
