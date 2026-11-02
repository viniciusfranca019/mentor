# CLAUDE.md — Socrates

Claude Code marketplace with a Socratic mentor (`socrates`) and the courses it runs, each
in its own plugin. Everything in US English. The repository is called `mentor` for
historical reasons.

## Structure

- `.claude-plugin/marketplace.json`: the `socrates` marketplace, one entry per plugin,
  `source: "./plugins/<plugin>"`. The entry's `name` equals the one in `plugin.json`.
- `plugins/socrates/`: the engine, the same for every course. Method in
  `skills/socrates/references/`, templates of the student's state in `templates/`, course
  catalog in `skills/socrates/catalog.md`, the entry points in `commands/`.
- `plugins/socrates-<course>/`: a course. Pure content in `course/`, plus the `course`
  skill that tells the engine where it is, and `"dependencies": [{ "name": "socrates", "version": ">=0.5.0" }]`. A new course
  does not touch the engine, only the catalog. The contract:
  `plugins/socrates/skills/socrates/references/course-contract.md`.
- `plugins/socrates-<extension>/`: a plugin that is not a course (the first is
  `socrates-pdi`). It brings its own method and reads the engine's criteria through the
  `socrates:criteria` skill. The contract:
  `plugins/socrates/skills/socrates/references/extension-contract.md`.
- The student's state lives in `~/.socrates`, never inside a plugin.

## Paths

`${CLAUDE_PLUGIN_ROOT}` is only substituted in the body of `SKILL.md` and of the commands,
and it is the root of the plugin that **owns** the file. One plugin does not read another
by relative path: the engine finds a course by loading the `socrates-<course>:course`
skill, which gives the absolute root. In `references/` and in course files, write `<root>`
(root of `socrates`) or `<course>` (root of the course). The `course` skill has no
`allowed-tools`: with it, loading the skill asks for approval, and headless it is denied.

## Versioning and release

SemVer per plugin, with tags `<plugin>--vX.Y.Z`. The `version` in each plugin's
`plugin.json` is what makes the update reach the student: without a version bump, no one
gets the change. Each plugin has its own `CHANGELOG.md`.

| Change | Version |
|--------|---------|
| Fix to text, to a question or to a criterion; a new line in the catalog | PATCH |
| New module or lesson, new command; changing questions of a published lesson | MINOR |
| Changing the format of `~/.socrates`, or the course contract, in a way that breaks what already exists | MAJOR |

While a plugin is in `0.x`, a breaking change is a MINOR, as SemVer allows, and its
CHANGELOG entry says what breaks and how the student migrates. One version, three places,
always the same number: the `version` in `plugin.json`, a `## [X.Y.Z]` heading in that
plugin's `CHANGELOG.md`, and one tag `<plugin>--vX.Y.Z`. A course or an extension that needs
a newer engine raises the range in its `dependencies` (`{ "name": "socrates", "version":
">=X.Y.Z" }`), which Claude Code checks when the plugin loads.

Release: in the plugin that changed, move `Unreleased` in `CHANGELOG.md` to the version
(ISO date of the day) and bump `version` in `plugin.json`; `claude plugin validate .` at
the root and `claude plugin validate plugins/<plugin>` in each plugin (the root one does
not open skills and commands); PR, merge, and only then, from the plugin directory on the updated
`main`, `claude plugin tag --push` (it validates, checks the version and creates
`<plugin>--vX.Y.Z`), or `git tag <plugin>--vX.Y.Z` on the merge commit and `git push --tags`.

## Testing

No suite. Test headless in an empty `.sandbox` folder, with the engine and the courses
loaded at once: `claude -p "/socrates:onboarding" --plugin-dir <worktree>/plugins`.
Outside the marketplace cache, reading the course files needs
`--allowedTools "Read(//<worktree>/plugins/**)"`; installed from the marketplace, the
commands' `Read(~/.claude/plugins/cache/socrates/**)` covers it. Delete the test
`~/.socrates` at the end.

## Git

Nothing is committed on `main`. Work in a worktree under `WIP/`, PR to `main`.
