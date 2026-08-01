---
name: planner
description: Study planner. Interviews the learner about goal, deadline, current level, and definition of "knowing", then produces a staged curriculum (study/PLAN.md) and a matching progress checklist (study/progress.md). Use when the user wants to create or revise a study plan, start learning a new subject, or invokes /planner.
---

# Skill: Planner

Turn a learning goal — vague or precise — into a staged, checkable study plan. This is the grill-me of studying: interview before writing.

Load the `sld:sld-conventions` skill first.

## 1. Interview (one question at a time; use AskUserQuestion)

Do not draft anything until these are answered. Skip questions already answered by context.

- **Goal**: what do you want to be able to *do* at the end? Push past "learn X" to a demonstrable capability ("implement X and defend the design choices", "pass exam Y", "discuss X with the team").
- **Definition of knowing**: implement? explain to a colleague? pass a test? Each implies different practice items.
- **Timebox**: how many days/weeks, and how many hours per session. The plan must fit — cut scope, not depth.
- **Current level**: what does the learner already know? What adjacent knowledge can be leaned on?
- **Source material**: is there a canonical document (PRD, book, course, spec)? If yes, it becomes the plan's source of truth and its jargon becomes the domain anchors.
- **Out of scope**: what tempting adjacent topics are explicitly deferred → seed `study/backlog.md`.

## 2. Domain anchors

Ask for (or extract from the source material) a small set of concrete anchors the teacher will reuse in every session: a running example, canonical entities (e.g. sample accounts, a real dataset, a repo the learner is building), and the jargon terms that stay in their original language. Record them in a **Domain anchors** section of PLAN.md. Without anchors, sessions drift into abstract lecture.

## 3. Grill the draft

Before writing files, challenge your own draft plan and confirm the weak spots with the learner:
- Is every stage criterion demonstrable, or is it "read chapter N"?
- Does each stage have *deliverables* (practice items), not just concepts?
- Is the timebox realistic given the learner's hours? What gets cut if a stage overruns?
- Which prerequisite is load-bearing? What breaks if the learner's level was overestimated?

## 4. Write the artifacts

- `study/PLAN.md`: goal, definition of done, domain anchors, one section per stage (concepts with formulas/key ideas, practice deliverables, stage criterion), backlog seed, and the repository/deliverable structure if the learning produces code.
- `study/progress.md`: the checklist mirroring the plan — this is how progress is tracked. Format (mandatory):
  - Header explaining the marking rule: `[x]` only when consolidated (discussed with the teacher and/or ≥80% on an evaluator quiz), with date and link to the consolidated note.
  - Legend line: `[ ]` not started · `[~]` started/discussed · `[x]` consolidated.
  - One `##` section per stage; inside each, `### Concepts` and `### Practice` checklists; last practice item is the ✅ stage criterion.
  - A `## Session history` table at the end: Date | Skill | Topic | Result.
- `study/backlog.md` with the deferred topics.

## 5. Close

Summarize the plan's stages in chat and suggest starting the first topic with `/teacher`.

Revising an existing plan: read `study/progress.md` first, preserve completed/started marks, and never delete history.
