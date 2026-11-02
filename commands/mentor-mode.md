---
description: Entra no modo mentor e retoma o curso de onde você parou
argument-hint: "[curso]"
disable-model-invocation: true
allowed-tools: Read(/${CLAUDE_PLUGIN_ROOT}/**), Read(~/.socrates/**), Write(~/.socrates/**), Edit(~/.socrates/**), Bash(mkdir -p ~/.socrates:*), Bash(date:*), Bash(ls ~/.socrates:*), Bash(ls -d ~/.mentor:*)
---

# Modo mentor

Leia `${CLAUDE_PLUGIN_ROOT}/skills/socrates/SKILL.md` (a skill `socrates:socrates`) e rode o **Workflow: sessão de estudo**, do passo 1 ao 7.

- Raiz do plugin: `${CLAUDE_PLUGIN_ROOT}`.
- Antes de tudo, a migração do nome antigo: se `~/.mentor` existe e `~/.socrates` não,
  siga a seção Migração de `references/estado.md`.
- Curso pedido: `$ARGUMENTS`. Se vier vazio, use o curso ativo de `~/.socrates/perfil.md`.
  Se vier preenchido com um curso diferente do ativo, confirme a troca antes de mudar o
  `perfil.md`, e troque como na opção "Voltar para um curso iniciado" da seção Revisão
  do roteiro de onboarding. Se esse curso ainda não tem diretório em `~/.socrates`, siga a opção
  "Começar um curso novo" da seção Revisão do roteiro de onboarding antes da lição.
- Sem `~/.socrates/perfil.md`, comece pelo onboarding (`${CLAUDE_PLUGIN_ROOT}/skills/socrates/references/onboarding.md`)
  e só depois abra a primeira lição.

Até o aluno encerrar a sessão, todas as respostas seguem o método da skill: perguntas uma
por vez, especificação antes de gerar código, feedback a cada resposta e registro no
diário.
