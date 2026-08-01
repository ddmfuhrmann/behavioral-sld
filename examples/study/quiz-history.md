# Quiz history

## 2026-08-01 — Windows vs GROUP BY, partitioning, ranking ties — 6.5/8 (~81%)

Composition: 3 conceptual MC · 2 exercises · 2 applied scenarios · 1 open explanation.

**Missed / partial:**

| # | Question (short) | Concept behind the miss |
|---|------------------|-------------------------|
| 3 | Predict RANK sequence after the 50.00 tie for customer 101 | RANK counts rows, not distinct values — answered as if DENSE_RANK (⚠️ reinforced in consolidated note) |
| 7 (half credit) | "Explain to a colleague when a window beats GROUP BY" | Mechanism stated well ("doesn't collapse rows"), but the *consequence* (enables row-level filters on group facts, e.g. top-N) came out only after a hint |

**Solid:** partitioning semantics, window-vs-GROUP-BY classification, rewriting an aggregate as a window column, ROW_NUMBER for dedup (scenario), HAVING-vs-window scenario.

**Outcome:** ≥80% → topic promoted to `[x]` in progress.md. Next: `/teacher` short drill on RANK/DENSE_RANK gaps before starting Stage 2 frames.
