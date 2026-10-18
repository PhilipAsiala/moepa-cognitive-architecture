# MOEPA Capability Matrix

The MOEPA Capability Matrix provides a single governance view of the **minimum capability baseline** across the Philosophical AI Architecture. It is intended to help leaders set priorities, identify gaps before funding, and roadmap delivery without changing the existing five-layer scoring model.

This matrix explicitly binds the **minimum set of capabilities** for each scored layer to **Score 3 — Defined & Contained — Minimum Acceptable Standard** in the existing **1–5 plus GO / CONDITIONAL GO / NO-GO** rubric described in [ARCHITECTURE.md](ARCHITECTURE.md) (§4.2) and each layer's scoring guide. Capabilities that contribute to Scores 4 and 5 are the ones that lift a layer beyond the minimum baseline.

This file stores the **durable capability taxonomy**: what must exist, who owns it, and how it contributes to maturity. Live delivery progress belongs in JIRA under the Praxeology workflow, not in committed markdown. The JIRA references below are therefore **illustrative bindings only**, aligned to [Praxeology tools](praxeology/tools.md), not embedded status fields.

The matrix is part of the single [MOEPA Catalog](README.md), which also contains detailed capabilities, recommended tools, patterns, scoring guides, and [cross-layer compositions](cross-layer-compositions.md).

## Related References

- [Catalog overview](README.md) (single holistic source for capabilities, tools, patterns, scoring, and cross-layer)
- [Metrology capabilities](metrology/capabilities.md) and [Metrology scoring](metrology/scoring.md)
- [Ontology capabilities](ontology/capabilities.md) and [Ontology scoring](ontology/scoring.md)
- [Epistemology capabilities](epistemology/capabilities.md) and [Epistemology scoring](epistemology/scoring.md)
- [Praxeology capabilities](praxeology/capabilities.md) and [Praxeology scoring](praxeology/scoring.md)
- [Axiology capabilities](axiology/capabilities.md) and [Axiology scoring](axiology/scoring.md)
- [ARCHITECTURE.md](ARCHITECTURE.md) for the scoring rubric (§4.2) and the Data Substrate (§5.1)
- [Praxeology tools](praxeology/tools.md) for the JIRA and delivery-workflow binding

## How to Use This Matrix

1. Assess current capabilities layer by layer against the tables below.
2. Identify any missing **minimum set** rows; those gaps indicate a score below 3 and therefore a governance problem that must be remediated.
3. Prioritize the capabilities that close Score 3 gaps first, then sequence the Score 4 and Score 5 capabilities that strengthen reuse, measurability, and resilience.
4. Track live delivery work through JIRA epics and stories under the Praxeology workflow so execution status remains current without turning this catalog into a stale project tracker.

## Metrology

See [layer details](metrology/capabilities.md) and [scoring guide](metrology/scoring.md).

| Capability | Minimum set? (Score 3) | Maturity contribution (3 / 4 / 5) | Owner | Delivery tracking (illustrative: JIRA epic) |
| --- | --- | --- | --- | --- |
| Raw data ingestion and scalable compute for batch and streaming workloads | Yes | 3 — establishes a controlled internal data foundation for operational use | Data platform owner | Illustrative: JIRA epic for governed ingestion and compute onboarding |
| Structured storage with versioning and replay support (for example, Delta Lake patterns) | Yes | 3 — enables repeatable storage, replay, and controlled operational use | Data platform owner | Illustrative: JIRA epic for versioned storage and replay |
| Data catalog operations for centralized metadata and discovery | No | 4 — strengthens discoverability, reuse, and governance at scale | Data governance owner | Illustrative: JIRA epic for catalog and metadata operations |
| Schema enforcement, data quality checks, and validation gates | Yes | 3 — provides the defined quality controls expected at the minimum acceptable standard | Data quality owner | Illustrative: JIRA epic for schema and quality controls |
| Access control, lineage, provenance, and time-travel inspection | Yes | 3 / 4 / 5 — baseline lineage and access control support Score 3, while deeper provenance and inspection lift audit readiness | Data governance owner | Illustrative: JIRA epic for access, lineage, and provenance controls |
| Semantic document ingestion producing Proto-SPOs (no chainsaw chunking) | No | 4 — preserves document structure and semantic intent for governed corpora | Data platform owner | Illustrative: JIRA epic for semantic ingestion and MCP ingestion server |

## Ontology

See [layer details](ontology/capabilities.md) and [scoring guide](ontology/scoring.md).

| Capability | Minimum set? (Score 3) | Maturity contribution (3 / 4 / 5) | Owner | Delivery tracking (illustrative: JIRA epic) |
| --- | --- | --- | --- | --- |
| Entity modeling for customers, businesses, accounts, and related actors | Yes | 3 — establishes governable core entities for the mission domain | Domain ontology owner | Illustrative: JIRA epic for core entity modeling |
| Relationship mapping across legal, financial, and operational domains | Yes | 3 — defines governable institutional relationships across key domains | Domain ontology owner | Illustrative: JIRA epic for relationship mapping |
| Knowledge graph construction with hierarchy and taxonomy support | No | 4 — expands reuse and institutional consistency through richer semantic governance | Knowledge graph owner | Illustrative: JIRA epic for knowledge graph and taxonomy build-out |
| Semantic linking to connect meaning across heterogeneous datasets | Yes | 3 / 4 — provides shared meaning across governed sources and improves reuse across programs | Domain integration owner | Illustrative: JIRA epic for semantic linking across datasets |
| Advanced graph querying with dynamic relationship updates | No | 5 — supports enterprise-scale reasoning and continuously evolving semantic operations | Knowledge graph owner | Illustrative: JIRA epic for advanced graph query services |
| Controlled integration with Metrology outputs | Yes | 3 — keeps semantic assets grounded in governed source data | Data and ontology steward | Illustrative: JIRA epic for ontology-to-metrology integration |

## Epistemology

See [layer details](epistemology/capabilities.md) and [scoring guide](epistemology/scoring.md).

| Capability | Minimum set? (Score 3) | Maturity contribution (3 / 4 / 5) | Owner | Delivery tracking (illustrative: JIRA epic) |
| --- | --- | --- | --- | --- |
| Grounded retrieval (RAG) over trusted enterprise sources | Yes | 3 — anchors conclusions in trusted enterprise evidence | Knowledge assurance owner | Illustrative: JIRA epic for grounded retrieval controls |
| Inference engines tuned for auditable decision support | Yes | 3 — makes decision support reviewable instead of purely prompt-driven | Decision assurance owner | Illustrative: JIRA epic for auditable inference services |
| Model validation for reliability, drift, and failure detection | No | 4 — adds continuous reliability measurement and control | Model assurance owner | Illustrative: JIRA epic for validation, drift, and failure monitoring |
| Provenance tracking for conclusions and generated outputs | Yes | 3 — preserves evidence chains needed for review, audit, and appeal | Knowledge assurance owner | Illustrative: JIRA epic for provenance and evidence chains |
| Uncertainty handling with knowledge quality scoring | Yes | 3 / 4 — exposes uncertainty at the baseline and strengthens governance when standardized | Decision assurance owner | Illustrative: JIRA epic for uncertainty and quality scoring |
| Explanation generation and consistency checks across outputs | No | 5 — supports audit-grade defensibility and enterprise trust | Explainability owner | Illustrative: JIRA epic for explanation and consistency controls |

## Praxeology

See [layer details](praxeology/capabilities.md), [scoring guide](praxeology/scoring.md), and [tools](praxeology/tools.md).

| Capability | Minimum set? (Score 3) | Maturity contribution (3 / 4 / 5) | Owner | Delivery tracking (illustrative: JIRA epic) |
| --- | --- | --- | --- | --- |
| Agent frameworks for goal-oriented execution | No | 4 — provides a reusable control plane for multi-step automation | Automation platform owner | Illustrative: JIRA epic for agent orchestration platform |
| Workflow automation for repeatable business operations | Yes | 3 — establishes defined and reviewable operational flows | Workflow owner | Illustrative: JIRA epic for repeatable workflow automation |
| Decision engines combining rule-based and AI recommendations | Yes | 3 — keeps actions bounded by explicit decision logic | Decision workflow owner | Illustrative: JIRA epic for hybrid decision services |
| Action orchestration and goal decomposition across multi-step plans | Yes | 3 / 4 — supports governable multi-step execution and lifts maturity when standardized | Workflow owner | Illustrative: JIRA epic for orchestration and goal decomposition |
| Real-time execution controls with human-in-the-loop checkpoints | Yes | 3 / 4 / 5 — mandatory checkpoints satisfy the minimum, while stronger runtime controls and approvals lift higher | Operations control owner | Illustrative: JIRA epic for approvals, checkpoints, and stop conditions |
| Process optimization using telemetry and feedback loops | No | 4 / 5 — improves resilience and scaled operational performance | Process improvement owner | Illustrative: JIRA epic for workflow telemetry and optimization |

## Axiology

See [layer details](axiology/capabilities.md) and [scoring guide](axiology/scoring.md).

| Capability | Minimum set? (Score 3) | Maturity contribution (3 / 4 / 5) | Owner | Delivery tracking (illustrative: JIRA epic) |
| --- | --- | --- | --- | --- |
| Bias and fairness monitoring for model and workflow outcomes | No | 4 — makes governance measurable and reviewable over time | Responsible AI owner | Illustrative: JIRA epic for fairness monitoring |
| Policy and rule enforcement aligned to regulatory and compliance requirements | Yes | 3 — defines enforceable control boundaries at the minimum acceptable standard | Policy owner | Illustrative: JIRA epic for policy and rule enforcement |
| Ethical alignment scoring and strategic objective alignment | Yes | 3 — ties initiatives to explicit mission and value criteria | Governance board owner | Illustrative: JIRA epic for ethical and strategic alignment |
| Privacy controls for customer and sensitive enterprise data | Yes | 3 — provides mandatory data protection and compliance boundaries | Privacy owner | Illustrative: JIRA epic for privacy controls |
| Transparency and explainability requirements for accountable decisions | Yes | 3 / 4 — supports accountable decisions at the baseline and stronger oversight at higher maturity | Accountability owner | Illustrative: JIRA epic for transparency and explainability |
| Compliance frameworks and value-based prioritization criteria | No | 5 — institutionalizes durable review and portfolio governance | Compliance portfolio owner | Illustrative: JIRA epic for compliance framework and prioritization |

## Data Substrate (Unscored Owned Foundation)

The Data Substrate is the shared owned foundation beneath the five scored layers. It is **not** a sixth scored layer and does not change the 1–5 MOEPA rubric. Its role is to provide the shared representation, lineage, and portability backbone described in [ARCHITECTURE.md](ARCHITECTURE.md) (§5.1). The same column shape is retained here for governance consistency; in this section, the **Minimum set? (Score 3)** column should be read as **foundational applicability**, not as a scored threshold.

| Capability | Minimum set? (Score 3) | Maturity contribution (3 / 4 / 5) | Owner | Delivery tracking (illustrative: JIRA epic) |
| --- | --- | --- | --- | --- |
| Shared SPO/quad backbone with base-triple-once storage | Unscored foundation | Provides the common representation layer beneath all scored capabilities | Data substrate owner | Illustrative: JIRA epic for shared triple backbone |
| Open-format lakehouse and graph storage for owned facts and relationships | Unscored foundation | Preserves portability, replay, and sovereign control of the owned foundation | Data substrate owner | Illustrative: JIRA epic for lakehouse and graph foundation |
| Structural lineage, versioning, and replay across substrate assets | Unscored foundation | Enables auditable change history for cross-layer assets | Data platform owner | Illustrative: JIRA epic for structural lineage and versioning |
| Cross-layer metadata envelopes for metrology, epistemology, praxeology, and axiology | Unscored foundation | Lets each scored layer attach its own controls without duplicating the base fact | Data substrate owner | Illustrative: JIRA epic for cross-layer metadata envelopes |
| PROV-O-compatible provenance and metadata exchange | Unscored foundation | Supports interoperable lineage and review across tools and teams | Governance metadata owner | Illustrative: JIRA epic for provenance exchange |
| Federation and edge-to-cloud scaling across graph and lakehouse deployments | Unscored foundation | Supports cross-layer queries and scale from lightweight edge deployments to enterprise operations | Platform architecture owner | Illustrative: JIRA epic for federation and edge-to-cloud scale |
