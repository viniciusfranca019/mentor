# Socrates

A Socratic mentor inside Claude Code. Socrates runs a course lesson by lesson: it asks
questions instead of giving answers, lets you build with AI while it questions every
decision and, at the end of the day, evaluates how you did.

Socrates does not forbid AI: it teaches you to drive AI. You use Claude Code to write
code all the time, but before generating anything you specify what you want, and
afterwards you explain what you got. A tool, AI included, is a shortcut for something you
already understand.

## The marketplace

Socrates is the mentor, and each course is a separate plugin that it runs. Installing a
course installs Socrates with it.

| Plugin | What it is |
|--------|------------|
| `socrates` | The mentor: Socratic method, levels by axis, day evaluation and your progress in `~/.socrates` |
| `socrates-pdi` | Extension: your PDI, Individual Development Plan, with the Socrates level scale, 70-20-10 actions and check-ins. Entry point: `/socrates-pdi:pdi` |
| `socrates-security-engineer` | Course: security engineer in the age of AI, for people with an IT background but little practice in programming, networks and infrastructure |

What each course already has available shows up in `/socrates:onboarding`.

## Setup

Prerequisite: [Claude Code](https://code.claude.com) installed.

```bash
claude plugin marketplace add viniciusfranca019/mentor
claude plugin install socrates-security-engineer@socrates
```

The second command installs the course and `socrates`. Another course, later, is just one
more `claude plugin install socrates-<course>@socrates`; `/socrates:onboarding` shows the
catalog and the command for each one. The PDI too: `claude plugin install socrates-pdi@socrates`.

Installed it back when it was still called Mentor? Swap the plugin once and move your
progress with `mv ~/.mentor ~/.socrates` (the first command also reminds you of this):

```bash
claude plugin uninstall mentor@mentor
claude plugin marketplace remove mentor
claude plugin marketplace add viniciusfranca019/mentor
claude plugin install socrates-security-engineer@socrates
```

Then, inside Claude Code:

| Command | When to use it |
|---------|----------------|
| `/socrates:onboarding` | The first time: shows the courses, the path and runs the diagnosis. Later: see the courses, switch course or adjust the pace |
| `/socrates:mentor-mode` | Every time you study. Picks up where you stopped |
| `/socrates:feedback` | When you finish the day's lessons. Evaluates how you did |

> Use the `socrates:` prefix on feedback: `/feedback` without a prefix is Claude Code's own
> command for sending feedback to Anthropic.

### Getting updates

New modules arrive as new versions of the course plugin, and improvements to the method as
new versions of `socrates`. To get them automatically,
turn on auto-update for this marketplace (it is off by default for third-party marketplaces):
`/plugin` → **Marketplaces** → `socrates` → **Enable auto-update**. Or update by hand:

```bash
claude plugin update socrates@socrates
claude plugin update socrates-security-engineer@socrates
```

An open session stays on the old version until `/reload-plugins` or a new session.

## Your progress

It lives on your machine, in `~/.socrates`, and is never deleted by a plugin update:

```
~/.socrates/
├── profile.md                    # you, the active course and the agreed pace
└── <course>/
    ├── progress.md               # where you stopped, what you finished, what to review
    └── journal/YYYY-MM-DD.md     # every question, your answer and the feedback
```

## How it works inside

| Piece | What it is |
|-------|------------|
| `plugins/socrates/` | The engine: the Socratic method, the levels, the feedback rubric, the state format and the course catalog. It is the same for every course |
| `plugins/socrates-pdi/` | An extension: brings its own method (build the PDI and run the check-in) and reads the criteria from Socrates, through the `socrates:criteria` skill |
| `plugins/socrates-<course>/` | A course: the track (`course/course.md`), one file per module and the `course` skill, which tells the engine where the content is |
| `.claude-plugin/marketplace.json` | The list of plugins that `marketplace add` brings |

To write a new course, see the
[course contract](plugins/socrates/skills/socrates/references/course-contract.md); for
an extension, the [extension contract](plugins/socrates/skills/socrates/references/extension-contract.md).

## Versioning

[Semantic Versioning](https://semver.org/) per plugin, with tags
`<plugin>--vX.Y.Z` (e.g. `socrates--v0.3.0`). The version in each plugin's `plugin.json` is
what triggers the update for people who already installed it: a new commit without a
version bump reaches no one. Each plugin has its own `CHANGELOG.md`.

## License

[Apache 2.0](LICENSE).
