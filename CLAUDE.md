# CLAUDE.md — Socrates

Marketplace do Claude Code com um mentor socrático (`socrates`) e os cursos que ele conduz,
cada um num plugin. Tudo em PT-BR. O repositório se chama `mentor` por história.

## Estrutura

- `.claude-plugin/marketplace.json`: o marketplace `socrates`, uma entrada por plugin,
  `source: "./plugins/<plugin>"`. O `name` da entrada é igual ao do `plugin.json`.
- `plugins/socrates/`: o motor, igual para todos os cursos. Método em
  `skills/socrates/references/`, templates do estado do aluno em `templates/`, catálogo
  de cursos em `skills/socrates/catalogo.md`, as entradas em `commands/`.
- `plugins/socrates-<curso>/`: um curso. Conteúdo puro em `curso/`, mais a skill `curso`
  que diz ao motor onde ele está, e `"dependencies": ["socrates"]`. Curso novo não mexe no
  motor, só no catálogo. O contrato: `plugins/socrates/skills/socrates/references/contrato-de-curso.md`.
- `plugins/socrates-<extensão>/`: um plugin que não é curso (o primeiro é `socrates-pdi`).
  Traz o próprio método e lê os critérios do motor pela skill `socrates:criterios`. O
  contrato: `plugins/socrates/skills/socrates/references/contrato-de-extensao.md`.
- O estado do aluno mora em `~/.socrates`, nunca dentro de um plugin.

## Caminhos

`${CLAUDE_PLUGIN_ROOT}` só é substituído no corpo do `SKILL.md` e dos commands, e vale a
raiz do plugin **dono** do arquivo. Um plugin não lê o outro por caminho relativo: o motor
acha um curso carregando a skill `socrates-<curso>:curso`, que diz a raiz absoluta. Em
`references/` e nos arquivos de curso, escreva `<raiz>` (raiz do `socrates`) ou `<curso>`
(raiz do curso). A skill `curso` não leva `allowed-tools`: com ele, carregá-la pede
aprovação, e no headless ela é negada.

## Versionamento e release

SemVer por plugin, com tags `<plugin>--vX.Y.Z`. A `version` do `plugin.json` de cada
plugin é o que faz a atualização chegar ao aluno: sem subir a versão, ninguém recebe a
mudança. Cada plugin tem o seu `CHANGELOG.md`.

| Mudança | Versão |
|---------|--------|
| Correção de texto, de pergunta ou de critério; uma linha nova no catálogo | PATCH |
| Módulo ou lição nova, comando novo; mudar perguntas de lição publicada | MINOR |
| Mudar o formato de `~/.socrates`, ou o contrato de curso, de um jeito que quebra o que já existe | MAJOR |

Release: no plugin que mudou, mover `Unreleased` do `CHANGELOG.md` para a versão (data
ISO do dia) e subir `version` no `plugin.json`; `claude plugin validate .` na raiz e
`claude plugin validate plugins/<plugin>` em cada plugin (o da raiz não abre skills e
commands); PR, merge, e só então `git tag <plugin>--vX.Y.Z` no commit do merge e
`git push --tags`.

## Testar

Sem suíte. Teste headless numa pasta vazia de `.sandbox`, com o motor e os cursos
carregados de uma vez: `claude -p "/socrates:onboarding" --plugin-dir <worktree>/plugins`.
Fora do cache do marketplace, a leitura dos arquivos do curso precisa de
`--allowedTools "Read(//<worktree>/plugins/**)"`; instalado pelo marketplace, o
`Read(~/.claude/plugins/cache/socrates/**)` dos comandos cobre. Apague o `~/.socrates`
de teste no fim.

## Git

Nada é commitado em `main`. Trabalho em worktree em `WIP/`, PR para `main`.
