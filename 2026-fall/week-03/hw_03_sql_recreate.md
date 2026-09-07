# HW 3: Recreate the Lab in SQL

## Goal

You already produced the headline AR numbers for Summit Gear in Excel during Lab 3. Now reproduce those same numbers in SQL against the source database, and explain a few of the SQL ideas in your own words.

There is no auto-grade on this homework. You will not see feedback while taking the quiz. Grades and per-question comments come back after the deadline, once each response has been read.

## Prerequisite

Lab 3 must be complete, including the `summary` sheet. The cell values on that sheet are your validation targets for every SQL query in Part 1.

## Where you work

All SQL queries are written in the in-browser SQL Workbench:

https://seanmccaman.com/acctg6155/2026-fall/week-3/interactive/sql_workbench.html

A few things to know:

- The 5 lab tables are preloaded into an in-browser SQLite database. Nothing to download.
- The right sidebar lists the 8 homework questions. Click one to load it into the editor.
- The AI tutor in the workbench is seeded with the schema, a glossary of the columns, and canonical hints. It will help you think through a query. It will not write the final answer for you.
- Your work is local to your browser. Copy your queries into the Canvas quiz as you go. Do not rely on the workbench to remember them tomorrow.

## How submission works

This week is different from Week 2. **There is no file upload.** Every SQL query and every concept answer goes into its own Canvas quiz question, pasted into the answer box.

Each SQL question expects only the query. You do not need to explain it. The concept questions at the end of the quiz cover the explanation work.

## Part 1: SQL queries (questions 1 to 8)

For each prompt below, write the query in the SQL Workbench, run it, confirm the row count or totals match your Excel summary sheet, then paste your SQL into the matching Canvas item.

HW-01 and HW-02 are worth 7 points each. HW-03 through HW-08 are worth 8 points each.

| # | Prompt | Expected result | Validates against |
|---|---|---|---|
| HW-01 | All rows and columns from `invoices` | 20,015 rows | `summary` "Total invoice count" |
| HW-02 | Distinct `customer_id` values from `invoices` | 1,500 rows | `summary` "Unique customer count" |
| HW-03 | Sum `amount` from `payments` grouped by `invoice_id` | 18,666 rows | `summary` "Total payment count" is 18,667, one higher, because one invoice has two payment rows; sum of total paid = "Total payments received" |
| HW-04 | CTE on HW-03 joined back to `invoices`, plus a computed `balance` column (LEFT JOIN + COALESCE) | 20,015 rows, total balance about $7.62M | `summary` "Total invoiced amount" minus "Total payments received" |
| HW-05 | Filter HW-04 to only OPEN invoices (`balance > 0`) | 1,404 rows, $7,656,873.45 | `summary` "Open invoice count" + "Total open balance" |
| HW-06 | Top 10 customers by total open balance, with name and segment | 10 rows, top around $69,562 | `top_customers` pivot |
| HW-07 | AR by aging bucket as of 2026-04-30, open invoices only (start from HW-05), using `CASE WHEN` + `julianday()` | 5 buckets, 1,404 invoices, $7,656,873.45 total | `aging_summary` pivot |
| HW-08 | Discrepancy hunt with three flavors (Paid-but-not, Open-but-paid, Void-with-payment) via `CASE` | 3 rows, 66 invoices each | `discrepancies` pivot, the Paid/Open, Open/Paid, and Void/Paid cells (Void/Open is not a discrepancy) |

## Part 2: Concept questions (questions 9 to 13, 7 or 8 points each)

Five short-answer questions on the core SQL ideas behind your Part 1 work. Length target: 50 to 150 words each. The CTE question (Q11) gets a slightly longer target.

| # | Concept |
|---|---|
| Q9 | What does `GROUP BY` do? |
| Q10 | Difference between `INNER JOIN` and `LEFT JOIN` |
| Q11 | What is a CTE (the `WITH` clause) and why use one? |
| Q12 | Difference between `COUNT(*)` and `COUNT(DISTINCT col)` |
| Q13 | Why wrap a column in `COALESCE(col, 0)`? |

AI-assisted drafts are fine. The grading bar is that the answer reads like your understanding, not a generic textbook definition. If you could not defend the wording in a one-on-one conversation, rewrite it.

## Validation discipline

Two independent calculations of the same number should agree. When they do not, one is wrong, and you do not move on until you know which one and why.

Common reasons your SQL number will not match your Excel number:

- Your SQL is excluding rows it should be including. Usually a missing LEFT JOIN, a forgotten COALESCE, or a WHERE clause that filters out NULLs.
- Your Excel cell is wrong. Lab 3 was the first time you built the summary sheet. Mistakes there are normal. The SQL pass often catches them.
- You and the SQL are using different definitions. For example, "open invoices" can mean `status = 'Open'` or `balance > 0`. Those are different sets. The HW expects `balance > 0`.

When the numbers match, you are done with that question. When they do not, the discrepancy is the assignment.

## Grading

Lab 3 grading is generous and so is this. HW-01 and HW-02 are 7 points each, HW-03 through HW-08 are 8 points each, and the concept questions are 7 or 8 points each. Four short intake questions at the end carry the last 2 points. There is no auto-grade. Each response is read, and grades plus per-question feedback come back after the deadline.

A query that runs cleanly and returns the expected row count earns full credit. A query that does not run, or that returns the wrong shape, loses marks. A concept answer that shows real understanding earns full credit. A generic answer that could have been written by anyone without doing the queries loses marks.

## FAQ and gotchas

**My WHERE clause on `balance` throws "no such column".** `balance` is not a column on `invoices`. It only exists once you compute it. Wrap HW-04 in a CTE and put the `WHERE balance > 0` in the outer query. That is HW-05. SQLite would also accept the filter inside HW-04's own SELECT, but use the CTE. It is the pattern that scales, and it is the example you will want for Q11.

**My HW-04 total is $7.62M but HW-05 is $7.66M.** Both are right. HW-04 nets every balance, and 56 overpaid invoices carry a small negative balance that pulls the total down. HW-05 keeps only `balance > 0`.

**My aging buckets have thousands of invoices in 90+.** You binned all 20,015 invoices. HW-07 is open invoices only, so start from HW-05. The counts should add to 1,404.

**My invoice count is 18,666 instead of 20,015.** You used an INNER JOIN to payments. 1,349 invoices have no payment row at all. Use LEFT JOIN, then wrap `total_paid` in `COALESCE(total_paid, 0)` so the arithmetic works.

**My aging buckets are off by one day.** Use `julianday('2026-04-30') - julianday(due_date)` and bucket on that integer. The cutoff date is 2026-04-30 for everything in this week.

**My distinct customer count is 1,499, not 1,500.** Check whether you have a stray WHERE clause filtering out a customer with only voided invoices. HW-02 is unfiltered; every customer with any invoice counts.

**My SQL total matches Excel to the dollar but my row count is off.** Two different bugs can produce the same total. Trust the row count. If HW-04 does not return exactly 20,015 rows, the query is wrong even if the dollars happen to tie out.

**My AI tutor will not give me the answer.** That is by design. It will explain a SQL clause, point you at a relevant pattern, and help you read an error message. It will not paste a working query into your editor. Run your attempts, read the result, ask the tutor what is off.
