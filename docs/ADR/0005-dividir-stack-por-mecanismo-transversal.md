---
status: accepted
date: 2026-09-05
layer: stack
title: "Dividir a stack do DevFlow-AI por mecanismo transversal, não por fase do ciclo"
description: "Por que camada = mecanismo transversal com responsabilidade única, em vez de fase do SDLC ou área ampla agregada, e por que registrar um menu de candidatas sem criá-las."
supersedes:
superseded-by:
---

# 0005. Dividir a stack do DevFlow-AI por mecanismo transversal, não por fase do ciclo

## Contexto e problema

A única camada registrada até aqui, `version-control` (ADR [0002](0002-usar-conventional-commits.md)),
não corresponde a uma fase do ciclo de desenvolvimento — corresponde a um mecanismo que atravessa
várias fases (como a mudança entra no histórico). Falta decidir se esse é o padrão a seguir ou uma
exceção, e falta um vocabulário-alvo para as próximas decisões de arquitetura saberem em qual
camada encaixar, sem que cada ADR proponha um nome novo. O escopo do framework é o processo de
desenvolvimento assistido por IA (planejar, codar, revisar, testar, entregar, operar), não o
produto de IA em si.

## Opções consideradas

- **Camadas mínimas por área ampla** — 3-4 camadas agregadas (ex.: `ai-collaboration`, `knowledge-context`, `quality-governance`), cada uma cobrindo várias responsabilidades distintas.
- **Camadas por fase do ciclo** — planejamento, codificação, revisão, teste, entrega, operação; exigiria reencaixar `version-control` como parte de uma fase.
- **Granular por mecanismo transversal, com menu de candidatas** — uma responsabilidade por camada, seguindo o precedente de `version-control`; um menu de nomes candidatos é registrado agora, mas cada camada só existe de fato quando um ADR específico a criar.
- **Só o critério, sem candidatas** — fixa "mecanismo transversal, uma responsabilidade" sem nomear nenhuma candidata.

## Decisão

Escolhida a granularidade por **mecanismo transversal com menu de candidatas**: camada = um
mecanismo que atravessa fases do ciclo, com responsabilidade única — mesmo padrão de
`version-control`. Ficam registradas como candidatas (nenhuma criada por este ADR, todas pendentes
do ADR que efetivamente as decidir): `agent-orchestration`, `context-knowledge`, `tool-integration`,
`prompt-instruction`, `guardrails-governance`, `testing-verification`, `delivery-observability`.
Este ADR não adiciona linha nenhuma em `layers.md` — a regra de que camada só existe pelo ADR que a
cria continua valendo para cada uma dessas candidatas.

## Consequências

- Bom: a próxima decisão de arquitetura já tem um nome candidato pra encaixar, em vez de inventar slug a cada ADR.
- Bom: mantém `layers.md` fiel só ao que foi de fato decidido — este registro é sobre o critério e o menu, não sobre criar camada.
- Ruim: o menu é uma previsão; candidatas podem nunca virar camada real, e necessidades não previstas vão exigir nome fora da lista.
- Ruim: nenhuma dessas candidatas está definida em termos de fronteira exata (o que entra e o que não entra) — isso fica para o ADR que efetivamente criar cada uma.
