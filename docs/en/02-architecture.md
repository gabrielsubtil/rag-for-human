# 02 - Architecture

The RAG architecture has **two phases**: build (ingestion/indexing) and runtime (query/serving).

## Phase 1 - Build (ingestion / indexing)

Prepares the knowledge to be queried:

1. **Collection** — gather the source documents (manuals, docs, tickets, PDFs).
2. **Preprocessing** — convert formats (PDF to text), enrich with metadata (author, category, date), expand abbreviations.
3. **Chunking** — split the text into coherent chunks. **This is the hardest problem**: the chunk needs to contain the evidence that answers the question.
4. **Embedding** — turn each chunk into a numerical vector (embedding) using an embedding model.
5. **Indexing** — store the vectors in a vector database for similarity search.

## Phase 2 - Runtime (query / serving)

Answers the user's question or grounds the agent's decision:

1. **Query** — the user sends a question (or the agent formulates a sub-query).
2. **Query embedding** — the question is turned into a vector using the **same** embedding model as the documents (otherwise the vector spaces do not match).
3. **Retrieval** — searches the top-K most relevant chunks by similarity.
4. **Augmentation** — injects the retrieved chunks into the prompt, along with the question.
5. **Generation** — the LLM generates the answer anchored in the provided context.

## Main components

| Component | Function | Key decisions |
|---|---|---|
| **Retriever** | Finds the relevant documents | sparse (BM25) vs. dense (vector) vs. hybrid; top-K; reranking |
| **Generator** | Synthesizes the answer from the context | prompt design; grounding; uncertainty handling |
| **Embedding model** | Converts text into vectors | same model for docs and queries |
| **Vector database** | Stores and searches vectors | FAISS, Chroma, Milvus, pgvector, etc. |
| **Chunking** | Splits the text into chunks | fixed size vs. by sections; overlap; contextual retrieval |

## Conceptual diagram

```
                     BUILD PHASE
  Documents → Collection → Preprocessing → Chunking
                                            ↓
                              Embedding model → Vector DB
                                            ↓
                    RUNTIME PHASE
  User/Agent → Query → Query embedding → Retrieval (top-K)
                                            ↓
                          Augmentation (prompt + context)
                                            ↓
                          Generation (LLM) → Answer
```

## The contract between retriever and generator

The retriever promises to return relevant documents; the generator promises to synthesize them into an answer. This separation creates a **clean contract**: the retriever's output becomes the generator's input. If the retriever retrieves poorly, the answer comes out wrong even with a perfect generator — and vice versa.
