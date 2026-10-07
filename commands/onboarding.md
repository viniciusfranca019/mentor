---
description: Apresenta o Mentor, escolhe o curso, faz o diagnóstico e combina o ritmo
disable-model-invocation: true
allowed-tools: Read(~/.mentor/**), Write(~/.mentor/**), Edit(~/.mentor/**), Bash(mkdir -p ~/.mentor:*), Bash(date:*), Bash(ls ~/.mentor:*)
---

# Onboarding do Mentor

Leia `${CLAUDE_PLUGIN_ROOT}/skills/mentor/SKILL.md` (a skill `mentor:mentor`) e rode o **Workflow: onboarding**, seguindo
`references/onboarding.md` bloco a bloco, esperando a resposta do aluno entre um bloco e
outro.

- Raiz do plugin: `${CLAUDE_PLUGIN_ROOT}`.
- Se `~/.mentor/perfil.md` já existir, ele está revendo: faça só o bloco 1 e pergunte se
  quer trocar de curso ou ajustar o ritmo.
