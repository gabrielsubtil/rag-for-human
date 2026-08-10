# 04 — Boas práticas

## Armadilhas comuns

### "RAG = vector database"
Não. Busca vetorial é só uma das opções de retrieval. Na prática, **busca híbrida** (vetorial + full-text/BM25) quase sempre supera só vetorial, porque os dois métodos têm pontos fortes diferentes.

### Chunking é o problema difícil
Se o chunk não contém a evidência que responde à pergunta, a retrieval falha — e tudo atrás se perde. O tamanho e a forma de cortar os chunks importam mais do que parece.

### Modelos de embedding diferentes
Docs e queries precisam usar o **mesmo** modelo de embedding. Se não, os vetores ficam em espaços diferentes e as comparações de similaridade não fazem sentido.

### Falta de grounding / citação
A resposta deve referenciar a fonte (documento, seção) para ser auditável. Sem isso, você não consegue verificar de onde veio a informação.

## Recomendações

### Grounding e citação
Sempre referencie a fonte na resposta. Isso torna o sistema auditável e dá confiança ao usuário.

### Guardrails de domínio
RAG restringe a resposta ao domínio dos documentos indexados — um limite implícito de escopo. Use isso a seu favor para evitar respostas fora do contexto do negócio.

### Observabilidade
RAG adiciona dependências upstream (várias etapas antes da geração). Sem tracing (um span por etapa), é muito difícil diagnosticar por que uma resposta saiu errada. Instrumente cada etapa.

### Multilíngue
Se a base está em um idioma e o usuário pergunta em outro, adicione uma etapa de tradução pré-query (traduzir a pergunta para o idioma da base) e pós-query (traduzir a resposta de volta).

### Contextual Retrieval
Quando é difícil achar um tamanho de chunk uniforme, o Contextual Retrieval (Anthropic) — reformular cada chunk com um LLM para torná-lo coerente — melhora significativamente a qualidade da recuperação.

## Checklist de arquitetura

- [ ] Mesmo modelo de embedding para docs e queries
- [ ] Chunking validado (os chunks contêm a evidência?)
- [ ] Retrieval híbrida (vetorial + BM25) considerada
- [ ] Grounding/citação na resposta
- [ ] Observabilidade (tracing por etapa)
- [ ] Guardrails de domínio definidos
- [ ] Tratamento multilíngue (se aplicável)
