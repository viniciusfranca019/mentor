---
description: Avaliação do Mentor sobre as suas lições de hoje
argument-hint: "[AAAA-MM-DD]"
disable-model-invocation: true
allowed-tools: Read(~/.mentor/**), Write(~/.mentor/**), Edit(~/.mentor/**), Bash(mkdir -p ~/.mentor:*), Bash(date:*), Bash(ls ~/.mentor:*)
---

# Feedback do dia

Leia `${CLAUDE_PLUGIN_ROOT}/skills/mentor/SKILL.md` (a skill `mentor:mentor`) e rode o **Workflow: avaliação do dia** com a rubrica de
`references/feedback.md`.

- Raiz do plugin: `${CLAUDE_PLUGIN_ROOT}`.
- Dia avaliado: `$ARGUMENTS`. Se vier vazio, é hoje (`date +%F`).
- A avaliação usa só o diário do curso ativo em `~/.mentor/<curso>/diario/<dia>.md`. Se
  ele não existir ou estiver vazio, diga isso e sugira `/mentor:mentor-mode`. Não avalie
  sem diário. Exceção: quando o dia fechou uma fase da trilha, a reavaliação do nível do
  eixo lê todos os diários da fase.
