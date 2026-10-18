# Owned vs. Rented AI: A Visual Comparison

A side-by-side architectural comparison of rented (vendor-dependent) vs. owned (sovereign) AI approaches across the MOEPA layers.

---

## The Two Architectures

```mermaid
graph LR
    subgraph RENT["❌ RENTED ARCHITECTURE\n(Vendor Dependency)"]
        direction TB
        R5["Axiology\nVendor guardrails\nNot inspectable\nCannot be verified"]
        R4["Praxeology\nVendor workflow engine\nAudit access limited\nBlack-box logic"]
        R3["Epistemology\nVendor confidence scores\nNo independent verification\nSource citations unavailable"]
        R2["Ontology\nVendor entity model\nDefinitions not owned\nCannot be exported"]
        R1["Metrology\nVendor data platform\nLineage controlled by vendor\nLock-in risk"]
        RDS[("Vendor Data Platform\nYour data in their systems\nExport may be limited\nAccess subject to contract")]
        R5 --- R4 --- R3 --- R2 --- R1 --- RDS
    end

    subgraph OWN["✅ OWNED ARCHITECTURE\n(Sovereign Brain)"]
        direction TB
        O5["Axiology\nPolicy-as-code (OPA)\nOrg-defined constraints\nRegularly tested"]
        O4["Praxeology\nOwned state machine (LangGraph)\nImmutable audit log\nHuman gates enforced"]
        O3["Epistemology\nOwned RAG via MCP server\nFact verification gates\nExact citations to substrate"]
        O2["Ontology\nOwned knowledge graph (Jena Fuseki / Neo4j)\nCanonical entity model\nVersion-controlled"]
        O1["Metrology\nSemantic ingestion → Proto-SPOs\nOpen-format lakehouse (Iceberg)\nFull provenance · MCP-exposed"]
        ODS[("Data Substrate\nOpen formats (Parquet/RDF)\nFull provenance + lineage\nOwned, portable, auditable")]
        O5 --- O4 --- O3 --- O2 --- O1 --- ODS
    end

    style RDS fill:#4a1a1a,color:#ffffff
    style R1 fill:#5a2a2a,color:#ffffff
    style R2 fill:#5a2a2a,color:#ffffff
    style R3 fill:#5a2a2a,color:#ffffff
    style R4 fill:#5a2a2a,color:#ffffff
    style R5 fill:#5a2a2a,color:#ffffff

    style ODS fill:#1a3a5c,color:#ffffff
    style O1 fill:#1a4a1a,color:#ffffff
    style O2 fill:#1a4a2a,color:#ffffff
    style O3 fill:#2a4a2a,color:#ffffff
    style O4 fill:#2a3a4a,color:#ffffff
    style O5 fill:#2a2a4a,color:#ffffff
```

---

## The Key Differences

*Illustrative positioning, not measured data. The placements express the design intent of each approach, not benchmarked results.*

```mermaid
quadrantChart
    title AI Architecture Quadrant: Sovereignty vs. Auditability
    x-axis Low Sovereignty --> High Sovereignty
    y-axis Low Auditability --> High Auditability
    quadrant-1 Ideal — Own and Audit
    quadrant-2 Can Audit, Cannot Own
    quadrant-3 Cannot Own, Cannot Audit
    quadrant-4 Own, But Cannot Audit
    Vendor Black-Box: [0.1, 0.1]
    Vendor with Audit API: [0.2, 0.55]
    Hybrid Transitional: [0.45, 0.5]
    Owned Open-Source Stack: [0.85, 0.85]
    Full MOEPA Owned Architecture: [0.92, 0.95]
```

---

## Layer-by-Layer Comparison Table

| Layer | Rented (Vendor) | Owned (MOEPA) | Migration Risk |
|---|---|---|---|
| **Data Substrate** | Vendor platform; export limited by contract | Open-format lakehouse (Iceberg/Parquet); fully portable | HIGH — historical data may not transfer |
| **Metrology** | Vendor manages quality rules and lineage | Organization-defined quality gates; full provenance records | HIGH — rules and history stay with vendor |
| **Ontology** | Vendor-defined entity model; schema not exportable; cloud-managed graph service (Neptune, Cosmos Gremlin) holds the only copy | Organization-owned knowledge graph (Jena Fuseki / Neo4j) rebuilt from the open-format record; version-controlled | HIGH — entity relationships may not transfer |
| **Epistemology** | Vendor confidence scores; no source access | Owned RAG; source-cited verification; confidence decomposed | MEDIUM — pipeline can be rebuilt with owned data |
| **Praxeology** | Vendor workflow engine; audit access limited | Owned state machine (LangGraph); immutable audit log | MEDIUM — workflow logic can be re-documented |
| **Axiology** | Vendor-provided guardrails; not inspectable | Policy-as-code (OPA); organization-defined; tested regularly | HIGH if rented — vendor guardrails cannot be exported; LOW once owned as Policy-as-Code |
| **Compute / Models** | Rented cloud compute + API-accessed models | Rented cloud compute + open-weight models (Llama, Mistral) | LOW — compute is commodity |

---

## When Renting Is Acceptable

Not all renting creates unacceptable risk. The decision depends on what is being rented:

```mermaid
flowchart TD
    Q1{"Does this vendor\ncontrol any of:\n- Your data\n- Your definitions\n- Your truth standards\n- Your decision logic\n- Your values/policy?"}

    Q1 -->|"YES"| Q2{"Is there a\ncontractual path to\nfull data/logic export?"}
    Q1 -->|"NO"| SAFE["✅ SAFE TO RENT\n(compute, infrastructure,\npre-trained model weights)"]

    Q2 -->|"YES with\nopen formats"| CONDITIONAL["⚠️ CONDITIONAL RENT\nAcceptable with:\n- Data portability clause\n- Audit access clause\n- Exit plan documented"]
    Q2 -->|"NO or unclear"| AVOID["❌ AVOID\nThis creates strategic\nlock-in. Require ownership\nbefore proceeding."]

    style SAFE fill:#1a4a1a,color:#ffffff
    style CONDITIONAL fill:#4a3a1a,color:#ffffff
    style AVOID fill:#4a1a1a,color:#ffffff
```

---

## The Long-Term Cost Curve

*Illustrative trajectory. Actual timing and magnitude depend on contract terms, team capacity, and the scale of adoption; the design has not yet produced measured cost data.*

| Year | Rented Architecture | Owned Architecture |
|---|---|---|
| Year 1 | Low cost; fast start; vendor manages complexity | Higher up-front investment; team capability building required |
| Year 2–3 | Vendor lock-in solidifying; switching cost rising | Compounding returns; data and logic assets accumulate value |
| Year 5+ | Vendor renewal leverage gone; costs and dependency high | Full sovereignty; costs declining; portable to any infrastructure |
| Oversight event | Cannot independently respond; dependent on vendor | Full audit capability from owned records |
| Policy change | Must request vendor update; timeline uncertain | Update owned policy-as-code; deploy immediately |

---

## Summary

> **The rented architecture is faster to start and slower to own.**  
> **The owned architecture is slower to start and faster to govern.**

For organizations with statutory audit obligations, long-term data custody requirements, and changing vendor landscapes, the owned architecture is the approach that keeps the ability to answer for a decision after the vendor relationship ends.

---

## Related Documents

- [Data Sovereignty Brief](../primer/data-sovereignty.md) — what the organization must be able to export when a contract ends
- [Enterprise Capability Matrix](../catalog/capability-matrix.md) — score any proposal on the 1–5 rubric
- [MOEPA Stack Diagram](moepa-stack.md) — full architecture diagram
