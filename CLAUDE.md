# CLAUDE.md — Mentor

Plugin do Claude Code com um mentor socrático e seus cursos. Tudo em PT-BR.

## Estrutura

- `skills/mentor/`: o motor, igual para todos os cursos. Método em `references/`,
  templates do estado do aluno em `templates/`.
- `cursos/<curso>/`: conteúdo puro (`curso.md` + `modulos/NN-nome.md`). Curso novo não
  mexe no motor. Formato: `skills/mentor/references/anatomia-do-curso.md`.
- `commands/`: as entradas `/mentor:onboarding`, `/mentor:mentor-mode`, `/mentor:feedback`.
- O estado do aluno mora em `~/.mentor`, nunca dentro do plugin.

## Caminhos

`${CLAUDE_PLUGIN_ROOT}` só é substituído no corpo do `SKILL.md` e dos commands. Em
`references/` e `cursos/`, escreva `<raiz>`: o `SKILL.md` diz ao modelo o que isso vale.

## Versionamento e release

SemVer com tags `vX.Y.Z`. A `version` de `.claude-plugin/plugin.json` é o que faz a
atualização chegar ao aluno: sem subir a versão, ninguém recebe a mudança.

| Mudança | Versão |
|---------|--------|
| Correção de texto, de pergunta ou de critério | PATCH |
| Módulo ou lição nova, curso novo, comando novo; mudar perguntas de lição publicada | MINOR |
| Mudar o formato de `~/.mentor` de um jeito que quebra o progresso de quem já começou | MAJOR |

Release: atualizar `CHANGELOG.md` (mover `Unreleased` para a versão, com a data ISO do
dia), subir `version` no `plugin.json`, `claude plugin validate .`, PR, merge, e só então
`git tag vX.Y.Z` no commit do merge e `git push --tags`.

## Git

Nada é commitado em `main`. Trabalho em worktree em `WIP/`, PR para `main`.
