# Student state: `~/.socrates`

The state lives on the student's machine, outside the plugin. Updating or reinstalling the plugin
never erases progress. Everything is Markdown, so the student can open and read their own history.

```
~/.socrates/
├── profile.md                         # who they are, active course, agreed pace
├── <extension>/                       # an extension's state, e.g.: pdi/ (extension-contract.md)
└── <course>/                          # one directory per started course
    ├── progress.md                  # where they are, what they completed, what to review
    └── journal/
        └── YYYY-MM-DD.md             # everything that happened that day
```

## Migration from Mentor

The plugin was called Mentor and kept its state in `~/.mentor`. Before reading any
state, check with `ls -d ~/.mentor ~/.socrates` which ones exist:

| Exists | What to do |
|--------|------------|
| Only `~/.mentor` | Stop and ask the student to move the folder themselves, by typing in Claude Code `! mv ~/.mentor ~/.socrates`, and to repeat what they asked for (the command, or the request that opened the session). The files do not change format, only location. You do not move it: writing outside the session folder asks for an approval that does not always show up |
| Both | Do not move anything. Use `~/.socrates` and say in one line that `~/.mentor` was left behind and can be deleted whenever they want |
| Only `~/.socrates`, or neither | Nothing to migrate. Go on without mentioning it |

## Templates

Create each file by copying the matching template and filling in the fields:

| File | Template |
|------|----------|
| `~/.socrates/profile.md` | `<root>/skills/socrates/templates/profile.md` |
| `~/.socrates/<course>/progress.md` | `<root>/skills/socrates/templates/progress.md` |
| `~/.socrates/<course>/journal/YYYY-MM-DD.md` | `<root>/skills/socrates/templates/journal.md` |

`progress.md` starts with the track from `course.md`: copy the course's list of modules and lessons
into the "Track" section, all unchecked.

## Writing rules

- **ISO dates** (`2026-10-02`), always the real date of the day. To get the date, use
  `date +%F`.
- **The journal only grows.** Append to the end and never rewrite old entries. It is the
  record of what happened.
- **Progress reflects the present.** It can be edited: check a lesson, move "Where I stopped",
  update "To review" and "Levels by axis".
- **Layers in every answer.** Each question in the journal records the layer it asked for and the
  layers the answer demonstrated (`references/levels.md`). It is the evidence for the level reassessment.
- **Faithful summary of the answer.** In the journal, summarize what they said in their own words.
  Do not improve the answer: `/socrates:feedback` needs to see what they actually answered.
- **New course, new directory.** Switching courses does not erase the other one; `profile.md` changes
  the active course and the status of both in the "Courses" table (`in progress` and `paused`).
- **Course version.** Note in `progress.md` the plugin version in which they started
  each module: the version of the course plugin, which the skill `socrates-<course>:course` gives. If the
  module changes in an update, you know the lesson in progress may have changed.
