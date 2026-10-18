# Data Substrate Capabilities (The Storage)

**The business problem:** When an organization stores its data, entity definitions, vector indexes, and decision logs inside a vendor's proprietary AI platform, it rents its own institutional memory. When the contract ends or the model changes, the organization cannot export what it knows or prove why past decisions were made.

**The capability pillar:** The **Data Substrate** is the organization-owned knowledge library beneath the five MOEPA layers. Every Agent reads from it and writes back to it. It is not a sixth scored layer on the intake rubric; it is the physical manifestation of what the organization owns across all five layers.

---

## Capability Summary

| ID | Capability | Primary MOEPA Layer | Business Outcome | Reference Stack Pattern |
| :--- | :--- | :--- | :--- | :--- |
| **DS1** | [Open-Format Lakehouse and Table Catalog](#ds1--open-format-lakehouse-and-table-catalog) | Metrology / Substrate | Tables and snapshots stay portable across clouds and engines | Apache Iceberg, Parquet, Apache Polaris |
| **DS2** | [Semantic Ingestion and Provenance Ledger](#ds2--semantic-ingestion-and-provenance-ledger) | Metrology | Raw documents and feeds become structured records with origin, timestamp, and error bounds | Docling / Unstructured (`Proto-SPO`), OpenLineage |
| **DS3** | [Canonical Entity Registry and Knowledge Graph](#ds3--canonical-entity-registry-and-knowledge-graph) | Ontology | One shared definition of "customer," "case," "asset," or "policy" across the enterprise | Neo4j / Neptune, RDF / JSON-LD, controlled vocabularies |
| **DS4** | [Owned Vector and Grounded Retrieval Index](#ds4--owned-vector-and-grounded-retrieval-index) | Ontology / Epistemology | Similarity search runs over owned records with source IDs and clearance tags attached | Self-hosted vector store (Qdrant / pgvector / Chroma) |
| **DS5** | [Cross-Layer Audit and Decision Ledger](#ds5--cross-layer-audit-and-decision-ledger) | Epistemology / Praxeology / Axiology | Tamper-evident history of every claim verified, workflow step approved, and policy rule applied | Append-only Iceberg ledger, cryptographic hashes, OPA bundles |
| **DS6** | [AI Demand Management and Asset Deduplication](#ds6--ai-demand-management-and-asset-deduplication) | Ontology / Governance | Proves a dataset, schema, or agent does not already exist before funding a duplicate | Catalog semantic search over registered entities and capabilities |

---

## DS1 — Open-Format Lakehouse and Table Catalog

- **What it does:** Stores enterprise tables, snapshots, and historical states in open table formats under an organization-controlled catalog, with role-based access and egress logging.
- **Enterprise risk it stops:** Hard vendor lock-in where historical data and feature tables cannot be read without paying a proprietary warehouse or SaaS platform.
- **Minimum standard (Score 3 baseline):** Core datasets are stored in exportable open formats (Parquet/CSV/JSON) with role-based access controls and audit logging; the team checks whether required data already exists on the enterprise platform before building a new pipeline.
- **Target maturity (Score 4–5):** Native open lakehouse (Apache Iceberg + Parquet) registered in a vendor-neutral catalog (Apache Polaris or equivalent), supporting time-travel replay, zero-trust egress monitoring, and zero copy across engines.

---

## DS2 — Semantic Ingestion and Provenance Ledger

- **What it does:** Parses unstructured documents (PDFs, policies, filings) along structural boundaries — tables, sections, citations — into **Proto-SPOs** (Sovereign Processing Objects) rather than fixed-token "chainsaw chunks," and stamps every ingested record with source provenance, collection timestamp, and quality status.
- **Enterprise risk it stops:** "Garbage-in at scale," where broken table rows or unverified feeds poison downstream RAG and agent decisions without a trace of where the bad data originated.
- **Minimum standard (Score 3 baseline):** Source system, collection date, and basic quality validation are recorded per batch; governed documents preserve section and citation boundaries.
- **Target maturity (Score 4–5):** Automated document-aware parsing pipelines with versioned configurations, cryptographic fingerprinting (SHA-256) of source artifacts, and PROV-O / OpenLineage provenance graphs from raw source to substrate write.

---

## DS3 — Canonical Entity Registry and Knowledge Graph

- **What it does:** Maintains a single authoritative registry of core business entities (customers, beneficiaries, legal entities, accounts, assets, policies), controlled vocabularies, and a queryable knowledge graph of how they relate across legal, financial, and operational domains.
- **Enterprise risk it stops:** Semantic silos — where Finance, Operations, and a vendor SaaS tool each define "active account" or "qualifying dependent" differently, producing conflicting AI decisions.
- **Minimum standard (Score 3 baseline):** Core domain entities, relationships, and code sets are documented in a governed dictionary with effective dates for schema changes.
- **Target maturity (Score 4–5):** Self-managed knowledge graph and SPO/quad store where each base fact is stored once, relationships are queryable at point-in-time effective dates, and domain stewards approve vocabulary changes aligned to policy updates.

---

## DS4 — Owned Vector and Grounded Retrieval Index

- **What it does:** Stores embeddings and retrieval indexes inside organization-controlled infrastructure, with every vector chunk bound to its canonical entity ID (`DS3`), source provenance (`DS2`), and access-control attributes.
- **Enterprise risk it stops:** Uploading sensitive enterprise documents into an external vendor's managed RAG box where embeddings cannot be audited, purged on schedule, or filtered by user clearance before retrieval.
- **Minimum standard (Score 3 baseline):** Retrieval index runs inside organization-controlled infrastructure and returns source citations for every retrieved passage.
- **Target maturity (Score 4–5):** Automated re-indexing when source records or policy effective dates change; pre-retrieval access control enforced against user clearance; every retrieved record resolves back to an immutable substrate ID.

---

## DS5 — Cross-Layer Audit and Decision Ledger

- **What it does:** Records an immutable, cross-referenced chain for every consequential transaction: the input measurement (`Metrology`), the entity version (`Ontology`), the retrieved evidence and confidence score (`Epistemology`), the workflow state and human approver (`Praxeology`), and the policy bundle version (`Axiology`). Also stores the versioned Policy-as-Code and constitutional baseline ("Golden Master").
- **Enterprise risk it stops:** Being unable to reconstruct for a regulator, auditor, inspector general, or customer *why* an automated system approved, escalated, or denied a case six months ago.
- **Minimum standard (Score 3 baseline):** Decision and workflow logs capture inputs, cited sources, outputs, policy checks, and human reviewer identity, retained per records policy.
- **Target maturity (Score 4–5):** Append-only, cryptographically signed ledger where all five layers attach metadata envelopes to the same base record without duplication, plus OS/infrastructure-locked policy baselines.

---

## DS6 — AI Demand Management and Asset Deduplication

- **What it does:** Uses the canonical entity registry (`DS3`) and capability catalog to search existing datasets, schemas, and agent workflows before a new AI project is funded.
- **Enterprise risk it stops:** Portfolio sprawl — funding ten teams to build ten separate document ingestion pipelines and ten overlapping customer schemas.
- **Minimum standard (Score 3 baseline):** Proposers check a shared inventory of existing datasets and capabilities by domain and taxonomy before intake scoring.
- **Target maturity (Score 4–5):** Mandatory semantic deduplication check against the knowledge graph and capability catalog at project intake, requiring documented proof that the capability does not already exist in the enterprise.

---

## Related Catalog Pages

- **[Enterprise Agent Capabilities](agents.md)** — the agents that read from and write to this Data Substrate (`AG1`–`AG6`)
- **[Enterprise Capability Matrix](capability-matrix.md)** — Score 3 baseline requirements and ownership for `DS1`–`DS6`
- **[End-to-End Business Compositions](cross-layer-compositions.md)** — how substrate and agent capabilities combine in production
- **[Technical Specification](ARCHITECTURE.md)** — §5 SPO/quad representation and incremental evolution path
