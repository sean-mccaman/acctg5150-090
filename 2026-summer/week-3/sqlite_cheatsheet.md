# SQLite Cheat Sheet — ACCTG 5150 Week 3
*Open this in another tab while you work the lab and homework. All examples use the Summit Gear Co. AR tables (customers, invoices, payments, invoice_terms, invoice_statuses).*

**Companion artifact:** the HTML cheat sheet at <https://seanmccaman.com/acctg5150/2026-summer/week-3/interactive/sqlite_cheatsheet.html> covers the same content with copy-paste buttons. Use whichever you prefer.

If you also want the schema reference — what each table holds, what joins to what, what the seeded edge cases are — see the [schema and lab explainer](https://github.com/sean-mccaman/acctg5150-090/blob/main/2026-summer/week-3/schema_and_lab_explainer.md).

---

## 1. Inspecting the database

Before you write a query, look at what is actually in the tables. Two cheap moves.

### `PRAGMA table_info(<table>)` — see the schema of a table

Returns one row per column: name, type, whether it is NOT NULL, and whether it is part of the primary key.

```sql
PRAGMA table_info(invoices);
```

Example — confirm the columns on `invoices` before joining:

```sql
PRAGMA table_info(invoices);
-- cid | name         | type     | notnull | dflt_value | pk
--  0  | invoice_id   | TEXT     | 1       |            | 1
--  1  | customer_id  | TEXT     | 1       |            | 0
--  2  | invoice_date | DATE     | 1       |            | 0
--  3  | due_date     | DATE     | 1       |            | 0
--  4  | amount       | NUMERIC  | 1       |            | 0
--  5  | status_id    | INTEGER  | 1       |            | 0
```

### `SELECT * ... LIMIT 5` — eyeball five sample rows

Fastest way to see what real values look like in a column.

```sql
SELECT * FROM <table> LIMIT 5;
```

Example — what does a payment row actually look like?

```sql
SELECT * FROM payments LIMIT 5;
```

---

## 2. SELECT / FROM / WHERE

Pick columns, pick a table, filter rows.

### `SELECT ... FROM` — bare minimum

```sql
SELECT <columns> FROM <table>;
```

Example — every invoice's ID and amount, all 20,000 of them:

```sql
SELECT invoice_id, amount
FROM invoices;
```

Use `SELECT *` only while exploring. In a final query, name the columns you want.

### `WHERE` — filter rows

Operators: `=`, `!=` (or `<>`), `<`, `>`, `<=`, `>=`. Combine with `AND` and `OR`. Strings go in single quotes.

```sql
SELECT <columns>
FROM <table>
WHERE <condition>;
```

Example — Q1 2026 invoices above 1,000 dollars:

```sql
SELECT invoice_id, invoice_date, amount
FROM invoices
WHERE invoice_date >= '2026-01-01'
  AND invoice_date <= '2026-03-31'
  AND amount > 1000;
```

### `BETWEEN` — range filter, inclusive on both ends

`BETWEEN a AND b` is the same as `>= a AND <= b`. Shorter to type, easier to read.

```sql
SELECT <columns>
FROM <table>
WHERE <column> BETWEEN <low> AND <high>;
```

Example — every payment in March 2026:

```sql
SELECT payment_id, payment_date, amount
FROM payments
WHERE payment_date BETWEEN '2026-03-01' AND '2026-03-31';
```

### `IN` — match any value in a list

Cleaner than chaining `OR`. Strings go in single quotes; integers go bare.

```sql
SELECT <columns>
FROM <table>
WHERE <column> IN (<v1>, <v2>, <v3>);
```

Example — only the Open and Partial invoices (skip Paid and Void):

```sql
SELECT invoice_id, amount, status_id
FROM invoices
WHERE status_id IN (1, 2);
```

### `LIKE` — string pattern match

`%` matches any number of characters; `_` matches exactly one. SQLite is case-insensitive for ASCII letters by default.

```sql
SELECT <columns>
FROM <table>
WHERE <column> LIKE '<pattern>';
```

Example — every customer whose name starts with "Park":

```sql
SELECT customer_id, customer_name
FROM customers
WHERE customer_name LIKE 'Park%';
```

---

## 3. ORDER BY / LIMIT

Sort the result, then optionally cap how many rows come back.

### `ORDER BY` — sort the result

`ASC` is ascending (default); `DESC` is descending. You can sort by multiple columns.

```sql
SELECT <columns>
FROM <table>
ORDER BY <column> [ASC | DESC];
```

Example — invoices sorted highest amount first:

```sql
SELECT invoice_id, customer_id, amount
FROM invoices
ORDER BY amount DESC;
```

### `LIMIT` — cap the row count

Use with `ORDER BY` to get a "top N" list.

```sql
SELECT <columns>
FROM <table>
ORDER BY <column> DESC
LIMIT <n>;
```

Example — the ten largest invoices in the dataset:

```sql
SELECT invoice_id, customer_id, amount
FROM invoices
ORDER BY amount DESC
LIMIT 10;
```

`LIMIT 5` is also useful while you are still writing a query and want to peek at the shape of the result before committing.

---

## 4. Aggregates

Aggregate functions collapse many rows into one number. Used alone they return one row total; combined with `GROUP BY` they return one row per group.

| Function | What it does |
|---|---|
| `COUNT(*)` | Count rows |
| `COUNT(<column>)` | Count rows where the column is not NULL |
| `SUM(<column>)` | Add up the values |
| `AVG(<column>)` | Mean value |
| `MIN(<column>)` | Smallest value |
| `MAX(<column>)` | Largest value |

```sql
SELECT COUNT(*), SUM(<column>), AVG(<column>)
FROM <table>;
```

Example — the totals for the whole invoices table:

```sql
SELECT
  COUNT(*)              AS n_invoices,
  SUM(amount)           AS total_billed,
  AVG(amount)           AS avg_invoice,
  MIN(invoice_date)     AS earliest,
  MAX(invoice_date)     AS latest
FROM invoices;
```

SQLite often returns long decimals on `AVG` and `SUM`. Wrap in `ROUND(..., 2)` for readability: `ROUND(AVG(amount), 2)`.

---

## 5. GROUP BY + HAVING

One row per group. Every non-aggregated column in `SELECT` must also appear in `GROUP BY`.

### `GROUP BY` — one row per group

```sql
SELECT <group_col>, <aggregate(s)>
FROM <table>
GROUP BY <group_col>;
```

Example — total billed per customer:

```sql
SELECT customer_id, COUNT(*) AS n_invoices, SUM(amount) AS total
FROM invoices
GROUP BY customer_id
ORDER BY total DESC;
```

### `HAVING` — filter on the aggregate

`WHERE` filters rows *before* grouping. `HAVING` filters groups *after* aggregating. Use `HAVING` when the condition is about an aggregate.

```sql
SELECT <group_col>, <aggregate>
FROM <table>
GROUP BY <group_col>
HAVING <condition on aggregate>;
```

Example — only customers who have been billed more than 50,000 dollars total:

```sql
SELECT customer_id, SUM(amount) AS total
FROM invoices
GROUP BY customer_id
HAVING SUM(amount) > 50000
ORDER BY total DESC;
```

Order of evaluation: `FROM` → `WHERE` → `GROUP BY` → `HAVING` → `SELECT` → `ORDER BY` → `LIMIT`. That order also explains why an alias defined in `SELECT` is not yet available in `WHERE` or `HAVING` (use the full expression there).

---

## 6. INNER JOIN

Combine rows from two tables where a key matches. Rows with no match on either side are dropped.

```sql
SELECT <columns>
FROM <left_table> <alias>
INNER JOIN <right_table> <alias> ON <left>.<key> = <right>.<key>;
```

`INNER JOIN` and `JOIN` mean the same thing in SQLite. Write `INNER JOIN` when you want to be explicit.

Example — pair every invoice with its customer's name and segment:

```sql
SELECT i.invoice_id, i.amount, c.customer_name, c.segment
FROM invoices i
INNER JOIN customers c ON c.customer_id = i.customer_id;
```

Use a short table alias (`i`, `c`, `p`) and prefix every column reference with it. Saves typing and makes which-table-this-came-from obvious.

---

## 7. LEFT JOIN

Keep every row from the left table, even when the right table has no match. Right-side columns come back as `NULL` for the unmatched rows.

```sql
SELECT <columns>
FROM <left_table> <alias>
LEFT JOIN <right_table> <alias> ON <left>.<key> = <right>.<key>;
```

### The completeness check

This is the move for cash application and aging. Every invoice must appear in your report — including the ones with zero payments yet. An `INNER JOIN` would silently drop them and your AR total would be too low. Use `LEFT JOIN` when you are counting or summing things from the left table.

Example — every invoice with its paid total (zero if no payments yet):

```sql
SELECT i.invoice_id, i.amount,
       COALESCE(SUM(p.amount), 0) AS paid_to_date,
       i.amount - COALESCE(SUM(p.amount), 0) AS balance
FROM invoices i
LEFT JOIN payments p ON p.invoice_id = i.invoice_id
GROUP BY i.invoice_id, i.amount;
```

### Find missing rows on the right side

Combine `LEFT JOIN` with `WHERE ... IS NULL` to find left rows with no match. This is how you identify invoices with no payments at all.

```sql
SELECT i.invoice_id, i.amount, i.due_date
FROM invoices i
LEFT JOIN payments p ON p.invoice_id = i.invoice_id
WHERE p.payment_id IS NULL;
```

---

## 8. Multi-table JOIN

Chain joins to walk relationships across three or more tables. Each `JOIN` adds another table; each `ON` clause says how it links.

```sql
SELECT <columns>
FROM <t1> a
JOIN <t2> b ON a.<key> = b.<key>
JOIN <t3> c ON b.<key> = c.<key>;
```

Example — invoice, customer name, customer's terms, and stored status. Four tables, three joins. Watch where each key lives: `customer_id` is on `invoices`, `terms_id` is on `customers` (not invoices), `status_id` is on `invoices`.

```sql
SELECT
  i.invoice_id,
  c.customer_name,
  t.terms_name,
  s.status_name,
  i.amount
FROM invoices i
JOIN customers        c ON c.customer_id = i.customer_id
JOIN invoice_terms    t ON t.terms_id    = c.terms_id
JOIN invoice_statuses s ON s.status_id   = i.status_id
WHERE c.customer_id = 'C-01000';
```

The Lab Part 3.4 / Part 8.4 trap: students often try `i.terms_id` because they expect terms to live on the invoice. Terms live on `customers` — net terms are a customer-level attribute, not a per-invoice attribute. Walk through `customers` to get there.

---

## 9. COALESCE — handle NULL

`COALESCE(a, b)` returns `a` if `a` is not NULL, otherwise `b`. Takes any number of arguments and returns the first non-NULL one.

```sql
COALESCE(<expr>, <fallback>)
```

The standard use case: after a `LEFT JOIN`, the right-side columns are `NULL` for unmatched left rows. `SUM` of zero rows returns `NULL`, not `0`. Wrap it in `COALESCE` so the math still works.

Example — give every invoice a paid total of `0` when it has no payments:

```sql
SELECT i.invoice_id, i.amount,
       COALESCE(SUM(p.amount), 0) AS paid_to_date,
       i.amount - COALESCE(SUM(p.amount), 0) AS balance
FROM invoices i
LEFT JOIN payments p ON p.invoice_id = i.invoice_id
GROUP BY i.invoice_id, i.amount;
```

Without the `COALESCE`, `balance` for an unpaid invoice would be `amount - NULL`, which is `NULL` — and your aging totals would silently lose those rows.

Note: cannot use `= NULL`. Always `IS NULL` / `IS NOT NULL`.

---

## 10. CASE WHEN — conditional bucketing

`CASE` is SQL's `IF`. Use it for aging buckets, status mapping, conditional flags.

```sql
CASE
  WHEN <condition_1> THEN <value_1>
  WHEN <condition_2> THEN <value_2>
  ELSE <default_value>
END
```

The `ELSE` catches anything that did not hit a `WHEN`. Without it, unmatched rows return `NULL`.

Example — bucket every invoice into an aging band:

```sql
SELECT invoice_id, due_date,
  CAST(julianday('2026-04-30') - julianday(due_date) AS INTEGER) AS days_past_due,
  CASE
    WHEN julianday('2026-04-30') - julianday(due_date) <= 0  THEN 'Current'
    WHEN julianday('2026-04-30') - julianday(due_date) <= 30 THEN '1-30'
    WHEN julianday('2026-04-30') - julianday(due_date) <= 60 THEN '31-60'
    WHEN julianday('2026-04-30') - julianday(due_date) <= 90 THEN '61-90'
    ELSE 'Over 90'
  END AS aging_bucket
FROM invoices;
```

### Custom sort order for buckets

Text sort puts `'1-30'` before `'Current'`. Force the order with `CASE` in `ORDER BY`.

```sql
SELECT aging_bucket, SUM(balance) AS total
FROM vw_aging_current
GROUP BY aging_bucket
ORDER BY
  CASE aging_bucket
    WHEN 'Current' THEN 1
    WHEN '1-30'    THEN 2
    WHEN '31-60'   THEN 3
    WHEN '61-90'   THEN 4
    WHEN 'Over 90' THEN 5
  END;
```

---

## 11. CTE — WITH ... AS

A "common table expression" lets you name a sub-query so the main query stays readable. Think of it as defining a temporary, query-scoped table.

```sql
WITH <name> AS (
  <sub-query>
)
SELECT ... FROM <name>;
```

Example — paid totals per invoice, then balances:

```sql
WITH applied AS (
  SELECT invoice_id, SUM(amount) AS paid_total
  FROM payments
  GROUP BY invoice_id
)
SELECT
  i.invoice_id,
  i.amount,
  COALESCE(a.paid_total, 0) AS paid_total,
  i.amount - COALESCE(a.paid_total, 0) AS balance
FROM invoices i
LEFT JOIN applied a ON a.invoice_id = i.invoice_id;
```

### Multiple CTEs

Comma-separate. Each CTE can reference the ones before it.

```sql
WITH <name_1> AS (
  <sub-query_1>
),
<name_2> AS (
  <sub-query_2 — can reference name_1>
)
SELECT ... FROM <name_2>;
```

Example — the aging view in two steps: apply payments through the as-of date, then derive balances and buckets:

```sql
WITH applied_as_of AS (
  SELECT invoice_id, SUM(amount) AS paid_total
  FROM payments
  WHERE payment_date <= '2026-04-30'
  GROUP BY invoice_id
),
balances AS (
  SELECT
    i.invoice_id, i.customer_id, i.due_date, i.amount,
    COALESCE(a.paid_total, 0) AS paid_total,
    i.amount - COALESCE(a.paid_total, 0) AS balance
  FROM invoices i
  LEFT JOIN applied_as_of a ON a.invoice_id = i.invoice_id
  WHERE i.invoice_date <= '2026-04-30'
)
SELECT customer_id, invoice_id, balance
FROM balances
WHERE balance > 0;
```

CTEs are the readable alternative to deeply-nested sub-queries. They are also how you stage logic so each step is testable on its own (run the first CTE alone, sanity-check the rows, then run the next).

---

## 12. Date math — julianday(), date(), CAST

SQLite stores dates as text in `YYYY-MM-DD` format. ISO date strings sort and compare correctly as text, so simple `<` / `>` / `BETWEEN` work without any conversion. For arithmetic — days between, days added — you need `julianday()`.

### `julianday(<date>)` — convert a date to a number

Returns the Julian day number (a real, with fractional days). Subtract two `julianday` values to get the days between.

```sql
julianday(<date>) - julianday(<date>)
```

Example — days past due for every invoice, as of 2026-04-30:

```sql
SELECT invoice_id, due_date,
  julianday('2026-04-30') - julianday(due_date) AS days_past_due
FROM invoices;
```

### `CAST(<expr> AS INTEGER)` — drop the decimal

`julianday` returns a real. For whole days, wrap in `CAST`.

```sql
CAST(<expr> AS INTEGER)
```

Example — clean integer days past due:

```sql
SELECT invoice_id,
  CAST(julianday('2026-04-30') - julianday(due_date) AS INTEGER) AS days_past_due
FROM invoices;
```

### `date(<date>, '<modifier>')` — add or subtract a period

Modifiers: `'+N days'`, `'-N days'`, `'+N months'`, `'-N years'`, `'start of month'`, `'start of year'`. Chain modifiers in one call.

```sql
date(<date>, '<modifier>')
```

Example — what each invoice's due date *would* be on Net 30 terms:

```sql
SELECT invoice_id, invoice_date,
  date(invoice_date, '+30 days') AS net_30_due
FROM invoices
LIMIT 5;
```

### `date('now')` — today

```sql
SELECT date('now');
-- returns the current date as 'YYYY-MM-DD'
```

In your notebook, prefer hard-coding the as-of date (`'2026-04-30'`) over `date('now')` — that way the result is reproducible.

---

## 13. CREATE VIEW vs CREATE TABLE AS SELECT

Two ways to save a query result. They do different things.

**`CREATE VIEW`** saves the *query*. Each time you `SELECT` from the view, SQLite re-runs the query against the live tables. If a new payment lands tomorrow, the view shows the updated number.

**`CREATE TABLE AS SELECT`** saves the *result rows*. The query runs once at creation; the rows are frozen. New payments do not change the table.

Pick based on whether the artifact should keep moving (view) or be a signed snapshot that must not move (table). Accountants freeze month-end and year-end aging because the report was signed on a specific date — the signed number must not change after the fact.

### `CREATE VIEW` — re-computes on every read

```sql
CREATE VIEW <view_name> AS
<query>;
```

Example — the current AR aging view, always reflecting the latest payments through `2026-04-30`:

```sql
CREATE VIEW vw_aging_current AS
WITH applied_as_of AS (
  SELECT invoice_id, SUM(amount) AS paid_total
  FROM payments
  WHERE payment_date <= '2026-04-30'
  GROUP BY invoice_id
)
SELECT
  i.invoice_id, i.customer_id, i.due_date,
  i.amount - COALESCE(a.paid_total, 0) AS balance,
  CAST(julianday('2026-04-30') - julianday(due_date) AS INTEGER) AS days_past_due
FROM invoices i
LEFT JOIN applied_as_of a ON a.invoice_id = i.invoice_id
WHERE i.amount - COALESCE(a.paid_total, 0) > 0;
```

### `CREATE TABLE AS SELECT` — frozen snapshot

```sql
CREATE TABLE <table_name> AS
<query>;
```

Example — the signed year-end aging at 2025-12-31:

```sql
CREATE TABLE ar_aging_2025_12_31 AS
WITH applied_as_of AS (
  SELECT invoice_id, SUM(amount) AS paid_total
  FROM payments
  WHERE payment_date <= '2025-12-31'
  GROUP BY invoice_id
)
SELECT
  i.invoice_id, i.customer_id, i.due_date,
  i.amount - COALESCE(a.paid_total, 0) AS balance
FROM invoices i
LEFT JOIN applied_as_of a ON a.invoice_id = i.invoice_id
WHERE i.invoice_date <= '2025-12-31'
  AND i.amount - COALESCE(a.paid_total, 0) > 0;
```

---

## 14. DROP VIEW IF EXISTS / DROP TABLE IF EXISTS

`CREATE VIEW` fails if a view by that name already exists. Same for tables. While you are iterating — fixing a CTE, tweaking a CASE — drop first, then recreate. The `IF EXISTS` keeps the statement from erroring on the first run.

```sql
DROP VIEW IF EXISTS <view_name>;
DROP TABLE IF EXISTS <table_name>;
```

Example — the re-runnable rebuild of the aging view:

```sql
DROP VIEW IF EXISTS vw_aging_current;

CREATE VIEW vw_aging_current AS
WITH applied_as_of AS (...)
SELECT ... FROM ...;
```

The pair `DROP ... IF EXISTS;` then `CREATE ...` is idempotent — safe to run repeatedly. Get into the habit of writing both as one block in your notebook.

---

## 15. INSERT INTO — write rows

The lab does not require INSERTs — the `summit_gear.sqlite` file ships pre-populated. But the homework loads a lockbox feed into a new table, so the pattern is useful.

### Single-row `VALUES`

```sql
INSERT INTO <table> (<col_1>, <col_2>, ...) VALUES (<v_1>, <v_2>, ...);
```

Example — record one lockbox payment by hand:

```sql
INSERT INTO payments (payment_id, invoice_id, payment_date, amount, payment_source)
VALUES ('PAY-LB-0001', 'INV-2026-005920', '2026-05-15', 4250.00, 'Lockbox');
```

### Many rows from Python — `executemany()`

When the lockbox JSON has 1,000 rows, write them in one round trip. `executemany` takes a parameterized SQL string and an iterable of tuples.

```python
import sqlite3, json

with open("lockbox_feed.json") as f:
    feed = json.load(f)

rows = [
    (p["payment_id"], p["invoice_ref"], p["date"], p["amount"], "Lockbox")
    for p in feed["payments"]
]

conn = sqlite3.connect("summit_gear.sqlite")
cur = conn.cursor()
cur.executemany(
    "INSERT INTO payments (payment_id, invoice_id, payment_date, amount, payment_source) "
    "VALUES (?, ?, ?, ?, ?)",
    rows,
)
conn.commit()
conn.close()
```

The `?` placeholders are positional and the driver handles quoting — never f-string user data into a SQL string.

---

## Appendix — Common errors and their fixes

Four mistakes that bite every first-time SQL student. Recognize them by the shape of the error.

### Single vs double quotes

`'Net 30'` is a string literal. `"Net 30"` is a quoted *identifier* — SQLite looks for a column named `Net 30` and fails with `no such column`.

```sql
-- Wrong: SQLite tries to find a column called Net 30
SELECT * FROM invoice_terms WHERE terms_name = "Net 30";

-- Right: 'Net 30' is the string we are filtering for
SELECT * FROM invoice_terms WHERE terms_name = 'Net 30';
```

Rule: strings in single quotes. Always.

### GROUP BY mismatch

If you `SELECT` a column that is neither in `GROUP BY` nor wrapped in an aggregate, the result is non-deterministic. Some databases reject it outright; SQLite picks an arbitrary value from the group and moves on, which gives you a query that *runs* but produces garbage.

```sql
-- Wrong: customer_name is not in GROUP BY and not aggregated.
-- The customer_name you get back is "some row in the group" — undefined.
SELECT customer_id, customer_name, SUM(amount)
FROM invoices i
JOIN customers c ON c.customer_id = i.customer_id
GROUP BY customer_id;

-- Right: every non-aggregated column is in GROUP BY.
SELECT customer_id, customer_name, SUM(amount)
FROM invoices i
JOIN customers c ON c.customer_id = i.customer_id
GROUP BY customer_id, customer_name;
```

Rule: every non-aggregated column in `SELECT` belongs in `GROUP BY`.

### Missing JOIN key — the Cartesian product

Forget the `ON` clause (or write `JOIN customers c` with nothing after it) and SQLite returns every row of the left table paired with every row of the right. With 20,000 invoices and 1,500 customers that is 30 million rows. The query will run; the result will be nonsense.

```sql
-- Wrong: no ON clause. Cartesian product.
SELECT i.invoice_id, c.customer_name
FROM invoices i
JOIN customers c;

-- Right: ON clause links the tables on the FK.
SELECT i.invoice_id, c.customer_name
FROM invoices i
JOIN customers c ON c.customer_id = i.customer_id;
```

Rule: every `JOIN` needs an `ON`. If the row count of your join result is suspiciously large, this is the first thing to check.

### Looking for terms on the wrong table

`terms_id` lives on `customers`, not on `invoices`. A student who reaches for `i.terms_id` gets `no such column`. Walk through `customers` to find an invoice's terms.

```sql
-- Wrong: invoices has no terms_id column.
SELECT i.invoice_id, t.terms_name
FROM invoices i
JOIN invoice_terms t ON t.terms_id = i.terms_id;

-- Right: terms live on the customer; walk through customers.
SELECT i.invoice_id, t.terms_name
FROM invoices i
JOIN customers     c ON c.customer_id = i.customer_id
JOIN invoice_terms t ON t.terms_id    = c.terms_id;
```

Rule: `PRAGMA table_info(<table>)` before you join. If a column is not in the schema, the join key is somewhere else.
