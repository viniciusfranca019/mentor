# Course contract

Reading for whoever **writes** courses, not for the student. The engine (`socrates:socrates`)
is the same for every course and does not change when a course is added. A course is only
data, in a separate plugin of the `socrates` marketplace, and this file is the contract that
plugin fulfills. Contract version: **2**.

Version 2 renamed the Portuguese names of v1 (skill `curso` → `course`, `curso/` →
`course/`, `curso.md` → `course.md`, `modulos/` → `modules/`), and course content is
written in English.

## The course plugin

```
plugins/socrates-<course>/                # <course> in kebab-case, e.g.: security-engineer
├── .claude-plugin/plugin.json           # name, version, "dependencies": ["socrates"]
├── skills/course/SKILL.md                # the bridge: tells the engine where the content is
├── course/
│   ├── course.md                         # vision, axes and diagnosis, track
│   └── modules/
│       ├── 00-<name>.md                 # one file per module
│       └── 01-<name>.md
├── CHANGELOG.md
└── LICENSE
```

| Piece | What the contract requires | Why |
|-------|----------------------------|-----|
| `plugin.json` | `name` equal to `socrates-<course>`, SemVer `version` and `"dependencies": ["socrates"]` | Installing the course installs the engine with it; the name is the prefix of the skill the engine looks for |
| `skills/course/SKILL.md` | `name: course`. The `description` starts with `Socrates course: <course>.` and gives who it is for, where you get to and the status (what is available). It is the **only** source of this data for an installed course: update it in the same PR as each new module. The body states the **course root** with `${CLAUDE_PLUGIN_ROOT}/course` and the contract version. **No** `allowed-tools` and **no** `disable-model-invocation` | The engine does not read files from another plugin by relative path: it is by loading this skill that it finds out the absolute path. With `allowed-tools`, loading the skill starts asking for approval, and in the headless test it was denied |
| `course/course.md` | The sections below | The diagnosis and the track come from here |
| `course/modules/<NN-name>.md` | The module format below | The lessons come from here |
| Marketplace | An entry in the root `.claude-plugin/marketplace.json`, with `source: "./plugins/socrates-<course>"` and `dependencies: ["socrates"]` | It is what the student installs |
| Catalog | A line in `plugins/socrates/skills/socrates/catalog.md`: who it is for, where you get to and the install command, without the status | It is the storefront for those who have not installed it yet. The installed course appears even without it, through the skill, so the course works without waiting for an engine release |

In the course files, `<root>` is still the root of the `socrates` plugin (the engine knows
it), and `<course>` is the course root that its skill points to. The data format is
Markdown: the model is what reads it, and the student opens and understands the same files.

## Creating a new course

1. Copy the structure above from `plugins/socrates-security-engineer/`, change the name and
   the `description` of the `course` skill.
2. Write `course/course.md` with the sections below and at least the first module complete.
3. Add the entry in `marketplace.json`, the line in the engine's catalog and the line in the
   table of the root `README.md`.
4. `claude plugin validate plugins/socrates-<course>` and `claude plugin validate .`.
5. The course starts at version `0.1.0`, with its own `CHANGELOG.md`. The catalog line
   bumps a PATCH of `socrates`, but the course does not depend on it to work: only to
   appear in the storefront for those who have not installed it yet.
6. With each new module: bump the course (MINOR) and the status in the `description` of the
   `course` skill. The engine does not change.

## `course.md`

| Section | Content |
|---------|---------|
| **Who it is for** | The target student and the expected starting point |
| **Where you get to** | What the student can do on finishing |
| **Course principle** | The idea that ties the whole course together |
| **Axes and diagnosis** | 3 to 6 axes, each linked to phases of the track. Per axis, a ladder of three questions: **R** (recognize, layers 1 and 2), **M** (mechanism, layer 3) and **D** (diagnosis and decision, layers 4 and 5), each with the layer's criteria, plus a **D2** (another diagnosis and decision problem) for whoever challenges level 3. Scale and rules in `<root>/skills/socrates/references/levels.md` |
| **Track** | Phases → modules → lessons, with the status of each module (`available` or `planned`) |

## Module (`modules/<NN-name>.md`)

Module header: **Goal** (one sentence), **Prerequisites** (previous modules) and
**Why it matters for the course** (the link to the final goal).

Each lesson has exactly these parts:

```markdown
## Lesson N.M — <name>

**Anchor concept:** <the idea the student needs to be able to explain at the end, in 1 or 2 sentences>

### Opening
1. <question>
   - A good answer contains: <criteria>
2. ...

### Mission
<What to build with Claude, in 2 or 3 sentences, and why that makes the concept visible.>

Specification questions (before generating the code):
1. <question>
   - A good answer contains: <criteria>

### Verification
1. <prediction, breaking or explanation question>
   - A good answer contains: <criteria>

### Tool
<The industry tool and the question that links the tool to the mission.>

### Explain back
<The final request. Criteria: what the explanation needs to contain for the lesson to close.>

### For Socrates
- **Common mistakes:** <typical confusions and how to clear them up>
- **Bridge to security:** <why this concept matters for the course's goal>
```

## Writing rules

- **One idea per lesson.** If the anchor concept needs an "and" to join two ideas, it is
  two lessons.
- **Questions without the answer inside.** See the table of good and bad questions in
  `references/method.md`.
- **Observable criteria.** "A good answer contains" lists ideas that can be checked in the
  answer, not "understands the subject well".
- **Small mission.** 10 to 60 lines of code, running on the student's machine, with no
  paid service.
- **Changes to a published module.** Fixing text is PATCH. Changing the questions or the
  mission of a published lesson is MINOR, with a note in the CHANGELOG, because students
  may be in the middle of it.
