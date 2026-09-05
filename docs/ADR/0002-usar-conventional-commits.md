---
status: accepted
date: 2026-09-05
layer: stack
title: "Usar Conventional Commits nas mensagens de commit"
description: "Por que mensagem de commit com tipo prefixado em vez de texto livre, para que a natureza da mudança seja legível por ferramenta e não só por pessoa."
supersedes:
superseded-by:
---

# 0002. Usar Conventional Commits nas mensagens de commit

## Contexto e problema

O repositório está sem commit nenhum, então a convenção de mensagem é escolhida antes de existir
histórico para migrar. A pergunta que o histórico precisa responder mais tarde — o que entrou de
funcionalidade, o que quebrou compatibilidade, o que virou release — só tem resposta automática se
a mensagem carregar essa informação em posição fixa. Esta decisão também **cria a camada
`version-control`**, que faltava no registro: é ela que responde por como a mudança entra no
histórico, e a convenção de commit é o primeiro item do seu interior.

## Opções consideradas

- **Conventional Commits 1.0.0** — `<tipo>[escopo]: <descrição>`, com `!` ou footer `BREAKING CHANGE` para mudança incompatível; spec estável e parseável.
- **Mensagem livre / estilo Git padrão** — assunto curto no imperativo e corpo explicando o porquê; legível por pessoa, opaco para ferramenta.

## Decisão

Escolhido o **Conventional Commits 1.0.0**, porque o tipo prefixado e o marcador de breaking change
tornam a natureza da mudança extraível do histórico sem ninguém reclassificar commit a mão depois —
que é exatamente o que a mensagem livre não entrega. A camada `version-control` entra em
`layers.md` no mesmo commit deste ADR.

## Consequências

- Bom: `feat`, `fix` e `BREAKING CHANGE`/`!` mapeiam para MINOR, PATCH e MAJOR do SemVer, então bump de versão e changelog podem ser gerados a partir do `git log`, sem passo manual de classificação.
- Bom: `git log --grep '^feat'` responde "o que entrou de funcionalidade" sem abrir diff.
- Ruim: nada valida o formato hoje — o repo não tem ferramenta nenhuma instalada, então mensagem fora do padrão só é pega por quem revisa, e passa em silêncio se ninguém revisar.
- Ruim: a fronteira entre `chore`, `refactor` e `build` é decidida a cada commit e diverge entre pessoas; o histórico fica consistente na forma e inconsistente na classificação.
- Ruim: camada e ferramenta estão no mesmo registro, então trocar a convenção de mensagem depois exige supersedir também a definição de `version-control`.

## Referências

Consultado em 2026-09-05.

- [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/) — versão vigente da spec, estrutura da mensagem, lista de tipos e as duas formas de marcar breaking change (`!` e footer).
