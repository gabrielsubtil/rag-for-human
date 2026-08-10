# 02 — Arquitetura

A arquitetura RAG tem **duas fases**: build (ingestão/indexação) e runtime (consulta/serving).

## Fase 1 — Build (ingestão / indexação)

Prepara o conhecimento para ser consultado:

1. **Coleta** — reunir os documentos-fonte (manuais, docs, tickets, PDFs).
2. **Pré-processamento** — converter formatos (PDF→texto), enriquecer com metadados (autor, categoria, data), expandir abreviações.
3. **Chunking** — dividir o texto em trechos (chunks) coerentes. **É o problema mais difícil**: o chunk precisa conter a evidência que responde à pergunta.
4. **Embedding** — transformar cada chunk em um vetor numérico (embedding) via modelo de embedding.
5. **Indexação** — armazenar os vetores em um banco vetorial (vector database) para busca por similaridade.

## Fase 2 — Runtime (consulta / serving)

Responde à pergunta do usuário ou fundamenta a decisão do agente:

1. **Query** — usuário envia uma pergunta (ou o agente formula uma sub-consulta).
2. **Embedding da query** — a pergunta é convertida em vetor usando o **mesmo** modelo de embedding dos documentos (senão os espaços vetoriais não batem).
3. **Retrieval** — busca os top-K chunks mais relevantes por similaridade.
4. **Augmentation** — injeta os chunks recuperados no prompt, junto com a pergunta.
5. **Generation** — o LLM gera a resposta ancorada no contexto fornecido.

## Componentes principais

| Componente | Função | Decisões-chave |
|---|---|---|
| **Retriever** | Encontra os documentos relevantes | sparse (BM25) vs. dense (vetorial) vs. híbrido; top-K; reranking |
| **Generator** | Sintetiza a resposta a partir do contexto | prompt design; grounding; tratamento de incerteza |
| **Embedding model** | Converte texto em vetores | mesmo modelo para docs e queries |
| **Vector database** | Armazena e busca vetores | FAISS, Chroma, Milvus, pgvector, etc. |
| **Chunking** | Divide o texto em trechos | tamanho fixo vs. por seções; overlap; contextual retrieval |

## Diagrama conceitual

```
                    ┌─────────────────────────────────────────────┐
                    │              FASE DE BUILD                  │
                    │                                             │
  Documentos ──► Coleta ──► Pré-processamento ──► Chunking       │
                    │                                             │
                    │        Embedding model ──► Vector DB        │
                    └────────────────────────────────────────────┘
                                        │
                                        ▼
                    ┌─────────────────────────────────────────────┐
                    │              FASE DE RUNTIME                │
                    │                                             │
  Usuário/Agente ─► Query ─► Embedding da query ─► Retrieval (top-K)│
                    │                                             │
                    │        Augmentation (prompt + contexto)      │
                    │        Generation (LLM) ──► Resposta         │
                    └─────────────────────────────────────────────┘
```

## O contrato entre retriever e generator

O retriever promete devolver documentos relevantes; o generator promete sintetizá-los em uma resposta. Essa separação cria um **contrato limpo**: a saída do retriever vira a entrada do generator. Se o retriever recupera mal, a resposta sai errada mesmo com um generator perfeito — e vice-versa.
