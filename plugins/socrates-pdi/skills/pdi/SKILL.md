---
name: pdi
description: >
  Use this skill when the student builds or reviews their PDI (Individual Development Plan)
  with Socrates: opened by /socrates-pdi:pdi, or when they ask about "my PDI",
  "development plan", "PDI check-in", "where I want to be in a year", "meu PDI",
  "plano de desenvolvimento", "check-in do PDI", "onde quero estar em um ano". It turns a
  career goal into competencies measured on the Socrates level scale, 70-20-10 actions
  with deadlines and evidence, and periodic check-ins, stored in ~/.socrates/pdi.
---

# PDI

The student's PDI, run the Socrates way: questions instead of ready answers, and level
measured by evidence, never by declaration. The plan is theirs. You ask, organize and
demand evidence; you do not choose the goal or the competencies for them.

## Where things live

| What | Where |
|------|-------|
| This method and the template | `${CLAUDE_PLUGIN_ROOT}/skills/pdi/` |
| Criteria (levels, rubric, state) | Load the `socrates:criteria` skill: it gives the paths. Read `levels.md` before talking about level |
| The student's PDI | `~/.socrates/pdi/pdi.md`, created from `${CLAUDE_PLUGIN_ROOT}/skills/pdi/templates/pdi.md` |
| The check-ins | Appended to the end of `pdi.md` itself, "Check-ins" section |
| The student's courses | `~/.socrates/profile.md` and `~/.socrates/<course>/progress.md`: **read only** |

Before reading or creating any file in `~/.socrates`, run the check in the Migration
section of Socrates' `state.md`.

## Workflow: build the PDI

One block at a time, one question at a time, waiting for the answer between them.

1. **Goal.** "Where do you want to be 12 months from now, and how will you know you got
   there?" If `~/.socrates/profile.md` has a Goal, show it and ask whether it is the same.
   The goal needs an observable arrival signal; if it comes vague ("be senior"), ask what
   someone would see them doing.
2. **Competencies.** "What do you need to be able to do to get there?" From 3 to 5. For
   each one, ask why it matters for the goal. If a competency matches an axis of a course
   they take, note the course and the axis.
3. **Current level, with evidence.** On the `levels.md` scale, with its rules
   (cumulative, when in doubt the layer does not count, by the answer and never by the
   declaration):
   - competency linked to a course axis: the level and the demonstrated layers come from
     the "Levels by axis" of their `progress.md`, with the evidence recorded there;
   - the others: the **diagnosis** from the Diagnosis section of `levels.md`, on the
     competency: the **M** question and, depending on the answer, the **D** or the **R**,
     which you write on the spot. No correcting. Level and layers come from the table
     there. If they prefer not to answer now, the level stays `declared: N`, with no
     layers, and the first check-in runs the diagnosis.
   Always record the **demonstrated layers**, not just the level: the check-in starts from
   them.
4. **Target level and gap.** For each competency, the level the goal requires and the next
   missing layer. **Without a course, the target goes up to 4:** layers 6 to 9 only come
   from the exit test of a course module (`levels.md`), and the PDI has no exit test. If
   they want a 5 in a competency, link it to a course axis or leave the target at 4 and
   say why. If the total gap is more than 12 months of work, say so and ask what goes.
5. **70-20-10 actions.** For each competency, at least one action of each type, each with
   a deadline and the **completion evidence** (what someone else would see):
   - **70, practice:** a project or a responsibility at work;
   - **20, with other people:** mentoring, pairing, review, teaching someone;
   - **10, study:** preferably a module of a Socrates course, cited by name; if there is
     none, the material they choose.
6. **Pace and record.** Agree on the check-in date (suggest once a month). Create
   `~/.socrates/pdi/pdi.md` from the template, show the path and close with: "On check-in
   day, just run `/socrates-pdi:pdi`."

## Workflow: check-in

1. Read `pdi.md` and, for each course linked to a competency, its `progress.md`.
2. For each action that is due or in progress, ask what was done and ask for the evidence.
   An action without evidence does not close, even if they say they did it.
3. **Levels**, by competency, always by the rules of `levels.md`:
   - **linked to a course axis:** copy from `progress.md` the level and the layers of the
     course's most recent reassessment. The PDI does not measure what the course already
     measures;
   - **`declared: N`:** run the diagnosis (M, then D or R), as in step 3 of building the
     PDI. The declaration does not choose the question;
   - **measured, without a course:** first the **review**: one question from the highest
     layer already demonstrated, recorded in the check-in with the result (`unaided`,
     `with hint` or `needed explanation`). If the review of this layer ended in `needed
     explanation` in this check-in and in the previous one, the layer leaves the
     demonstrated ones and the level is recalculated (the drop rule of Reassessment in
     `levels.md`, applied to reviews). Then ask about the layers missing for the next
     level, starting from the "Next layer", one at a time, with no hint. A layer they
     demonstrate goes into "Demonstrated layers", and the level only rises when **all**
     the layers up to the weight of the next level are there (cumulative rule), at most
     up to 4.
4. **Update the plan and record.** In `pdi.md`, update the tables to the present:
   Status of each action (`open`, `closed` with the evidence, or `cancelled` with the
   reason), Current level, Demonstrated layers, Level evidence, Next layer and Next
   check-in. Then append the check-in section at the end (date, closed actions with the
   evidence, layers and levels that changed and why, what changes in the plan). The
   sections of old check-ins are never rewritten. Show them the summary in the tone of
   the Socrates rubric: honest, specific, comparing them with themselves.
5. Ask whether the goal is still the same. If it changed, redo blocks 2 to 5 of building
   the PDI.

## Critical Rules

- MUST NOT choose a goal, competency or action for them. Why: a PDI they did not choose
  is a PDI they do not follow.
- MUST measure the level by the answer or by the course record, never by the
  declaration. Why: it is the Socrates rule, and a plan built on an inflated level gets
  the gap wrong.
- MUST NOT write to a course's state (`progress.md`, journals). Why: it belongs to the
  engine, and the level reassessment depends on it being intact.
- MUST ask for evidence to close an action. Why: without evidence, the check-in becomes a
  list of intentions.
