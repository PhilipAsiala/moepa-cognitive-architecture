# Information Flow Across MOEPA Layers

How data, knowledge, verification, and agent decisions flow through the MOEPA Cognitive Architecture — from raw source data to a governed, auditable decision on the organization-owned Data Substrate.

---

## End-to-End Information Flow

```mermaid
flowchart TD
    SRC["External Sources\n(Third-party reporters, APIs,\ndocuments, sensor data)"]

    subgraph M["LAYER 1 — METROLOGY"]
        M0["Semantic Parsing\n(Docling / Unstructured)\n→ Proto-SPOs"]
        M1["Quality Gate\n(completeness, accuracy,\nformat validation)"]
        M2["Provenance Stamp\n(source, timestamp, hash,\nquality results)"]
        M3["Data Observability\n(drift detection, profiling,\nanomalies)"]
    end

    MCP["MCP Integration Layer\n(orchestrators discover\ntools here only)"]

    subgraph SUB["DATA SUBSTRATE (Shared)"]
        DS["Open-Format Lakehouse\n+ Knowledge Graph\n+ Audit Log\n(Iceberg / Parquet / Neo4j)"]
    end

    subgraph O["LAYER 2 — ONTOLOGY"]
        O1["Entity Resolution\n(link record to canonical entity)"]
        O2["Graph Enrichment\n(add relationships, context,\nrelated entities)"]
        O3["Vector Indexing\n(embed for semantic retrieval)"]
    end

    subgraph E["LAYER 3 — EPISTEMOLOGY"]
        E1["RAG Retrieval\n(retrieve owned evidence\nfor this query)"]
        E2["Fact Verification\n(compare inference against\nowned ground truth)"]
        E3["Confidence Scoring\n(evidence strength,\nsource quality, gaps)"]
    end

    subgraph P["LAYER 4 — PRAXEOLOGY"]
        P1["Workflow Gate\n(is this case in scope\nfor automated processing?)"]
        P2["Human Review Gate\n(required for confidence\n< 90% or escalation cases)"]
        P3["Action Execution\n(authorized action with\nfull audit logging)"]
    end

    subgraph A["LAYER 5 — AXIOLOGY"]
        A1["Policy Check\n(does this action comply\nwith all policies?)"]
        A2["Constitutional Filter\n(does output violate\nany inviolable constraint?)"]
        A3["Compliance Log\n(record policy status\nfor audit)"]
    end

    OUT["Governed Output\n(decision / recommendation /\naction with full audit trail)"]

    ORCH["AI Orchestrator\n(Bedrock / LangGraph /\nagent runtime)"]

    ORCH --> MCP
    MCP -. "tool calls" .-> E1
    MCP -. "tool calls" .-> P1
    MCP -. "tool calls" .-> A1

    SRC --> M0
    M0 --> M1
    M1 -->|"PASS"| M2
    M1 -->|"FAIL"| QUARANTINE["Quarantine +\nAlert + Escalation"]
    M2 --> M3
    M2 --> DS
    M3 --> DS

    DS --> O1
    O1 --> O2
    O2 --> O3
    O3 --> DS

    DS --> E1
    E1 --> E2
    E2 --> E3
    E3 --> DS

    E3 -->|"HIGH confidence (≥90%)"| P1
    E3 -->|"MEDIUM confidence (70-89%)"| P2
    E3 -->|"LOW confidence (<70%)"| ESCALATE["Escalation\nWorkflow"]

    P1 --> A1
    P2 --> A1
    A1 -->|"PASS"| A2
    A1 -->|"FAIL"| BLOCKED["Action Blocked\n+ Violation Log"]
    A2 -->|"PASS"| P3
    A2 -->|"FAIL"| BLOCKED
    P3 --> A3
    A3 --> DS
    P3 --> OUT

    style DS fill:#1a3a5c,color:#ffffff
    style OUT fill:#1a4a1a,color:#ffffff
    style BLOCKED fill:#4a1a1a,color:#ffffff
    style QUARANTINE fill:#4a3a1a,color:#ffffff
    style ESCALATE fill:#3a2a4a,color:#ffffff
```

---

## Key Handoffs Between Layers

### Metrology → Data Substrate → Ontology
Every record that passes Metrology's quality gate enters the Data Substrate with a provenance stamp. Ontology then resolves the record's entity references against the canonical entity model and enriches the record with graph context.

**What passes:** Quality-validated, provenanced data records  
**What gets added:** Entity linkage, relationship context, semantic embeddings

---

### Ontology → Data Substrate → Epistemology
Ontology's enriched records and vector embeddings are stored in the Data Substrate. Epistemology retrieves them during RAG and graph-augmented verification.

**What passes:** Enriched records with entity graph context  
**What gets added:** Verification results, confidence scores, source citations

---

### Epistemology → Praxeology
Epistemology's confidence score determines how Praxeology routes the case. This is the primary gate between "knowing" and "acting."

**Routing logic:**
- ≥ 90% confidence → automated workflow eligible
- 70–89% → human review required before action
- < 70% → escalation required; no automated action

---

### Praxeology → Axiology → Output
Every proposed action passes through Axiology's policy check and constitutional filter before execution. No action bypasses this check.

**What passes:** Proposed action + full context  
**What gets added:** Policy compliance status, constitutional check result, compliance log entry

---

## What the Data Substrate Stores After Each Layer

| Layer | Records Written to Substrate |
|---|---|
| Metrology | Quality-validated records with provenance stamps and quality metrics |
| Ontology | Entity linkages, relationship graph updates, vector index entries |
| Epistemology | Verification results, confidence scores, source citations, hallucination flags |
| Praxeology | Workflow state snapshots, human approval records, audit log entries |
| Axiology | Policy check results, constitutional filter outcomes, compliance log entries |

The Data Substrate accumulates a complete, immutable record of everything the system has observed, known, decided, and done.

---

## MCP Integration Boundary

AI orchestrators (Bedrock Agents, LangGraph routers, policy-governed agent runtimes)
discover and invoke layer capabilities **only through MCP** — never by calling
data, RAG, or workflow APIs directly. Semantic ingestion, retrieval,
verification, workflow steps, and policy checks are each exposed as MCP servers
or facades. See [Enterprise Agent Capabilities (`AG6`)](../catalog/agents.md#ag6--mcp-capability-bus-cross-cutting) and [ARCHITECTURE.md §5.2](../catalog/ARCHITECTURE.md).
