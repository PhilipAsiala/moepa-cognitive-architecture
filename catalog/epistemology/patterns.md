# Epistemology Patterns and Anti-Patterns

## Why These Patterns Matter to Leaders

Weak validation patterns create public risk. They allow plausible but unsupported outputs to appear authoritative, which is especially dangerous in regulated or customer-facing contexts.

## Durable Governance Patterns

- Verify-Then-Act: no downstream action without validation pass
- Source-Cited Response Contracts: require evidence references by default
- Uncertainty Bands: classify confidence ranges for operational use
- Dual-Path Consistency Checks: compare independent reasoning/retrieval paths

## Named Implementation Patterns

### Pattern E-A: Grounded Response with Citation Chain
Every response includes: the answer, the records retrieved to support it, the confidence score, and a list of source citations with IDs and timestamps. Responses that cannot be grounded in owned sources are returned as "insufficient evidence" rather than as a best-guess.

### Pattern E-B: Two-Layer Verification (Inference + Verification)
AI inference layer produces a candidate answer. A separate, deterministic verification layer checks that answer against owned ground-truth records. The final output includes both the inference and the verification result — distinguishing "model said X" from "verified against record Y: confirmed / unconfirmed / conflicting."

### Pattern E-C: Confidence Banding
Outputs are classified into confidence bands that determine required handling:
- **High (≥ 90%)**: Automated processing with human spot-check
- **Medium (70–89%)**: Human review before action
- **Low (< 70%)**: Escalation required; no automated action

Band thresholds are policy-configurable and version-controlled.

## Costly Patterns to Avoid

- Directly executing model output with no grounding checks
- RAG pipelines that cite sources but skip content verification
- Confidence scores without calibration or test evidence
- Prompt-only safety claims with no deterministic validators

## Common Weaknesses to Watch For

| Weakness | Risk | Signal |
|---|---|---|
| No source citations on AI outputs | Cannot audit or defend decisions | "The model gave us a score of 87" |
| Verification depends on vendor data | Cannot independently confirm results | "We verify using [Vendor]'s cross-reference service" |
| Confidence scores without methodology | Numbers mean nothing; false confidence | Scores reported but not explained |
| No hallucination detection | Fabricated facts reach decision-makers | No testing for unsupported claims |
| Audit logs not immutable | Log tampering risk; compliance gap | Logs stored in editable format |

## What Leaders Should Watch For

- Citation laundering where references do not support conclusions
- Silent retrieval failures treated as high-confidence answers
- Drift in model behavior without updated quality thresholds

See [Business Value](../../docs/business-value.md) and [ARCHITECTURE.md](../ARCHITECTURE.md) for why verified knowledge is essential to trustworthy AI decisions.
