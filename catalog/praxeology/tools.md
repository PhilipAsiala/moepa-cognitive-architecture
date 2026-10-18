# Praxeology Tools

## Executive Summary

These tool categories matter because they determine whether workflow logic, approvals, and action histories remain under institutional control. Leaders should treat orchestration choices as accountability choices.

## Recommended Self-Hosted and Open Options

| Capability | Tools | Leadership Decision Lens |
| --- | --- | --- |
| MCP integration | Model Context Protocol servers and facades | Workflow steps and approvals exposed as MCP tools — orchestrators invoke Praxeology only through MCP, not direct engine callbacks. |
| Agent orchestration (state machines) | LangGraph, Temporal, CrewAI (self-hosted) | Favor options that make workflow state, approvals, and boundaries visible to oversight bodies. Expose steps as MCP tools behind the orchestration engine. |
| Workflow orchestration | Temporal, Camunda, Apache Airflow, Prefect, n8n (self-hostable) | Process definitions and audit trails should remain portable and reviewable. Temporal excels for long-running durable workflows; Camunda for BPMN-style governance. |
| Decision / rule engines | Drools, OpenL Tablets, OPA (Open Policy Agent) | Decision logic should be inspectable and not buried inside application code or prompts. |
| Human-in-the-loop / approvals | Internal approval services, Jira workflows, ServiceNow (with export), custom queues | Approval records should be identity-backed and easy to reconstruct in review. |
| Fine-grained authorization (tool scope) | OpenFGA / Zanzibar, OPA | Enforce "this agent in this state can call these tools on these entities" at the authorization layer. |
| Observability & tracing | OpenTelemetry, Prometheus, Grafana | Runtime traces should support operational review, policy review, and incident response. |

## Deployment Notes

- **Agentic workflows with human oversight**: LangGraph is the leading open-source library designed for stateful, graph-based, human-in-the-loop agent workflows.
- **Enterprise process governance**: Camunda is mature and widely used in government; strong BPMN + audit features.
- **Policy-as-code enforcement**: OPA can enforce both workflow rules and Axiology constraints in one place.
- **Long-running / durable execution**: Temporal is excellent when workflows must survive restarts and provide replay for audits.

## Leadership Guidance

- Keep workflow state and action logs in enterprise-controlled systems.
- Enforce tool allowlists and scoped credentials for agent calls.
- Require deterministic rollback strategies for critical flows.
- Cross-check orchestration choices against [Business Value](../../docs/business-value.md) and the [Owned-Brain Strategy](../ARCHITECTURE.md).
