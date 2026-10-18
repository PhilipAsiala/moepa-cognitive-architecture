# Zero-trust governance

**The worry:** a fluent system treats a rumor as a fact, shows a restricted record to the wrong person, or lets a prompt stand in for a legal rule.

Two layers carry that worry, and they are not the same job.

**Epistemology (truth and permission)** asks whether a claim is justified and whether this user may see the material it rests on. A language model can draft the sentence. It does not get to decide that the sentence is true.

**Axiology (rules that do not negotiate)** sits outside the model and can refuse the action. Policy-as-code means the rule is written so a system can enforce it. A system prompt is not that mechanism.

## Probabilistic proposal, deterministic refusal

| Step | Kind of system | What "pass" means |
| :--- | :--- | :--- |
| A model drafts an answer or a plan | Probabilistic | A proposal exists. It is not yet a decision. |
| Epistemology checks source, corroboration, and access | Deterministic gate | The claim cites an owned source, and the reader is allowed to have it. Otherwise it does not enter the record. |
| Axiology checks the proposed action against encoded rules | Deterministic gate | The action is allowed, or it is blocked. There is no "usually." |

The limit is the rule that was written. A missing rule is not enforced. A gate does not fix a measurement that Metrology never qualified. High confidence from a model is not, by itself, permission to act. Consequential actions still keep a human checkpoint in **Praxeology (how action is taken)**.

## What zero trust changes in intake

- No claim the organization will rely on without a source it can open.
- No access decision hidden inside the model's context window. Clearance and need-to-know are checks, not prompt text.
- No compliance story that begins and ends with "we told the model the policy."
- Every consequential action has an owner who can stop it, and a record of why it was allowed.

## What to decide

1. List the claims this system will be allowed to treat as fact, and the source for each.
2. List the actions it may take, and the encoded rule that can refuse each one.
3. Score Epistemology, Praxeology, and Axiology against the [Enterprise Capability Matrix](../catalog/capability-matrix.md).

Builder detail: [Enterprise Agent Capabilities](../catalog/agents.md) (`AG3` Verification Agents and `AG5` Policy Gate Agents).
