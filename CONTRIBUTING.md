# Contributing

This repository is the canonical reference for the draft **Philosophical AI
Architecture** shared for discussion, refinement, and review. Feedback is
welcome — including disagreement. This is a proposal, not a deployed system:
contributions are documentation and design feedback, not code to build or run.

All feedback must align with the narrative in
[docs/pitch-strategy.md](docs/pitch-strategy.md). For term definitions, see
[docs/glossary.md](docs/glossary.md).

Architecture evolution requirements are defined in
[docs/MOEPA-Architectural-Governance-and-Evolution-Guidelines.md](docs/MOEPA-Architectural-Governance-and-Evolution-Guidelines.md).

## How to contribute (issues only)

**Please open an issue — do not open a pull request.**

This repository uses an **issue-first** contribution model:

| You can | You cannot |
| --- | --- |
| Open a [Feedback / Question](https://github.com/PhilipAsiala/philosophical-ai-architecture/issues/new?template=feedback.yml) issue | Open a pull request with direct edits |
| Open a [Proposal / RFC](https://github.com/PhilipAsiala/philosophical-ai-architecture/issues/new?template=proposal-rfc.yml) for substantive design changes | Push branches or submit PRs from a fork expecting merge |
| Comment on existing issues and RFCs | Bypass discussion by submitting a patch |

The **repository maintainer** reviews issues, decides what changes fit the
architecture, and opens pull requests to implement accepted work on `main`.

If you want to use this material in your own organization, the MIT license
allows that — fork and adapt locally without needing a pull request here.

### Why this model

MOEPA is a cohesive reference architecture. Direct pull requests from many
authors create terminology drift, scoring inconsistencies, and review burden
that works against the framework's goal of a single auditable narrative.
Issues keep discussion open while preserving editorial control on `main`.

## Ways to participate

- **Questions, typos, or clarifications:** [Feedback / Question issue](https://github.com/PhilipAsiala/philosophical-ai-architecture/issues/new?template=feedback.yml)
- **Substantive design changes:** [Proposal / RFC issue](https://github.com/PhilipAsiala/philosophical-ai-architecture/issues/new?template=proposal-rfc.yml)
- **Accepted changes:** implemented by the maintainer via pull request after issue discussion

## Helpful feedback

- Logical inconsistencies or contradictions across documents
- Unclear, ambiguous, or unsupported claims
- Gaps in the five-layer model or the scoring rubric
- **Business-first drift** — technical jargon (tools, protocols, storage formats) appearing in leader-facing docs before business outcomes
- Drift from MCP-first integration, semantic ingestion, or Proto-SPO requirements in **builder-tier** documents
- Real-world examples, references, or counterexamples
- Drift from the pitch strategy terminology or tone

## Proposal / RFC process

For changes that affect the layer model, scoring semantics, or governance approach:

1. Open a **Proposal / RFC** issue describing the problem and the proposed change.
2. Discuss and refine in the issue thread.
3. If accepted, the **maintainer** opens a pull request that links the issue and implements the change.
4. Substantive changes are versioned using semantic versioning (MAJOR.MINOR.PATCH).

Include in RFC issues (when capability-related) the same impact notes used for
implementation review:

1. MCP server or MCP facade introduced or reused (if applicable)
2. Ingestion/parsing approach and Proto-SPO metadata fields (if applicable)
3. Five-layer MOEPA impact notes (Metrology through Axiology)
4. Citation and provenance behavior in generated outputs (if applicable)
5. Any exceptions and approved compensating controls

Proposals that cannot map to these requirements should be scored CONDITIONAL GO
or NO-GO under the MOEPA intake rubric.

## Style notes (for accepted changes)

- **Business first** — leader-facing docs lead with MOEPA disciplines as business outcomes; technical detail links out to `ARCHITECTURE.md` or the governance guidelines.
- **Readability** — follow the [readability standard](docs/pitch-strategy.md#readability-standard-every-document) in the pitch strategy: purpose and audience first, plain definitions on first use, one operational effect per major element, risks paired with a control already in the design, and no absolute claims without a stated limit.
- Direct and specific — executive-to-executive for leaders; engineer-to-engineer only in builder-tier documents. Confident, and neutral about results the design has not yet demonstrated.
- Ground abstract concepts in physical metaphors (Data Substrate, Control Plane).
- Never conflate the **Philosophical AI Architecture** (ecosystem) with the **MOEPA 5-Layer Framework** (engineering blueprint and intake rubric).
- Treat **SPO/quad on a federated hypergraph + lakehouse** as the imperative **Substrate End State**; allow **Substrate Evolution Path** staging in implementation guidance.
- Preserve the five-layer structure (Metrology, Ontology, Epistemology, Praxeology, Axiology).
- Keep the GO / CONDITIONAL / NO-GO scoring model consistent with `ARCHITECTURE.md` and the evaluation checklist.

## Maintainer notes (repository owner)

Recommended GitHub settings to reinforce this policy on `main`:

1. **Branch protection** — Settings → Branches → add rule for `main`:
   - Require a pull request before merging
   - Require review from code owners (see [.github/CODEOWNERS](.github/CODEOWNERS))
   - Restrict who can push to matching branches (maintainer only)
2. **Workflow** — [.github/workflows/maintainer-pr-only.yml](.github/workflows/maintainer-pr-only.yml) auto-closes pull requests opened by non-maintainers with a pointer back to this file.

External contributors can still open pull requests on public repositories; branch protection and the workflow ensure they are not merged without maintainer action.
