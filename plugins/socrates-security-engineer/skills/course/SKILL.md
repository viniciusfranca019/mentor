---
name: course
description: >
  Socrates course: security-engineer. Who it is for: people with an IT degree but little
  practice in programming, networks and infrastructure. Where you get to: security engineer
  in the age of AI. Status: modules 00 and 01 available, of 42. Use only when the Socrates
  engine (socrates:socrates) lists, diagnoses or teaches this course; never on its own.
---

# Course security-engineer

This file is the Socrates course contract, version 2. It teaches nothing: it tells the
engine (`socrates:socrates`) where this course's content is.

- **Course:** `security-engineer`
- **Course root:** `${CLAUDE_PLUGIN_ROOT}/course`
- **Track, axes and diagnosis:** `${CLAUDE_PLUGIN_ROOT}/course/course.md`
- **Modules:** `${CLAUDE_PLUGIN_ROOT}/course/modules/<NN-name>.md`
- **Course version:** the `version` in `${CLAUDE_PLUGIN_ROOT}/.claude-plugin/plugin.json`

In the course files, `<course>` means the course root above, and `<root>` means the root
of the `socrates` plugin, which the engine knows.
