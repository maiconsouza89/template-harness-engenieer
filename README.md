# DevFlow-AI

Framework de processo para apoiar o ciclo de vida de desenvolvimento de software com uso de IA.
Sem runtime próprio: o que existe aqui é convenção, template e decisão registrada — pensado de
forma análoga a uma stack, em camadas compostas, cada uma com responsabilidade definida, escolhida
e trocável de forma explícita.

## Estado atual

Repositório em estágio inicial: ainda não há nenhuma camada de metodologia além do controle de
decisão e do controle de versão. O que existe hoje:

- **Registro de decisões** — todo ADR aceito vive em [`docs/ADR/`](docs/ADR/index.md), com a
  camada da stack a que pertence declarada no front-matter.
- **Controle de versão** — mensagens de commit seguem Conventional Commits, restrito a seis
  tipos; ver [`CONTRIBUTING.md`](CONTRIBUTING.md) e
  [ADR 0002](docs/ADR/0002-usar-conventional-commits.md).

Quais outras camadas vão existir (codificação assistida, revisão, testes, etc.) ainda é decisão em
aberto — ver [`CLAUDE.md`](CLAUDE.md).

## Como a stack funciona

Uma camada só existe quando uma decisão real a cria: o ADR que decide algo dentro dela declara a
camada no campo `layer`, e ela entra em [`docs/ADR/layers.md`](docs/ADR/layers.md) no mesmo commit.
Não há roteiro fixo de camadas definido de antemão — o vocabulário de camadas cresce como
consequência de decisões, não como planejamento especulativo.

Para saber por que uma camada é o que é — e o que foi cogitado e descartado — o motivo está sempre
no próprio ADR, nunca só em conversa ou PR.

## Como contribuir

- Decisão cara de reverter vira ADR antes de virar código — ver a skill `adr-writer` e
  [ADR 0001](docs/ADR/0001-usar-adrs-para-decisoes-de-arquitetura.md).
- Documentação, discussão e ADRs em **português**; código, nomes e mensagens de commit em
  **inglês** — ver [`CLAUDE.md`](CLAUDE.md).
- Mensagens de commit seguem Conventional Commits — ver [`CONTRIBUTING.md`](CONTRIBUTING.md).

## Licença

[Apache License 2.0](LICENSE).
