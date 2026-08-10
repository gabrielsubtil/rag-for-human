# 05 - Human first: RAG for AI agents

## The thesis

An **AI agent** is not a passive chatbot: it **acts** — it decides, executes, chains steps. To act safely, it needs reliable knowledge. RAG is what gives this agent access to external knowledge (non-parametric memory) in a **grounded and auditable** way.

The **"human first"** design means the architecture is designed for the **human** who supervises the agent — not for the model. The human needs to be able to:

- **Understand** why the agent decided what it decided.
- **Verify** where every piece of information came from (grounding/citation).
- **Control** the scope of what the agent can access and do.

## Why RAG is essential for agents

Without RAG, an agent acts based only on what it "remembers" from training — fixed, outdated, non-auditable knowledge. With RAG, the agent:

- **Grounds every decision** in verifiable sources.
- **Accesses up-to-date knowledge** without retraining.
- **Shows the origin** of every piece of information used.
- **Respects scope limits** defined by the indexed documents.

## The 5 "human first" principles

1. **Transparency** — the agent must show where every piece of information came from (citation by document and section).
2. **Verifiability** — the human must be able to check the source and the decision.
3. **Scope control** — the agent only accesses what was indexed; domain guardrails limit what it can do.
4. **Observability** — every step (query → retrieval → augmentation → generation) is traceable.
5. **Trust** — the human trusts the agent because they can audit the reasoning, not because "the model said so".

## How RAG enables each principle

| Principle | How RAG enables it |
|---|---|
| **Transparency** | Grounding/citation: the answer references document and section |
| **Verifiability** | The source is traceable and checkable by the human |
| **Scope control** | Domain guardrails: the agent only accesses what was indexed |
| **Observability** | Per-step tracing: you can see the decision path |
| **Trust** | Auditability: the reasoning can be checked |

## Agent + RAG: the loop

An agent with RAG does not make a single query — it **chains** steps, each one grounded:

```
User's goal
      │
      ▼
Agent formulates sub-query ──► RAG (retrieval + augmentation)
      │                                    │
      │                                    ▼
      │                          Grounded context
      │                                    │
      ▼                                    ▼
Agent decides / acts ◄────────── LLM generates based on context
      │
      ▼
Result + citations (for the human to verify)
```

## The human's role

In the "human first" design, the human is not a spectator — they are a **supervisor**:

- **Reviews** the citations before trusting the decision.
- **Audits** the path (which documents were used, in what order).
- **Defines** the scope (which documents the agent can access).
- **Intervenes** when the agent goes out of scope or the evidence is weak.

## "Human first" checklist for agents

- [ ] Every agent decision references the source (document + section)
- [ ] The decision path is traceable (tracing per step)
- [ ] The access scope is defined and limited
- [ ] The human can audit the reasoning
- [ ] The agent signals uncertainty when the evidence is weak
- [ ] Trust comes from auditability, not from the model's authority
