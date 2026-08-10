# 03 - Design patterns

A central architectural decision is **when** retrieval happens relative to generation. This affects latency, complexity, and the system's capabilities.

## Retrieval timing

### Retrieve-then-read (single-shot)
Retrieves once, then generates. Simple and common. The retriever's output becomes the generator's input in a single flow.

### Iterative / multi-hop
Retrieves, partially generates, identifies a gap, formulates a more specific sub-query, and retrieves again. For complex questions that require multiple steps.

### RETRO (Retrieval-Enhanced Transformer)
Retrieves **during** generation, token by token (DeepMind). Each generated chunk has access to the most relevant passages, dynamically updated. Extreme and complex.

### Self-RAG
Retrieval is an **adaptive decision** of the model, not an unconditional operation. The model decides when to retrieve and when not to.

## Architectural variations

| Variation | Central idea |
|---|---|
| **Fusion-in-Decoder (FiD)** | Processes documents independently to scale the number of chunks |
| **End-to-end RAG / REALM** | Trains the retriever aligned with generation quality |
| **Contextual Retrieval (Anthropic)** | Uses an LLM to rephrase each chunk coherently, improving retrieval quality |

## Sparse vs. dense retrieval

- **Sparse (BM25)** — searches by exact term matching. Excellent for specific terms, names, codes.
- **Dense (vector)** — searches by semantic similarity. Captures synonyms and related concepts.
- **Hybrid** — combines both. In practice, almost always outperforms either one alone.

## The key point

The "retrieve-then-read" pattern is just one point in a large design space. The choice of timing and variation depends on the use case: simple questions do not need multi-hop; bases with overlapping terminology benefit from hybrid.
