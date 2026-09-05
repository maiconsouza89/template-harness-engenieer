---
status: accepted
date: 2026-09-05
layer: version-control
title: "Usar GitHub Flow como estratégia de branch"
description: "Por que uma única branch estável com branches curtas por PR em vez de main+develop, dado que não há versões antigas para manter e múltiplos autores (humanos e agentes) trabalham em paralelo."
supersedes:
superseded-by:
---

# 0003. Usar GitHub Flow como estratégia de branch

## Contexto e problema

O repositório não tem branch além de `main` e todo commit até aqui foi feito direto nela. O projeto
vai passar a ter múltiplos autores trabalhando em paralelo — o usuário, colaboradores humanos e
agentes de IA — e vai adotar versionamento formal em SemVer, sem necessidade de manter versões
antigas em paralelo (fluxo forward-only). É preciso uma convenção de branch e merge antes que o
primeiro desses autores paralelos precise de uma. Esta decisão estende a camada `version-control`
(criada pelo ADR [0002](0002-usar-conventional-commits.md)), que já responde por como a mudança
entra no histórico.

## Opções consideradas

- **GitHub Flow** — uma única branch de longa duração (`main`), sempre estável; todo trabalho nasce numa branch curta e volta por Pull Request; release é tag de SemVer sobre um commit da `main`.
- **Git Flow** — `main` + `develop` permanentes, mais branches de `release-*`/`hotfix-*`; desenhado para manter várias versões em produção ao mesmo tempo.
- **Trunk-Based Development estrito** — commits diretos ou branches de poucas horas direto na trunk, escondendo trabalho incompleto atrás de feature flags.

## Decisão

Escolhido o **GitHub Flow**: `main` é a única branch de longa duração e sempre reflete o estado
atual; todo trabalho — de qualquer autor — nasce em uma branch nomeada `<tipo>/<descricao-curta>`
(os mesmos seis tipos do Conventional Commits, ex.: `feat/branch-strategy-adr`), entra por Pull
Request revisado e é apagada após o merge; releases são tags `vX.Y.Z` sobre commits da `main`, sem
branch de release dedicada. Git Flow perde por resolver um problema que este repositório não tem
(múltiplas versões em produção); Trunk-Based estrito perde porque depende de feature flags para
esconder trabalho incompleto, e este repositório não tem runtime que "rode incompleto" — é
documentação e convenção.

## Consequências

- Bom: com PR sempre obrigatório, dois agentes trabalhando em paralelo nunca escrevem direto na
  `main` ao mesmo tempo — cada um fica isolado na própria branch até o merge.
- Bom: não existe branch `develop` para manter sincronizada com `main`, então não há merge duplo
  nem risco de `main` e `develop` divergirem silenciosamente.
- Bom: cortar uma release não exige branch nem merge extra — é aplicar uma tag num commit que já
  está na `main`.
- Ruim: sem branch de release, um bug encontrado após a tag só pode ser corrigido avançando a
  `main` e cortando uma tag nova — não há como aplicar hotfix isolado numa versão antiga.
- Ruim: esta decisão não define o critério de quando cortar uma release (o que conta como MINOR vs
  PATCH) nem exige checks de CI no PR — ambos ficam em aberto para um ADR futuro.

## Referências

Consultado em 2026-09-05.

- [GitHub Flow](https://docs.github.com/en/get-started/using-github/github-flow) — confirma que o modelo tem uma única branch de longa duração (a "default branch"), branches de trabalho descartáveis e Pull Request como mecanismo central de revisão antes do merge.
- [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/) — descreve o Git Flow (branches `master`/`develop` permanentes, `release-*`/`hotfix-*`) como modelo desenhado para versionamento explícito com múltiplas versões em produção simultânea; o próprio autor reconhece, em atualização de 2020, que modelos mais simples como GitHub Flow servem melhor entrega contínua.
