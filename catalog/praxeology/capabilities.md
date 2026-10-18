# Praxeology Capabilities

## What Leaders Need to Know

Bottom line: this layer governs how AI turns into action. It helps leaders decide where automation is appropriate, where human approval is mandatory, and where operational risk is too high.

See [ARCHITECTURE.md](../ARCHITECTURE.md) for the strategic rationale and [Business Value](../../docs/business-value.md) for the investment lens.

## Mission and Governance Outcomes

- Predictable automation with auditable approvals and actions.
- Lower operational risk from bounded, reviewable workflows.
- Better oversight of where AI is allowed to act versus merely advise.
- Greater ownership of workflow logic instead of hiding it inside vendor tools.

## What Praxeology Covers

| Capability Domain | Description |
|---|---|
| **Workflow definition and enforcement** | Defining and enforcing the sequence of steps for any consequential action |
| **State machine governance** | Tracking workflow state so nothing can skip steps or run out of sequence |
| **Human-in-the-loop controls** | Ensuring human review at defined decision points before consequential actions |
| **Audit trail generation** | Creating an immutable record of every workflow execution |
| **Tool scope enforcement** | Limiting what actions an AI agent can take to its defined scope |
| **Escalation and exception handling** | Governing what happens when automated processing cannot complete |

## Core Capabilities

### P1 — Deterministic Workflow State Machine
**What it does:** Represents each workflow as an explicit state machine — a defined set of states, transitions, and conditions. The system can only move between defined states in defined ways; no transitions are possible outside the state machine.

**Why it matters for government:** "Agentic" AI that follows instructions step-by-step with no formal state model can get into undefined states — doing things it wasn't intended to do, or skipping steps that were required. A state machine makes workflows provably correct and auditable.

**Minimum acceptable standard (Score 3):** Workflows documented with required steps; execution follows defined sequence.

**Good practice (Score 4–5):** Formal state machine implementation; transitions logged at each state change; state model version-controlled; impossible to skip required states.

---

### P2 — Human-in-the-Loop Checkpoints
**What it does:** Defines mandatory pause points in workflows where a human must review the situation and explicitly approve before the system can proceed. These checkpoints cannot be bypassed by the system or by prompt engineering.

**Why it matters for government:** Automated AI systems making consequential decisions about citizens — issuing notices, updating records, triggering audits — must have defined points where a responsible official reviews and approves. This is not just a governance preference; it is a legal and due process requirement in many government contexts.

**Minimum acceptable standard (Score 3):** Human review required before any externally visible action; approval logged.

**Good practice (Score 4–5):** Checkpoint enforcement at the infrastructure level (not just application logic); bypassing a checkpoint produces a system error; approver identity and timestamp recorded in immutable log.

---

### P3 — Agent Scope Enforcement (Tool Boundaries)
**What it does:** Explicitly defines what actions an AI agent is authorized to take — what tools it can call, what systems it can write to, what data it can access — and prevents any action outside that scope.

**Why it matters for government:** Agentic AI systems are given access to tools (database updates, API calls, document generation, communication systems). Without explicit scope enforcement, a model could take unintended actions based on ambiguous instructions. Scope enforcement is the "blast radius" limiter.

**Minimum acceptable standard (Score 3):** Documented list of authorized agent actions; unauthorized actions blocked.

**Good practice (Score 4–5):** Tool scope enforced at the infrastructure level; unauthorized action attempts logged and alerted; scope changes require formal review and approval.

---

### P4 — Immutable Workflow Audit Log
**What it does:** Records every workflow event — state transitions, tool calls, human approvals, exceptions — in a tamper-evident log with timestamp and actor identity.

**Why it matters for government:** The workflow audit log is the evidentiary record for investigations, appeals, oversight inquiries, and compliance audits. It must be complete, accurate, and impossible to alter after the fact.

**Minimum acceptable standard (Score 3):** Workflow events logged; log retained per policy; accessible for audit review.

**Good practice (Score 4–5):** Cryptographically signed log entries; append-only storage; every event includes actor identity, timestamp, state before/after, and context reference; log immutable after write.

---

### P5 — Feedback and Adaptation Controls
**What it does:** Defines how workflow logic is updated based on outcomes — and controls that process so changes go through review rather than happening automatically.

**Why it matters for government:** Systems that learn and adapt need governance over how they adapt. An AI that autonomously changes its decision logic based on feedback could silently drift from its approved behavior. Adaptation must be a controlled, reviewed process.

**Minimum acceptable standard (Score 3):** Workflow logic changes go through documented review; changes are version-controlled.

**Good practice (Score 4–5):** Formal change control process for all workflow modifications; approved changes tested before deployment; previous versions archived and retrievable.

---

### P6 — Escalation and Exception Handling
**What it does:** Defines what happens when a workflow cannot be completed automatically — insufficient evidence, conflicting signals, boundary conditions. Escalation paths are explicit, logged, and governed.

**Why it matters for government:** The edge cases are where errors concentrate. A workflow that handles 95% of cases automatically but has no defined process for the remaining 5% will produce unpredictable outcomes for the citizens in that 5%.

**Minimum acceptable standard (Score 3):** Exception conditions documented; escalation path defined; exceptions logged.

**Good practice (Score 4–5):** Automated escalation routing based on exception type; escalation outcomes tracked; exception patterns reviewed regularly to improve workflow coverage.

---

## Capability Matrix

The matrix below binds the minimum set of Praxeology capabilities to **Score 3 — Defined & Contained — Minimum Acceptable Standard** in the existing [Praxeology scoring guide](scoring.md). Capabilities that contribute to Scores 4 and 5 lift the layer beyond that baseline. Live delivery status should be tracked through the [Praxeology workflow](tools.md); the JIRA epic column below is illustrative only.

| Capability | Minimum set? (Score 3) | Maturity contribution (3 / 4 / 5) | Owner | Delivery tracking (illustrative: JIRA epic) |
| --- | --- | --- | --- | --- |
| Agent frameworks for goal-oriented execution | No | 4 — provides a reusable control plane for multi-step automation | Automation platform owner | Illustrative: JIRA epic for agent orchestration platform |
| Workflow automation for repeatable business operations | Yes | 3 — establishes defined and reviewable operational flows | Workflow owner | Illustrative: JIRA epic for repeatable workflow automation |
| Decision engines combining rule-based and AI recommendations | Yes | 3 — keeps actions bounded by explicit decision logic | Decision workflow owner | Illustrative: JIRA epic for hybrid decision services |
| Action orchestration and goal decomposition across multi-step plans | Yes | 3 / 4 — supports governable multi-step execution and lifts maturity when standardized | Workflow owner | Illustrative: JIRA epic for orchestration and goal decomposition |
| Real-time execution controls with human-in-the-loop checkpoints | Yes | 3 / 4 / 5 — mandatory checkpoints satisfy the minimum, while stronger runtime controls and approvals lift higher | Operations control owner | Illustrative: JIRA epic for approvals, checkpoints, and stop conditions |
| Process optimization using telemetry and feedback loops | No | 4 / 5 — improves resilience and scaled operational performance | Process improvement owner | Illustrative: JIRA epic for workflow telemetry and optimization |

## Questions Leaders Should Ask Before Funding

- What actions can this system take without human approval?
- Where are the mandatory checkpoints, escalation paths, and stop conditions?
- Can leadership reconstruct who approved what, when, and on what basis?
- If the workflow fails, can it be paused, rolled back, and reviewed safely?

## Related

See also the layer overview in [Praxeology README](README.md), [scoring guide](scoring.md), [tools](tools.md), and [patterns](patterns.md). Cross-layer interactions are described in [cross-layer-compositions.md](../cross-layer-compositions.md).
