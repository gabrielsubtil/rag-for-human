# 03 — Padrões de design

Uma decisão arquitetural central é **quando** a retrieval ocorre em relação à geração. Isso afeta latência, complexidade e as capacidades do sistema.

## Timing da retrieval

### Retrieve-then-read (single-shot)
Recupera uma vez, depois gera. Simples e comum. A saída do retriever vira a entrada do generator em um único fluxo.

### Iterative / multi-hop
Recupera, gera parcialmente, identifica uma lacuna, formula uma sub-consulta mais específica e recupera de novo. Para perguntas complexas que exigem múltiplos passos.

### RETRO (Retrieval-Enhanced Transformer)
Recupera **durante** a geração, token a token (DeepMind). Cada chunk gerado tem acesso aos trechos mais relevantes, atualizados dinamicamente. Extremo e complexo.

### Self-RAG
A retrieval é uma **decisão adaptativa** do modelo, não uma operação incondicional. O modelo decide quando buscar e quando não buscar.

## Variações arquiteturais

| Variação | Ideia central |
|---|---|
| **Fusion-in-Decoder (FiD)** | Processa documentos independentemente para escalar o número de chunks |
| **End-to-end RAG / REALM** | Treina o retriever alinhado à qualidade da geração |
| **Contextual Retrieval (Anthropic)** | Usa um LLM para reformular cada chunk de forma coerente, melhorando a qualidade da recuperação |

## Sparse vs. dense retrieval

- **Sparse (BM25)** — busca por correspondência exata de termos. Excelente para termos específicos, nomes, códigos.
- **Dense (vetorial)** — busca por similaridade semântica. Captura sinônimos e conceitos relacionados.
- **Híbrido** — combina os dois. Na prática, quase sempre supera qualquer um isolado.

## O ponto-chave

O padrão "retrieve-then-read" é apenas um ponto em um grande espaço de design. A escolha do timing e da variação depende do caso de uso: perguntas simples não precisam de multi-hop; bases com terminologia sobreposta se beneficiam de híbrido.
