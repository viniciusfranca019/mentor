# Student state: `~/.socrates`

The state lives on the student's machine, outside the plugin. Updating or reinstalling the plugin
never erases progress. Everything is Markdown, so the student can open and read their own history.

```
~/.socrates/
├── profile.md              # who they are, language, active course, agreed pace
├── <extension>/            # an extension's state, e.g.: pdi/ (extension-contract.md)
└── <course>/               # one directory per started course
    ├── progress.md         # where they are, what they completed, what to review
    └── journal/
        └── YYYY-MM-DD.md   # everything that happened that day
```

## Migration

Two older layouts can still be on the student's machine: the plugin was called Mentor and
kept its state in `~/.mentor`, and up to Socrates 0.4.0 the state files had Portuguese names
(`perfil.md`, `<course>/progresso.md`, `<course>/diario/`). Before reading any state, check
with `ls -d ~/.mentor ~/.socrates ~/.socrates/perfil.md` which ones exist (a path that does not
exist shows up as an error, which is the answer):

| Exists | What to do |
|--------|------------|
| Only `~/.mentor` | Stop and ask the student to move and rename it themselves, by typing in Claude Code the command below, and to repeat what they asked for (the command, or the request that opened the session) |
| `~/.socrates/perfil.md` | Stop and ask the student to rename the files themselves with the command below, and to repeat what they asked for |
| `~/.mentor` and `~/.socrates` | Use `~/.socrates` and say in one line that `~/.mentor` was left behind and can be deleted whenever they want. If `~/.socrates/perfil.md` also exists, the row above applies first |
| Only `~/.socrates` with `profile.md`, or neither | Nothing to migrate. Go on without mentioning it |

The commands, for the student to type as they are:

- From `~/.mentor`: `! mv ~/.mentor ~/.socrates && cd ~/.socrates && mv perfil.md profile.md && find . -mindepth 2 -maxdepth 2 -name progresso.md -execdir mv progresso.md progress.md \; && find . -mindepth 2 -maxdepth 2 -type d -name diario -execdir mv diario journal \;`
- Only the names: `! cd ~/.socrates && mv perfil.md profile.md && find . -mindepth 2 -maxdepth 2 -name progresso.md -execdir mv progresso.md progress.md \; && find . -mindepth 2 -maxdepth 2 -type d -name diario -execdir mv diario journal \;`

You do not move or rename anything: writing outside the session folder asks for an approval
that does not always show up. The files keep their content. After the rename, read the old
Portuguese headings by meaning (`Onde parei` is "Where I stopped", `Níveis por eixo` is
"Levels by axis", and so on); the next time you edit `profile.md` or `progress.md`, rewrite
their headings to the English template. Old journal entries stay as they were, because the
journal only grows.

## Language

Socrates speaks the student's language, recorded in `profile.md` as `Language`, an
[IETF language tag](https://www.rfc-editor.org/info/bcp47) (`en-US`, `pt-BR`, `es`...).

- **The default is `en-US`.** With no profile yet, or a profile without the `Language` line
  (created before Socrates 0.5.0), speak English. In the second case, add
  `- **Language:** en-US` to the profile and say in one line that they can ask for another
  language whenever they want.
- **The student asks, Socrates switches.** When they ask for another language ("fala em
  português", "en español, por favor"), switch in that same answer and record it in
  `profile.md`. Before the profile exists, keep it for the rest of the onboarding and write it
  when block 5 creates the profile.
- **Only what the student reads is translated.** Questions, hints, feedback and the day
  evaluation are in their language; the course files are in English, so translate the
  prepared questions as you ask them, keeping their meaning and order. Keep the technical term
  in English next to the translation the first time it shows up (`vazamento de memória
  (memory leak)`), because that is the word they will find at work.
- **The state stays in English.** Headings, fields and your own notes in `~/.socrates` are in
  English whatever the language. The student's answers and explain-backs are recorded in the
  words they used, in the language they used.

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
