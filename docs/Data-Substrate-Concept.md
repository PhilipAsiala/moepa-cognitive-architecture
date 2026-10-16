# The Data Substrate: Your Organization's Unified Knowledge Library

> For leaders who need one place an audit can start, and for architects who design that place. The **Data Substrate** is the organization-owned knowledge library that all five MOEPA layers read from and write to — truth, values, rules, and lineage in open formats. It is not a scored layer. Owning it means a determination can be reconstructed from the organization's own records.

---

## The Core Idea

Imagine your organization's knowledge as a library. Five departments — measurement science, domain modeling, fact verification, workflow management, and ethics compliance — all need to use and contribute to that library. 

Without a shared library, each department keeps its own filing system and its own terminology. Cross-reference fails. An audit has to visit every system. When staff leave or vendors change, the record leaves with them.

The **Data Substrate** is the design for that shared library. It is a unified, open-format knowledge store that:
- Every MOEPA layer reads from to ground its work in organizational fact
- Every MOEPA layer writes to when it produces verified knowledge
- Carries full provenance, lineage, and version history for everything stored in it
- Is owned by your organization, in formats you can export without the vendor

---

## What the Data Substrate Contains

The Data Substrate holds four categories of organizational knowledge:

### 1. Facts and Observations (from Metrology)
Raw, quality-validated data records with full provenance:
- Who collected this data, from what source, at what time
- What quality checks it passed
- Whether it has been updated or superseded
- *Example:* An employer wage record, stamped with source system, collection date, validation status, and hash fingerprint

### 2. Entities and Relationships (from Ontology)
Structured representations of your domain's reality:
- Core entities (applicant, employer, household unit, dependent) with canonical definitions
- Relationships between entities (employer reported wages to applicant for program year)
- Version history of how definitions have evolved
- *Example:* The knowledge graph entry for "third-party income reporter" including all known relationships to applicants in the current program year

### 3. Verified Knowledge and Decisions (from Epistemology)
Claims that have been validated against evidence:
- Verified facts distinguished from model inferences
- Confidence levels and supporting evidence citations
- Audit trails for how a conclusion was reached
- *Example:* "Applicant 123's reported income is verified at 98.3% confidence against 4 independent third-party sources — see records A, B, C, D"

### 4. Workflow Events and Audit Records (from Praxeology and Axiology)
An immutable log of what the system did and why:
- Decision workflow executions with timestamps and approvals
- Human oversight checkpoints and outcomes
- Policy enforcement events (what was blocked and why)
- *Example:* "Audit flag triggered at 14:32 EST, reviewed by examiner ID 4471, approved for escalation — workflow state: ESCALATED"

---

## End State vs. Evolution Path

The repository draws a deliberate line between **what the substrate must become** and **how an agency gets there**.

### End state (imperative)

At maturity, every agency-owned Data Substrate **must** converge on this logical architecture:

- **SPO/quad as the universal representation** — every base fact stored once as a Subject–Predicate–Object triple (with context as a quad)
- **Layer metadata envelopes** — Metrology, Ontology, Epistemology, Praxeology, and Axiology attach their own metadata to the same base fact without duplication
- **SPO-centric hypergraph + lakehouse** — graph semantics and tabular storage federated as one queryable, auditable whole
- **Cross-layer queries** — e.g. high-confidence facts that satisfy axiological fairness and support praxeological auto-approval
- **Agency ownership throughout** — open formats, full provenance, point-in-time reconstruction

This is not optional at end state. A substrate that cannot represent facts as owned SPO/quad records with cross-layer envelopes does not meet the architectural target.

### Evolution path (allowed)

Agencies **evolve** toward that end state incrementally. Interim physical implementations are valid when they are **explicitly staged** and **SPO-compatible** (mappable to triples without loss of meaning):

| Stage | Typical implementation | End-state alignment |
|---|---|---|
| **1 — Foundation** | Inventory sources; define core entity model; establish provenance standards | Ownership and audit requirements locked in from day one |
| **2 — Lakehouse** | Iceberg/Parquet for validated tabular facts | Records use SPO-compatible schemas; triple mapping documented |
| **3 — Pilot graph** | Owned SPO triple store (or JSON triples + SQLite) for one domain | First domain converges to end-state logical model |
| **4 — Enterprise graph** | Property graph or RDF store integrated with lakehouse | Semantic layer matches SPO/quad backbone |
| **5 — Federation** | Trino, LangGraph router, or equivalent cross-plane query layer | Full hypergraph + lakehouse end state operational |

> **Rule of thumb:** Start where you are. Document the migration path. Every new dataset and AI project must move the institution closer to owned SPO/quad representation — not create another vendor silo.

### What is imperative from day one

Even before the full SPO hypergraph exists, these are non-negotiable:

- **Agency ownership** of the knowledge library (not a vendor platform)
- **Open, portable formats** with a documented export path
- **Provenance standards** for every record entering the substrate
- **A published roadmap** showing how current storage evolves to SPO/quad end state

---

## The SPO/Quad Data Model (End-State Logical Standard)

At end state, the Data Substrate uses a **Subject–Predicate–Object (SPO)** model, extended to a **quad** (four-part) model with a named context:

```
Subject       Predicate              Object              Context/Provenance
──────────    ──────────────────     ─────────────────   ──────────────────
Applicant:123 hasReportedIncome      $87,400             Source:WageReport_2024
Employer:ABC  reportedWagesFor      Applicant:123       ReportDate:2025-01-31
Claim:X47     hasConfidenceScore     0.983               VerifiedBy:EpisLayer_v2.1
```

This model allows:
- **Traversal:** "Show me all income sources for Applicant 123 and their verification status"
- **Provenance:** "Who recorded this fact, from what source, when?"
- **Versioning:** "What did we know about this entity on January 15th?"
- **Cross-layer queries:** "Show me all workflow decisions involving records with confidence below 0.9"

---

## Open Formats and Vendor Independence

The Data Substrate is designed using **open, non-proprietary formats** so your organization retains full ownership and portability:

| Component | Recommended Open Standard | What It Stores |
|---|---|---|
| **Lakehouse storage** | Apache Iceberg + Apache Parquet | Tabular facts, observations, metrics |
| **Knowledge graph** | RDF/SPARQL or property graph (Neo4j export) | Entities, relationships, ontology |
| **Document/blob storage** | Open object storage (S3-compatible, self-hosted) | Source documents, evidence artifacts |
| **Lineage and schema metadata** | Apache Atlas or an equivalent open metadata standard | Data lineage, schema, provenance |
| **Version control** | Git-compatible versioning | Schema changes, ontology versions |

> **Why open formats matter:** If your data is stored in a vendor's proprietary format, migrating away requires their cooperation. With open formats, you own an asset that can be moved to any infrastructure provider — or run on-premises — at any time.

---

## Semantic Ingestion and Proto-SPOs

Data enters the Data Substrate through **semantic ingestion** — not chainsaw
chunking. Document-aware parsers (Docling, Unstructured, or equivalent) preserve
structure, boundaries, and meaning from source documents.

Each parsed segment is a **Proto-SPO** (Sovereign Processing Object): a
self-contained unit that carries:

- **Provenance** — source document, parser version, ingestion timestamp
- **Structure** — headings, tables, sections, entity references preserved from the source
- **Semantic metadata** — document type, domain tags, entity linkages, confidence in parsing

Proto-SPOs are the ingestion-stage precursors to owned SPO/quad records. They
ensure semantic intent survives from source document through quality gates,
entity resolution, and retrieval — so Epistemology can cite exact evidence, not
reconstructed fragments.

Ingestion pipelines expose this capability through an **MCP ingestion server**
so orchestrators never call parsers or storage layers directly. See
[Architectural Governance and Evolution Guidelines](MOEPA-Architectural-Governance-and-Evolution-Guidelines.md).

---

## Provenance and Lineage: The Accountability Chain

Every record in the Data Substrate carries a **provenance record** answering four questions:

1. **Origin** — Where did this data come from? (source system, external reporter, internal process)
2. **Transformation** — What happened to it on the way in? (cleaning, normalization, validation)
3. **Validation** — What quality checks did it pass, and when?
4. **Custody** — Who has accessed, modified, or acted on it?

This provenance chain is what makes AI-assisted decisions **auditable and defensible**. When an oversight body asks "How did you reach this conclusion?", the answer is not "the model said so" — it is a traceable chain of evidence, transformations, and human approvals.

---

## Versioning: Knowledge That Evolves Correctly

The Data Substrate maintains **version history** for:
- **Ontology definitions** — when entity meanings or relationship structures change
- **Policy and guardrail configurations** — which version of compliance rules was active when a decision was made
- **Fact records** — when a source record is updated or corrected, the history is preserved
- **Model configurations** — which model version was used for which decisions

This enables **point-in-time reconstruction**: the ability to reproduce exactly what the system knew and how it reasoned at any historical moment. For benefits programs, regulatory enforcement, and high-stakes federal determinations, this is a legal and compliance necessity.

---

## The Substrate vs. a Vendor Data Platform

| Capability | Organization-Owned Data Substrate | Vendor Data Platform |
|---|---|---|
| Data portability | Full — open formats, self-hosted | Limited — vendor-dependent export |
| Provenance control | Complete organizational ownership | Vendor defines and controls lineage |
| Schema/ontology ownership | Yours | Typically vendor-defined |
| Audit access | Unrestricted, direct | Subject to vendor API and terms |
| Switching cost | Low — data moves with you | High — schema and history may not transfer |
| Compliance evidence | Produced by your systems | Dependent on vendor-supplied reports |

---

## What the Data Substrate Is Not

- **Not a data warehouse** — it is a knowledge store with semantics, provenance, and versioning, not just rows and columns
- **Not a vendor product** — it is an architectural pattern implemented with open tools
- **Not a scored MOEPA layer** — it is the shared foundation all layers depend on
- **Not optional** — without it, the five layers have no shared organizational memory, and the framework collapses into siloed tools

---

## Getting Started

A Data Substrate evolves toward the SPO/quad end state — it is not a single cutover event. A practical starting sequence:

1. **Inventory existing data sources** — what does your agency hold, where, in what format?
2. **Define your core entity model** — what are the 10–20 most important entities in your domain?
3. **Establish provenance standards** — what must be recorded for each incoming data record?
4. **Publish the evolution roadmap** — document how current storage maps to SPO/quad end state and by when
5. **Select open-format storage** — start with Iceberg/Parquet using SPO-compatible schemas; add a graph store as the pilot domain matures
6. **Integrate the MOEPA layers** — connect each layer to read from and write to the shared substrate, enriching records toward full metadata envelopes

---

## Related Documents

- [MOEPA 5-Layer Framework](MOEPA-5-Layer-Framework.md) — how each layer uses the substrate
- [Architectural Governance and Evolution Guidelines](MOEPA-Architectural-Governance-and-Evolution-Guidelines.md) — MCP-first rules and Proto-SPO requirements
- [Full Architecture Specification](../ARCHITECTURE.md) — technical design details
