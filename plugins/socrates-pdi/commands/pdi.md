---
description: Build your PDI with Socrates, or run the check-in of the PDI you already have
disable-model-invocation: true
allowed-tools: Read(/${CLAUDE_PLUGIN_ROOT}/**), Read(~/.claude/plugins/cache/socrates/**), Read(~/.socrates/**), Write(~/.socrates/**), Edit(~/.socrates/**), Bash(mkdir -p ~/.socrates:*), Bash(date:*), Bash(ls ~/.socrates:*), Bash(ls -d ~/.mentor:*)
---

# PDI

Read `${CLAUDE_PLUGIN_ROOT}/skills/pdi/SKILL.md` (the `socrates-pdi:pdi` skill) and follow it.

- PDI root: `${CLAUDE_PLUGIN_ROOT}`. The criteria come from Socrates: load the
  `socrates:criteria` skill and read the files it points to.
- No `~/.socrates/pdi/pdi.md`: **Workflow: build the PDI**. With it: **Workflow: check-in**.
