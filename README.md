# The MOEPA Cognitive Architecture
### A Business and Architectural Primer for Deterministic, Sovereign Enterprise AI

Modern enterprise AI has an architecture problem. Organizations plug probabilistic large language models directly into sensitive data and enterprise APIs, and hope that prompt wording plus a thin guardrail will prevent hallucinations, compliance violations, and data leakage.

In high-stakes environments — defense, finance, healthcare, and critical infrastructure — **"mostly accurate" is an operational failure.**

The **MOEPA Cognitive Architecture** is a separation of concerns for AI systems. It borrows five disciplines from classical philosophy. Each discipline is a question the organization must be able to answer before a system is allowed to act. The names stay, because each name is a different owner, a different failure, and a different control.

This repository is a draft decision frame, not a deployed system. The practical output is an intake decision: **GO**, **CONDITIONAL GO**, or **NO-GO**, with the evidence and the gaps written down.

> **Own the brain. Rent the muscles.** Own the data, the definitions, the verification rules, the workflows, and the policy constraints. Rent compute and commercial models when those owned layers stay under organizational control.

---

## Why these words

Ambiguous product language produces brittle systems. When a vendor folds ingestion, search, guessing, and execution into one box called "agentic AI," the organization cannot say which part failed, or which part it still owns.

MOEPA keeps the five questions separate. If a system fails, the record shows which layer broke.

| MOEPA pillar | The plain question | The business function | What fails without it |
| :--- | :--- | :--- | :--- |
| **1. Metrology** | What did we actually measure? | Sensory and telemetry ingestion. Raw signals, uncertainty, and provenance, recorded before interpretation. | Uncalibrated sensors, unverified documents, and noisy inputs poison later decisions. |
| **2. Ontology** | What do these things mean, and how do they relate? | Enterprise meaning. Shared definitions and relationships the organization can export. | Every team defines "customer," "asset," or "threat" differently. A proprietary schema holds the definitions. |
| **3. Epistemology** | How do we know this is true, and who is allowed to know it? | Truth checks and context routing. Source, corroboration, and access, before the system reasons. | A rumor or a stale document is treated as fact, or a restricted record reaches the wrong person. |
| **4. Praxeology** | What action are we taking, and toward what goal? | Intent and execution. Verified context becomes a workflow, a tool call, or a task, with a human checkpoint where the action is consequential. | Agents loop, call the wrong interface, or optimize the wrong metric. |
| **5. Axiology** | Should we do this? | Policy and value, enforced outside the model. | A system prompt is asked to enforce a statute, a spending limit, or a safety rule. |

---

## Probabilistic power, deterministic law

Large language models are probabilistic. They continue a pattern. They do not keep a statute. Enterprise compliance is deterministic. A written rule is followed or it is broken.

| | Probabilistic | Deterministic |
| :--- | :--- | :--- |
| **What it does** | Drafts, summarizes, ranks, proposes | Measures, checks a source, allows or refuses an action |
| **Where MOEPA uses it** | Praxeology may call a model to propose a plan | Metrology records the measurement. Epistemology checks the claim. Axiology refuses a plan that breaks an encoded rule |
| **What leaders should not do** | Treat a fluent answer as a fact | Ask the model to police itself |

Praxeology can spend a small local model, or ordinary code, on a routine step, and reserve a larger model for synthesis. Axiology does not "usually" allow an action. When the rule is encoded and the action must pass the gate, a violation is blocked. A rule that was never written is not enforced. The gate does not repair a bad measurement from an earlier layer.

---

## The five pillars

### 1. Metrology: the science of measurement

Before a system can think, it has to observe. Metrology ingests a raw signal — an edge camera, a financial feed, a user prompt — and attaches the metadata a later audit will need: when it was captured, by what source, and with what uncertainty.

The operational effect is that raw input is not trusted by default. Model output and telemetry are measurements with error, not facts. Noise can be stopped before it is written into the organization's record.

### 2. Ontology: the architecture of meaning

An ontology is the shared vocabulary of the organization. It names what exists — people, systems, transactions, policies — and how those things connect, without depending on one vendor's labels.

The operational effect is data the organization can leave with. Definitions live in an open model the organization owns. Swapping a model or a cloud provider does not, by itself, rebuild institutional meaning, provided the definitions were never stored only inside the vendor product. If export terms are missing, the lock-in returns.

### 3. Epistemology: the standard of truth

Language models are fluency engines. Epistemology is the gate that asks where a claim came from, whether another owned source agrees, and whether this user may see it.

The operational effect is an auditable analyst rather than a closed guess. Each assertion that the organization will rely on points at a source it can open. That is how hallucination risk is cut in decision support: unsupported text does not become a record. It does not make a model incapable of being wrong.

### 4. Praxeology: the logic of action

Praxeology is purposeful action. Here it is the layer that takes verified context and routes it to a tool, a workflow, or a model in order to finish a concrete job.

The operational effect is a bounded spend and a named owner for the action. Routine steps stay in deterministic workflow. Heavy compute is reserved for work that needs it. Consequential actions keep a human checkpoint. The repository does not claim a measured savings figure. What it does specify is a workflow the organization can stop, audit, and reuse.

### 5. Axiology: value and law, outside the model

Axiology is value, ethics, and rules. A probabilistic model cannot be the authority that polices itself. Axiology is policy written so a machine can enforce it, sitting outside the model, with the power to refuse.

The operational effect is a compliance decision that does not depend on the model's mood. Federal rules, rules of engagement, and corporate limits are blocked when they are encoded and every proposed action must pass that gate. Prompt text is not that gate.

---

## How a transaction moves

1. **Measure (Metrology).** Capture the signal and record its quality and uncertainty.
2. **Structure (Ontology).** Map it onto the organization's open model.
3. **Verify (Epistemology).** Check provenance, corroboration, and whether this user may use it.
4. **Plan (Praxeology).** Route the verified context to the workflow or model that should propose the action.
5. **Govern (Axiology).** Pass the proposal through policy-as-code before anything executes.

Predictive work (scores, forecasts, match confidence) and generative work (summaries, explanations, recommendations) both have to cite owned evidence. A score without a source, or a narrative without a checkpoint on a consequential decision, does not clear verification or action.

---

## What to do with a proposal

Score the proposal on all five questions. A proposal that cannot be mapped to every layer does not pass intake. The bands are **GO**, **CONDITIONAL GO**, and **NO-GO**. The rubric is the [evaluation checklist](docs/5-Layer-Evaluation-Checklist.md).

---

## Repository navigation

Three doors. Read the one that matches the decision in front of you.

* **[Business briefs](primer/)** — two-page playbooks for data sovereignty, zero-trust governance, and what the investment can defend. Longer leader guides and worked scenarios are linked from there.
* **[Enterprise capability catalog](catalog/)** — the concrete **[Data Substrate capabilities](catalog/data-substrate.md)** and **[Enterprise Agent capabilities](catalog/agents.md)** needed to run the business, plus the [capability matrix](catalog/capability-matrix.md) and [technical specification](catalog/ARCHITECTURE.md).
* **[Glossary and longer guides](docs/)** — term hierarchy, pitch rules, and the public-sector and enterprise handouts.

---

## How we build it

Tool names stay out of the definitions above on purpose. They belong here, and in the [technical specification](catalog/ARCHITECTURE.md).

| Layer | What the organization keeps | Patterns named in the specification |
| :--- | :--- | :--- |
| **Metrology and the Data Substrate** | Measurements, quality rules, lineage | Open table formats (Apache Iceberg, Parquet, Polaris) under organizational control |
| **Ontology** | Entities and relationships | Organization-managed graphs and an open semantic model, not a vendor's private schema |
| **Epistemology** | What counts as justified | Citation and grounding checks against owned sources, before execution |
| **Praxeology** | Workflows and checkpoints | Deterministic workflow engines; a model proposes, the workflow bounds the action |
| **Axiology** | Rules that can refuse an action | Policy-as-code (Open Policy Agent) outside the model |

Iceberg and Polaris are how an owned table stays portable. They are not the definition of Ontology. Ontology is the meaning. The tables are one way to keep that meaning in a format the organization can export.

---

## Names in this repository

The repository rests on three terms: the thesis, the storage, and the engine.

| Term | Role | What it is |
| :--- | :--- | :--- |
| **MOEPA Cognitive Architecture** | The thesis | The five-layer separation of concerns (Metrology, Ontology, Epistemology, Praxeology, Axiology) and the intake scorecard (**GO**, **CONDITIONAL GO**, **NO-GO**). |
| **Data Substrate** | The storage | The organization-owned library where truth, definitions, rules, and lineage are stored in open, portable formats. It sits beneath the five layers and is not a sixth scored layer. |
| **Agents** | The engine | The models and workflows that consume the Data Substrate, propose plans in Praxeology, and are bounded by deterministic verification (Epistemology) and policy gates (Axiology). |

Feedback is by [issue](https://github.com/PhilipAsiala/philosophical-ai-architecture/issues/new?template=feedback.yml). The maintainer implements accepted changes on `main`. See [CONTRIBUTING.md](CONTRIBUTING.md). MIT licensed. Theory and documentation only.

*MOEPA Cognitive Architecture · business primer · technical specification v2.3 in the catalog · MIT License*
