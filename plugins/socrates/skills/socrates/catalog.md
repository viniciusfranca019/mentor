# Course catalog

The showcase of the courses that exist in the `socrates` marketplace, so the student can see what they can
install. Each course is a plugin; installing a course also installs `socrates`, if it is missing.
The command goes in Claude Code; after it, `/reload-plugins`.

This catalog only serves a course that is **not installed**. For an installed course, what says who it is
for, where you get to and what is available is the `description` of the skill
`socrates-<course>:course`, which changes along with the course. An installed course that is not here
shows up anyway.

| Course | Who it is for | Where you get to | Install |
|--------|---------------|------------------|---------|
| `security-engineer` | People with an IT background but little practice in programming, networking and infrastructure | Security engineer in the AI era: understands how systems work, models threats and protects applications, infrastructure and AI agents | `/plugin install socrates-security-engineer@socrates` |

## Extensions

Plugins that are not courses: they bring their own method and use the Socrates criteria
(levels, rubric, state). They also install with one command, and also bring
`socrates` along. As with courses, an installed extension shows up through its skill
(`socrates-<extension>:<extension>`), even if it is not here.

| Extension | What it does | How to use | Install |
|-----------|--------------|------------|---------|
| `pdi` | Individual Development Plan: goal, competencies with a level measured by the Socrates scale, 70-20-10 actions and check-ins with evidence | `/socrates-pdi:pdi` | `/plugin install socrates-pdi@socrates` |
