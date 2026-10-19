# Brief 1: Data Sovereignty
### Owning the Data Substrate While Renting Commodity Models

**The Executive Risk:** Most organizations rent both the AI model and the meaning underneath it. When documents, entity definitions, vector embeddings, and audit logs live inside a vendor's proprietary platform, switching models or ending a contract strands the organization's institutional memory.

---

## How the Three Tiers Solve It

1. **MOEPA Cognitive Architecture (The Thesis):** Treats **Metrology** (*what we measured and where it came from*) and **Ontology** (*what our business entities mean and how they relate*) as non-negotiable ownership layers.
2. **Data Substrate (The Storage):** Stores all measurements, entity definitions, embeddings, and audit trails in open, vendor-neutral formats (`DS1`–`DS5`, `DS7`) inside organization-controlled infrastructure.
3. **Agents (The Engine):** Connects models and workflows to the Data Substrate through standardized **Model Context Protocol (MCP)** interfaces (`AG6`). Because Agents do not own the data or the schema, the underlying LLM can be swapped without rebuilding the business logic.

---

## Own the Brain, Rent the Muscles

Ownership means the ability to export, audit, and keep using the asset without a vendor's permission:

| Own Permanently (The Data Substrate) | Rent as a Commodity (Compute & Models) |
| :--- | :--- |
| **Open Lakehouse & Provenance (`DS1`, `DS2`):** Raw tables, `Proto-SPO` document segments, and lineage in Apache Iceberg / Parquet. | Cloud GPU capacity and inference clusters. |
| **Canonical Entity Registry & Graph (`DS3`):** The enterprise definition of a customer, case, account, asset, or policy. | Commercial frontier LLM APIs or interchangeable open-weight models. |
| **Owned Retrieval, Audit Ledger & Policy (`DS4`, `DS5`, `DS7`):** In-house vector indexes, the immutable record of every decision, and the policy rules that governed it. | Commodity object storage where formats and egress stay under your control. |

---

## Red Flags at Project Intake

A proposal fails the Data Sovereignty check (automatic **NO-GO** on Metrology or Ontology) if:

- Core entities ("customer," "beneficiary," "asset," "threat") are defined only inside a vendor's proprietary schema.
- Document chunks and embeddings are uploaded into an external SaaS RAG box the organization cannot audit or export.
- The team proposes building a duplicate data pipeline or schema without checking the enterprise asset registry first (`DS6`).

## Decision Checklist for Leaders

1. **Verify Substrate Reuse (`DS1`, `DS6`):** Does this proposal use existing governed data and entity definitions on the Data Substrate?
2. **Verify Portability (`DS1`–`DS4`, `AG6`):** If we turn off the model vendor tomorrow, do our tables, knowledge graph, vector index, and MCP tool contracts remain intact?
3. **Score the Proposal:** Require a **Score ≥ 3** on Metrology and Ontology in the [Enterprise Capability Matrix](../catalog/capability-matrix.md) before funding.

*Next: [Zero-Trust Governance](zero-trust-governance.md) · Builder specs: [Data Substrate Capabilities (`DS1`–`DS8`)](../catalog/data-substrate.md) · Diagram: [Owned vs. Rented](../diagrams/owned-vs-rented.md)*
