# Contribuindo

## Branches

Este projeto usa [GitHub Flow](https://docs.github.com/en/get-started/using-github/github-flow).
O porquê está no [ADR 0003](docs/ADR/0003-usar-github-flow-como-estrategia-de-branch.md).

- `main` é a única branch de longa duração e sempre reflete o estado atual.
- Todo trabalho nasce em uma branch curta nomeada `<tipo>/<descricao-curta>`, usando os mesmos seis
  tipos do Conventional Commits (ex.: `feat/branch-strategy-adr`, `fix/audit-layer-check`).
- Entra na `main` por Pull Request revisado — nunca commit direto na `main`.
- A branch é apagada após o merge.
- Release é uma tag `vX.Y.Z` sobre um commit da `main`; não há branch de release nem de hotfix.

## Commits

Este projeto usa [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/).
O porquê está no [ADR 0002](docs/ADR/0002-usar-conventional-commits.md).

### Formato

```
<tipo>[escopo opcional]: <descrição>

[corpo opcional]

[rodapé opcional]
```

### Tipos

| tipo | quando |
|---|---|
| `feat` | nova funcionalidade |
| `fix` | correção de bug |
| `docs` | só documentação (inclui ADR) |
| `refactor` | muda o código sem mudar o comportamento |
| `test` | só teste |
| `chore` | o resto: build, CI, dependências, config |

Só esses seis. Se nenhum serve, o commit provavelmente está fazendo duas coisas.

### Regras

- **Mensagem de commit é código: escreva em inglês.** Documentação e ADRs são em português (ver `CLAUDE.md`).
- Descrição no **imperativo presente**: `add`, não `added` nem `adds`.
- Minúscula no início, **sem ponto final**, até ~72 caracteres.
- O corpo explica **por que**, não o que — o diff já diz o que.
- Um commit, uma mudança.

### Certo e errado

```
✅ feat: add layer validation to ADR audit script
✅ fix: reject duplicate ADR numbers instead of overwriting
✅ docs: add ADR 0002 on conventional commits
✅ chore: pin python version in CI
✅ refactor(adr): extract front-matter parsing into helper

❌ Add layer validation                    → falta o tipo
❌ feat: Added layer validation            → passado + maiúscula
❌ feat: add layer validation.             → ponto final
❌ feat: adiciona validação de camada      → commit vai em inglês
❌ fix: fix bug                            → não diz o que foi corrigido
❌ chore: updates                          → vago; não responde nada em seis meses
❌ feat: add validation and fix index bug  → duas mudanças, dois commits
```

### Breaking change

Duas formas, ambas válidas — use `!` para o caso simples e o rodapé quando precisar explicar:

```
✅ feat!: require layer field in ADR front-matter

✅ feat: require layer field in ADR front-matter

   BREAKING CHANGE: ADRs sem `layer` passam a falhar na auditoria.
   Rode `audit.py docs/ADR` e preencha o campo antes de atualizar.
```

`BREAKING CHANGE` vai em maiúsculas, no rodapé, após uma linha em branco.

### Escopo

Opcional. Use quando restringir a mudança a uma parte já nomeada do repo (`feat(adr):`).
Não invente escopo para commit que toca o projeto inteiro.

## Release

Este projeto usa [SemVer](https://semver.org/), com uma única linha de versão para o projeto
inteiro. O porquê está no [ADR 0004](docs/ADR/0004-usar-semver-para-versionar-o-devflow-ai.md).

Não há automação ainda — release é manual, sob demanda:

1. Veja os commits desde a última tag: `git log <última-tag>..HEAD --oneline` (ou o histórico
   inteiro, se ainda não existe nenhuma tag).
2. Determine o bump pelo tipo mais alto presente entre esses commits:
   - `BREAKING CHANGE`/`!` → MINOR enquanto o MAJOR estiver travado em `0`, MAJOR a partir de `1.0.0`
   - `feat` → MINOR
   - só `fix`/outros tipos → PATCH
3. Adicione uma seção ao `CHANGELOG.md` com a versão, a data e os commits agrupados por tipo.
4. Commite o `CHANGELOG.md`: `chore: release vX.Y.Z`.
5. Crie a tag anotada sobre esse commit e publique: `git tag -a vX.Y.Z -m "vX.Y.Z"` seguido de
   `git push --tags`.
