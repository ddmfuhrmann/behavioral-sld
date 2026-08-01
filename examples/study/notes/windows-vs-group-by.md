# Windows vs GROUP BY · PARTITION BY / ORDER BY

*Consolidated 2026-08-01 after /teacher session. Written in the learner's own vocabulary from the discussion.*

## Definition (as I said it)

> "GROUP BY squashes the rows into one per group. A window function looks at the same group but **leaves my rows alone** — every order row stays, and the aggregate rides along as an extra column."

`OVER (PARTITION BY customer_id)` = "compute per customer, but don't collapse". `ORDER BY` inside `OVER` turns the window into a *sequence* (needed for ranks and running totals); without it the window is just a bag.

## Worked example (anchor table)

```sql
SELECT order_id, customer_id, amount,
       SUM(amount) OVER (PARTITION BY customer_id)              AS customer_total,
       ROW_NUMBER() OVER (PARTITION BY customer_id
                          ORDER BY amount DESC)                 AS rn
FROM orders;
```

Customer 101 has the tie case (two orders of 50.00): `ROW_NUMBER` arbitrarily breaks the tie (1, 2), `RANK` gives (1, 1, **3**), `DENSE_RANK` gives (1, 1, **2**).

## Insight from the discussion

The question "why can't HAVING do this?" landed it: HAVING filters *groups after collapsing*; a window lets me filter *rows by a group-level fact* while keeping the rows. That's the whole reason top-N-per-group needs windows.

## ⚠️ Review

- ⚠️ **RANK vs DENSE_RANK gap**: I predicted RANK's next value after a tie wrong (said 2, it's 3 — RANK counts *rows*, DENSE_RANK counts *distinct values*). Missed again in the quiz — drill this.
- ⚠️ **Default frame**: teacher previewed that `ORDER BY` inside `OVER` silently sets the frame to `RANGE UNBOUNDED PRECEDING` — I can repeat the phrase but can't yet explain the consequence. Full treatment in Stage 2.

## Connection to the plan

Feeds directly into Stage 1's remaining practice (rewrite the GROUP BY report) and is the foundation for top-N-per-group and dedup in Stage 3.
