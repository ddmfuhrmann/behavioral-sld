# Study plan — SQL Window Functions

## Goal

Write and defend analytics queries using window functions confidently: rankings, running totals, moving averages, and top-N-per-group patterns — without reaching for self-joins or subquery workarounds.

**Definition of knowing**: implement each pattern on the anchor dataset from memory, and explain to a colleague *when a window function beats GROUP BY and why*.

**Timebox**: 2 weeks, ~45 min/day (≈10 sessions). Anything that doesn't fit goes to `backlog.md`.

**Current level**: comfortable with SELECT/JOIN/GROUP BY/HAVING; has never used `OVER ()`.

## Domain anchors

All examples, exercises, and quizzes use this table:

```sql
orders(order_id INT, customer_id INT, order_date DATE, amount NUMERIC)
```

Sample rows: customers 101/102/103, orders across Jan–Mar, amounts with deliberate ties (two orders of 50.00 for customer 101) so ranking-tie behavior always has a concrete case.

Jargon kept in English (SQL standard terms): window function, `OVER`, `PARTITION BY`, frame, `ROWS` / `RANGE`, `LAG` / `LEAD`, `ROW_NUMBER` / `RANK` / `DENSE_RANK`.

## Stage 1 — Foundations (days 1–4)

### Concepts
- What a window is: per-row computation over a related set; windows vs GROUP BY (rows are not collapsed)
- `PARTITION BY` and `ORDER BY` inside `OVER`
- Ranking functions: `ROW_NUMBER`, `RANK`, `DENSE_RANK` and tie behavior

### Practice
- Rank each customer's orders by amount; show the tie case with all three ranking functions
- Rewrite a GROUP BY report (total per customer) as a window so each order row keeps its detail

**✅ Stage criterion**: given a query result, say for each column whether it needed a window or GROUP BY, and predict rank values on ties — without running the query.

## Stage 2 — Frames and offsets (days 5–8)

### Concepts
- Frame clause: `ROWS BETWEEN ... AND ...`; default frame when `ORDER BY` is present (`RANGE UNBOUNDED PRECEDING`) and why it surprises people
- Running totals and moving averages
- `LAG` / `LEAD` and gaps between events

### Practice
- Running total of `amount` per customer by `order_date`
- 3-order moving average; show how the result changes with `ROWS` vs `RANGE` on tied dates
- Days since each customer's previous order via `LAG`

**✅ Stage criterion**: explain, with the tied-dates case, why `RANGE` and `ROWS` give different running totals — from memory.

## Stage 3 — Applied patterns (days 9–14)

### Concepts
- Top-N per group (window in a subquery/CTE + filter)
- Deduplication with `ROW_NUMBER`
- Sessionization / gaps-and-islands sketch (recognize the pattern; full mastery deferred)

### Practice
- Each customer's 2 largest orders (top-N per group)
- Dedup `orders` keeping the latest row per `(customer_id, order_date)`
- One written comparison: the same report via self-join vs window — readability and cost

**✅ Stage criterion**: implement top-N-per-group and dedup on the anchor table from memory, and explain to a colleague why the window version replaces the self-join.

## Deferred → backlog

Query-planner internals for windows, `FILTER` clause, `GROUPS` frame mode, full gaps-and-islands, vendor-specific extensions.
