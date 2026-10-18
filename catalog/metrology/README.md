# Metrology Catalog

**Metrology (what was actually measured):** uncalibrated sensors, unverified documents, and noisy feeds poison every decision that follows. This catalog is the measurement layer — source, time, and uncertainty — before anyone interprets the signal.

Metrology is the measurement and data foundation layer. It ensures data is ingestion-ready, quality-assured, versioned, governed, and discoverable before higher layers consume it.

## Executive Summary

Bottom line: if this layer is weak, no higher-layer AI investment is trustworthy. Organization leaders should view Metrology as the foundation for auditability, compliance, sovereignty, and defensible decision-making.

See the strategic rationale in [ARCHITECTURE.md](../ARCHITECTURE.md) and the investment framing in [Business Value](../../docs/business-value.md).

## Layer Scope

- Semantic document ingestion producing Proto-SPOs (no chainsaw chunking)
- Raw data ingestion and scalable compute
- Structured storage with versioning and time travel
- Data catalog and metadata operations
- Schema enforcement and quality validation
- Access control, lineage, and provenance
- MCP ingestion servers for governed orchestrator access

## Integration Points

- Below: infrastructure and storage systems
- Above: [Ontology](../ontology/README.md) consumes clean, governed datasets

## Leadership Lens

- Protects the organization from funding AI on unreliable data.
- Reduces vendor lock-in by preserving ownership of data, metadata, and lineage.
- Supports records management, privacy controls, and oversight review.

## File Guide

- [Capabilities](capabilities.md)
- [Tools](tools.md)
- [Patterns and Anti-Patterns](patterns.md)
- [Scoring](scoring.md)
- [Examples](examples/README.md)
