---
description: Shows the courses, explains the path, runs the diagnosis and agrees on the pace; later, switches courses
disable-model-invocation: true
allowed-tools: Read(/${CLAUDE_PLUGIN_ROOT}/**), Read(~/.claude/plugins/cache/socrates/**), Read(~/.socrates/**), Write(~/.socrates/**), Edit(~/.socrates/**), Bash(mkdir -p ~/.socrates:*), Bash(date:*), Bash(ls ~/.socrates:*), Bash(ls -d ~/.mentor:*)
---

# Socrates onboarding

Read `${CLAUDE_PLUGIN_ROOT}/skills/socrates/SKILL.md` (the skill `socrates:socrates`) and run the **Workflow: onboarding**, following
`references/onboarding.md` block by block, waiting for the student's answer between one block and
the next.

- Plugin root: `${CLAUDE_PLUGIN_ROOT}`.
- First of all, the migration from the old name: run the check in the Migration from Mentor section of
  `references/state.md` (`ls -d ~/.mentor ~/.socrates`) and do what its table says.
- Without `~/.socrates/profile.md`, it is the first time: blocks 1 to 5 of the script.
- If `~/.socrates/profile.md` already exists, they are coming back: follow the **Review** section of
  the script (the courses with the status of each and the four options).
