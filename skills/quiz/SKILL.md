---
name: quiz
description: Quick multiple-choice quiz on the study plan. Five fast questions, always 4 options, one at a time, one-line correction, about two minutes. Never promotes a topic; only logs misses so the reviewer picks them up. Use when the user wants a quick quiz, a fast check, a warm-up, "just a few questions", multiple-choice only, or invokes /quiz. For a full quiz that can promote a topic, use the evaluator.
---

# Skill: Quiz

A two-minute check, not a measurement. You ask a handful of multiple-choice questions on what the learner has already seen, and you leave a trail of what they missed.

Load the `sld:sld-conventions` skill first. If `study/PLAN.md` does not exist, stop and run the planner. If no topic is `[~]` or `[x]` yet, say so and point to `/teacher`.

## What this is not

Multiple choice measures recognition, not recall. So this skill:

- **never** changes a checkbox in `study/progress.md` — no promotion to `[x]`, no demotion to `[~]`, whatever the score;
- **never** touches the schedule in `study/review-history.md`.

If the learner wants a result that counts, hand over to `/evaluator` (promotion) or `/reviewer` (retention).

## Scope

- User-named topic if given. It must be `[~]` or `[x]`; if it is `[ ]`, say it has not been studied yet and offer `/teacher`.
- Otherwise mix, in this order of priority: (a) concepts missed in `study/quiz-history.md` and `study/review-history.md`, (b) ⚠️ points in `study/notes/*.md`, (c) the most recently studied topic.
- Source of truth: `study/PLAN.md` and the consolidated notes. Do not invent details beyond them.

## Questions

- Default 5; the learner may ask for another number (cap at 10 — beyond that it is an evaluator quiz).
- Always exactly 4 options, exactly one correct. No "all of the above", no "none of the above".
- Distractors must be mistakes a real learner makes — the ⚠️ points and logged misses are the best source. No filler, no joke options.
- Vary the angle: definition, predict-the-output, spot-the-error, small scenario from the plan's domain anchors. Numeric questions are fine when the arithmetic fits in the head.
- Vary the position of the correct option; keep the four options similar in length and tone so the form does not give the answer away.
- Fresh questions: do not repeat ones already logged in the history files.

## Running it

- ONE question at a time. If a clickable-choice tool is available (e.g. `AskUserQuestion`), use it with the four options and mark none as recommended; otherwise list them as A–D and wait.
- After each answer: right or wrong, the correct option, and ONE line of why. If wrong, one more line on why the chosen option is tempting but wrong. No follow-up questions, no mini-lecture — keep the pace.
- No preamble and no recap between questions.

## Wrap-up

- Score, then the missed concepts as a short list. Nothing else.
- Append a compact block to `study/quiz-history.md` (create the file if missing):

```markdown
## YYYY-MM-DD — Quick quiz — <topics> — 4/5

| # | Question (short) | Concept behind the miss |
|---|------------------|-------------------------|
| 2 | … | … |
```

  With no misses, write the heading line only.
- Append one row to the session-history table in `study/progress.md`, labelled as a quick quiz.
- Suggest a next step only when it is earned: 2 or more misses on the same topic → `/teacher <topic>`; a clean run on a `[~]` topic → `/evaluator <topic>` to promote it.

Respond in the user's language; keep domain-anchor jargon in its original language.
