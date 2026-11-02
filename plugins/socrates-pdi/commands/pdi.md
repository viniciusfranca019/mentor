---
description: Monta o seu PDI com o Socrates ou faz o check-in do PDI que você já tem
disable-model-invocation: true
allowed-tools: Read(/${CLAUDE_PLUGIN_ROOT}/**), Read(~/.claude/plugins/cache/socrates/**), Read(~/.socrates/**), Write(~/.socrates/**), Edit(~/.socrates/**), Bash(mkdir -p ~/.socrates:*), Bash(date:*), Bash(ls ~/.socrates:*), Bash(ls -d ~/.mentor:*)
---

# PDI

Leia `${CLAUDE_PLUGIN_ROOT}/skills/pdi/SKILL.md` (a skill `socrates-pdi:pdi`) e siga-a.

- Raiz do PDI: `${CLAUDE_PLUGIN_ROOT}`. Os critérios vêm do Socrates: carregue a skill
  `socrates:criterios` e leia os arquivos que ela indica.
- Sem `~/.socrates/pdi/pdi.md`: **Workflow: montar o PDI**. Com ele: **Workflow: check-in**.
