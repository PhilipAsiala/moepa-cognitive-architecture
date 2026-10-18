# Layered Architecture Diagram

This diagram is for readers who need the stack on one page before they score a proposal. It shows the MOEPA Cognitive Architecture as a flow from measurement up through shared meaning, verification, action, and value constraints. The practical effect of reading it this way is to see which question a weak layer fails.

The **Data Substrate** is the organization-owned knowledge library (in the technical design, an SPO/quad store plus a lakehouse — each fact kept once, in open formats). All five layers write to it and read from it. It is not a scored layer.

```mermaid
graph TD
    SUB[["Data Substrate<br/>(Set-Theoretic Backbone)<br/>SPO/Quad + Lakehouse<br/><i>shared storage — not a scored layer</i>"]]

    A[Metrology] --> B[Ontology]
    B --> C[Epistemology]
    C --> D[Praxeology]
    D --> E[Axiology]

    A --- A1[Measurements, telemetry, and evidence capture]
    A --- A2[Data quality, provenance, and observability]

    B --- B1[Entities, relationships, and domain boundaries]
    B --- B2[Shared schemas, concepts, and semantic structure]

    C --- C1[Truth evaluation, validation, and uncertainty handling]
    C --- C2[Inference rules, justification, and verification loops]

    D --- D1[Decision flows, orchestration, and agent execution]
    D --- D2[Feedback cycles, adaptation, and operational policy]

    E --- E1[Human values, ethics, and strategic priorities]
    E --- E2[Governance constraints, compliance, and acceptable outcomes]

    A -. stores into .-> SUB
    B -. stores into .-> SUB
    C -. stores into .-> SUB
    D -. stores into .-> SUB
    E -. stores into .-> SUB
```

## Reading Guide

- **Data Substrate** is the shared SPO/quad backbone and lakehouse that all five layers store into; it is the set-theoretic representation medium and is **not** a scored layer.
- **Metrology** establishes the empirical base by defining what is measured, how signals are captured, and how evidence quality is maintained.
- **Ontology** organizes reality into usable structures, including entities, relationships, boundaries, and shared semantic models.
- **Epistemology** determines what can be treated as knowledge through validation, reasoning, traceability, and uncertainty-aware verification.
- **Praxeology** translates knowledge into action through workflows, orchestration, decision logic, and adaptive execution.
- **Axiology** governs the entire stack through values, ethics, policy constraints, and definitions of acceptable outcomes.

## Why this is layered

The stack is intentionally cumulative:

1. **Metrology** provides the measurable inputs.
2. **Ontology** gives those inputs structure and meaning.
3. **Epistemology** tests whether the resulting claims are justified.
4. **Praxeology** uses justified knowledge to drive action.
5. **Axiology** evaluates whether those actions align with human and institutional values.

## Design implication for AI architecture

In an AI system, each layer answers a different question:

- **Metrology:** What are we observing?
- **Ontology:** What does it represent?
- **Epistemology:** How do we know it is true or reliable?
- **Praxeology:** What should the system do?
- **Axiology:** What should the system never violate, and what outcomes matter most?

Taken together, the diagram is not just a conceptual ladder; it is a control architecture for building AI systems that are measurable, structured, explainable, effective, and aligned.
