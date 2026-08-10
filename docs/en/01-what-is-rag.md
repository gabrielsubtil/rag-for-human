# 01 - What is RAG

## The problem

LLMs are trained on a huge volume of data, but that knowledge is **fixed**: it has a cutoff date and cannot be updated without retraining. For specific domains (internal documentation, business rules, proprietary knowledge), the model simply does not know the answer — or, worse, it **makes it up** (hallucinates).

## The solution

RAG solves this without retraining: instead of the model answering only with what it "remembers", the system **retrieves** the relevant knowledge from an external base and injects it into the prompt as context. The model then generates the answer anchored in that context.

## Parametric vs. non-parametric memory

| | Parametric memory | Non-parametric memory |
|---|---|---|
| **What it is** | Knowledge in the LLM weights | External knowledge (docs, databases, APIs) |
| **Updating** | Requires retraining | Just update the base |
| **Auditability** | Low (black box) | High (traceable source) |
| **Example** | Facts learned during training | Product manual, internal policy |

RAG combines both: the LLM (parametric) uses the retrieved knowledge (non-parametric) as context.

## Why RAG?

- **Reduces hallucinations** — the answer is anchored in verifiable sources.
- **Up-to-date knowledge** — no retraining, just update the base.
- **Citable answers** — you can reference the source (grounding).
- **Domain guardrails** — restricts the answer to the scope of the indexed documents.
- **Cheaper than fine-tuning** — no model training required.

## When to use RAG

- Large volumes of documentation that need to be consulted for authoritative answers.
- Chatbots with proprietary or domain-specific knowledge.
- **AI agents that need to act with grounding and auditability.**
- Preventing hallucinations and outdated answers.
- When you need **citable** and auditable answers.

## When NOT to use RAG

- When the knowledge is small and stable (a well-written prompt solves it).
- When the answer does not need external sources.
- When retrieval latency does not pay off against the precision gain.
