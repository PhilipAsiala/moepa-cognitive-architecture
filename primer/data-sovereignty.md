# Data sovereignty

**The worry:** the model is rented, and so is the meaning. When the contract ends, the organization cannot take its definitions, its lineage, or its audit record with it.

**Ontology (shared meaning)** is how the organization stops that. It is the vocabulary of customers, assets, threats, cases, and policies, and the relationships among them, stored so a different model can read the same record. **Metrology (measurement)** is the layer under it: if the organization does not own the quality rules and the provenance, the vocabulary is a label on someone else's data.

## What "own" means here

Ownership is the ability to export, audit, and keep using the asset without the vendor's permission. A copy hosted inside a vendor product, with no export terms, does not meet that test.

| Keep | Rent, when the owned layers stay in house |
| :--- | :--- |
| The Data Substrate: truth, values, rules, and lineage | GPU capacity and cloud compute |
| Entity definitions and relationships (Ontology) | Commercial model access |
| Quality rules and provenance (Metrology) | Storage, if formats are open and egress is yours |
| Verification standards, workflows, and policy | Pre-trained weights |

The Data Substrate is the library underneath the five scored layers. It is not itself a scored layer. Intake uses it to show what the institution already owns and what a new project must add. The business design is the [Data Substrate concept](../docs/Data-Substrate-Concept.md). Storage mechanics are in the [technical specification](../catalog/ARCHITECTURE.md).

## How a proposal fails this brief

- "Customer," "asset," or "threat" is defined inside the vendor schema, and the organization cannot export the model.
- Lineage of a training or decision record exists only in the vendor's console.
- A new project adds a second definition of the same entity instead of extending the owned one.

Those are Ontology and Metrology gaps. They are also the usual path to lock-in. Switching cost is low only when the formats are open and the contract actually requires export. Skip either condition and the lock-in returns.

## What to decide

1. Name the entities this proposal will define or reuse.
2. State where those definitions will live, and how they leave if the vendor changes.
3. Score Metrology and Ontology on the [evaluation checklist](../docs/5-Layer-Evaluation-Checklist.md) before the model is chosen.

The full own-versus-rent map is the [Owned vs. Rented AI Strategy](../docs/Owned-vs-Rented-AI-Strategy.md). The builder patterns for meaning are the [Ontology catalog](../catalog/ontology/README.md).
