# RAG for Humans

> Arquitetura de Retrieval-Augmented Generation (RAG) explicada para humanos — didática, conceitual, sem scripts.

Este repositório é um **guia de arquitetura** de RAG. O objetivo é ensinar o *porquê* e o *como* da arquitetura, não entregar código. É um conceito, uma referência para quem quer entender como sistemas RAG funcionam por dentro.

## O que é RAG?

RAG é um **padrão arquitetural** que combina a capacidade generativa de um LLM com conhecimento externo recuperado de uma base de dados, para produzir respostas factualmente corretas e ancoradas em fontes verificáveis — **sem retreinar o modelo**.

Em uma frase: o LLM usa o conhecimento que você fornece (não o que ele "lembra" do treinamento) como contexto para gerar a resposta.

## Índice

- [01 — O que é RAG](docs/01-o-que-e-rag.md) — conceito, motivação e memória paramétrica vs. não-paramétrica
- [02 — Arquitetura](docs/02-arquitetura.md) — as duas fases (build e runtime) e os componentes
- [03 — Padrões de design](docs/03-padroes.md) — timing da retrieval e variações arquiteturais
- [04 — Boas práticas](docs/04-boas-praticas.md) — armadilhas e recomendações

## Conceito central em 30 segundos

- **Memória paramétrica** = conhecimento gravado nos pesos do LLM (fixo, com data de corte).
- **Memória não-paramétrica** = conhecimento externo consultado em tempo de execução (atualizável, auditável).

RAG conecta as duas: o LLM usa o conhecimento recuperado como contexto para gerar a resposta.

## Licença

MIT
