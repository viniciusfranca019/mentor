---
description: Socrates evaluation of your lessons today
argument-hint: "[YYYY-MM-DD]"
disable-model-invocation: true
allowed-tools: Read(/${CLAUDE_PLUGIN_ROOT}/**), Read(~/.claude/plugins/cache/socrates/**), Read(~/.socrates/**), Write(~/.socrates/**), Edit(~/.socrates/**), Bash(mkdir -p ~/.socrates:*), Bash(date:*), Bash(ls ~/.socrates:*), Bash(ls -d ~/.mentor:*)
---

# Day feedback

Read `${CLAUDE_PLUGIN_ROOT}/skills/socrates/SKILL.md` (the skill `socrates:socrates`) and run the **Workflow: day evaluation** with the rubric in
`references/feedback.md`.

- Plugin root: `${CLAUDE_PLUGIN_ROOT}`.
- First of all, the migration from the old name: run the check in the Migration from Mentor section of
  `references/state.md` (`ls -d ~/.mentor ~/.socrates`) and do what its table says.
- Day evaluated: `$ARGUMENTS`. If empty, it is today (`date +%F`).
- The evaluation uses only the active course's journal in `~/.socrates/<course>/journal/<day>.md`. If
  it does not exist or is empty, say so and suggest `/socrates:mentor-mode`. Do not evaluate
  without a journal. Exception: when the day closed a phase of the track, the reassessment of the axis
  level reads all of the phase's journals.
