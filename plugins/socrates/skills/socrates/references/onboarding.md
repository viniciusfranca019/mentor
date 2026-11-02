# Onboarding

The student's first contact with Socrates. They leave knowing which course they will take,
how to use Socrates day to day and how to switch courses later, with the diagnosis done
and `~/.socrates` created.

**Show what exists before explaining how it works.** The student chooses first and
understands the method when they use it: the four phases of the lesson are explained in
the first lesson, not here. Run it in short blocks and wait for their answer between one
block and the next.

Before anything else, check whether `~/.socrates/profile.md` exists:

| Situation | Path |
|-----------|------|
| Does not exist | First time: blocks 1 to 5, in order |
| Exists | The student is coming back: go to **Review**, at the end of this file |

## Block 1 — The courses

The first message has only this, in this order:

1. **What Socrates is, in up to 3 lines.** A mentor inside Claude Code that runs a course
   lesson by lesson: it asks instead of giving the answer, and the student builds with the
   AI and explains what they built.
2. **The courses.** A single table, with course, who it is for, where you get to, what is
   already available and whether it is **installed**, built from two sources:
   - each `socrates-<course>:course` skill among the session's skills is an **installed**
     course, and its `description` gives who it is for, where you get to and what is
     available;
   - each line of `<root>/skills/socrates/catalog.md` whose course is not installed goes in
     as **not installed**, with the install command in place of what is available.
3. **One sentence on how courses arrive:** Socrates is the mentor, and each course is a
   separate plugin that it runs. Installing a course is a single command. Do not show the
   Extensions here: they appear in block 2.
4. **One line on language:** the language Socrates is speaking, and that the student can ask
   for another one at any moment (`references/state.md`, Language).
5. **One question:** which course they want to take. With only one course in the table, ask
   whether it is that one.

If the chosen course is not installed, the next answer is only this: the command from the
catalog's "Install" column, for them to run in Claude Code, then `/reload-plugins` and
`/socrates:onboarding` again, which now shows the course installed. Do not
go on without the course: the track and the diagnosis come from it.

No lesson phases, commands or history in this message: each thing appears when the
student needs it.

## Block 2 — The track and the routine

Once the course is chosen, answer in a **single message**, without stopping midway to ask:

1. **The track.** Load the `socrates-<course>:course` skill, read the `course.md` from the
   root it points to and list the phases: the name of each one and what
   the student will know at its end, one line each, without the list of lessons.
2. **The routine.** How Socrates fits into their routine:

| When | What to do |
|------|------------|
| **Today, once** | Diagnosis and pace, about 20 minutes. This is what comes next |
| **Each study day** | `/socrates:mentor-mode`: picks up exactly where they stopped |
| **End of the day** | `/socrates:feedback`: evaluates the day and says what to review |
| **Career plan, whenever you want** | The PDI is an extension of Socrates: it builds their development plan with the same level scale, and links the actions to course modules. Show the line from the catalog's Extensions section, with the install command, or `/socrates-pdi:pdi` if the `socrates-pdi:pdi` skill is already installed |
| **Another course, whenever you want** | `/socrates:onboarding`: shows the catalog with the status of each course. A new course is a plugin: install it with the catalog command. Switching courses does not erase the progress of the other one |

Right below, the agreement in two lines: they use Claude to write the code, but first
they say what they want to build, and afterwards they explain what they got.

Mention that typing `/socrates` shows the three commands in the menu, and that for
feedback the prefix matters: `/feedback` without `socrates:` is the Claude Code command
for sending feedback to Anthropic. Their history lives in `~/.socrates`, to open whenever
they want.

Close with: "Any questions? If not, I'll start the diagnosis."

## Block 3 — Diagnosis

The diagnosis measures their level **on each axis of the course**, with the ladders from
the "Axes and diagnosis" section of `course.md` and the rules in
`<root>/skills/socrates/references/levels.md`. Say beforehand: "This is not a test, there
is no grade. It is so I know where you are starting from on each subject."

- One question at a time, two per axis: the **M** and, depending on the answer, the **D**
  or the **R**.
- Do not correct the answers now. Thank them and move on. The diagnosis measures the
  starting point, it does not teach.
- At the end, show the result table: axis, level, the next missing layer and what that
  changes in their track. If they challenge a level, follow the Challenge section of
  `levels.md`.

## Block 4 — Goal and pace

One question at a time, in order, waiting for the answer between them.

1. What they want to be called. It goes into `profile.md`.
2. "Why do you want to take this course? Where do you want to be a year from now?" Write it
   down in their words: the feedback will remind them of it on hard days.
3. Agree on the pace: which days, how long per session. Recommend at least 3 sessions of
   1 hour per week. Consistency is worth more than a marathon.
4. Ask which machine they use (Windows, Linux, macOS). The course's module 00 depends on
   it.

## Block 5 — Create the state and close

1. Create `~/.socrates/profile.md` from the template, with everything that was agreed and
   the `Language`: the one the student asked for during the onboarding, or `en-US`.
2. Create `~/.socrates/<course>/progress.md` from the template, with the track copied from
   `course.md`, "Where I stopped" at the first lesson and the "Levels by axis" section
   filled in with the diagnosis result.
3. Create the day's journal with an "Onboarding" section that records the diagnosis: each
   question, the summarized answer, the layer it asked for and the layers the answer
   demonstrated.
4. Show them the paths created and close: "Whenever you want to start, just run `/socrates:mentor-mode`."

## Review — when the profile already exists

The student came back to onboarding to see the courses, switch courses or change the pace.

1. **The courses, with their status.** Show the block 1 course table with one more column, read from
   `~/.socrates/profile.md` and from each `~/.socrates/<course>/progress.md`:

   | Status | When |
   |--------|------|
   | **active**, at `<lesson>` | It is the profile's active course |
   | **started**, stopped at `<lesson>` | Has a directory in `~/.socrates`, but is not the active one |
   | **not started** | Has no directory in `~/.socrates`, but the plugin is installed |
   | **not installed** | It is in the catalog, but the plugin is not installed (there is no `socrates-<course>:course` skill) |

   A started course whose plugin was uninstalled shows as **started**, with the note
   "reinstall to continue": their progress in `~/.socrates` is still there.

2. **One question, with four options:** continue the active course, go back to a started
   course, start a new course, or adjust the pace. Below the options, one line with the
   catalog's Extensions and the status of each one (installed or the install command).

| Option | What to do |
|--------|------------|
| Continue | Suggest `/socrates:mentor-mode` and finish |
| Go back to a started course | If the course plugin is not installed, give the install command and stop without touching `profile.md`. Installed: switch the active course in `profile.md` and the "Status" column of the "Courses" table for both courses (`in progress` and `paused`). Their progress is intact |
| Start a new course | If the course is not installed, give the install command and stop, as in block 1. Installed: do only block 3 with that course's diagnosis, create `~/.socrates/<course>/` as in block 5 (steps 2 and 3), switch the active course, add the course to the profile's "Courses" table (the previous one becomes `paused`) and ask whether the pace stays the same. Do not redo the goal or the machine, and do not touch the other course's directory |
| Adjust the pace | Redo step 3 of block 4 and update `profile.md` |
