# Glossary

## Business First

The repository's primary communication rule: MOEPA philosophical disciplines describe **business outcomes** leaders must own (trusted data, shared meaning, verifiable truth, governed action, enforced values). Technical implementation detail belongs in builder-tier documents (`catalog/ARCHITECTURE.md` and the governance guidelines). See [pitch strategy §0](pitch-strategy.md), including the readability standard that applies to every page.

## Core Terms: Thesis, Storage, Engine

The repository uses three core terms rather than separate labels for the executive frame, the intake rubric, and the technical specification:

- **MOEPA Cognitive Architecture (the thesis)** — the five-layer separation of concerns (Metrology, Ontology, Epistemology, Praxeology, Axiology) and the intake scorecard (1–5 per layer, **GO**, **CONDITIONAL GO**, **NO-GO**). Leader guides use it to decide ownership; [ARCHITECTURE.md](../catalog/ARCHITECTURE.md) specifies how to build it.
- **Data Substrate (the storage)** — the organization-owned knowledge library where truth, definitions, values, rules, and lineage are stored in open, portable formats. All five layers read from and write to it; it is not a sixth scored layer.
- **Agents (the engine)** — the models and workflows that consume the Data Substrate to propose and execute work across the layers, bounded by deterministic verification (Epistemology) and policy gates (Axiology).

## Cognition, Affect, Conation

The three human cognitive functions the MOEPA Cognitive Architecture maps into software:

- **Cognition** (knowing) — how the system defines and verifies reality → Metrology, Ontology, Epistemology
- **Affect** (valuing) — how the system encodes what matters and what is forbidden → Axiology
- **Conation** (acting) — how the system executes decisions under oversight → Praxeology

## Philosophy vs. Psychology (in the stack)

- **Philosophy** — the operating system of cognition: strict logical rules for defining reality and truth (Metrology, Ontology, Epistemology).
- **Psychology** — the mechanics of behavior: how values and execution drives steer the engine (Axiology, Praxeology).

## Data Substrate (Set-Theoretic Backbone)

The agency-owned knowledge library — the cross-cutting representation medium where truth, values, rules, and lineage live in open, portable formats. At end state: an SPO/quad backbone plus federated lakehouse storage that all five MOEPA layers read from and write to. The substrate holds each base fact once; every layer attaches its own metadata envelope without duplicating the base triple. Explicitly **not** a sixth scored layer. Agencies evolve toward end state incrementally; see [Substrate Evolution Path](#substrate-evolution-path).

## Substrate End State

The imperative logical target for a mature Data Substrate: owned SPO/quad representation, one base fact per triple, layer metadata envelopes, SPO-centric hypergraph + lakehouse federation, and cross-layer queryability. Not optional once the substrate is considered enterprise-ready.

## Substrate Evolution Path

The allowed incremental journey from current agency storage to Substrate End State — typically lakehouse (SPO-compatible schemas) → pilot triple store → enterprise graph → federation layer. Interim implementations are valid when agency-owned, open-format, provenance-complete, and backed by a documented migration roadmap.

## SPO Triple / Quad

At end state, the universal structural unit of the Data Substrate: a Subject-Predicate-Object triple (or quad, when a context/graph identifier is added as a fourth element). Example: `(IncomeVerification:TX12345, hasAmount, 85000)`. Earlier evolution stages must maintain SPO-compatible mapping so records can converge to this form without semantic loss.

## MOEPA

The acronym for the five layers of the MOEPA Cognitive Architecture:

- Metrology: measurement, telemetry, and data foundation
- Ontology: structured reality and knowledge representation
- Epistemology: truth, verification, and justification
- Praxeology: purposeful action and workflow governance
- Axiology: value, ethics, and policy alignment

## Agents

The execution engine of the architecture: the workflows and models that read the Data Substrate, propose plans in Praxeology, and remain subject to deterministic verification (Epistemology) and policy refusal (Axiology).

## Owned Brain

The organization owns its Data Substrate, semantic models, validation rules, and policy controls — rather than outsourcing them to a vendor.

## Rented Compute

Commodity infrastructure (GPUs, clusters, cloud capacity, commercial LLM APIs) that the organization rents while retaining sovereignty over the cognitive layers and Data Substrate.

## Golden Master

A locked configuration baseline used in the axiological layer to preserve policy and prevent easy modification.

## Cognitive Control Plane

The combined governance surface — MOEPA Cognitive Architecture intake scoring and Data Substrate ownership — that lets leadership govern AI agents without relying on standard IT infrastructure metrics alone.

## Model Context Protocol (MCP)

The standardized interface for all data and tool access in the MOEPA Cognitive Architecture. MCP keeps capabilities portable across orchestration hosts (Bedrock, self-hosted runtimes, or equivalent) and prevents vendor-locked glue code from becoming the integration layer.

## MCP Server

An MCP-compliant service that exposes a governed capability — ingestion, retrieval, workflow step, policy check — with a stable tool contract. New capabilities are defined as MCP servers so execution logic remains inspectable and host-independent.

## MCP Facade

A thin MCP wrapper around a legacy or high-throughput API. Used when direct integration is required for performance, but orchestrators must still discover and govern the capability through MCP rather than calling the underlying API directly.

## Proto-SPO (Sovereign Processing Object)

A semantically parsed document segment that carries its own provenance, structure, and context — not a naive text chunk. Proto-SPOs are the ingestion-stage precursors to owned SPO/quad records on the Data Substrate. They preserve semantic intent from source document through retrieval and verification.

## Semantic Ingestion

Document-aware parsing during data ingress (for example: Docling, Unstructured, or equivalent) that produces Proto-SPOs with provenance and structural metadata. Explicitly excludes "chainsaw chunking" — fixed-size splits that discard document structure and semantic boundaries.