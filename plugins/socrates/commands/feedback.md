---
description: Avaliação do Socrates sobre as suas lições de hoje
argument-hint: "[AAAA-MM-DD]"
disable-model-invocation: true
allowed-tools: Read(/${CLAUDE_PLUGIN_ROOT}/**), Read(~/.claude/plugins/cache/socrates/**), Read(~/.socrates/**), Write(~/.socrates/**), Edit(~/.socrates/**), Bash(mkdir -p ~/.socrates:*), Bash(date:*), Bash(ls ~/.socrates:*), Bash(ls -d ~/.mentor:*)
---

# Feedback do dia

Leia `${CLAUDE_PLUGIN_ROOT}/skills/socrates/SKILL.md` (a skill `socrates:socrates`) e rode o **Workflow: avaliação do dia** com a rubrica de
`references/feedback.md`.

- Raiz do plugin: `${CLAUDE_PLUGIN_ROOT}`.
- Antes de tudo, a migração do nome antigo: se `~/.mentor` existe e `~/.socrates` não,
  siga a seção Migração de `references/estado.md`.
- Dia avaliado: `$ARGUMENTS`. Se vier vazio, é hoje (`date +%F`).
- A avaliação usa só o diário do curso ativo em `~/.socrates/<curso>/diario/<dia>.md`. Se
  ele não existir ou estiver vazio, diga isso e sugira `/socrates:mentor-mode`. Não avalie
  sem diário. Exceção: quando o dia fechou uma fase da trilha, a reavaliação do nível do
  eixo lê todos os diários da fase.
