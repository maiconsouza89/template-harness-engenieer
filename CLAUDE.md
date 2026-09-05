# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Estado atual

Ainda **sem código nem stack escolhida** — só convenções de processo fechadas até aqui (ADRs 0001–0004: uso de
ADR, Conventional Commits, GitHub Flow, SemVer). Não existe arquitetura para descrever ainda — as seções
"Comandos" e "Arquitetura" abaixo são placeholders e devem ser preenchidas por quem implementar cada decisão,
no mesmo commit que introduzir a ferramenta.

## O que é o DevFlow-AI

Framework para apoiar o **ciclo de vida de desenvolvimento de software com uso de IA**, pensado de forma análoga
a uma stack: camadas compostas, cada uma com responsabilidade definida, escolhidas e trocáveis de forma explícita.
O escopo de cada camada (e quais camadas existem) ainda é decisão em aberto.

## Como trabalhar neste repositório

### 1. Decidir antes de implementar

Cada passo do projeto é **levantado e discutido** antes de virar código. Não presuma stack, linguagem, estrutura de
pastas ou dependências — proponha opções com trade-offs e espere a decisão. Se uma dúvida bloquear parte do trabalho,
entregue o que não depende dela e traga a pergunta.

Decisões fechadas viram registro em `docs/ADR/NNNN-titulo-kebab-case.md` (ADR: contexto, opções consideradas,
decisão, consequências), com o campo `layer` dizendo a que camada da stack a decisão pertence — as camadas válidas
ficam em `docs/ADR/layers.md` e cada uma entra ali pelo ADR que a criou. Use a skill `adr-writer`: ela traz o
template, o ciclo de status e `scripts/audit.py`, que valida numeração, camada, cadeias de supersede e o índice.
Uma decisão só é "nossa" quando está escrita ali; conversa de sessão não persiste.

### 2. Pesquisar sempre, nesta ordem

Antes de recomendar ou usar qualquer biblioteca, framework, SDK, API ou ferramenta CLI:

1. **`docs/` deste repositório** — ADRs e notas já escritas aqui têm precedência sobre qualquer fonte externa.
2. **context7** (MCP) — `resolve-library-id` seguido de `query-docs`, mesmo para libs que você "já conhece";
   o conhecimento do modelo pode estar defasado.
3. **Documentação oficial** do projeto/fornecedor.
4. **Busca web** — para comparações, estado da arte e material que não está na doc oficial.

Cite a fonte (link ou versão consultada) nos ADRs e em recomendações. Não afirme comportamento de API de memória.

### 3. Idioma

**Português (pt-BR)** em tudo que é comunicação: respostas ao usuário, discussões, ADRs, README, comentários de
documentação e qualquer texto em `docs/`.

**Inglês** em tudo que é código: nomes de variáveis, funções, classes, arquivos e diretórios, comentários inline,
mensagens de erro/log da aplicação, mensagens de commit e descrições de PR.

### 4. Commits, branch e release

[Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/), com o conjunto de seis tipos
(`feat`, `fix`, `docs`, `refactor`, `test`, `chore`) e os exemplos de certo e errado em `CONTRIBUTING.md`.
O porquê da escolha está no ADR 0002. `CONTRIBUTING.md` também é a referência operacional para a estratégia de
branch (GitHub Flow, ADR 0003) e para o runbook de release manual (SemVer, ADR 0004).

## Comandos

_A definir._ Ainda não há build, lint ou testes. Ao introduzir a primeira ferramenta, registre aqui os comandos de
build, lint, suíte completa de testes e **execução de um teste isolado**.

## Arquitetura

_A definir._ Documente aqui apenas o que exige ler vários arquivos para entender (fronteiras entre camadas, fluxo de
dados, pontos de extensão) — não a árvore de diretórios.
