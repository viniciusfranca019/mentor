# Extension contract

Reading for whoever **writes** a Socrates extension that is not a course: a method that
uses the Socrates criteria for something else, like the PDI (`socrates-pdi`). A course
follows `course-contract.md`; this contract is for everything else. Version: **1**.

The difference: a course is only data, and the engine runs it. An extension brings its own
workflow (skill and command), and uses only the criteria and the state from Socrates.

## The extension plugin

```
plugins/socrates-<extension>/
├── .claude-plugin/plugin.json      # name socrates-<extension>, version, "dependencies": ["socrates"]
├── commands/<extension>.md          # the entry point: /socrates-<extension>:<extension>
├── skills/<extension>/
│   ├── SKILL.md                    # the extension's method
│   └── templates/                  # the format of its state
├── CHANGELOG.md
└── LICENSE
```

| The contract requires | Why |
|-----------------------|-----|
| `"dependencies": ["socrates"]` in `plugin.json` and in the marketplace entry | Installing the extension installs Socrates, which has the criteria |
| Loading the skill `socrates:criteria` before using a scale or a rubric, and reading the files it points to | The criteria belong to Socrates, in one place only. The extension does not copy the level scale or the rubric: a copy diverges at the first change |
| The state in `~/.socrates/<extension>/`, with the same migration check from `state.md` before reading or creating any file | The student has a single place for their history, and the extension survives updates like the courses do |
| Reading the courses' state (`profile.md`, `progress.md`, journals), **never writing** to it | A course's progress belongs to the engine. An extension that writes there breaks the level reassessment, which depends on the journal |
| Commands with `disable-model-invocation: true` and `allowed-tools` with `Read(/${CLAUDE_PLUGIN_ROOT}/**)`, `Read(~/.claude/plugins/cache/socrates/**)` and access to `~/.socrates/**` | This is what lets the first turn read the extension, the criteria and the state without asking for approval |
| The entry skill **without** `allowed-tools` | With it, loading the skill asks for approval |
| A line in the Extensions section of `plugins/socrates/skills/socrates/catalog.md` | The Socrates onboarding shows what exists before it is installed |

The name `<extension>` cannot be a course's name: the two share `~/.socrates/`.
