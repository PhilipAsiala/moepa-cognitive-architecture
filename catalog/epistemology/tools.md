# Epistemology Tools

## Executive Summary

These tool categories matter because they determine whether validation, explanation, and evidence remain under institutional control. Leaders should favor approaches that preserve inspectability and defensible reasoning over black-box convenience.

## Recommended Self-Hosted and Open Options

| Capability | Tools | Leadership Decision Lens |
| --- | --- | --- |
| Retrieval infrastructure | OpenSearch, Elasticsearch (self-managed), PGVector, Qdrant, Chroma | Keep indexes and source mappings inside controlled infrastructure so evidence remains exportable. |
| RAG orchestration (MCP-exposed) | LlamaIndex, Haystack (behind MCP servers); LangChain only as legacy facade | Retrieval and grounding policies must be inspectable, versioned, and reachable through MCP — not called directly from orchestrator glue code. |
| MCP integration | Model Context Protocol servers and facades | Epistemology capabilities (retrieval, verification, citation) exposed as MCP tools for governed orchestrator access. |
| Validation and guardrails | Guardrails AI, NeMo Guardrails, custom policy engines | Choose options that allow leadership and auditors to inspect how conclusions are checked. Guardrails AI is particularly strong for open, declarative constraints. |
| Experiment and model evaluation | MLflow (self-managed), Evidently, RAGAS, TruLens, Giskard | Reliability data should remain under enterprise control, not only in vendor dashboards. |
| Explainability and consistency | Captum, SHAP, custom consistency tests | Rationale artifacts should support audit, appeal, and oversight needs. |
| Cryptographic signing & integrity | Sigstore / cosign, in-toto | Use for signing model configs, data artifacts, and pipeline definitions so you can prove "this is exactly what was approved." |
| Audit / observability | OpenTelemetry + structured logging (Loguru, etc.) | Distributed traces and immutable logs are the backbone of E4 (Immutable Decision Audit Log). |

## Deployment Notes

- **For RAG**: LlamaIndex and Haystack both integrate well with self-hosted vector stores (Chroma, Qdrant) and self-hosted LLMs (Ollama, vLLM).
- **For output validation**: Guardrails AI is the leading open-source tool for defining and enforcing output schemas and constraints.
- **For audit logging**: OpenTelemetry is the open standard; integrates with most observability backends.
- **Air-gapped**: All the above can run without internet access when paired with self-hosted models and stores.

## Leadership Guidance

- Separate model output generation from verification decisions.
- Keep source-of-truth indexes and citation metadata exportable.
- Require signed evidence bundles for high-risk decisions.
- Cross-check validation choices against [Business Value](../../docs/business-value.md) and the [Owned-Brain Strategy](../ARCHITECTURE.md).
