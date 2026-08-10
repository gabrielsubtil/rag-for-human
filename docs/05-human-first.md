# 05 — Human first: RAG para agentes de IA

## A tese

Um **agente de IA** não é um chatbot passivo: ele **age** — decide, executa, encadeia passos. Para agir com segurança, ele precisa de conhecimento confiável. RAG é o que dá a esse agente acesso a conhecimento externo (memória não-paramétrica) de forma **fundamentada e auditável**.

O design **"human first"** significa que a arquitetura é desenhada para o **humano** que supervisiona o agente — não para o modelo. O humano precisa conseguir:

- **Entender** por que o agente decidiu o que decidiu.
- **Verificar** de onde veio cada informação (grounding/citação).
- **Controlar** o escopo do que o agente pode acessar e fazer.

## Por que RAG é essencial para agentes

Sem RAG, um agente age com base apenas no que "lembra" do treinamento — conhecimento fixo, desatualizado e não auditável. Com RAG, o agente:

- **Fundamenta cada decisão** em fontes verificáveis.
- **Acessa conhecimento atualizado** sem retreinar.
- **Mostra a origem** de cada informação usada.
- **Respeita limites de escopo** definidos pelos documentos indexados.

## Os 5 princípios "human first"

1. **Transparência** — o agente deve mostrar de onde veio cada informação (citação por documento e seção).
2. **Verificabilidade** — o humano deve conseguir conferir a fonte e a decisão.
3. **Controle de escopo** — o agente só acessa o que foi indexado; guardrails de domínio limitam o que ele pode fazer.
4. **Observabilidade** — cada etapa (query → retrieval → augmentation → generation) é rastreável.
5. **Confiança** — o humano confia no agente porque consegue auditar o raciocínio, não porque "o modelo disse".

## Como o RAG habilita cada princípio

| Princípio | Como o RAG habilita |
|---|---|
| **Transparência** | Grounding/citação: a resposta referencia documento e seção |
| **Verificabilidade** | A fonte é rastreável e conferível pelo humano |
| **Controle de escopo** | Guardrails de domínio: o agente só acessa o que foi indexado |
| **Observabilidade** | Tracing por etapa: dá para ver o caminho da decisão |
| **Confiança** | Auditabilidade: o raciocínio pode ser conferido |

## Agente + RAG: o loop

Um agente com RAG não faz uma única consulta — ele **encadeia** passos, cada um fundamentado:

```
Objetivo do usuário
      │
      ▼
Agente formula sub-consulta ──► RAG (retrieval + augmentation)
      │                                    │
      │                                    ▼
      │                          Contexto fundamentado
      │                                    │
      ▼                                    ▼
Agente decide / age ◄────────── LLM gera com base no contexto
      │
      ▼
Resultado + citações (para o humano verificar)
```

## O papel do humano

No design "human first", o humano não é espectador — é **supervisor**:

- **Revisa** as citações antes de confiar na decisão.
- **Audita** o caminho (quais documentos foram usados, em que ordem).
- **Define** o escopo (quais documentos o agente pode acessar).
- **Intervém** quando o agente sai do escopo ou a evidência é fraca.

## Checklist "human first" para agentes

- [ ] Cada decisão do agente referencia a fonte (documento + seção)
- [ ] O caminho da decisão é rastreável (tracing por etapa)
- [ ] O escopo de acesso é definido e limitado
- [ ] O humano consegue auditar o raciocínio
- [ ] O agente sinaliza incerteza quando a evidência é fraca
- [ ] A confiança vem da auditabilidade, não da autoridade do modelo
