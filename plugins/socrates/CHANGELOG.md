# Changelog

Format based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), versions
in [Semantic Versioning](https://semver.org/).

## [Unreleased]

### Changed

- The repository is now `viniciusfranca019/socrates`. The old name `viniciusfranca019/mentor`
  redirects, so an existing install keeps working; new installs use
  `claude plugin marketplace add viniciusfranca019/socrates`.

## [0.5.0] - 2026-11-02

### Changed

- Everything in English: the method, references, templates, catalog and commands. Socrates
  speaks the student's language, recorded as `Language` in `profile.md`: `en-US` by default,
  switched when the student asks. It translates what the student reads and keeps the state
  in English.
- English names for the state and the skills: `profile.md`, `<course>/progress.md`,
  `<course>/journal/`, the skill `socrates:criteria`, and course contract version 2 (skill
  `socrates-<course>:course`, `course/course.md`, `course/modules/`). The references are
  `state.md`, `levels.md`, `method.md`, `course-contract.md` and `extension-contract.md`.
  Needs a course plugin on contract 2.

### Added

- Migration of the Portuguese state names: with `~/.socrates/perfil.md`, the first command
  stops and gives the student one `!` command that renames the files; from `~/.mentor`, the
  same command also moves the folder.

## [0.4.0] - 2026-11-02

### Added

- `socrates:criterios` skill: tells an extension where the levels, the rubric, the state
  format and the contracts are, because one plugin does not read another by relative path.
- `references/contrato-de-extensao.md`: what a plugin that is not a course needs to have
  (its own method, `dependencies: ["socrates"]`, state in `~/.socrates/<extension>/`, and
  never writing to a course's state).
- The catalog gets the Extensions section, with the PDI (`socrates-pdi`), and onboarding
  shows the PDI in the path and in the review.

## [0.3.0] - 2026-11-02

### Changed

- The repository becomes a marketplace with one plugin per piece: `socrates` is the engine
  (method, levels, evaluation, student state), and each course is a separate plugin,
  `socrates-<curso>`, that requires `socrates`. The first is `socrates-security-engineer`.
  Versions and tags per plugin (`socrates--v0.3.0`).
- The engine finds a course through the `socrates-<curso>:curso` skill, which gives the
  content root. Course not installed: Socrates shows the install command and stops.
- Onboarding shows in the catalog whether each course is installed and teaches that
  courses are plugins. The review gets the **not installed** status.
- `references/anatomia-do-curso.md` becomes `references/contrato-de-curso.md`: what a
  course plugin needs to have, in addition to the course and module format.

- The plugin is now called **Socrates**: the plugin and the marketplace are `socrates`
  (`claude plugin install socrates@socrates`), the commands become `/socrates:onboarding`,
  `/socrates:mentor-mode` and `/socrates:feedback`, and the skill becomes `socrates:socrates`
  (`skills/socrates/`). The repository stays `viniciusfranca019/socrates`.
- The student's state moves from `~/.mentor` to `~/.socrates`, in the same format. If only
  the old folder exists, the first command asks the student to run
  `! mv ~/.mentor ~/.socrates` and repeat the command.

### Fixed

- The commands pre-authorize reading the plugin's own files
  (`Read(/${CLAUDE_PLUGIN_ROOT}/**)`): installed from the marketplace, `/socrates:onboarding`
  stopped on the first turn, unable to read SKILL.md, the references and the catalog.

## [0.2.0] - 2026-10-06

### Added

- Levels by course axis, from 1 (layperson) to 5 (expert), with depth weights
  1, 2, 3, 5 and 9 measured across nine layers of knowledge and practice
  (`skills/mentor/references/niveis.md`).
- Adaptive diagnosis by axis in onboarding: two questions per axis, with the result shown
  to the student and recorded in `progresso.md`. In `security-engineer`, the axes are
  Systems, Networks, Building with AI, Infrastructure and Security.
- Exit test: on an axis at level 4 or 5, the module can be validated by proving layers
  6 to 9, without skipping content by declaration.
- Reassessment of the axis level by `/mentor:feedback` at the end of each phase. The
  journal records the layers of each answer.

### Changed

- Straight-to-the-point onboarding: the first message shows the course catalog and asks
  which one the student wants, and the "The path" block shows on one screen
  the day-to-day use and how to switch course later.
- The four lesson phases are now explained at the start of the first lesson, not in
  onboarding.
- Revisiting onboarding with a profile already created shows the courses with the status
  of each one (active, started, not started) and the options: continue, go back to a
  course, start a new course or adjust the pace. Starting another course runs only its
  diagnosis.

## [0.1.0] - 2026-10-06

### Added

- Mentoring engine (`skills/mentor`): Socratic method in four phases (Opening, Mission,
  Verification, Tool), hint ladder, AI-assisted building guided by specification, student
  state in `~/.mentor` and templates for profile, progress and journal.
- Commands `/mentor:onboarding`, `/mentor:mentor-mode` and `/mentor:feedback`.
- `security-engineer` course: a track of 42 modules in 8 phases, initial diagnosis,
  module 00 (Your lab) and module 01 (How the computer represents things).

[Unreleased]: https://github.com/viniciusfranca019/socrates/compare/socrates--v0.5.0...HEAD
[0.5.0]: https://github.com/viniciusfranca019/socrates/compare/socrates--v0.4.0...socrates--v0.5.0
[0.4.0]: https://github.com/viniciusfranca019/socrates/compare/socrates--v0.3.0...socrates--v0.4.0
[0.3.0]: https://github.com/viniciusfranca019/socrates/compare/v0.2.0...socrates--v0.3.0
[0.2.0]: https://github.com/viniciusfranca019/socrates/compare/v0.1.0...v0.2.0
[0.1.0]: https://github.com/viniciusfranca019/socrates/releases/tag/v0.1.0
