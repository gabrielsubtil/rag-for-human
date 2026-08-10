# 01 — O que é RAG

## O problema

LLMs são treinados em um volume enorme de dados, mas esse conhecimento é **fixo**: tem uma data de corte e não pode ser atualizado sem retreinar. Para domínios específicos (documentação interna, regras de negócio, conhecimento proprietário), o modelo simplesmente não sabe a resposta — ou, pior, **inventa** (alucina).

## A solução

RAG resolve isso sem retreinar: em vez de o modelo responder só com o que "lembra", o sistema **busca** o conhecimento relevante em uma base externa e o injeta no prompt como contexto. O modelo então gera a resposta ancorada nesse contexto.

## Memória paramétrica vs. não-paramétrica

| | Memória paramétrica | Memória não-paramétrica |
|---|---|---|
| **O que é** | Conhecimento nos pesos do LLM | Conhecimento externo (docs, bases, APIs) |
| **Atualização** | Requer retreinar | Basta atualizar a base |
| **Auditabilidade** | Baixa (caixa preta) | Alta (fonte rastreável) |
| **Exemplo** | Fatos aprendidos no treinamento | Manual de produto, política interna |

RAG combina as duas: o LLM (paramétrico) usa o conhecimento recuperado (não-paramétrico) como contexto.

## Por que RAG?

- **Reduz alucinações** — a resposta é ancorada em fontes verificáveis.
- **Conhecimento atualizado** — sem retreinar, basta atualizar a base.
- **Respostas citáveis** — dá para referenciar a fonte (grounding).
- **Guardrails de domínio** — restringe a resposta ao escopo dos documentos indexados.
- **Custo menor que fine-tuning** — não precisa treinar o modelo.

## Quando usar RAG

- Grande volume de documentação que precisa ser consultada para respostas autorizadas.
- Chatbots com conhecimento proprietário ou de domínio específico.
- Prevenção de alucinações e respostas desatualizadas.
- Quando você precisa de respostas **citáveis** e auditáveis.

## Quando NÃO usar RAG

- Quando o conhecimento é pequeno e estável (um prompt bem escrito resolve).
- Quando a resposta não precisa de fontes externas.
- Quando a latência da busca não compensa o ganho de precisão.
