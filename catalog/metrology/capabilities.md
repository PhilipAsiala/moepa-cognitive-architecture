# Metrology Capabilities

## What Leaders Need to Know

Bottom line: an organization that controls its data foundation can make more defensible decisions, withstand audit scrutiny, and avoid long-term dependency on external platforms.

See [ARCHITECTURE.md](../ARCHITECTURE.md) for the strategic rationale and [Business Value](../../docs/business-value.md) for the investment lens.

## Mission and Governance Outcomes

- Trustworthy decision-making based on governed source data.
- Better audit readiness through lineage, provenance, and replay.
- Reduced vendor lock-in by owning storage, metadata, and control boundaries.
- Stronger privacy and records-management posture for regulated workloads.

## What Metrology Covers

| Capability Domain | Description |
|---|---|
| **Data ingestion and validation** | Controls for what data enters the system and how it is checked |
| **Data quality measurement** | Ongoing measurement of completeness, accuracy, consistency, and freshness |
| **Provenance and lineage** | Tracking where data came from, how it was transformed, and who validated it |
| **Observability and monitoring** | Real-time visibility into data health, drift, and anomalies |
| **Storage and portability** | How data is stored to ensure ownership and long-term access |

## Core Capabilities

### M1 — Data Quality Rules Engine
**What it does:** Enforces defined quality rules at ingestion — completeness thresholds, format validation, range checks, referential integrity.

**Why it matters for government:** An income verification program relying on wage data with 15% null fields in the employer identifier column will produce systematically incorrect matches. Quality rules catch this before it propagates.

**Minimum acceptable standard (Score 3):** Basic rules exist for core fields; failures are logged and escalated.

**Good practice (Score 4–5):** Automated quality profiling on every ingestion batch; failures block downstream processing; quality metrics are published and tracked over time.

---

### M2 — Data Provenance Recording
**What it does:** Creates and maintains a record of each data item's origin, collection context, and transformation history.

**Why it matters for government:** When a constituent challenges a decision, the agency must demonstrate that the underlying data was collected lawfully, from an authorized source, and processed correctly. Provenance is the evidence chain.

**Minimum acceptable standard (Score 3):** Source system, collection date, and basic transformation steps recorded per record.

**Good practice (Score 4–5):** Cryptographic fingerprinting of source records; immutable audit log of all transformations; chain-of-custody from source to model input.

---

### M3 — Statistical Profiling and Drift Detection
**What it does:** Continuously measures the statistical properties of data (distributions, null rates, value ranges) and alerts when those properties change unexpectedly.

**Why it matters for government:** Model behavior can degrade silently when input data distributions shift — for example, when a third-party income reporter changes their reporting format. Drift detection catches this before it causes systematic errors.

**Minimum acceptable standard (Score 3):** Periodic profiling with manual review of major anomalies.

**Good practice (Score 4–5):** Automated continuous profiling; alerting on statistical drift with defined thresholds; trend tracking over time.

---

### M4 — Open-Format Data Storage
**What it does:** Stores all data in open, non-proprietary formats that can be read and migrated without vendor cooperation.

**Why it matters for government:** Proprietary data formats create hard lock-in. When a contract ends, you need your data — not a vendor's promise to provide an export.

**Minimum acceptable standard (Score 3):** Core data exportable in a standard format (CSV, JSON, Parquet).

**Good practice (Score 4–5):** All data stored natively in open-format lakehouse (Iceberg + Parquet); no proprietary format dependencies; self-hosted storage with full agency control.

---

### M5 — Data Access Controls and Egress Logging
**What it does:** Enforces who can access what data, and logs all access events for audit purposes.

**Why it matters for government:** Privacy Act, FOIA, and cybersecurity requirements all depend on knowing who accessed what data and when. Egress logging is the evidentiary foundation.

**Minimum acceptable standard (Score 3):** Role-based access control enforced; access logs available for audit.

**Good practice (Score 4–5):** Zero-trust access model; real-time egress monitoring; automated alerts on unusual access patterns; logs tamper-evident and retained per retention schedule.

---

### M6 — Agency Data Platform Availability Assessment
**What it does:** Prior to ingestion, determines whether the required source data is already available, governed, and staged within the agency's data platform (lakehouse or equivalent) or whether it must be newly provisioned or supplied by the mission program. This assessment directly informs ingestion timelines, cost, and risk.

**Why it matters for government:** Program-supplied data pipelines create hidden integration debt, duplicate storage, and delayed delivery. Explicitly checking platform availability enforces reuse of existing governed agency assets and prevents unnecessary data movement.

**Minimum acceptable standard (Score 3):** Basic statement of data source is provided.

**Good practice (Score 4–5):** Formal agency data platform availability check is completed and documented before project intake proceeds; data already present in the governed platform is used by default; program-supplied data is accepted only with explicit justification and timeline impact assessment.

---

### M8 — Semantic Document Ingestion (Proto-SPO)
**What it does:** Parses unstructured documents with document-aware semantic parsers, producing Proto-SPOs that carry provenance, structure, and semantic metadata before substrate write.

**Why it matters for government:** Regulatory documents, policy manuals, and case files lose meaning when split by token count. Semantic ingestion preserves tables, sections, and citations so Epistemology can return exact evidence — not reconstructed fragments.

**Minimum acceptable standard (Score 3):** Core document types parsed with structure preserved; each segment carries source provenance; no fixed-size-only chunking for governed corpora.

**Good practice (Score 4–5):** Full semantic parsing pipeline with versioned parser configs; Proto-SPO metadata schema documented; ingestion exposed as MCP server; segments map cleanly to SPO/quad end state.

---

### M7 — Post-Launch KPI Measurement and Objective Baselining
**What it does:** Establishes objective pre-launch performance and data quality baselines and implements a scheduled post-launch measurement program for model effectiveness, data drift, outcome KPIs (accuracy, equity, cost-per-transaction, throughput, compliance rates), and business impact.

**Why it matters for government:** Without post-launch baselining and measurement, leadership cannot determine whether an investment delivered the promised ROI or created unintended consequences. This capability closes the governance loop.

**Minimum acceptable standard (Score 3):** High-level commitment to measure outcomes after launch.

**Good practice (Score 4–5):** Pre-launch baselines are captured and recorded in the catalog; a documented post-launch KPI measurement schedule (with owners and reporting cadence) is in place; results feed back into Axiology ROI validation and future intake decisions.

---

## Capability Matrix

The matrix below binds the minimum set of Metrology capabilities to **Score 3 — Defined & Contained — Minimum Acceptable Standard** in the existing [Metrology scoring guide](scoring.md). Capabilities that contribute to Scores 4 and 5 lift the layer beyond that baseline. Live delivery status should be tracked through the [Praxeology workflow](../praxeology/tools.md); the JIRA epic column below is illustrative only.

| Capability | Minimum set? (Score 3) | Maturity contribution (3 / 4 / 5) | Owner | Delivery tracking (illustrative: JIRA epic) |
| --- | --- | --- | --- | --- |
| Raw data ingestion and scalable compute for batch and streaming workloads | Yes | 3 — establishes a controlled internal data foundation for operational use | Data platform owner | Illustrative: JIRA epic for governed ingestion and compute onboarding |
| Structured storage with versioning and replay support (for example, Delta Lake patterns) | Yes | 3 — enables repeatable storage, replay, and controlled operational use | Data platform owner | Illustrative: JIRA epic for versioned storage and replay |
| Data catalog operations for centralized metadata and discovery | No | 4 — strengthens discoverability, reuse, and governance at scale | Data governance owner | Illustrative: JIRA epic for catalog and metadata operations |
| Schema enforcement, data quality checks, and validation gates | Yes | 3 — provides the defined quality controls expected at the minimum acceptable standard | Data quality owner | Illustrative: JIRA epic for schema and quality controls |
| Access control, lineage, provenance, and time-travel inspection | Yes | 3 / 4 / 5 — baseline lineage and access control support Score 3, while deeper provenance and inspection lift audit readiness | Data governance owner | Illustrative: JIRA epic for access, lineage, and provenance controls |
| Agency data platform availability assessment prior to ingestion (M6) | No | 4 — prevents duplicate pipelines and accelerates delivery by preferring existing governed assets | Data platform owner | Illustrative: JIRA epic for platform data discovery and availability gating |
| Post-launch KPI measurement, objective baselining, and drift reporting | No | 4 / 5 — closes the governance loop by proving whether promised business outcomes and ROI were achieved | Data platform + Business owner | Illustrative: JIRA epic for KPI baseline capture and scheduled measurement program |
| Semantic document ingestion producing Proto-SPOs (M8) | No | 4 — preserves document structure and semantic intent for governed corpora | Data platform owner | Illustrative: JIRA epic for semantic ingestion and MCP ingestion server |

## Questions Leaders Should Ask Before Funding

- Is the authoritative data source internal, governed, and contractually controllable?
- Can the team show where every critical dataset came from and how it changed over time?
- Are data quality failures blocked before they affect downstream decisions?
- If the current platform or vendor changes, does the organization retain its data and metadata?

## Related

See also the layer overview in [Metrology README](README.md), [scoring guide](scoring.md), [tools](tools.md), and [patterns](patterns.md). Cross-layer interactions are described in [cross-layer-compositions.md](../cross-layer-compositions.md).
