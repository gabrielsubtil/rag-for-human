# 04 - Best practices

## Common pitfalls

### "RAG = vector database"
No. Vector search is just one retrieval option. In practice, **hybrid search** (vector + full-text/BM25) almost always outperforms vector-only, because the two methods have different strengths.

### Chunking is the hard problem
If the chunk does not contain the evidence that answers the question, retrieval fails — and everything behind it is lost. The size and the way you cut chunks matter more than it seems.

### Different embedding models
Docs and queries need to use the **same** embedding model. Otherwise, the vectors end up in different spaces and similarity comparisons make no sense.

### Lack of grounding / citation
The answer should reference the source (document, section) to be auditable. Without this, you cannot verify where the information came from.

## Recommendations

### Grounding and citation
Always reference the source in the answer. This makes the system auditable and gives the user confidence.

### Domain guardrails
RAG restricts the answer to the domain of the indexed documents — an implicit scope limit. Use this to your advantage to avoid answers outside the business context.

### Observability
RAG adds upstream dependencies (several steps before generation). Without tracing (one span per step), it is very hard to diagnose why an answer came out wrong. Instrument every step.

### Multilingual
If the base is in one language and the user asks in another, add a pre-query translation step (translate the question into the base's language) and a post-query step (translate the answer back).

### Contextual Retrieval
When it is hard to find a uniform chunk size, Contextual Retrieval (Anthropic) — rephrasing each chunk with an LLM to make it coherent — significantly improves retrieval quality.

## Architecture checklist

- [ ] Same embedding model for docs and queries
- [ ] Validated chunking (do the chunks contain the evidence?)
- [ ] Hybrid retrieval (vector + BM25) considered
- [ ] Grounding/citation in the answer
- [ ] Observability (tracing per step)
- [ ] Domain guardrails defined
- [ ] Multilingual handling (if applicable)
