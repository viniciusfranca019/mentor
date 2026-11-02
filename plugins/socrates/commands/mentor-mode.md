---
description: Enters mentor mode and resumes the course where you stopped
argument-hint: "[course]"
disable-model-invocation: true
allowed-tools: Read(/${CLAUDE_PLUGIN_ROOT}/**), Read(~/.claude/plugins/cache/socrates/**), Read(~/.socrates/**), Write(~/.socrates/**), Edit(~/.socrates/**), Bash(mkdir -p ~/.socrates:*), Bash(date:*), Bash(ls ~/.socrates:*), Bash(ls -d ~/.mentor:*)
---

# Mentor mode

Read `${CLAUDE_PLUGIN_ROOT}/skills/socrates/SKILL.md` (the skill `socrates:socrates`) and run the **Workflow: study session**, from step 1 to 7.

- Plugin root: `${CLAUDE_PLUGIN_ROOT}`.
- First of all, the migration from the old name: run the check in the Migration section of
  `references/state.md` (`ls -d ~/.mentor ~/.socrates ~/.socrates/perfil.md`) and do what its table says.
- Requested course: `$ARGUMENTS`. If empty, use the active course from `~/.socrates/profile.md`.
  If it names a course other than the active one, first check whether the skill
  `socrates-<course>:course` exists: without it, give the install command and stop without touching
  `profile.md`. If installed, confirm the switch before changing
  `profile.md`, and switch as in the option "Go back to a started course" of the Review section
  of the onboarding script. If that course has no directory in `~/.socrates` yet, follow the option
  "Start a new course" of the Review section of the onboarding script before the lesson.
- The course comes from another plugin, `socrates-<course>`: load the skill `socrates-<course>:course`
  to learn where its files are. If it does not exist in this session, the course is not
  installed: give the command from the "Install" column of the catalog and stop.
- Without `~/.socrates/profile.md`, start with the onboarding (`${CLAUDE_PLUGIN_ROOT}/skills/socrates/references/onboarding.md`)
  and only then open the first lesson.

Until the student ends the session, every answer follows the skill's method: questions one
at a time, specification before generating code, feedback on each answer and a record in the
journal.
