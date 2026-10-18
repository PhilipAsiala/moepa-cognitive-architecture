# Epistemology Capabilities

## What Leaders Need to Know

Bottom line: this layer determines whether leaders can trust AI conclusions. It separates what the model proposes from what the institution can verify, explain, and defend.

See [ARCHITECTURE.md](../ARCHITECTURE.md) for the strategic rationale and [Business Value](../../docs/business-value.md) for the investment lens.

## Mission and Governance Outcomes

- Lower risk of acting on hallucinations or unsupported conclusions.
- Better audit and appeals posture through evidence-backed explanations.
- Stronger stakeholder trust when decisions can be justified clearly.
- Reduced dependence on vendor claims about model reliability.

## What Epistemology Covers

| Capability Domain | Description |
|---|---|
| **Fact verification** | Distinguishing confirmed facts from model-generated inferences |
| **Retrieval-Augmented Generation (RAG)** | Grounding AI responses in owned, cited sources |
| **Confidence scoring** | Quantifying and communicating uncertainty in outputs |
| **Audit trail generation** | Creating an evidence chain for every significant decision |
| **Hallucination detection** | Catching outputs not supported by owned evidence |
| **Cryptographic validation** | Tamper-evident verification of pipeline integrity |

## Core Capabilities

### E1 — Source-Grounded Retrieval (Owned RAG)
**What it does:** Before generating a response, retrieves relevant documents, records, and facts from the agency's owned knowledge store and uses them as the primary context for the response — with citations.

**Why it matters for government:** A model that answers questions from its training data alone is essentially citing "things I've heard." A model grounded in your agency's owned, up-to-date records is citing "our official data, record ID X, validated on date Y." The difference is auditable accountability.

**Minimum acceptable standard (Score 3):** RAG pipeline retrieves from agency-controlled document store; source citations included in responses.

**Good practice (Score 4–5):** RAG grounded in the Data Substrate; every response cites specific records with IDs and validation timestamps; confidence score reported; responses that cannot be grounded are flagged rather than guessed.

---

### E2 — Fact Verification Gate
**What it does:** For high-stakes decisions, compares the AI system's output against independently verified ground truth before that output is acted upon.

**Why it matters for government:** When an AI system says "applicant's income is $87,400 from three sources," a verification gate checks that claim against the agency's own authoritative data before any action is taken. This is the difference between using AI as a decision support tool and using it as an unquestioned oracle.

**Minimum acceptable standard (Score 3):** Key outputs verified against a primary source before consequential actions; mismatches logged.

**Good practice (Score 4–5):** Automated verification gate for all consequential outputs; multi-source cross-checking; verification results stored in Data Substrate; discrepancies trigger review workflow.

---

### E3 — Confidence Scoring and Uncertainty Communication
**What it does:** Every significant output carries a confidence score with an explanation of its components — and that score is communicated meaningfully to the decision-maker.

**Why it matters for government:** A confidence score of "94%" means nothing without knowing what contributes to it. Is that 94% based on one source or five? Is the remaining 6% uncertainty due to a missing record or a conflicting one? Decision-makers need to understand uncertainty, not just receive a number.

**Minimum acceptable standard (Score 3):** Confidence scores reported; methodology documented.

**Good practice (Score 4–5):** Confidence scores decomposed by contributing evidence; uncertainty sources identified (missing data, conflicting sources, model uncertainty); scores are traceable to specific records.

---

### E4 — Immutable Decision Audit Log
**What it does:** Creates a tamper-evident record of every significant AI-assisted decision: what question was asked, what sources were retrieved, what the output was, what the confidence was, who reviewed it, and what action was taken.

**Why it matters for government:** The audit log is the evidentiary foundation for every investigation, appeal, oversight inquiry, and compliance review. Without it, an agency cannot demonstrate what happened — only assert it.

**Minimum acceptable standard (Score 3):** Decision log maintained; includes inputs, outputs, and reviewer; retained per policy.

**Good practice (Score 4–5):** Cryptographically signed log entries; immutable storage; end-to-end trace from input data through verification through decision; searchable by case, date, reviewer, or confidence band.

---

### E5 — Hallucination Detection
**What it does:** Detects when a model's output makes claims that are not supported by the retrieved sources or the owned knowledge base — and flags or blocks those outputs before they reach decision-makers.

**Why it matters for government:** Language models sometimes state things confidently that are simply wrong. In a benefits or eligibility context, an undetected hallucination could affect thousands of citizens before the error is discovered.

**Minimum acceptable standard (Score 3):** Response-level hallucination checking for high-stakes workflows; flagged outputs reviewed before use.

**Good practice (Score 4–5):** Automated hallucination detection on all consequential outputs; output not passed to decision-maker if it cannot be grounded; detection results logged.

---

### E6 — Cryptographic Pipeline Integrity
**What it does:** Uses cryptographic hashes (SHA-256 or equivalent) to verify that the data, model configuration, and pipeline components used for a given decision are exactly what they are supposed to be — and have not been tampered with.

**Why it matters for government:** Compliance and security frameworks require assurance that the system being run is the system that was approved. Cryptographic integrity checks make it possible to prove this.

**Minimum acceptable standard (Score 3):** Model configuration files hashed and verified at deployment; mismatches block deployment.

**Good practice (Score 4–5):** End-to-end pipeline integrity verification; every artifact (data, model, config, code) hashed and verified before execution; continuous integrity monitoring in production.

---

## Capability Matrix

The matrix below binds the minimum set of Epistemology capabilities to **Score 3 — Defined & Contained — Minimum Acceptable Standard** in the existing [Epistemology scoring guide](scoring.md). Capabilities that contribute to Scores 4 and 5 lift the layer beyond that baseline. Live delivery status should be tracked through the [Praxeology workflow](../praxeology/tools.md); the JIRA epic column below is illustrative only.

| Capability | Minimum set? (Score 3) | Maturity contribution (3 / 4 / 5) | Owner | Delivery tracking (illustrative: JIRA epic) |
| --- | --- | --- | --- | --- |
| Grounded retrieval (RAG) over trusted enterprise sources | Yes | 3 — anchors conclusions in trusted enterprise evidence | Knowledge assurance owner | Illustrative: JIRA epic for grounded retrieval controls |
| Inference engines tuned for auditable decision support | Yes | 3 — makes decision support reviewable instead of purely prompt-driven | Decision assurance owner | Illustrative: JIRA epic for auditable inference services |
| Model validation for reliability, drift, and failure detection | No | 4 — adds continuous reliability measurement and control | Model assurance owner | Illustrative: JIRA epic for validation, drift, and failure monitoring |
| Provenance tracking for conclusions and generated outputs | Yes | 3 — preserves evidence chains needed for review, audit, and appeal | Knowledge assurance owner | Illustrative: JIRA epic for provenance and evidence chains |
| Uncertainty handling with knowledge quality scoring | Yes | 3 / 4 — exposes uncertainty at the baseline and strengthens governance when standardized | Decision assurance owner | Illustrative: JIRA epic for uncertainty and quality scoring |
| Explanation generation and consistency checks across outputs | No | 5 — supports audit-grade defensibility and enterprise trust | Explainability owner | Illustrative: JIRA epic for explanation and consistency controls |

## Questions Leaders Should Ask Before Funding

- Can each conclusion be traced to source evidence that an auditor or reviewer could inspect?
- What happens when the system is uncertain or unsupported by the available evidence?
- Are validation controls mandatory before outputs affect customers, staff, or operations?
- Can the organization explain and defend the system's conclusions in an audit, appeal, or hearing?

## Related

See also the layer overview in [Epistemology README](README.md), [scoring guide](scoring.md), [tools](tools.md), and [patterns](patterns.md). Cross-layer interactions are described in [cross-layer-compositions.md](../cross-layer-compositions.md).
