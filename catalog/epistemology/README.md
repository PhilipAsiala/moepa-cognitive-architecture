# Epistemology Catalog

**Epistemology (truth and permission):** the failure mode is a fluent answer treated as a fact, or a restricted record shown to the wrong person. This catalog is how a claim is tied to a source the organization can check, and how access is decided before reasoning begins.

Epistemology is the truth and verification layer. It ensures model outputs are grounded, validated, explainable, and traceable to trusted sources.

## Executive Summary

Bottom line: this layer separates what the model guessed from what the organization can defend. Organization leaders should care because stakeholder trust, auditability, and appeals depend on it.

See the strategic rationale in [ARCHITECTURE.md](../ARCHITECTURE.md) and the investment framing in [Business Value](../../docs/business-value.md).

## Layer Scope

- Grounded retrieval and inference (exposed via MCP servers — not direct orchestrator calls)
- Model validation and reliability checks
- Provenance tracking for conclusions with exact citations to owned substrate records
- Uncertainty handling and quality scoring
- Explanation generation and consistency checks

## Integration Points

- Below: [Ontology](../ontology/README.md) supplies semantic context and relationships
- Above: [Praxeology](../praxeology/README.md) consumes verified outputs for action workflows

## Leadership Lens

- Prevents black-box conclusions from driving public decisions.
- Improves audit and review posture by preserving evidence and explanations.
- Helps leadership distinguish between experimental AI and decision-ready AI.

## File Guide

- [Capabilities](capabilities.md)
- [Tools](tools.md)
- [Patterns and Anti-Patterns](patterns.md)
- [Scoring](scoring.md)
- [Examples](examples/README.md)
