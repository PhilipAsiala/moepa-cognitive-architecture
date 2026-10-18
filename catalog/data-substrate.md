# Data Substrate Capabilities (The Storage)

**The business problem:** When an organization stores its data, entity definitions, vector indexes, and decision logs inside a vendor's proprietary AI platform, it rents its own institutional memory. When the contract ends or the model changes, the organization cannot export what it knows or prove why past decisions were made.

**The capability pillar:** The **Data Substrate** is the organization-owned knowledge library beneath the five MOEPA layers. Every Agent reads from it and writes back to it. It is not a sixth scored layer on the intake rubric; it is the physical manifestation of what the organization owns across all five layers.

---

## Capability Summary

| ID | Capability | Primary MOEPA Layer | Business Outcome | Reference Stack Pattern |
| :--- | :--- | :--- | :--- | :--- |
| **DS1** | [Open-Format Lakehouse and Table Catalog](#ds1--open-format-lakehouse-and-table-catalog) | Metrology / Substrate | Tables and snapshots stay portable across clouds and engines | Apache Iceberg, Parquet, Apache Polaris |
| **DS2** | [Semantic Ingestion and Provenance Ledger](#ds2--semantic-ingestion-and-provenance-ledger) | Metrology | Raw documents and feeds become structured records with origin, timestamp, and error bounds | Docling / Unstructured (`Proto-SPO`), OpenLineage |
| **DS3** | [Canonical Entity Registry and Knowledge Graph](#ds3--canonical-entity-registry-and-knowledge-graph) | Ontology | One shared definition of "customer," "case," "asset," or "policy" across the enterprise | RDF / JSON-LD with an owned context document; Apache Jena Fuseki (SPARQL) or Neo4j as a projection of the record store; controlled vocabularies |
| **DS4** | [Owned Vector and Grounded Retrieval Index](#ds4--owned-vector-and-grounded-retrieval-index) | Epistemology | Similarity search runs over owned records with source IDs and clearance tags attached | Self-hosted vector store (Qdrant / pgvector / Chroma) rebuilt from embeddings persisted in the lakehouse |
| **DS5** | [Cross-Layer Audit and Decision Ledger](#ds5--cross-layer-audit-and-decision-ledger) | Epistemology / Praxeology / Axiology | Tamper-evident history of every claim verified, workflow step approved, and policy rule applied | Append-only Iceberg ledger, cryptographic hashes |
| **DS6** | [Enterprise Capability and Asset Registry](#ds6--enterprise-capability-and-asset-registry) | Ontology / Portfolio | A searchable inventory of every governed dataset, schema, agent, and prior intake decision, so duplicates are visible before they are funded | Catalog with semantic search over registered entities and capabilities |
| **DS7** | [Policy-as-Code and Constitutional Baseline](#ds7--policy-as-code-and-constitutional-baseline) | Axiology | The organization's rules, limits, and values exist as versioned, owned code that gates can enforce and auditors can read | OPA/Rego bundles, Cedar policies, signed "Golden Master" configuration |

---

## DS1 — Open-Format Lakehouse and Table Catalog

- **What it does:** Stores enterprise tables, snapshots, and historical states in open table formats under an organization-controlled catalog, with role-based access and egress logging. The lakehouse is the **only system of record** for the substrate: the graph store (`DS3`), vector index (`DS4`), and the policy engine's loaded bundle (`DS7`) are projections that can be emptied and rebuilt from it ([ARCHITECTURE.md §5](ARCHITECTURE.md)).
- **Enterprise risk it stops:** Hard vendor lock-in where historical data and feature tables cannot be read without paying a proprietary warehouse or SaaS platform; and a second "source of truth" quietly forming inside a graph or vector engine that cannot be audited against the record.
- **Minimum standard (Score 3 baseline):** Core datasets are stored in exportable open formats (Parquet/CSV/JSON) with role-based access controls and audit logging; every governed dataset is listed in the asset registry (`DS6`).
- **Target maturity (Score 4–5):** Native open lakehouse (Apache Iceberg + Parquet) registered in a vendor-neutral catalog (Apache Polaris or equivalent), supporting time-travel replay, zero-trust egress monitoring, and zero copy across engines. Table snapshot and manifest statistics (row counts, null counts, commit age) are exposed as first-class Metrology observations (`AG1`) rather than re-computed by a separate tool.

---

## DS2 — Semantic Ingestion and Provenance Ledger

- **What it does:** Parses unstructured documents (PDFs, policies, filings) along structural boundaries — tables, sections, citations — into **Proto-SPOs** (provenance-stamped semantic segments not yet normalized into Subject-Predicate-Object triples) rather than fixed-token "chainsaw chunks," and stamps every ingested record with source provenance, collection timestamp, and quality status.
- **Enterprise risk it stops:** "Garbage-in at scale," where broken table rows or unverified feeds poison downstream RAG and agent decisions without a trace of where the bad data originated.
- **Minimum standard (Score 3 baseline):** Source system, collection date, and basic quality validation are recorded per batch; governed documents preserve section and citation boundaries.
- **Target maturity (Score 4–5):** Automated document-aware parsing pipelines with versioned configurations, cryptographic fingerprinting (SHA-256) of source artifacts, and PROV-O / OpenLineage provenance graphs from raw source to substrate write.

---

## DS3 — Canonical Entity Registry and Knowledge Graph

- **What it does:** Maintains a single authoritative registry of core business entities (customers, beneficiaries, legal entities, accounts, assets, policies), controlled vocabularies, and a queryable knowledge graph of how they relate across legal, financial, and operational domains.
- **Enterprise risk it stops:** Semantic silos — where Finance, Operations, and a vendor SaaS tool each define "active account" or "qualifying dependent" differently, producing conflicting AI decisions.
- **Minimum standard (Score 3 baseline):** Core domain entities, relationships, and code sets are documented in a governed dictionary with effective dates for schema changes.
- **Target maturity (Score 4–5):** Self-managed knowledge graph and SPO/quad store where each base fact is stored once, relationships are queryable at point-in-time effective dates, and domain stewards approve vocabulary changes aligned to policy updates. The graph engine is a projection rebuilt from the record store (`DS1`), and the same open-source image runs on any Kubernetes; cloud-managed graph services (Amazon Neptune, Azure Cosmos Gremlin, Spanner Graph) are rented and may hold a projection but never the owned record.

---

## DS4 — Owned Vector and Grounded Retrieval Index

- **What it does:** Stores embeddings and retrieval indexes inside organization-controlled infrastructure, with every vector chunk bound to its canonical entity ID (`DS3`), source provenance (`DS2`), and access-control attributes.
- **Enterprise risk it stops:** Uploading sensitive enterprise documents into an external vendor's managed RAG box where embeddings cannot be audited, purged on schedule, or filtered by user clearance before retrieval.
- **Minimum standard (Score 3 baseline):** Retrieval index runs inside organization-controlled infrastructure and returns source citations for every retrieved passage.
- **Target maturity (Score 4–5):** Automated re-indexing when source records or policy effective dates change; pre-retrieval access control enforced against user clearance (the clearance-versus-marking rule itself is Policy-as-Code in `DS7`, applied here before any evidence reaches a model); every retrieved record resolves back to an immutable substrate ID. Embedding vectors are persisted in the lakehouse (`DS1`) keyed to the record ID and content fingerprint, so the live index can be emptied and rebuilt, an unchanged record is not re-embedded, and a failed rebuild is reported as an unhealthy service rather than served as stale results.

---

## DS5 — Cross-Layer Audit and Decision Ledger

- **What it does:** Records an immutable, cross-referenced chain for every consequential transaction: the input measurement (`Metrology`), the entity version (`Ontology`), the retrieved evidence and confidence score (`Epistemology`), the workflow state and human approver (`Praxeology`), and the policy bundle version applied (`Axiology`, referencing `DS7`).
- **Enterprise risk it stops:** Being unable to reconstruct for a regulator, auditor, inspector general, or customer *why* an automated system approved, escalated, or denied a case six months ago.
- **Minimum standard (Score 3 baseline):** Decision and workflow logs capture inputs, cited sources, outputs, policy checks, and human reviewer identity, retained per records policy. Every gate outcome is written — refusals as well as approvals — with the request ID, the record IDs consulted, the action requested, the caller's clearance, and the hash of the policy bundle in force (`DS7`).
- **Target maturity (Score 4–5):** Append-only, cryptographically signed ledger where all five layers attach metadata envelopes to the same base record without duplication. At Score 4 and above the gate **fails closed**: if the ledger write does not succeed, the action is not released. A gate that answers before its decision row has landed is a Score 3 posture and must be documented as such.

---

## DS6 — Enterprise Capability and Asset Registry

- **What it does:** Maintains the organization-owned inventory of governed datasets (`DS1`), document corpora (`DS2`), entity definitions (`DS3`), retrieval indexes (`DS4`), agent capabilities (`AG1`–`AG6`), and prior intake decisions (`DS5`), indexed by domain and taxonomy. The intake workflow (`AG4`, [ARCHITECTURE.md §4.4](ARCHITECTURE.md)) searches this registry as its first step; the registry is the asset, the deduplication check is the workflow that uses it.
- **Enterprise risk it stops:** Portfolio sprawl — funding ten teams to build ten separate document ingestion pipelines and ten overlapping customer schemas because nobody could see what already existed.
- **Minimum standard (Score 3 baseline):** A shared inventory of existing datasets, schemas, and agents exists, is searchable by domain, and is updated when a capability is funded or retired.
- **Target maturity (Score 4–5):** Registry entries are linked to canonical entities in the knowledge graph (`DS3`) and support semantic search; every funded capability carries a registry record and a documented non-duplication proof from intake.

---

## DS7 — Policy-as-Code and Constitutional Baseline

- **What it does:** Holds the organization's statutory, privacy, spending, ethics, and Rules-of-Engagement constraints as versioned, machine-enforceable policy (the "Golden Master"), owned by the organization and evaluated by the Policy Gate Agents (`AG5`) outside any model. This includes the classification ladder (for example `PUBLIC` < `CUI` < `CONFIDENTIAL` < `SECRET`) and the rule that a caller's clearance must meet a record's marking — the marking lives on the record's Axiology envelope, the rule lives here. Every policy version is signed or hashed so `DS5` can record exactly which rule set governed a decision; the engine evaluates the loaded bundle and never reads the lakehouse on the request path.
- **Enterprise risk it stops:** Compliance rules that live only in a system prompt or inside a vendor's uninspectable guardrails, where they can be bypassed by prompt injection, silently changed by the vendor, or lost when the contract ends.
- **Minimum standard (Score 3 baseline):** Core compliance rules are written as machine-checkable policy in a version-controlled repository the organization owns; changes require a documented approval.
- **Target maturity (Score 4–5):** Policy bundles are cryptographically signed, locked against edge or developer modification by OS or infrastructure controls, tested by scheduled adversarial red-teaming, and reviewed at the executive level alongside the quantified ROI and chargeback model.

---

## Related Catalog Pages

- **[Enterprise Agent Capabilities](agents.md)** — the agents that read from and write to this Data Substrate (`AG1`–`AG6`)
- **[Enterprise Capability Matrix](capability-matrix.md)** — Score 3 baseline requirements and ownership for `DS1`–`DS7`
- **[End-to-End Business Compositions](cross-layer-compositions.md)** — how substrate and agent capabilities combine in production
- **[Technical Specification](ARCHITECTURE.md)** — §5 SPO/quad representation and incremental evolution path
