# Executive Briefs

These three briefs translate the repository's three core tiers into executive decisions on vendor risk, compliance, and investment:

1. **MOEPA Cognitive Architecture (The Thesis)** — The five governance layers (**M**etrology, **O**ntology, **E**pistemology, **P**raxeology, **A**xiology) and the **GO / CONDITIONAL GO / NO-GO** intake scorecard.
2. **Data Substrate (The Storage)** — The organization-owned library (`DS1`–`DS7`) where data, entity definitions, verified claims, audit logs, and policy rules live in open formats.
3. **Agents (The Engine)** — The specialized workflows and deterministic gates (`AG1`–`AG6`) that consume the Data Substrate to run the business.

| Brief | Core Question | Primary Focus |
| :--- | :--- | :--- |
| **[1. Data Sovereignty](data-sovereignty.md)** | *What happens when we change models or leave a vendor?* | Owning the **Data Substrate** (`DS1`–`DS3`, `DS6`) while renting commodity compute. |
| **[2. Zero-Trust Governance](zero-trust-governance.md)** | *How do we stop hallucinations, data leaks, and rogue actions?* | Bounding probabilistic **Agents** with deterministic verification (`AG3`), human checkpoints (`AG4`), and Policy-as-Code (`AG5`). |
| **[3. Investment & ROI](roi.md)** | *Are we buying another disposable tool, or building a compounding asset?* | Scoring proposals (`GO` / `CONDITIONAL GO` / `NO-GO`) on reusable **Data Substrate** and **Agent** capabilities. |

For the concrete builder specifications behind these briefs, continue to the **[Enterprise Capability Catalog](../catalog/)** or view the **[Architecture Diagrams](../diagrams/)**.
