# Axiology Tools

## Executive Summary

These tool categories matter because they determine whether policy, privacy, fairness, and compliance controls are truly enforceable. Leaders should prefer options that keep control evidence inspectable and under institutional authority.

## Recommended Self-Hosted and Open Options

| Capability | Tools | Leadership Decision Lens |
| --- | --- | --- |
| Policy enforcement (as code) | Open Policy Agent (OPA), Gatekeeper, Kyverno, Conftest | Policy artifacts should be versioned, reviewable, and enforceable under institutional control. OPA is the de-facto standard for government and cloud-native environments. |
| Output / guardrail enforcement | Guardrails AI, LLM Guard | Open frameworks for defining and enforcing output structure, content constraints, and safety rules at runtime. |
| Prompt injection & security scanning | Rebuff, LLM Guard, Trivy (for configs/images) | Lightweight, self-hostable detection for the leading attack vector against LLM systems. |
| Fairness / bias measurement | Fairlearn, AI Fairness 360 (AIF360), Giskard | Open toolkits for measuring and mitigating systematic disparities; suitable for producing auditable reports. |
| Red-teaming / adversarial testing | Giskard, custom adversarial suites | Tools that help teams deliberately try to break guardrails and document the results. |
| Compliance evidence & GRC | OSCAL tooling, internal GRC platforms, SIEM integrations | Evidence should support audit and oversight without depending on external portals alone. |
| Privacy controls | Apache Ranger, HashiCorp Vault (self-hosted), internal tokenization / DLP | Privacy controls must remain inspectable and aligned to statutory obligations (Privacy Act, etc.). |

## Deployment Notes

- **Policy-as-code**: OPA + Rego is mature, widely adopted in government, and integrates with Kubernetes, API gateways, CI/CD, and application code.
- **Guardrails at inference time**: Guardrails AI can run in-process; combine with context separation for stronger constitutional patterns.
- **Bias & fairness**: Fairlearn and AIF360 produce the kinds of metrics and reports that oversight bodies expect.
- **Evidence**: Use OSCAL or equivalent structured formats so compliance artifacts are machine-readable and portable.

## Leadership Guidance

- Treat policy artifacts as first-class intellectual property.
- Store compliance evidence in enterprise systems, not vendor portals only.
- Align control mappings with organizational and statutory obligations.
- Cross-check governance controls against [Business Value](../../docs/business-value.md) and the [Owned-Brain Strategy](../ARCHITECTURE.md).
