# Contribuindo

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
