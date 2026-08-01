# Behavioral SLD — Study-Driven Learning

A Claude Code plugin that applies the [behavioral-sdd](https://github.com/ddmfuhrmann/behavioral-sdd) thesis to personal learning: **a written, challenged plan before execution; versioned state; explicit gates.**

In behavioral-SDD, execution is code and review is a diff audit. Here, execution is **socratic discussion** and review is a **quiz** — and the definition of done is *consolidated in the learner's own vocabulary*, never "I read the material."

## Why this fork

This workflow was born in a real, timeboxed study lab on a dense technical subject. Three things made it work, and they are what this plugin generalizes:

1. **The plan is the source of truth.** The teacher and the evaluator serve a curriculum; they don't improvise one. The planner skill closes the loop that the original lab had pre-made by hand.
2. **Staged, checkable progress.** The plan compiles into `study/progress.md` — one section per stage, concepts + practice deliverables, a demonstrable ✅ criterion per stage, and a session-history table. `[x]` is earned (discussed and/or ≥80% on a quiz), not ticked.
3. **Consolidation records the learner, not the AI.** Notes are written *after* discussion, in the vocabulary the learner actually used, with hesitation points marked ⚠️ — which then drive what the evaluator tests and what the teacher reviews next.

## The loop

```
/planner  →  interviews you, writes study/PLAN.md + study/progress.md
/teacher  →  socratic sessions per topic, consolidates notes + index.html
/evaluator →  quizzes, records results, promotes topics to consolidated
     ↳ misses and ⚠️ points feed back into the next teacher session
```

## Install

behavioral-sld installs as a Claude Code plugin. Add the marketplace, then install:

```bash
/plugin marketplace add ddmfuhrmann/behavioral-sld
```

```bash
/plugin install sld@behavioral-sld
```

Then, in the project where you want to study, start with `/planner` — it interviews you and writes `study/PLAN.md` and `study/progress.md`.

## Update

To get the latest version:

```bash
/plugin marketplace update behavioral-sld
```

```bash
/plugin update sld@behavioral-sld
```

Updates only change the plugin's skills — your `study/` state files are never touched.

## Skills

| Skill | Role |
|---|---|
| `planner` | Grill-me-style interview (goal, timebox, level, definition of "knowing", domain anchors) → staged curriculum + progress checklist |
| `teacher` | Layered explanation, mandatory one-question-at-a-time socratic discussion, consolidation in the learner's vocabulary |
| `evaluator` | Mixed-format quizzes (conceptual, exercise, applied scenarios on the plan's domain anchors), per-concept diagnosis |
| `sld-conventions` | The contract: state files under `study/`, stage gates, hand-offs between skills |

## State files

Everything lives under `study/` in your project: `PLAN.md`, `progress.md`, `notes/` (per-topic notes + a self-contained `index.html`), `quiz-history.md`, `backlog.md`.

See [`examples/`](examples/) for a mockup of the full state after one planner → teacher → evaluator loop on a sample subject (SQL window functions).

## License

MIT
