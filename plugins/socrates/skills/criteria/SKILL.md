---
name: criteria
description: >
  Socrates criteria for its extensions: the levels-by-axis scale, the evaluation
  rubric, the state format in ~/.socrates and the course and extension contracts.
  Use only when a Socrates extension (a socrates-<x> plugin such as socrates-pdi) needs
  the Socrates scale, rubric, state format or contracts; it runs no workflow by itself.
---

# Socrates criteria

This file runs nothing. It tells a Socrates extension where the criteria that hold
for all of them are, because one plugin does not read another by relative path.

- **Socrates root:** `${CLAUDE_PLUGIN_ROOT}`. In the files below, `<root>` is this path.
- **Socrates version:** the `version` in `${CLAUDE_PLUGIN_ROOT}/.claude-plugin/plugin.json`.

| Criterion | File | What for |
|-----------|------|----------|
| Levels by axis | `${CLAUDE_PLUGIN_ROOT}/skills/socrates/references/levels.md` | The 1-to-5 scale, the nine layers and the rule "by the answer, never by the claim" |
| Evaluation | `${CLAUDE_PLUGIN_ROOT}/skills/socrates/references/feedback.md` | The rubric and the tone: honest, specific, each statement tied to a record |
| Student state | `${CLAUDE_PLUGIN_ROOT}/skills/socrates/references/state.md` | The format of `~/.socrates`, the migration from Mentor and the writing rules |
| Course contract | `${CLAUDE_PLUGIN_ROOT}/skills/socrates/references/course-contract.md` | What a course plugin must have |
| Extension contract | `${CLAUDE_PLUGIN_ROOT}/skills/socrates/references/extension-contract.md` | What a plugin that is not a course (like the PDI) must have and may do |
