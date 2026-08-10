# RAG for Humans

> Arquitetura de Retrieval-Augmented Generation (RAG) para **agentes de IA**, pensada para humanos — **"human first"**.

Este repositório é um **guia de arquitetura** de RAG. O objetivo é ensinar o *porquê* e o *como* da arquitetura, não entregar código. É um conceito, uma referência para quem quer entender como sistemas RAG funcionam por dentro — e como desenhá-los para que **humanos** consigam entender, verificar e controlar o que um agente de IA faz.

## A tese

RAG não é só para chatbots responderem perguntas. É o mecanismo que dá a um **agente de IA** acesso a conhecimento externo — e o design **"human first"** garante que o humano consiga **entender, verificar e controlar** o que o agente faz.

## O que é RAG?

RAG é um **padrão arquitetural** que combina a capacidade generativa de um LLM com conhecimento externo recuperado de uma base de dados, para produzir respostas factualmente corretas e ancoradas em fontes verificáveis — **sem retreinar o modelo**.

Em uma frase: o LLM usa o conhecimento que você fornece (não o que ele "lembra" do treinamento) como contexto para gerar a resposta ou fundamentar a decisão do agente.

## Índice

- [01 — O que é RAG](docs/01-o-que-e-rag.md) — conceito, motivação e memória paramétrica vs. não-paramétrica
- [02 — Arquitetura](docs/02-arquitetura.md) — as duas fases (build e runtime) e os componentes
- [03 — Padrões de design](docs/03-padroes.md) — timing da retrieval e variações arquiteturais
- [04 — Boas práticas](docs/04-boas-praticas.md) — armadilhas e recomendações
- [05 — Human first](docs/05-human-first.md) — RAG para agentes de IA, design centrado no humano

## Conceito central em 30 segundos

- **Memória paramétrica** = conhecimento gravado nos pesos do LLM (fixo, com data de corte).
- **Memória não-paramétrica** = conhecimento externo consultado em tempo de execução (atualizável, auditável).

RAG conecta as duas: o LLM usa o conhecimento recuperado como contexto para gerar a resposta ou fundamentar a decisão do agente.

## Licença

MIT
