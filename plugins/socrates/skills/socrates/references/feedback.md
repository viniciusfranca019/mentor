# Day evaluation (`/socrates:feedback`)

`/socrates:feedback` evaluates the study day from the journal, and only from it. Every
claim in the evaluation points to a recorded answer. If the day's journal does not exist
or is empty, say so and suggest a `/socrates:mentor-mode`. Do not make up an evaluation.

## Procedure

1. Read `~/.socrates/profile.md`, the active course's `progress.md` and today's journal
   (`date +%F`). Also read the two previous journals, if they exist, to compare.
2. Count, for the day: questions answered, how many `unaided`, `with hint` and `needed
   explanation`; specs given and how many were complete on the first try; code explained
   before running.
3. Evaluate the five dimensions of the rubric below.
4. Write the evaluation in the format below, show it to the student and append it to the
   end of the journal, in the "Day evaluation" section.
5. Update "To review" in `progress.md` with the concepts that were weak.
6. If the day closed the last lesson of a phase of the track, reassess the level of that
   phase's axis by reading **all** the journals of the phase, not just today's, as the
   Reassessment section of `levels.md` says, and update "Levels by axis" in `progress.md`.

## Rubric

Each dimension gets a level. The level comes from the journal, never from the overall
impression.

| Dimension | What it measures | Strong | Developing | Weak |
|-----------|------------------|--------|------------|------|
| **Understanding** | Does the student understand the day's concepts? | Explained back with no hint | Explained with 1 or 2 hints | Needed explanation on the anchor concept |
| **Reasoning** | Does the student reach the answer or guess? | Answers with a correct "because" | Right answers without justification | Guesses or memorized answers |
| **Autonomy** | How much did the student rely on hints? | Mostly `unaided` | Mostly `with hint` | Mostly `needed explanation` or many "explain" |
| **Directing the AI** | Does the student direct Claude or get led? | Complete specs and code explained before running | Complete spec only after questions | Vague requests or code run without reading |
| **Prediction** | Does the student predict the behavior before testing? | Right predictions, or wrong ones with a clear hypothesis | Vague predictions | Does not risk a prediction |

**Directing the AI** is the dimension that matters most in this plugin: it is what sets the
engineer apart from the tool operator. Give it matching emphasis.

## Evaluation format

```markdown
### Summary
<Two sentences: what the student did today and the main conclusion.>

### Numbers for the day
- Lessons completed: <N> · Questions: <N> (<n> unaided · <n> with hint · <n> with explanation)
- Specs for Claude: <N> (<n> complete on the first try) · Code explained before running: <n>/<N>

### Dimensions
| Dimension | Level | Evidence in the journal |
|-----------|-------|-------------------------|
| Understanding | <level> | <the answer that shows it> |
| ... | | |

### What went well
<1 to 3 concrete items, each tied to one of the student's answers.>

### What to improve
<1 to 3 items, each with what to do differently in the next session.>

### Axis level
<Only when the day closed a phase: the axis, the previous level, the level now and the
answer that justified the change, or "unchanged" and why.>

### To review
<The concepts that went into "To review" in the progress.>

### Next session
<Where the student will start and the warm-up question that will open it.>
```

## Tone

- Honest and specific. "You did well" says nothing. "You correctly predicted the file
  would get corrupted and explained why" says something.
- Compare the student with themselves, never with other people. If previous journals
  exist, show the progress: "on Tuesday it was 2 complete specs out of 5, today 4 out of 5".
- If the day was weak, say so, and also say what to do. If the profile has the student's
  goal, remind them of it in one sentence when the day was hard.
