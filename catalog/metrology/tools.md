# Metrology Tools

## Executive Summary

These tool categories matter because they determine whether the organization owns its data foundation or depends on external platforms for storage, metadata, and governance. Leaders should treat tool selection as a sovereignty decision, not just a procurement choice.

## Recommended Self-Hosted and Open Options

| Capability | Tools | Leadership Decision Lens |
| --- | --- | --- |
| Semantic document parsing | Docling, Unstructured, layout-aware PDF parsers | Produce Proto-SPOs with provenance and structure — never chainsaw chunks. Expose via MCP ingestion server. |
| Ingestion and orchestration | Apache Kafka, Apache NiFi, Airbyte, Apache Airflow | Prefer options that keep ingestion logic under institutional control and easy to inspect. |
| MCP integration | Model Context Protocol servers and facades | Standard interface for orchestrators; keeps ingestion logic portable across hosts. |
| Storage and versioning (lakehouse) | Apache Iceberg, Apache Hudi, Delta Lake, MinIO | Favor open formats (Iceberg + Parquet preferred) and portable storage so the data foundation can move without replatforming risk. |
| Catalog and metadata / lineage | Apache Atlas, DataHub, OpenMetadata, Amundsen, OpenLineage | Metadata ownership is strategic. Avoid making a vendor portal the only source of lineage truth. OpenLineage is the open standard for pipeline lineage. |
| Data quality | Great Expectations, Soda Core, Deequ | Quality controls should be enforceable and reviewable, not informal or hidden inside pipelines. Great Expectations is the most widely adopted open choice. |
| Access and governance | Apache Ranger, OPA (Open Policy Agent), Keycloak | Access decisions should be auditable and aligned to enterprise identity and policy controls. |

## Deployment Notes for Government

- **Air-gapped / high-sovereignty environments**: Apache Iceberg + Parquet + Great Expectations + OpenLineage can be run entirely on-premises with MinIO or equivalent object storage.
- **Lineage standard**: Adopt OpenLineage wherever possible — it integrates with Spark, dbt, Airflow, and most modern pipelines.
- **Catalog**: Apache Atlas for enterprise-grade open-source governance; DataHub or Amundsen for lighter-weight or more modern UI needs.

## Leadership Guidance

- Avoid vendor-only metadata lock-in for core datasets.
- Store schema and quality rules as code with review workflows.
- Require exportable lineage and provenance records.
- Cross-check high-impact choices against [Business Value](../../docs/business-value.md) and the [Owned-Brain Strategy](../ARCHITECTURE.md).
