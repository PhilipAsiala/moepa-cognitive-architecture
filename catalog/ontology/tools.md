# Ontology Tools

## Executive Summary

These tool categories matter because they determine whether the organization owns its semantic model or leaves core institutional meaning embedded inside vendor products or isolated projects.

## Recommended Self-Hosted and Open Options

| Capability | Tools | Leadership Decision Lens |
| --- | --- | --- |
| Graph storage and querying | Neo4j (self-managed), JanusGraph, ArangoDB | Favor options that keep graph structures exportable and under institutional control. Neo4j is the most mature and widely supported choice for government knowledge graphs. |
| RDF and semantic web | Apache Jena, RDF4J, Blazegraph, Oxigraph | Standards-based options are useful when long-term interoperability and W3C compliance matter. |
| Vector + hybrid search (for RAG) | Chroma, Qdrant, Weaviate | Self-hosted vector stores keep embeddings under agency control rather than sending knowledge to vendor embedding APIs. |
| Ontology modeling / authoring | Protégé, (self-hosted TopBraid or similar) | Semantic definitions should be treated as governed institutional assets, not project artifacts. Protégé is the established open tool in government/academic settings. |
| NLP / entity extraction | spaCy + Prodigy, custom pipelines | Custom entity recognition for domain-specific terms should run inside controlled environments. |
| Graph ETL / integration | Apache Spark GraphFrames, Kafka Connect, Airflow | Build graph pipelines so source lineage and accountability remain visible. |

## Deployment Notes

- **Knowledge graphs**: Neo4j Community Edition is free and suitable for most government use cases.
- **RDF/SPARQL**: Apache Jena is the mature, battle-tested open-source option.
- **Vector search (self-hosted RAG)**: Chroma for lightweight needs; Qdrant for higher performance at scale.
- **Controlled vocabularies**: Use SKOS (W3C standard) for taxonomies and thesauri.

## Leadership Guidance

- Keep canonical entity definitions inside internal repositories.
- Require change governance for taxonomy and relationship updates.
- Export graph snapshots for continuity and portability.
- Cross-check major semantic decisions against [Business Value](../../docs/business-value.md) and the [Owned-Brain Strategy](../ARCHITECTURE.md).
