---
status: accepted
date: 2026-09-05
layer: version-control
title: "Usar SemVer para versionar o DevFlow-AI"
description: "Por que uma única linha SemVer para o projeto inteiro, começando em 0.1.0, em vez de CalVer ou referência só por commit SHA."
supersedes:
superseded-by:
---

# 0004. Usar SemVer para versionar o DevFlow-AI

## Contexto e problema

O ADR [0002](0002-usar-conventional-commits.md) já mapeou `feat`/`fix`/`BREAKING CHANGE` para
MINOR/PATCH/MAJOR, e o ADR [0003](0003-usar-github-flow-como-estrategia-de-branch.md) já assumiu
release como tag `vX.Y.Z` sobre a `main` — mas nenhum dos dois fixou o esquema de versionamento
como decisão própria, nem definiu versão inicial, o que conta como bump durante a fase anterior a
`1.0.0`, nem o gatilho de release. Falta essa decisão antes da primeira tag.

## Opções consideradas

- **SemVer** — `X.Y.Z`, com o feat/fix/breaking já convencionado pelo ADR 0002 mapeando direto para MINOR/PATCH/MAJOR.
- **CalVer** — versão como data (ex.: `2026.09.0`); comunica quando saiu, não o que mudou, e joga fora a granularidade que os Conventional Commits já capturam.
- **Sem versionamento formal** — referência só por commit SHA; abandona o valor que o ADR 0002 já investiu em Conventional Commits.

## Decisão

Escolhido o **SemVer**, com uma única linha de versão para o projeto inteiro (não uma por camada),
começando em `0.1.0`. Bump: `feat` → MINOR, `fix` → PATCH, `BREAKING CHANGE`/`!` → MINOR enquanto o
MAJOR estiver travado em `0` (fase inicial, sem contrato estável); a partir de `1.0.0`,
`BREAKING CHANGE`/`!` passa a subir MAJOR. O gatilho de release é manual: alguém decide quando os
commits acumulados em `main` desde a última tag justificam uma release, calcula o bump pelos tipos
de commit e aplica a tag (mecanismo já fixado no ADR 0003). Cada release soma uma seção ao
`CHANGELOG.md`.

## Consequências

- Bom: reaproveita direto o mapeamento do ADR 0002, sem convenção nova pra aprender.
- Bom: fase `0.y.z` permite reestruturar o projeto sem prometer compatibilidade, compatível com o
  estado atual (nem stack escolhida).
- Ruim: sem automação, quem corta a release calcula o bump e escreve o `CHANGELOG.md` à mão —
  sujeito a esquecimento até uma ferramenta de release entrar.
- Ruim: o critério de "quando" cortar release fica subjetivo, sem checklist ou threshold.
- Ruim: "uma versão só pro projeto inteiro" mistura mudança de documentação com futura mudança de
  código na mesma linha; se uma camada virar pacote publicado separadamente, esta decisão precisa
  ser supersedida.

## Referências

Consultado em 2026-09-05.

- [Semantic Versioning 2.0.0](https://semver.org/) — confirma a fase `0.y.z` como desenvolvimento
  inicial sem contrato estável e a regra de que o MAJOR só passa a valer normalmente a partir de
  `1.0.0`.
