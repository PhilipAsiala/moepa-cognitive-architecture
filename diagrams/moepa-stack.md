# MOEPA Stack Diagram

The five layers of the MOEPA Cognitive Architecture, backed by the organization-owned Data Substrate and executed by governed Agents.

---

## Full Stack with Data Substrate

```mermaid
graph TB
    subgraph STACK["MOEPA Cognitive Architecture"]
        direction TB

        A5["━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\n  LAYER 5 — AXIOLOGY\n  Values · Ethics · Mission Alignment\n  Policy enforcement · Guardrails\n  Constitutional constraints\n━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━"]

        A4["━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\n  LAYER 4 — PRAXEOLOGY\n  Decision Workflows · Human Oversight\n  State machines · Audit trails\n  Tool scope enforcement\n━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━"]

        A3["━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\n  LAYER 3 — EPISTEMOLOGY\n  Truth & Verification · Owned RAG\n  Confidence scoring · Fact-checking\n  Hallucination detection\n━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━"]

        A2["━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\n  LAYER 2 — ONTOLOGY\n  Structured Knowledge · Entity Model\n  Knowledge graph · Embeddings\n  Semantic consistency\n━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━"]

        A1["━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\n  LAYER 1 — METROLOGY\n  Data Quality · Provenance\n  Measurement · Observability\n  Open-format storage\n━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━"]

        SUB[["══════════════════════════════════════\n  DATA SUBSTRATE\n  Unified Knowledge Library\n  SPO/Quad + Open Lakehouse (Iceberg/Parquet)\n  Provenance · Versioning · Lineage\n  (shared foundation — all layers read/write here)\n══════════════════════════════════════"]]
    end

    A5 --> A4 --> A3 --> A2 --> A1 --> SUB
    A1 -. reads/writes .-> SUB
    A2 -. reads/writes .-> SUB
    A3 -. reads/writes .-> SUB
    A4 -. reads/writes .-> SUB
    A5 -. reads/writes .-> SUB

    style SUB fill:#1a3a5c,color:#ffffff,stroke:#4a90d9
    style A1 fill:#2d4a2d,color:#ffffff,stroke:#5a9a5a
    style A2 fill:#3a4a2d,color:#ffffff,stroke:#7a9a5a
    style A3 fill:#4a3a2d,color:#ffffff,stroke:#9a7a5a
    style A4 fill:#4a2d3a,color:#ffffff,stroke:#9a5a7a
    style A5 fill:#3a2d4a,color:#ffffff,stroke:#7a5a9a
```

---

## Layer Definitions at a Glance

| Layer | Philosophical Discipline | AI Governance Role | Core Tool Examples |
|---|---|---|---|
| **5 — Axiology** | Study of value and ethics | What the system must never do; what it must preserve | Open Policy Agent, Guardrails AI, LLM Guard |
| **4 — Praxeology** | Study of purposeful action | How the system acts; who approves; what is logged | LangGraph, Temporal, Camunda, OPA |
| **3 — Epistemology** | Study of knowledge and truth | What counts as a verified fact vs. inference | LlamaIndex, Guardrails AI, RAGAS, TruLens |
| **2 — Ontology** | Study of being and relationships | What entities exist; how they relate; what terms mean | Neo4j, Apache Jena, Chroma, Qdrant |
| **1 — Metrology** | Study of measurement | What data is trusted; how quality is assured; where it came from | Great Expectations, Apache Iceberg, OpenLineage |
| **Data Substrate** | *(architectural pattern)* | Shared knowledge library; owned by the organization | Iceberg + Parquet + Neo4j + Atlas |

---

## The Governance Property of the Stack

The stack is **cumulative**: each layer builds on the reliability of the layer below it.

- If **Metrology** is weak, the entire stack is built on untrustworthy data
- If **Ontology** is weak, Epistemology cannot verify facts because the entity model is inconsistent
- If **Epistemology** is weak, Praxeology is taking action based on unverified claims
- If **Praxeology** is weak, Axiology constraints are applied to an uncontrolled execution environment
- If **Axiology** is weak, the system may optimize for the wrong objectives even while all other layers function

This is why the [Enterprise Capability Matrix](../catalog/capability-matrix.md) and [ARCHITECTURE.md §4.2](../catalog/ARCHITECTURE.md) use the **lowest layer score** as the overall recommendation — not an average.

**Cross-cutting integration:** AI orchestrators access layer capabilities only through the **Model Context Protocol (MCP)** — not vendor glue code or direct data/RAG API calls. Semantic ingestion produces **Proto-SPOs** before records enter the substrate. See [ARCHITECTURE.md §5.2](../catalog/ARCHITECTURE.md).
