# Praxeology Patterns and Anti-Patterns

## Why These Patterns Matter to Leaders

Weak action patterns create operational risk quickly. They lead to automation that is difficult to stop, difficult to explain, and difficult to assign responsibility for when something goes wrong.

## Durable Governance Patterns

- State Machine First: every workflow step has explicit transitions
- Policy Gate Checkpoints: evaluate compliance before sensitive actions
- Human Approval Escalation: mandatory intervention for high-risk outcomes
- Idempotent Tool Wrappers: retry-safe operations with audit identifiers

## Named Implementation Patterns

### Pattern P-A: Human Gate State
Every consequential workflow includes at least one `PENDING_HUMAN_REVIEW` state. The workflow cannot transition from this state to `APPROVED` or `ESCALATED` except through an explicit human action. Timeout in the `PENDING_HUMAN_REVIEW` state escalates automatically — it never auto-approves.

```
INITIATED → EVIDENCE_GATHERING → PENDING_HUMAN_REVIEW → [APPROVED | ESCALATED | REJECTED]
                                        ↑
                               Human action required
                               Timeout → ESCALATED (never auto-approved)
```

### Pattern P-B: Tool Call Authorization
Before any tool call, the agent checks an authorization policy: is this agent permitted to call this tool in this workflow state, for this entity type, with these parameters? Unauthorized calls are blocked and logged, not silently skipped.

### Pattern P-C: Immutable Workflow Snapshot
At each state transition, the full workflow context — current state, input data references, evidence references, confidence scores, approver identity, timestamp — is written as an immutable snapshot to the Data Substrate. This snapshot is the basis for any future audit or reproduction of the decision.

## Costly Patterns to Avoid

- Open-ended autonomous loops with unrestricted tool access
- Workflow logic split across prompts and undocumented scripts
- Human review configured but bypassable in production
- No rollback path for multi-step side effects

## Common Weaknesses to Watch For

| Weakness | Risk | Signal |
|---|---|---|
| No formal state machine | Workflow can get into undefined states | "It's just a sequence of API calls" |
| Human checkpoints bypassable | High-stakes decisions happen without review | "We have a review step but it can be skipped in urgent cases" |
| Agent has broad tool access | Unintended actions take place | "The agent has access to whatever it needs" |
| Audit log is editable | Compliance and evidentiary integrity at risk | Logs stored in standard database without append-only enforcement |
| No escalation path | Edge cases produce unpredictable outcomes | "If the system can't decide, it just returns an error" |

## What Leaders Should Watch For

- State desynchronization between orchestrator and tool systems
- Approval bottlenecks due to poor risk segmentation
- Excessive automation of decisions that require policy interpretation

See [Business Value](../../docs/business-value.md) and [ARCHITECTURE.md](../ARCHITECTURE.md) for why controlled execution is part of long-term institutional ownership.
