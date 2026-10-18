# Axiology Capabilities

## What Leaders Need to Know

Bottom line: this layer keeps AI aligned to law, policy, ethics, privacy, and organizational mission. It determines whether an initiative deserves stakeholder trust and executive approval.

See [ARCHITECTURE.md](../ARCHITECTURE.md) for the strategic rationale and [Business Value](../../docs/business-value.md) for the investment lens.

## Mission and Governance Outcomes

- Stronger compliance and public-trust posture.
- Clear alignment between AI investments and institutional values.
- Better visibility into fairness, privacy, and accountability obligations.
- Reduced risk that policy becomes advisory rather than enforceable.

## What Axiology Covers

| Capability Domain | Description |
|---|---|
| **Policy enforcement** | Translating laws, regulations, and agency policy into technical constraints |
| **Guardrail implementation** | Hard limits on what the system can and cannot do |
| **Constitutional AI design** | Principles that the system must never violate regardless of instructions |
| **Compliance monitoring** | Continuously verifying that the system operates within defined boundaries |
| **Value alignment testing** | Regularly testing that guardrails work as intended |
| **Mission priority governance** | Ensuring AI optimization objectives align to agency mission |

## Core Capabilities

### A1 — Policy-as-Code Enforcement
**What it does:** Translates agency policy, legal requirements, and compliance mandates into explicit, machine-enforceable rules — not just documentation or prompt instructions.

**Why it matters for government:** A prompt instruction like "do not share PII" can be bypassed by a sophisticated user or an edge-case input. A policy-as-code rule that blocks PII from being included in any outbound response cannot. The difference between soft and hard enforcement is the difference between a policy that applies in all cases and one that applies in most.

**Minimum acceptable standard (Score 3):** Key compliance requirements encoded as enforceable rules; violations blocked.

**Good practice (Score 4–5):** All statutory and regulatory constraints encoded as versioned, auditable policy code; enforcement at infrastructure level (not application logic); policy changes go through formal review.

---

### A2 — Constitutional Guardrails (Inviolable Constraints)
**What it does:** Defines a set of constraints that the system must never violate regardless of instructions, context, or prompt engineering — and enforces those constraints at a layer the system itself cannot override.

**Why it matters for government:** Constitutional guardrails are the equivalent of statutory limits that no employee, manager, or executive can waive. For AI systems, this means constraints like: never disclose PII without authorization, never process data outside the authorized environment, never take an action that waives a citizen's legal rights.

**Minimum acceptable standard (Score 3):** Inviolable constraints documented; enforced at application level.

**Good practice (Score 4–5):** Inviolable constraints enforced at OS/infrastructure level; enforcement tested regularly with adversarial inputs; constraints version-controlled and change-managed; enforcement logs available for audit.

---

### A3 — Prompt Injection Defense
**What it does:** Detects and blocks attempts by users or external data sources to use carefully crafted inputs to override the system's instructions or bypass its constraints.

**Why it matters for government:** Prompt injection is the leading attack vector against AI systems. An attacker who can inject instructions into a document the AI reads, or into data the AI retrieves, may be able to cause the AI to take unauthorized actions or disclose protected information.

**Minimum acceptable standard (Score 3):** Basic input sanitization; known injection patterns blocked; suspicious inputs flagged.

**Good practice (Score 4–5):** Multi-layer injection defense (input sanitization, context separation, output validation); injection attempts logged and alerted; regular red-team testing; context integrity verified before execution.

---

### A4 — Mission Alignment Configuration
**What it does:** Maintains a versioned, approved configuration of the AI system's objectives, priorities, and optimization targets — aligned to agency mission and reviewed regularly.

**Why it matters for government:** AI systems optimize for their defined objectives. If those objectives are set by a vendor ("maximize engagement," "minimize latency"), they may not align to agency mission ("maximize accuracy and equity," "minimize processing errors for vulnerable populations"). Mission alignment configuration makes the optimization target explicit and owned.

**Minimum acceptable standard (Score 3):** System objectives documented and approved; reviewed periodically.

**Good practice (Score 4–5):** Mission alignment formally encoded in system configuration; objectives reviewed against mission and statutory requirements on a defined schedule; changes require leadership approval; alignment testing included in deployment validation.

---

### A5 — Bias and Equity Monitoring
**What it does:** Monitors AI outputs for systematic disparities across demographic, geographic, or population groups — and triggers review when disparities exceed defined thresholds.

**Why it matters for government:** Government agencies are subject to equal protection and anti-discrimination requirements. An AI system that systematically produces different outcomes for different demographic groups — even unintentionally — creates legal and mission risk. Monitoring is the only way to detect this before it causes harm at scale.

**Minimum acceptable standard (Score 3):** Periodic bias audits for high-stakes decision workflows; results reviewed.

**Good practice (Score 4–5):** Continuous equity monitoring across defined demographic dimensions; automated alerting when disparities exceed thresholds; monitoring results publicly reportable; remediation process defined.

---

### A6 — Value Alignment Testing
**What it does:** Regularly tests the system with boundary cases, adversarial inputs, and edge conditions designed to reveal whether guardrails are working as intended.

**Why it matters for government:** Guardrails that have never been tested are wishful thinking. Regular red-team testing — including tests designed by people trying to break the system — is the only way to validate that constraints hold under real-world pressure.

**Minimum acceptable standard (Score 3):** Periodic testing of key guardrails; results documented and reviewed.

**Good practice (Score 4–5):** Scheduled red-team testing; adversarial test suite version-controlled alongside system; test results reviewed by governance board; failures trigger formal remediation.

---

### A7 — Weighted Business ROI Quantification
**What it does:** Requires every proposal to document and quantify expected business and mission ROI (e.g., cost avoidance, risk reduction, throughput gains, equity or compliance improvements) with traceable assumptions, baselines, and sensitivity analysis. ROI becomes a primary weighted input to the Axiology score in high-volume intake environments.

**Why it matters for government:** In enterprise-scale intake (1,000+ requests), decisions must be driven by objective business value rather than technical feasibility or development capacity alone. Without quantified ROI, leadership cannot rationally prioritize or defend investments to oversight bodies.

**Minimum acceptable standard (Score 3):** High-level ROI narrative or qualitative benefits statement is provided.

**Good practice (Score 4–5):** Detailed, auditable ROI model with quantified benefits, cost assumptions, risk adjustments, and linkage to mission outcomes; model is reviewed and accepted by business owners and finance.

---

### A8 — Chargeback and Showback Modeling
**What it does:** Defines and documents how the full costs of the AI system — including platform compute, data storage, governance overhead, maintenance, and support — will be attributed to business owners through showback reports (visibility) or formal chargeback mechanisms (actual billing).

**Why it matters for government:** Sustainable platforms require clear accountability for consumption and cost. Absent a chargeback or showback model, demand is unbounded and true total cost of ownership remains hidden from decision-makers.

**Minimum acceptable standard (Score 3):** High-level cost attribution approach is described.

**Good practice (Score 4–5):** Formal, approved chargeback/showback model in place with defined rates or allocation rules, integration with enterprise financial systems, and acceptance by the accountable business owner prior to scaling.

---

## Capability Matrix

The matrix below binds the minimum set of Axiology capabilities to **Score 3 — Defined & Contained — Minimum Acceptable Standard** in the existing [Axiology scoring guide](scoring.md). Capabilities that contribute to Scores 4 and 5 lift the layer beyond that baseline. Live delivery status should be tracked through the [Praxeology workflow](../praxeology/tools.md); the JIRA epic column below is illustrative only.

| Capability | Minimum set? (Score 3) | Maturity contribution (3 / 4 / 5) | Owner | Delivery tracking (illustrative: JIRA epic) |
| --- | --- | --- | --- | --- |
| Bias and fairness monitoring for model and workflow outcomes | No | 4 — makes governance measurable and reviewable over time | Responsible AI owner | Illustrative: JIRA epic for fairness monitoring |
| Policy and rule enforcement aligned to regulatory and compliance requirements | Yes | 3 — defines enforceable control boundaries at the minimum acceptable standard | Policy owner | Illustrative: JIRA epic for policy and rule enforcement |
| Ethical alignment scoring and strategic objective alignment | Yes | 3 — ties initiatives to explicit mission and value criteria | Governance board owner | Illustrative: JIRA epic for ethical and strategic alignment |
| Privacy controls for customer and sensitive enterprise data | Yes | 3 — provides mandatory data protection and compliance boundaries | Privacy owner | Illustrative: JIRA epic for privacy controls |
| Transparency and explainability requirements for accountable decisions | Yes | 3 / 4 — supports accountable decisions at the baseline and stronger oversight at higher maturity | Accountability owner | Illustrative: JIRA epic for transparency and explainability |
| Compliance frameworks and value-based prioritization criteria | No | 5 — institutionalizes durable review and portfolio governance | Compliance portfolio owner | Illustrative: JIRA epic for compliance framework and prioritization |
| Weighted Business ROI quantification and sensitivity analysis | No | 4 — enables objective, value-driven prioritization at enterprise scale (1,000+ requests) | Business owner + Finance | Illustrative: JIRA epic for ROI modeling and validation |
| Chargeback and showback cost attribution modeling | No | 4 — ensures sustainable platform economics and clear accountability for consumption | Platform owner + Business owner | Illustrative: JIRA epic for chargeback model definition and approval |

## Questions Leaders Should Ask Before Funding

- Are policy, privacy, and fairness controls mandatory rather than optional?
- How will leadership know if those controls drift or are bypassed?
- Can the organization produce evidence for auditors, regulators, or public oversight bodies?
- How does this proposal advance mission outcomes without weakening stakeholder trust?

## Related

See also the layer overview in [Axiology README](README.md), [scoring guide](scoring.md), [tools](tools.md), and [patterns](patterns.md). Cross-layer interactions are described in [cross-layer-compositions.md](../cross-layer-compositions.md).
