# Example: `study/` state after one full loop

This is a **mockup** of what behavioral-sld's state files look like after:

1. `/planner` — interviewed a fictional learner (a backend developer who knows basic SQL and wants to master **SQL window functions** in 2 weeks, ~45 min/day) and generated `PLAN.md`, `progress.md`, and `backlog.md`.
2. `/teacher` — one socratic session on the first topic (*windows vs GROUP BY, PARTITION BY / ORDER BY*), consolidated into `notes/windows-vs-group-by.md` and `notes/index.html`, with two ⚠️ fragile points recorded.
3. `/evaluator` — one 8-question quiz on that topic (6.5/8 ≈ 81%), recorded in `quiz-history.md`; the score promoted the topic to `[x]` consolidated.

None of this is generated at install time — the plugin's skills build these files incrementally as you actually study. The example is in English; in real use the skills write study documents in the learner's own language.
