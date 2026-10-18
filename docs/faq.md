# FAQ

## Is a special storage format required on day one?

No. Own the data from the start, in open formats you can export, with a written path toward the end-state library. The operational effect is that a contract ending does not strand the record.

**For architects:** The end state is owned SPO/quad representation (each fact stored once as subject–predicate–object, plus context) with layer metadata on a federated hypergraph and lakehouse. Teams may start with open-format lakehouse storage (Iceberg/Parquet) using SPO-compatible schemas, then add a pilot triple store, then an enterprise graph and federation. Interim storage is acceptable when the data is organization-owned, provenance-complete, open-format, and backed by a documented migration path. See [End State vs. Evolution Path](Data-Substrate-Concept.md#end-state-vs-evolution-path).

## Is the Data Substrate a sixth layer?

No. The **Data Substrate** is the organization-owned knowledge library beneath the five scored layers. It holds truth, values, rules, and lineage in formats the organization can export. It is not scored on the 1–5 rubric. See §5 of [ARCHITECTURE.md](../catalog/ARCHITECTURE.md) for the storage specification.

## Is this a finished architecture?

No. This repository describes a draft **Philosophical AI Architecture** for discussion, refinement, and review. The **MOEPA 5-Layer Framework** (engineering blueprint and intake scoring) and **MOEPA Cognitive Architecture** (technical specification in [ARCHITECTURE.md](../catalog/ARCHITECTURE.md)) are components within that ecosystem — all are proposals, not deployed systems.

## What is the difference between Philosophical AI Architecture, MOEPA 5-Layer Framework, and MOEPA Cognitive Architecture?

- **Philosophical AI Architecture** — the full ecosystem: Data Substrate, guardrails, own-vs-rent strategy, cognitive control plane.
- **MOEPA 5-Layer Framework** — the engineering blueprint and governance engine inside the architecture: five layers, intake scoring, GO / CONDITIONAL GO / NO-GO decisions.
- **MOEPA Cognitive Architecture** — the technical stack design in [ARCHITECTURE.md](../catalog/ARCHITECTURE.md): storage mapping and recommended tools.

See the [Naming section in the README](../README.md#naming), [Pitch Strategy](pitch-strategy.md), and [Glossary](glossary.md).

## What are Cognition, Affect, and Conation?

The three human cognitive functions the Philosophical AI Architecture maps into software:

- **Cognition** (knowing) → Metrology, Ontology, Epistemology
- **Affect** (valuing) → Axiology
- **Conation** (acting) → Praxeology

Philosophy (Metrology, Ontology, Epistemology) is the operating system for reality and truth. Psychology (Axiology, Praxeology) is the mechanics of values and execution.

## What is the main idea?

Separate what you rent (compute and commercial models) from what you own: the knowledge library, shared definitions, verification rules, workflows, and policy constraints. Predictive outputs (scores and forecasts) and generative outputs (summaries and recommendations) both have to be explainable from those owned assets.

## Why five layers?

Each layer is one question leadership must be able to answer. The technical form of the answer belongs with architects.

- **Metrology** — measurement and telemetry. Do we trust the data?
- **Ontology** — shared definitions. Do we own what the terms mean?
- **Epistemology** — verification. Can we show why a score or a written answer is justified?
- **Praxeology** — action. Who approves what the system does?
- **Axiology** — value and priority constraints. Which rules can a prompt not switch off?

## Where should I start?

**Enterprise and commercial leaders:** [Business Leader Guide](moepa-business-leaders-guide.md) → [Evaluation Checklist](5-Layer-Evaluation-Checklist.md) → [Pitch Strategy](pitch-strategy.md)

**Public sector leaders:** [Public Sector Leader Guide](moepa-public-sector-leaders-guide.md) → [Evaluation Checklist](5-Layer-Evaluation-Checklist.md) → [Pitch Strategy](pitch-strategy.md)

**Technical architects:** [MOEPA 5-Layer Framework](MOEPA-5-Layer-Framework.md) → [Data Substrate Concept](Data-Substrate-Concept.md) → [ARCHITECTURE.md](../catalog/ARCHITECTURE.md)

**All readers:** [Glossary](glossary.md) → [5-Layer Framework](MOEPA-5-Layer-Framework.md)

## Does this include an implementation?

Not yet. The repository focuses on the proposal, the MOEPA 5-Layer Framework governance model, and the intended operating principles for a governed Data Substrate.

## Why MCP-first?

**For leaders:** Every data, retrieval, workflow, and policy capability should be callable through one governed interface, so an inventory and an audit do not depend on a vendor's private glue. **MCP** (Model Context Protocol) is that interface in this design.

**For architects:** Vendor orchestration glue (native Bedrock tooling, LangChain chains, framework-specific callbacks) hides capability boundaries from review. Each capability is exposed as an MCP server or facade. Orchestrators discover tools through MCP rather than calling retrieval or data layers directly. See [Architectural Governance Guidelines](MOEPA-Architectural-Governance-and-Evolution-Guidelines.md).

## What is a Proto-SPO and why does chunking matter?

**For leaders:** Documents should be split on meaning (a table, a section, a citation), not on an arbitrary length. Otherwise a later answer cannot point back to the source.

**For architects:** A **Proto-SPO** (Sovereign Processing Object) is a semantically parsed document segment that carries its own provenance, structure, and context. **Chainsaw chunking** — splitting documents by fixed token counts — drops tables, sections, and citations. Semantic parsers (Docling, Unstructured, or equivalent) produce Proto-SPOs that keep that structure through retrieval and verification. See [Data Substrate Concept — Semantic Ingestion](Data-Substrate-Concept.md#semantic-ingestion-and-proto-spos) and the [Glossary](glossary.md).