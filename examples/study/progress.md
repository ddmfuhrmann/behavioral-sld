# Progress — SQL Window Functions

Checklist per topic. Mark `[x]` only when consolidated (discussed with /teacher and/or ≥80% on an /evaluator quiz). Note the date and link the consolidated note when there is one.

Legend: `[ ]` not started · `[~]` started/discussed · `[x]` consolidated

## Stage 1 — Foundations

### Concepts
- [x] Windows vs GROUP BY; `PARTITION BY` / `ORDER BY` — 2026-08-01, [consolidated](notes/windows-vs-group-by.md)
- [~] Ranking functions and tie behavior — discussed 2026-08-01; ⚠️ RANK vs DENSE_RANK gap still shaky
- [ ] Default frame with `ORDER BY` (preview given; revisit in Stage 2)

### Practice
- [x] Rank each customer's orders; tie case with all three ranking functions
- [ ] Rewrite GROUP BY report as a window keeping row detail
- [ ] ✅ Stage criterion: classify columns (window vs GROUP BY) and predict ranks on ties, without running

## Stage 2 — Frames and offsets

### Concepts
- [ ] Frame clause; default frame surprise (`RANGE UNBOUNDED PRECEDING`)
- [ ] Running totals and moving averages
- [ ] `LAG` / `LEAD` and gaps between events

### Practice
- [ ] Running total per customer
- [ ] Moving average; `ROWS` vs `RANGE` on tied dates
- [ ] Days since previous order via `LAG`
- [ ] ✅ Stage criterion: explain `RANGE` vs `ROWS` on tied dates from memory

## Stage 3 — Applied patterns

### Concepts
- [ ] Top-N per group
- [ ] Deduplication with `ROW_NUMBER`
- [ ] Sessionization / gaps-and-islands (recognition only)

### Practice
- [ ] Each customer's 2 largest orders
- [ ] Dedup keeping latest row per `(customer_id, order_date)`
- [ ] Self-join vs window written comparison
- [ ] ✅ Stage criterion: top-N and dedup from memory + explain why the window replaces the self-join

## Session history

| Date | Skill | Topic | Result |
|------|-------|-------|--------|
| 2026-08-01 | /planner | Plan created: goal, anchors (`orders` table), 3 stages / 2 weeks | PLAN.md + progress.md written |
| 2026-08-01 | /teacher | Windows vs GROUP BY, PARTITION BY / ORDER BY (+ ranking-ties preview) | Consolidated — solid on partitioning; 2 ⚠️ points recorded |
| 2026-08-01 | /evaluator | Quiz: windows vs GROUP BY, partitioning, ranking ties | 6.5/8 (~81%) — topic promoted to [x]; DENSE_RANK gap reinforced as ⚠️ |
