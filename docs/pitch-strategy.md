# Pitch Strategy: The MOEPA Cognitive Architecture

> **Repository directive.** Every document, diagram, and architectural decision in this repository must serve this narrative. Use this guide when writing, reviewing, or presenting any material derived from the repo.

---

## 0. Business First

**Lead with business outcomes, not technology.** MOEPA is named after philosophical disciplines because leaders must be able to describe what the organization needs — trusted data, shared meaning, verifiable truth, governed action, and enforced values — before anyone names a tool, protocol, or platform.

| Rule | What it means |
|---|---|
| **Disciplines describe outcomes** | Metrology = trusted measurement. Ontology = shared reality. Epistemology = defensible truth. Praxeology = accountable action. Axiology = enforced values. |
| **Leaders ask ownership questions** | Every layer reduces to: *Do we own this outcome, or does a vendor?* |
| **Technology follows** | Stack choices, protocols, and implementation patterns belong in builder documents — not executive briefings, leader guides, or the README's primary narrative. |
| **One vocabulary per audience** | Executives hear mission, risk, auditability, and ROI. Architects hear substrates and interfaces. Never mix the two in the same paragraph. |

### Document tiers

| Tier | Audience | Lead with | Technical depth |
|---|---|---|---|
| **Leader-facing** | Executives, program managers, acquisition | Business outcomes per MOEPA layer; ownership questions; use-case walkthroughs. Start at the repository README and [primer/](../primer/) | None in body copy — link to builder tier |
| **Builder-facing** | Architects, engineers, reviewers | Engineering translation of each layer; substrate end state; tool patterns | Full — [catalog/ARCHITECTURE.md](../catalog/ARCHITECTURE.md) and governance guidelines |
| **Contributor** | Doc authors, RFC proposers | Pitch strategy + business-first test before adding technical detail | Scoped to the tier being edited |

If a leader-facing document mentions MCP, RAG, Iceberg, LangGraph, or similar before stating the business outcome that layer protects, rewrite it.

### Readability standard (every document)

Leader-facing and builder-facing documents both follow this standard. Builder documents keep technical precision. They still have to be readable by a senior leader who did not help write them.

1. **Purpose first.** Open with one or two sentences on what the design is for and who it serves.
2. **Work, not only structure.** Say how the design changes workflows, decision rights, speed, risk, cost, or service outcomes.
3. **Predictive and generative.** When both are in scope, separate them. Predictive work detects patterns, forecasts, or scores. Generative work writes summaries, narratives, or recommendations. State the practical effect of each.
4. **Define terms on first use.** Keep MOEPA names. Add a plain gloss: Metrology is measurement and telemetry; Ontology is shared definitions; Epistemology is how a claim is verified; Praxeology is how action is taken; Axiology is value and priority constraints; policy-as-code means rules written so a system can enforce them; the Data Substrate is the organization-owned knowledge library.
5. **Claim, then support.** Short sentences. One idea per paragraph. Headings a reader can scan.
6. **Qualified claims.** Do not write “entirely solves,” “impenetrable,” “massive,” “zero lock-in,” “immunity,” or “impossible” unless the same passage states the condition and the limit.
7. **Operational effect.** Each major element names at least one tangible effect, such as earlier risk interception, less manual review, clearer accountability, or faster service response.
8. **Risk with a control.** Name bias, opacity, overhead, or unsupported answers only with a control already in the design (human checkpoint, monitoring, policy gate, audit trail) and the main trade-off.
9. **Close the loop.** Leader-facing pieces end with what to decide or do next.
10. **No new evidence.** Do not add metrics, case studies, or capabilities that are not already in the source. If a claim has no support, soften it or mark the gap.

Tone stays confident and neutral. Promotional language is out of scope for both internal and external leadership audiences.

---

## 1. The Core Mindset

**The industry blind spot:** The market obsesses over the *Artificial* — infrastructure, compute, LLMs — and treats *Intelligence* as an uncontrollable black box.

**Our solution:** We open the black box. We decode Intelligence by mapping human cognitive functions into strict, governable software:

| Function | What it is | MOEPA expression |
|---|---|---|
| **Cognition** (knowing) | How the system defines and verifies reality | Metrology, Ontology, Epistemology |
| **Affect** (valuing) | How the system encodes what matters and what is forbidden | Axiology |
| **Conation** (acting) | How the system executes decisions under human oversight | Praxeology |

**Philosophy vs. psychology in the stack:**

- **Philosophy** is the operating system — the strict logical rules for defining reality and truth (Metrology, Ontology, Epistemology).
- **Psychology** is the mechanics of behavior — how values and execution drives steer the cognitive engine (Axiology, Praxeology).

**The mission:** We do not build black boxes. We build auditable, institutional brains.

---

## 2. Core Terms: Thesis, Storage, Engine

Keep the vocabulary to three core terms rather than splitting the architecture into multiple names:

| Term | Role | What it is |
|---|---|---|
| **MOEPA Cognitive Architecture** | The thesis | The five-layer separation of concerns (Metrology, Ontology, Epistemology, Praxeology, Axiology) and the go/no-go intake scorecard (1–5 per layer, **GO / CONDITIONAL GO / NO-GO**) |
| **Data Substrate** | The storage | The organization-owned library where truth, definitions, values, rules, and lineage live in open formats — never a vendor lock-in store |
| **Agents** | The engine | The workflows and models that consume the Data Substrate to propose and execute work across the layers, bounded by Epistemology verification and Axiology policy gates |

---

## 3. Pitching the Technical Team (The Builders)

**The hook:** Validate their mastery of the Artificial. Challenge them to engineer the Intelligence.

**The translation:** Map human sciences directly to system architecture.

| MOEPA layer | Scientific anchor | Engineering translation |
|---|---|---|
| **Metrology** | Measurement | Telemetry, audit trails, performance scoring |
| **Ontology** | Domain / reality | Knowledge graphs, approved vocabularies, data models |
| **Epistemology** | Truth | Evidence mapping, RAG validation, authoritative source indexing |
| **Praxeology** | Action | Digitized SOPs, workflows, agentic execution playbooks |
| **Axiology** | Values / rules | Encoded guardrails, access controls, NIST-aligned compliance |

Introduce the **MOEPA Cognitive Architecture** as their engineering blueprint — not a presentation-layer abstraction, but the control plane for how institutional knowledge is stored on the Data Substrate and how Agents are verified, routed, and governed.

---

## 4. Pitching Enterprise Leadership (The Buyers)

**The hook:** Vendors sell compelling demos. Your organization needs a framework that separates what you must own from what you can rent.

**The governance lever:** Position the **MOEPA Cognitive Architecture** as the organization's go/no-go project intake rubric. A proposal that cannot be mapped to all five layers does not pass intake.

**The own-vs-rent strategy:** The organization owns the **Data Substrate** — the truth, the values, the rules. Rent commercial LLMs and compute for the **Agents** that consume it. Institutional knowledge stays portable when the substrate is owned and contracts require export. Lock-in returns if those conditions are skipped.

**Primary guide:** [Business Leader Guide](moepa-business-leaders-guide.md)

---

## 5. Pitching Public Sector Leadership (Federal, State, and Local)

**The hook:** You cannot govern an AI mind with standard IT infrastructure metrics. You need a **cognitive control plane**.

**The governance lever:** Position the **MOEPA Cognitive Architecture** as the organization's go/no-go project intake rubric. A proposal that cannot be mapped to all five layers does not pass intake.

**The own-vs-rent strategy:** The institution owns the **Data Substrate** — the truth, the values, the rules. Rent commercial LLMs and compute. A model or vendor change does not, by itself, move the rules, the data, or the audit trail, provided the substrate is owned and export terms are real.

**End state vs. evolution:** The organization must eventually own a single, auditable knowledge library (the Data Substrate) that every layer reads from and writes to. Public institutions get there incrementally — starting with what they have, documenting the path, and refusing new vendor silos. Technical storage targets belong in builder conversations; leaders hear *ownership, portability, and audit lineage*.

**Primary guide:** [Public Sector Leader Guide](moepa-public-sector-leaders-guide.md)

---

## 6. Golden Rules of Tone and Execution

- **Business first:** State the outcome each MOEPA layer protects before any implementation detail. If the reader is a leader, stop when the ownership question is answered.
- **Voice:** Direct and specific. Executive-to-executive for leaders; engineer-to-engineer only in builder-tier documents. Confident, and neutral about results the design has not yet demonstrated.
- **Clarity:** Ground abstract philosophy in physical metaphors — Data Substrate, Control Plane, Management Lever — and define each specialist term on first use.
- **Actionable output:** Leader guides and examples must show how philosophical disciplines change a decision, a workflow, or an audit — not only how the stack is drawn.
- **Technical containment:** MCP, semantic ingestion, and substrate storage patterns belong in `catalog/ARCHITECTURE.md` and the governance guidelines — not in README intros, leader handouts, or executive summaries.
- **Readability:** Apply the [readability standard](#readability-standard-every-document) in §0 to every new or revised page.

---

## 7. Architectural Evolution (Builders Only)

When describing implementation paths, align with the
[Architectural Governance and Evolution Guidelines](MOEPA-Architectural-Governance-and-Evolution-Guidelines.md):

| Principle | Pitch to builders |
|---|---|
| Governance over abstraction | MCP is the integration layer — not Bedrock-native tooling or LangChain glue |
| Fragments to semantic objects | Docling/Unstructured-style parsing produces Proto-SPOs with provenance, not naive chunks |
| MOEPA standard | Every feature scores across all five layers with exact citations where evidence is claimed |
| MCP-first pattern | Data and RAG access live in MCP servers; legacy APIs get MCP facades |

---

## Related Documents

- [Business Value](business-value.md) — investment case in business-outcome terms
- [Glossary](glossary.md) — canonical term definitions
- [MOEPA Cognitive Architecture for Leaders](MOEPA-5-Layer-Framework.md) — per-layer leadership questions
- [Architectural Governance and Evolution Guidelines](MOEPA-Architectural-Governance-and-Evolution-Guidelines.md) — MCP-first evolution rules and PR gate
- [Business Leader Guide](moepa-business-leaders-guide.md) — enterprise intake and ownership pitch
- [Public Sector Leader Guide](moepa-public-sector-leaders-guide.md) — government intake and accountability pitch
- [Own vs. Rented AI Strategy](Owned-vs-Rented-AI-Strategy.md) — own substrate, rent compute
- [MOEPA Cognitive Architecture Spec](../catalog/ARCHITECTURE.md) — technical implementation