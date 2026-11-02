---
description: Mostra os cursos, explica o caminho, faz o diagnóstico e combina o ritmo; depois, troca de curso
disable-model-invocation: true
allowed-tools: Read(/${CLAUDE_PLUGIN_ROOT}/**), Read(~/.claude/plugins/cache/socrates/**), Read(~/.socrates/**), Write(~/.socrates/**), Edit(~/.socrates/**), Bash(mkdir -p ~/.socrates:*), Bash(date:*), Bash(ls ~/.socrates:*), Bash(ls -d ~/.mentor:*)
---

# Onboarding do Socrates

Leia `${CLAUDE_PLUGIN_ROOT}/skills/socrates/SKILL.md` (a skill `socrates:socrates`) e rode o **Workflow: onboarding**, seguindo
`references/onboarding.md` bloco a bloco, esperando a resposta do aluno entre um bloco e
outro.

- Raiz do plugin: `${CLAUDE_PLUGIN_ROOT}`.
- Antes de tudo, a migração do nome antigo: rode a checagem da seção Migração de
  `references/state.md` (`ls -d ~/.mentor ~/.socrates`) e faça o que a tabela dela manda.
- Sem `~/.socrates/profile.md`, é a primeira vez: blocos 1 a 5 do roteiro.
- Se `~/.socrates/profile.md` já existir, ele está voltando: siga a seção **Revisão** do
  roteiro (os cursos com a situação de cada um e as quatro opções).
