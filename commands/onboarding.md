---
description: Mostra os cursos, explica o caminho, faz o diagnóstico e combina o ritmo; depois, troca de curso
disable-model-invocation: true
allowed-tools: Read(~/.mentor/**), Write(~/.mentor/**), Edit(~/.mentor/**), Bash(mkdir -p ~/.mentor:*), Bash(date:*), Bash(ls ~/.mentor:*)
---

# Onboarding do Mentor

Leia `${CLAUDE_PLUGIN_ROOT}/skills/mentor/SKILL.md` (a skill `mentor:mentor`) e rode o **Workflow: onboarding**, seguindo
`references/onboarding.md` bloco a bloco, esperando a resposta do aluno entre um bloco e
outro.

- Raiz do plugin: `${CLAUDE_PLUGIN_ROOT}`.
- A primeira mensagem já mostra o catálogo de cursos e pergunta qual ele quer.
- Se `~/.mentor/perfil.md` já existir, ele está voltando: siga a seção **Revisão** do
  roteiro (os cursos com a situação de cada um e as quatro opções).
