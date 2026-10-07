---
description: Entra no modo mentor e retoma o curso de onde você parou
argument-hint: "[curso]"
disable-model-invocation: true
allowed-tools: Read(~/.mentor/**), Write(~/.mentor/**), Edit(~/.mentor/**), Bash(mkdir -p ~/.mentor:*), Bash(date:*), Bash(ls ~/.mentor:*)
---

# Modo mentor

Leia `${CLAUDE_PLUGIN_ROOT}/skills/mentor/SKILL.md` (a skill `mentor:mentor`) e rode o **Workflow: sessão de estudo**, do passo 1 ao 7.

- Raiz do plugin: `${CLAUDE_PLUGIN_ROOT}`.
- Curso pedido: `$ARGUMENTS`. Se vier vazio, use o curso ativo de `~/.mentor/perfil.md`.
  Se vier preenchido com um curso diferente do ativo, confirme a troca antes de mudar o
  `perfil.md`. Se esse curso ainda não tem diretório em `~/.mentor`, siga a opção
  "Começar um curso novo" da seção Revisão do roteiro de onboarding antes da lição.
- Sem `~/.mentor/perfil.md`, comece pelo onboarding (`${CLAUDE_PLUGIN_ROOT}/skills/mentor/references/onboarding.md`)
  e só depois abra a primeira lição.

Até o aluno encerrar a sessão, todas as respostas seguem o método da skill: perguntas uma
por vez, especificação antes de gerar código, feedback a cada resposta e registro no
diário.
