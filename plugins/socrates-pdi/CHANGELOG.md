# Changelog: socrates-pdi

Format based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), versions
in [Semantic Versioning](https://semver.org/).

## [Unreleased]

## [0.2.0] - 2026-11-02

### Changed

- The PDI is in English and speaks the student's language, the `Language` of
  `profile.md`. It reads the criteria through `socrates:criteria` and the course levels
  from `<course>/progress.md`. Declares `socrates` `>=0.5.0` in `dependencies`, so it stays disabled on an older engine.

## [0.1.0] - 2026-11-02

### Added

- `/socrates-pdi:pdi`: builds the student's PDI (a goal with an arrival signal, 3 to 5
  competencies, current level on the Socrates scale, target level, 70-20-10 actions with
  deadline and evidence) and, with the PDI already created, runs the check-in.
- A competency's level follows the Socrates scale: it comes from the course record or from
  the diagnosis (M, then D or R), with the demonstrated layers recorded, never from the
  declaration. Without a course, the target goes up to 4, because layers 6 to 9 only come
  from a module's exit test. The criteria are read from Socrates through the
  `socrates:criterios` skill.
- The check-in updates the plan's tables (actions, levels, next check-in) and appends the
  day's section; old check-ins do not change.
- The PDI lives in `~/.socrates/pdi/pdi.md`, with the check-ins appended at the end.

[Unreleased]: https://github.com/viniciusfranca019/socrates/compare/socrates-pdi--v0.2.0...HEAD
[0.2.0]: https://github.com/viniciusfranca019/socrates/compare/socrates-pdi--v0.1.0...socrates-pdi--v0.2.0
[0.1.0]: https://github.com/viniciusfranca019/socrates/releases/tag/socrates-pdi--v0.1.0
