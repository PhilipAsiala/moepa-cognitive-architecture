# Technical catalog

This is the builder tier. The business case is the [repository primer](../README.md) and the [briefs](../primer/). Open this directory after the ownership decision is clear.

The specification uses the same five names. Each one is anchored to the failure it is there to stop:

| Layer | Anchor | Catalog |
| :--- | :--- | :--- |
| **Metrology** | What was actually measured, with what uncertainty? | [Metrology](metrology/README.md) |
| **Ontology** | What do our terms mean, in a model we can export? | [Ontology](ontology/README.md) |
| **Epistemology** | Which claims are justified, and who may see them? | [Epistemology](epistemology/README.md) |
| **Praxeology** | Which workflow acts, and where is the human checkpoint? | [Praxeology](praxeology/README.md) |
| **Axiology** | Which encoded rule can refuse the action? | [Axiology](axiology/README.md) |

Planning may use a probabilistic model. Permission to act is deterministic. Axiology is that refusal. It is not a system prompt.

## Start here if you are implementing

1. [MOEPA Cognitive Architecture specification](ARCHITECTURE.md) — storage mapping, scoring rubric, and the tool patterns (Iceberg, Parquet, Polaris, organization-managed graphs, policy-as-code).
2. [Capability matrix](capability-matrix.md) — minimum capabilities tied to the score-3 baseline.
3. [Cross-layer compositions](cross-layer-compositions.md) — how the layers call one another.
4. [Architectural governance guidelines](../docs/MOEPA-Architectural-Governance-and-Evolution-Guidelines.md) — how the implementation is allowed to evolve.
5. [Data Substrate concept](../docs/Data-Substrate-Concept.md) — the owned library beneath the five layers.
6. [Diagrams](../diagrams/) — stack, information flow, and owned versus rented.

Tool choices are in each layer's `tools.md`. They are not required to understand the layer. Read the layer README first.
