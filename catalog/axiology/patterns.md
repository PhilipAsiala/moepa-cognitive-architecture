# Axiology Patterns and Anti-Patterns

## Why These Patterns Matter to Leaders

Weak governance patterns rarely fail quietly. They show up as compliance incidents, fairness concerns, privacy failures, and erosion of stakeholder trust.

## Durable Governance Patterns

- Policy as Code Baseline: encode mandatory controls in versioned policies
- Fairness Monitoring Loops: continuous metric tracking and remediation triggers
- Privacy by Design: enforce minimization and access boundaries upfront
- Value Alignment Reviews: periodic checks against mission and strategic goals

## Named Implementation Patterns

### Pattern A-A: Constitutional Layer Wrapper
Wrap all AI inference calls in a constitutional layer that evaluates both the input and output against inviolable constraints before either enters the system or reaches the user. The constitutional layer is a separate service that cannot be bypassed by the inference pipeline.

```
User Input → Constitutional Input Filter → Inference Engine
                     ↓ (blocked if violates constraints)
                 Violation Log + Alert

Inference Output → Constitutional Output Filter → User
                          ↓ (blocked if violates constraints)
                      Violation Log + Alert + Human Escalation
```

### Pattern A-B: Policy Versioning with Effective Dates
All policy-as-code configurations include an effective date and an expiry date. Before executing any workflow, the system retrieves the policy version that was active at the time of the initiating event — not just the current policy. This enables correct handling of decisions made under superseded policy.

### Pattern A-C: Equity Monitoring Baseline
At deployment, compute a baseline output distribution across demographic and geographic dimensions for the intended population. Set alerting thresholds at ±2 standard deviations from baseline. Review triggered when any dimension crosses the threshold. Baseline reviewed and updated annually.

## Costly Patterns to Avoid

- Ethical rules embedded only as optional prompt guidance
- Manual compliance documentation disconnected from runtime telemetry
- Privacy controls added post-deployment after incidents occur
- Fairness checks performed only once during pilot phases

## Common Weaknesses to Watch For

| Weakness | Risk | Signal |
|---|---|---|
| Guardrails only in system prompt | Bypassable by sophisticated prompt engineering | "Our guidelines are embedded in the instructions we give the model" |
| No testing of guardrails | Guardrails may not work under real conditions | "We haven't done adversarial testing" |
| Vendor defines compliance controls | Agency cannot verify or modify constraints | "Compliance is handled by the platform's built-in features" |
| No bias monitoring | Systematic inequity undetected | "We haven't measured outcomes across demographic groups" |
| Policy not version-controlled | Cannot reconstruct which rules were active for a historical decision | "We updated the policy guidelines last quarter" |

## What Leaders Should Watch For

- Control drift where deployed behavior diverges from approved policy
- Incomplete evidence trails for high-impact decisions
- Strategic misalignment between optimization metrics and mission outcomes

See [Business Value](../../docs/business-value.md) and [ARCHITECTURE.md](../ARCHITECTURE.md) for why enforceable governance is part of the Owned-Brain Strategy.
