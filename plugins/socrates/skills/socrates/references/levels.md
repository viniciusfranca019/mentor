# Levels by axis

The student's level is measured **per course axis**, never as a single level: someone who
already programs but has never seen networking is a practitioner on one axis and a
layperson on the other. Each course's axes, and the question ladder for each axis, are in
its `course.md`.

## The scale

There are five levels. The weight of each level is the **depth** it requires, counted in
layers of knowledge and practice: 1, 2, 3, 5 and 9. From 1 to 3 it goes up one layer at a
time. From 3 to 4 the jump is two layers, and from 4 to 5, four.

| Level | Name | Weight | What the person can do |
|-------|------|--------|------------------------|
| 1 | Layperson | 1 | Knows it exists, vaguely |
| 2 | Beginner | 2 | Recognizes the terms and follows a tutorial |
| 3 | Practitioner | 3 | Explains the mechanism in their own words and does the common case alone |
| 4 | Proficient | 5 | Diagnoses what went wrong and chooses between approaches with a reason |
| 5 | Expert | 9 | Does the uncommon case, teaches, anticipates attacks and knows their own limits |

## The nine layers

| Layer | The student demonstrates | Completes level |
|-------|--------------------------|-----------------|
| 1. Notion | Knows it exists and what it is for, even if vaguely | 1 |
| 2. Definition | Defines it correctly, with the right term | 2 |
| 3. Mechanism | Explains how it works in their own words and does the common case | 3 |
| 4. Diagnosis | Finds the cause when something goes wrong | |
| 5. Decision | Chooses between approaches and states the reason and cost of each | 4 |
| 6. Real execution | Does an uncommon case with no script and no hint | |
| 7. Teaching | Explains it to a layperson, with an example from their world | |
| 8. Attacker's view | Anticipates how it fails or how it would be attacked | |
| 9. Connection and limits | Links the subject to other domains and says where their own knowledge ends | 5 |

## How to classify

- **Cumulative.** The level is the highest one whose layers, up to its weight, are **all**
  demonstrated. Someone who talks about trade-offs (layer 5) but does not explain the
  mechanism (layer 3) stays at level 2: a layer is missing in the middle, and advanced
  vocabulary without a base does not raise the level.
- **When in doubt, the layer does not count.** Only record the layer the answer shows
  clearly. Overestimating is the most expensive mistake: in security, thinking you know
  what you do not is exactly what the course exists to correct.
- **By the answer, never by the claim.** "I already know this" demonstrates no layer. If
  the student challenges a level, follow the Challenge section.

## Diagnosis (in onboarding)

Each axis has a ladder of three questions in `course.md`:

| Rung | Asks for | Layers it tests |
|------|----------|-----------------|
| **R** Recognize | Saying what it is | 1 and 2 |
| **M** Mechanism | Explaining how it works | 3 |
| **D** Diagnose | Finding the cause of a problem **and** choosing the fix, with its cost | 4 and 5 |

Per axis, start with M. If the answer met the criteria, ask D. If not, ask R.
That is two questions per axis. One question at a time, without correcting, as in the rest
of the diagnosis. The level comes from this path, and only from it:

| M | Second question | Level | Layers recorded |
|---|-----------------|-------|-----------------|
| reached layer 3 | D with layers 4 **and** 5 | 4 | 1 to 5 |
| reached layer 3 | D without both | 3 | 1 to 3, plus 4 if it appeared |
| did not reach | R with layer 2 | 2 | 1 and 2 |
| did not reach | R without layer 2 | 1 | 1 if it appeared, otherwise none |

On the diagnosis ladder, reaching M also counts layers 1 and 2, because explaining the
mechanism presupposes knowing what the thing is. Level 1 is the floor: it applies even with
no layer demonstrated.

## Challenge

If the student challenges a level in the diagnosis result, a new question decides, never
their claim:

| Challenged level | Question | If it meets the criteria |
|------------------|----------|--------------------------|
| 1 or 2 | The axis's **M**, reworded (rung 1 of the hint ladder) | Ask the **D** and classify with the table above |
| 3 | The axis's **D2**, in `course.md`: another diagnosis and decision problem | Level 4 |
| 4 | None. Layers 6 to 9 only come from the exit test, offered in the axis's first module | — |

The diagnosis goes up to level 4: layers 1 to 5 show up in a conversation. Layers 6 to 9
require doing, teaching and attacking, and only come from the exit test.

**The result for the student.** At the end of the diagnosis, show a table: axis, level,
the next missing layer and what that changes in their track (table below). Record the
level, the layers and the answer that justified each one in the "Levels by axis" section of
`progress.md`.

## What the level changes in the track

| Level on the axis | How to run that axis's modules |
|-------------------|--------------------------------|
| 1 and 2 | Full track, unhurried Openings, hints earlier |
| 3 | Full track, faster Openings |
| 4 and 5 | Before each module of the axis, offer the **exit test** |

The level never skips content on its own. It only unlocks the exit test, and who skips
the module is whoever passes it.

## Exit test

Offered at the start of a module whose axis is at level 4 or 5. The student can decline and
do the module normally. The test checks layers 6 to 9 on the module's content, one question
at a time:

1. **Real execution (6).** A variation of the Mission of one of the module's lessons,
   different from the written mission, done with no hint. The student specifies and
   explains the code, as in any Mission.
2. **Teaching (7).** Explain the anchor concept of each lesson in the module to a
   layperson, with an example from that person's world.
3. **Attacker's view (8).** How it fails, or how it would be attacked.
4. **Connection and limits (9).** Where it shows up on another axis of the course, and what
   the student still does not know about the subject.

| Result | What happens |
|--------|--------------|
| All four layers demonstrated | Module **validated**: mark the lessons as `[v]` in `progress.md`, with the date, and the axis goes to level 5 |
| Some layer missing | The module runs normally, with no penalty, and the axis stays at the level it was |

Validating the module waives the lessons, not what they leave ready. If a lesson's Mission
produces something the following modules use, such as the module 00 lab or an installed
tool, the student does that part even with the module validated.

Record the test in the journal like any question, with the layers demonstrated.

## Reassessment

The level changes with what the student demonstrates during the track, not only in the
diagnosis.

- **On every answer**, the journal records the layer the question asked for (the deepest
  one its criteria require) and the layers **the student** demonstrated, unaided or with a
  hint. What came from your explanation never goes into "Layers".
- **At the end of each phase of the track**, `/socrates:feedback` reads **all** the
  journals of the phase, from the first day of its first lesson until today, and reassesses
  the axis:
  - **Up** when the layers missing for the next level showed up clearly in the answers,
    up to level 4. Level 5 only comes from the exit test.
  - **Down** when the last two questions that asked for the same layer N, even with other
    questions between them, ended with Result `needed explanation`, N being a layer
    already recorded as demonstrated. Layer N leaves the "Demonstrated layers", and the
    level becomes the highest one whose layers all remain demonstrated (cumulative rule).
  - Update "Levels by axis" with the date and the answers that justified it.
- **Student without the "Levels by axis" section** in `progress.md` (started on an earlier
  version of the plugin): run the level diagnosis at the start of the next session, before
  the lesson.
