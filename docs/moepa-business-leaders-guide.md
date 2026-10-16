# MOEPA: A Business Leader's Guide to Owning AI Strategy

## A Strategic Handout for Executives and Decision-Makers

## What it does

This guide is for executives and business-unit owners who approve AI investments and own the risk. It is a decision aid for funding, ownership, and risk.

The **Philosophical AI Architecture** is the frame. The **MOEPA 5-Layer Framework** is the intake rubric inside it. MOEPA names five responsibilities: **Metrology** (measurement and telemetry), **Ontology** (shared definitions), **Epistemology** (how a claim is verified), **Praxeology** (how action is taken), and **Axiology** (value and priority constraints). Leadership scores a proposal on those five questions before funding. A vendor feature list does not substitute for that score.

Using the rubric changes the work:

- Ownership is decided explicitly: what the organization must keep, and what it can rent.
- Predictive outputs (scores, forecasts, match confidence) and generative outputs (summaries, explanations, recommendations) are both required to cite evidence.
- Consequential actions keep a named human checkpoint and an audit trail.
- Accountability sits with the business owner, which adds intake time and up-front cost in exchange for a record that can be defended later.

## Why the five layers show up in ordinary work

The five names are ordinary steps, applied to systems that act at scale: measure, understand what is in the situation, check the facts, do the work, and judge whether the result is the one you wanted.

A simple example is repainting a living room:

- **Metrology (Measurement):** Measure the walls to figure out how much paint to buy. Better measurement means fewer mistakes, less waste, and lower cost.
- **Ontology (Relationships and Reality):** Understand who and what exists in the space—people, pets, furniture, routines, and constraints. The project does not happen in a vacuum.
- **Epistemology (Truth and Verification):** Measure twice to confirm the numbers are accurate before acting. Good decisions require verified facts.
- **Praxeology (Human Action):** Plan and execute the work—move furniture, tape edges, buy supplies, paint carefully, and stay within budget.
- **Axiology (Value and Aesthetics):** Decide what outcome is actually desirable. Which color fits the home? Which tradeoffs matter most? What does “good” look like?

The five steps matter because each one is a place where a system can drift without a named owner.

## How work changes

Tools change faster than mission, accountability, and stakeholder trust. When vendors or technical teams set AI strategy alone, the usual result is fragmented tools, weak data ownership, and decisions that are hard to explain to an oversight body.

MOEPA starts with measurement, structure, verification, action, and values, and only then chooses technology. The operational effect is a different approval conversation: where to invest, what the organization will control, and which risks it will accept, written down before the contract.

## The Five Layers of AI in Business Terms

MOEPA organizes AI into five interdependent layers. Each layer represents a distinct leadership responsibility.

| Layer | Business Meaning | Core Leadership Question | What Weakness Looks Like |
| --- | --- | --- | --- |
| Metrology | Foundation of trusted data and measurement | Do we control and trust the data this system uses? | Poor data quality, hidden lineage, vendor-owned data |
| Ontology | How reality is structured and represented | Do we own the meaning and relationships in our data? | Inconsistent definitions, vendor-controlled semantics |
| Epistemology | How truth is determined and verified | Can we verify outputs and maintain accountability? | Black-box answers, untraceable recommendations |
| Praxeology | How the system takes action and makes decisions | Do we control workflows and maintain human oversight? | Autonomous actions without proper guardrails |
| Axiology | Values, rules, and mission alignment | Does this system reflect mission values, and can we enforce them? | Mission drift, policy bypass, ethical failures |

What leaders need at each layer is a clear answer on ownership. Implementation detail stays with architects.

## The Own vs. Rent Decision Framework

One of the most important AI strategy decisions is determining what the organization should own versus what it can safely rent.

Core principle:
Own the layers that represent institutional knowledge, decision authority, values, and accountability. Rent commoditized capabilities that do not create long-term dependency.

Recommended approach:

- Metrology and Ontology: strongly prefer ownership. These layers contain organization data and meaning. Losing control here creates durable dependency.
- Epistemology: own verification and truth standards. Rent raw model capability only if verification remains under organizational control.
- Praxeology: own decision workflows and human oversight points. Rent execution engines only when guardrails are strong.
- Axiology: must be owned. Values, policy, and mission alignment cannot be safely outsourced.

This framework helps leaders challenge proposals that hide ownership decisions inside technical architecture choices.

## Evaluating AI Use Cases with a Rational Business Lens

Not every AI opportunity deserves investment. Use the MOEPA layers to evaluate proposals systematically.

Recommended evaluation process:

1. Map the proposed use case to all five layers.
2. Assess current maturity of each layer inside the organization.
3. Identify what must be owned versus what can be rented.
4. Score the proposal on risk, mission alignment, and long-term control.
5. Determine whether the proposal strengthens or weakens organizational position in each layer.
6. Make a clear GO, CONDITIONAL, or NO-GO recommendation with documented rationale.

**Additional Enterprise Criteria — Demand Management and Cost Attribution:**

Before advancing any proposal, leaders must require two additional controls:

- **Demand Management (Deduplication):** The proposing team must show, by search of the organization's owned semantic model (Ontology), that the requested capability, data model, or infrastructure does not already exist elsewhere in the enterprise. This prevents duplicate solutions and uncontrolled infrastructure proliferation. A high-scoring Ontology layer is what makes that search possible.

- **Cost & Chargeback Model:** A formal cost attribution model (showback reporting or chargeback mechanism) must be defined, reviewed by the relevant platform and finance stakeholders, and accepted by the business owner before approval. This model must clearly attribute platform compute, data, governance, and ongoing operational costs. Proposals without an approved cost model cannot receive an unconditional GO.

This reframes the conversation from "What technology should we buy?" to "Does this investment increase control, reduce risk, serve mission, avoid duplication, and have a sustainable, transparent cost model?"

## Key Questions Every Leader Should Ask

Use these questions when reviewing AI proposals, vendor pitches, or internal initiatives:

- Who will own the data, meaning, and decision logic five years from now?
- What happens if a vendor changes pricing or terms, or exits the market?
- Can we explain to executives, auditors, or regulators how this system reached a decision?
- Where are the human oversight points, and are they meaningful?
- Does this solution make us more or less dependent on external parties over time?
- What are we giving up by choosing convenience over ownership?
- How will we update values and rules when policy or mission priorities change?

## Controls and limits

When technology choices run ahead of business ownership, the same problems recur. Each one has a control already in this design, and a cost.

| Risk | Control already in the design | Trade-off |
| --- | --- | --- |
| Vendor lock-in that is expensive to unwind | Own-vs-rent map: keep data, definitions, verification, workflows, and policy; rent compute | Higher up-front cost than a subscription pilot |
| Decisions the organization cannot explain | Epistemology: material outputs cite evidence and a confidence level | Slower to production than an uncited demo |
| Mission drift toward vendor metrics | Axiology: rules the system enforces, not only prompt text | A policy change needs a governed update |
| Actions with no oversight | Praxeology: a human checkpoint before a consequential action, plus an audit log | Some cases stay in a queue |
| Duplicate builds | Search of the owned semantic model (Ontology) before a new capability is approved | An extra step before funding |
| A decision that cannot be defended to oversight | The same evidence trail, produced from owned records | Staff time to keep the record complete |

These show up when AI is bought as a product feature and the ownership questions are left for later.

## What leaders need to decide

Organization leaders can begin applying MOEPA immediately:

- Require all new AI proposals to be evaluated against the five layers
- Require every new capability to map to all five layers with evidence of ownership — architects handle implementation detail separately
- Establish clear ownership criteria before approving funding
- Build internal capability to score and govern AI investments
- Start with high-visibility or high-risk use cases to demonstrate value
- Use the framework in vendor conversations to shift discussion from features to control and accountability

Adopt AI on the organization's terms: clear ownership, manageable risk, and alignment to mission and stakeholder trust. The intake step is the price of that control.

---

*For the public sector companion to this guide — statutory accountability, oversight-body audit framing, and government ownership patterns — see [moepa-public-sector-leaders-guide.md](moepa-public-sector-leaders-guide.md).*
