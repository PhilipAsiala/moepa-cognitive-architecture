# Brief 2: Zero-Trust Governance
### Bounding Probabilistic Agents with Deterministic Law

**The Executive Risk:** Large language models are fluency engines, not truth or compliance engines. Plugging an LLM directly into enterprise data and APIs — and relying on a system prompt like *"do not hallucinate or break regulations"* — leads to fabricated citations, unauthorized data disclosure, and rogue automated actions.

---

## How the Three Tiers Solve It

1. **MOEPA Cognitive Architecture (The Thesis):** Separates **Epistemology** (*is this claim verified and is the user cleared to see it?*), **Praxeology** (*what workflow steps and human checkpoints govern the action?*), and **Axiology** (*does this action pass our hard rules?*).
2. **Data Substrate (The Storage):** Holds the authoritative ground truth (`DS3`, `DS4`), the immutable cross-layer audit ledger (`DS5`), and the versioned Policy-as-Code baseline (`DS7`).
3. **Agents (The Engine):** Splits execution into **probabilistic planning** and **deterministic gates**. A model may draft a plan, but deterministic gate agents verify the facts (`AG3`), enforce the state machine (`AG4`), and hold veto power over every action (`AG5`).

---

## Probabilistic Proposal vs. Deterministic Refusal

In a zero-trust AI architecture, a model never polices itself:

| Stage | Tier & Capability | Mode | What Happens |
| :--- | :--- | :--- | :--- |
| **1. Quality & Entity Check** | `AG1` (Metrology) + `AG2` (Ontology) | Deterministic / Hybrid | Bad inputs are quarantined; valid inputs are mapped to canonical entities on the Data Substrate (`DS2`, `DS3`). |
| **2. Grounding & Verification** | `AG3` (Epistemology) over `DS4` | **Deterministic Gate** | Checks user clearance before retrieval. Every claim in a proposed answer must cite an owned substrate record, or it is blocked. |
| **3. Workflow Routing** | `AG4` (Praxeology) | Probabilistic Plan + **Deterministic State Machine** | Models propose; the state machine enforces step sequence, tool allow-lists, and mandatory human-in-the-loop checkpoints. |
| **4. Policy Enforcement** | `AG5` (Axiology) over `DS7` | **Deterministic Refusal** | Policy-as-Code (Open Policy Agent) loaded from the owned policy baseline evaluates the proposed action *outside* the model. Any rule violation is blocked. |
| **5. Immutable Audit** | `DS5` (Data Substrate) | Append-Only Ledger | Records input provenance, cited sources, confidence breakdown, human approver, and policy version for every decision. |

*Note on scope:* A deterministic gate blocks 100% of actions that violate an **encoded** rule on the gate path. It cannot enforce a policy that was never written, and high model confidence never overrides a missing source citation or a required human checkpoint.

---

## Decision Checklist for Leaders

1. **No Unverified Claims (`AG3`):** Can every factual assertion or risk score be traced back to a specific record on the Data Substrate (`DS4`, `DS5`)?
2. **Bounded Action (`AG4`):** Are agent tool permissions explicitly allow-listed, and is there an infrastructure-enforced human checkpoint before any consequential action?
3. **Policy Outside the Prompt (`AG5`):** Are legal, privacy, and spending constraints enforced by deterministic Policy-as-Code rather than prompt instructions?

*Next: [Investment & ROI](roi.md) · Builder specs: [Enterprise Agent Capabilities (`AG1`–`AG8`)](../catalog/agents.md)*
