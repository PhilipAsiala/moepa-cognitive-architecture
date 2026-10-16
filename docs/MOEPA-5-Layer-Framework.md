# The MOEPA 5-Layer Framework for Leaders

> For leaders who must approve, pause, or reject an AI proposal, and for the engineers who implement that decision. Each layer is one question to answer with evidence before funding. This document defines the **MOEPA 5-Layer Framework**. See the [Glossary](glossary.md) and [Pitch Strategy](pitch-strategy.md).

---

## Why Five Layers?

When an organization adopts an AI system, decisions about data, meaning, facts, workflows, and values are made somewhere — inside a vendor platform, by a technical team, or by default. MOEPA makes those decisions visible and assigns them to leadership. The examples below use public-sector stakes because the audit demand is high. The same questions apply to any regulated or high-impact business process.

Each layer is one domain of control. A weak layer limits what the others can defend. The operational effect of scoring all five is a single intake decision: proceed, proceed with named controls, or stop.

The layers are numbered from foundation to governance:

```
┌─────────────────────────────────────────────────────┐
│  LAYER 5 — AXIOLOGY       Values & Mission Alignment │
├─────────────────────────────────────────────────────┤
│  LAYER 4 — PRAXEOLOGY     Decision Workflows         │
├─────────────────────────────────────────────────────┤
│  LAYER 3 — EPISTEMOLOGY   Truth & Verification       │
├─────────────────────────────────────────────────────┤
│  LAYER 2 — ONTOLOGY       Structured Knowledge       │
├─────────────────────────────────────────────────────┤
│  LAYER 1 — METROLOGY      Data Quality & Measurement │
╠═════════════════════════════════════════════════════╣
│  DATA SUBSTRATE           Shared Knowledge Library   │
│                           (foundation — not scored)  │
└─────────────────────────────────────────────────────┘
```

---

## Layer 1 — Metrology: The Data Foundation

**Plain English:** Metrology is the science of measurement. In AI terms, it is about whether the data your system uses is accurate, traceable, and controlled by your organization.

**Why it matters to government leaders:** AI systems are only as trustworthy as the data they are trained on or retrieve from. If your data is incomplete, stale, or locked inside a vendor's platform, every decision the system makes is built on an uncertain foundation. For tax compliance, benefits eligibility, or fraud detection, this is not an acceptable risk.

**What good looks like:**
- Your agency owns and controls the raw data and can audit its source at any time
- Data quality is measured and monitored with defined standards
- Every data record carries a provenance trail — where it came from, when it was collected, who validated it
- Data is stored in open, portable formats (not proprietary vendor formats)

**What poor looks like:**
- Data quality rules are defined and enforced by a vendor platform
- You cannot export or migrate your data without vendor assistance
- There is no clear record of how input data was collected or transformed
- Different systems use the same term (e.g., "income") to mean different things

> **Leader question for Layer 1:**
> *"If this vendor's contract ended tomorrow, could we fully reproduce the data foundation this system relies on — and prove its quality to an auditor?"*

---

## Layer 2 — Ontology: Structured Knowledge and Meaning

**Plain English:** Ontology is the study of what exists and how things relate to each other. In AI terms, it is about whether your organization owns the definitions, entities, and relationships that the system uses to understand your domain.

**Why it matters to government leaders:** When an AI system understands the concept of "applicant," "employer," "income source," or "dependent," it is working from a model of those relationships. If that model lives inside a vendor's platform, your agency's understanding of its own domain is being rented. Changing vendors means rebuilding meaning from scratch.

**What good looks like:**
- Your agency maintains a governed knowledge graph or entity model for core domain concepts
- Terms like "applicant," "beneficiary," and "third-party reporter" have explicit, version-controlled definitions
- Relationships between entities (e.g., employer → employee → wage report) are explicitly modeled and owned
- The semantic model evolves with policy changes, not just vendor updates

**What poor looks like:**
- Entity definitions are embedded in a vendor's proprietary system and not exportable
- Different teams or systems use the same terms with different meanings
- There is no canonical authority for domain definitions within the agency
- Vendor-provided "AI understanding" of your domain cannot be inspected or audited

> **Leader question for Layer 2:**
> *"Do we own a documented, version-controlled model of our domain's core entities and relationships — or does the vendor?"*

---

## Layer 3 — Epistemology: Truth, Verification, and Accountability

**Plain English:** Epistemology is the study of how we know what we know. In AI terms, it is about whether the system's outputs can be verified, traced to sources, and distinguished from guesses.

**Why it matters to government leaders:** AI systems produce probabilistic outputs — they are making educated guesses, not looking up facts in a database. When an AI system recommends denying a benefit, flagging a case for review, or scoring a project proposal, that recommendation needs to be traceable to evidence, not just to model weights. Oversight bodies, courts, and constituents will ask "why."

**What good looks like:**
- Every AI output is tagged with its sources and a confidence level
- Verification gates distinguish confirmed facts (from owned data) from model inferences
- Audit trails are created at every decision point
- The system can answer "show me why you said that" with evidence — not just a score

**What poor looks like:**
- The system produces a score or recommendation with no explanation
- Outputs cannot be traced to specific data records
- There is no process for distinguishing a verified fact from a model prediction
- Errors or hallucinations would not be caught before affecting a citizen

> **Leader question for Layer 3:**
> *"When this system makes a recommendation that affects a citizen, can we trace that recommendation back to specific, verifiable evidence — and explain it in plain terms to a Congressional oversight hearing?"*

---

## Layer 4 — Praxeology: Decision Workflows and Human Oversight

**Plain English:** Praxeology is the study of human action and intentional decision-making. In AI terms, it is about whether the system's actions are governed by defined workflows with clear human oversight checkpoints.

**Why it matters to government leaders:** Agentic AI systems — systems that can take actions, send communications, update records, or trigger processes — are becoming common. Without explicit workflow governance, these systems can take consequential actions with no human review. For government agencies, this creates legal, compliance, and public trust risks.

**What good looks like:**
- Every consequential AI action requires a defined approval step before execution
- Workflows are documented, auditable, and cannot be bypassed
- Human override is always possible at defined checkpoints
- Actions and their approvals are logged permanently
- The system cannot independently act outside its defined scope

**What poor looks like:**
- The AI can take actions (update records, send notices, trigger processes) without human review
- Workflow logic lives entirely in vendor code and cannot be inspected
- There is no immutable audit log of what the system did and when
- "Agentic" features were enabled without a formal governance review

> **Leader question for Layer 4:**
> *"Can I show an auditor exactly what this system did, when it did it, who approved each step, and how a human could have intervened at any point?"*

---

## Layer 5 — Axiology: Values, Ethics, and Mission Alignment

**Plain English:** Axiology is the study of value — what matters, what should be preserved, and what is unacceptable. In AI terms, it is whether the organization's values and compliance rules are enforced by the system. A prompt edit alone should not turn them off. That enforcement still has to be tested; an untested rule is only a claim.

**Why it matters to government leaders:** AI systems optimize for the objectives they are given. If those objectives are set by a vendor, or if guardrails are only soft guidelines embedded in prompts, they can drift or be bypassed. Government agencies have statutory obligations, constitutional constraints, and public trust responsibilities that must be non-negotiable — not best-effort.

**What good looks like:**
- Prohibited actions (e.g., sharing PII, bypassing appeal rights) are enforced at the infrastructure level, not just in prompts
- The system's value constraints are documented, version-controlled, and auditable
- Compliance requirements (e.g., Privacy Act, ADA, FOIA) are explicitly encoded
- Attempts to bypass policy (including prompt attacks) are tested, and failures are logged rather than assumed away
- Values are tested and verified regularly, not assumed

**What poor looks like:**
- Guardrails are implemented as prompt instructions that a skilled user could work around
- There is no mechanism to verify that the system is still aligned with policy over time
- Values and compliance rules are defined by the vendor, not by the agency
- There is no formal process for testing whether the system behaves appropriately at its boundaries

> **Leader question for Layer 5:**
> *"If a determined employee or external actor tried to use this system in a way that violates agency policy or law, would the system prevent it — and can we prove that to an auditor?"*

---

## The Five Questions Together

Use these five questions as a rapid evaluation tool in any AI briefing:

| Layer | Leader Question | Score it: Can you answer YES with evidence? |
|---|---|---|
| Metrology | Do we own and can we fully audit the data foundation? | Y / Partially / N |
| Ontology | Do we own the meaning and entity model for our domain? | Y / Partially / N |
| Epistemology | Can we trace every recommendation to verifiable evidence? | Y / Partially / N |
| Praxeology | Are all consequential actions governed with human oversight? | Y / Partially / N |
| Axiology | Are agency values and compliance constraints hard-enforced? | Y / Partially / N |

**A "Partially" or "N" on any layer is a governance gap that must be resolved before approval or scale-up.**

---

## Next Steps

- Use the [5-Layer Evaluation Checklist](5-Layer-Evaluation-Checklist.md) to formally score a proposal
- Review the [Own vs. Rent Strategy](Owned-vs-Rented-AI-Strategy.md) to understand which layers must be owned
- Read [Business Value](business-value.md) for the investment case
- Architects: read the [Full Architecture Specification](../ARCHITECTURE.md) and [Governance Guidelines](MOEPA-Architectural-Governance-and-Evolution-Guidelines.md) for implementation depth
