# HW 3: Recreate the Lab in SQL

## Goal

You already produced the headline AR numbers for Summit Gear in Excel. Now reproduce those same numbers in SQL against the source database. The point is not to learn new answers. The point is to learn that two different tools, pointed at the same data, should give you the same answer. When they do not, one of them is wrong and you have to find out which.

## Prerequisite

Lab 3 must be complete, including the `summary` sheet. You will use the 7 headline cells and the `top_customers` pivot from that sheet as your validation targets. If your Excel summary is wrong, your SQL will not match it, and you will chase the wrong bug. Finish the lab first.

## Where you will work

You will write all of your SQL in the course SQL Workbench:

https://seanmccaman.com/acctg5150/2026-summer/week-3/interactive/sql_workbench.html

A few things to know about the workbench:

- The 5 lab tables are preloaded into an in-browser SQLite database. There is nothing to download.
- The right sidebar lists the 8 homework questions. Click one to load it into the editor and run it.
- The AI tutor in the workbench is seeded with the schema, a glossary of the columns, and canonical hints. It will help you debug a query. It will not write the final query for you.
- Your work is local to your browser. Copy your queries out as you go. Do not rely on the workbench to remember them tomorrow.

## The 8 questions

Each question is a step toward reproducing one of the summary-sheet cells. Validate the row count and the dollar totals against your Excel summary as you go.

| # | Question | Expected result | Validates against |
|---|---|---|---|
| HW-01 | Select all columns and rows from `invoices`. | 20,015 rows | `summary!total_invoices` |
| HW-02 | Select the distinct customer IDs from `invoices`. | 1,500 rows | `summary!total_customers` |
| HW-03 | Sum `amount` from `payments` grouped by `invoice_id`. | ~18,666 rows (one per invoice that has at least one payment) | Spot check vs. `payments` row count |
| HW-04 | JOIN the aggregated payments from HW-03 as a CTE to `invoices`. Add a computed `balance = amount - total_paid`. Use LEFT JOIN plus COALESCE so invoices with no payment still appear. | 20,015 rows; total balance ~$7.62M | `summary!total_billed` minus `summary!total_collected` |
| HW-05 | Filter HW-04 down to OPEN invoices only (`balance > 0`). | 1,404 rows; total open balance $7,656,873.45 | `summary!open_balance` |
| HW-06 | Top 10 customers by total open balance. Include `customer_name` and `segment`. | 10 rows; top customer ~$69,562 | `summary!top_customers` pivot |
| HW-07 | AR by aging bucket as of 2026-04-30 using `CASE WHEN` and `julianday()`. | 5 buckets | Lab Part 3 aging pivot |
| HW-08 | Discrepancy hunt. Three flavors in one query using `CASE`: Paid-but-not-marked-paid, Open-but-fully-paid, Void-with-payment. | 3 rows, 66 invoices each | Lab Part 4 discrepancy pivot |

## The flow

1. Re-open your `lab_03.xlsx` workbook. Keep the `summary` sheet visible. It is your answer key.
2. Open the SQL Workbench at the URL above.
3. Work through HW-01 through HW-08 in order. Each one builds on the previous query, so do not skip around.
4. After each query, compare the SQL result to the matching cell or pivot in your Excel summary. They should match exactly. If they do not, stop and find the bug before moving on.
5. When all 8 are passing, ask Gemini, ChatGPT, or Claude to help you write a short explainer of what you wrote and what you learned. Details in the section below.

## Validation discipline

This is the accounting reconciliation beat. Two independent calculations of the same number should agree. When they do not, one is wrong. You do not move on until you know which one and why.

Common reasons your SQL number will not match your Excel number:

- Your SQL is excluding rows it should be including. Usually a missing LEFT JOIN, a COALESCE you forgot, or a WHERE clause that filters out the NULLs.
- Your Excel cell is wrong. Lab 3 was the first time you built the summary sheet. Mistakes there are normal. The SQL pass often catches them.
- You and the SQL are using different definitions. For example, "open invoices" can mean `status = 'Open'`, or it can mean `balance > 0`. Those are different sets. The HW expects `balance > 0`.

When the numbers match, you are done with that question. When they do not, the discrepancy is the assignment.

## The explainer (about 300 to 500 words)

After your SQL is working, generate a short markdown explainer with help from an AI tutor (Gemini, ChatGPT, or Claude). The explainer is what you would hand a classmate who missed this week and needs to understand what you did.

A reasonable workflow:

1. Paste your full `hw_03.sql` into the chat.
2. Paste a few representative result tables next to the queries that produced them.
3. Ask the model to walk through each query in plain English and explain why it is structured the way it is. Pay attention to HW-04 (the CTE plus LEFT JOIN plus COALESCE pattern) and HW-07 (the CASE WHEN bucketing). Those are the two patterns worth understanding.
4. Ask the model what the queries collectively tell you about Summit Gear's AR position.
5. Iterate. The first draft will be too long or too generic. Push back until it reads like something you would actually hand to a peer.

The explainer should cover what the queries do, what they showed you about the data, and what surprised you. It does not need to be polished prose. It does need to be substantive and your own thinking, not the model's first pass.

## Submission

Submit two files to the Canvas HW 3 assignment:

- `hw_03.sql`: every SQL query you wrote, in order, with a one-line comment above each query naming the question (for example `-- HW-04: invoices with computed balance`). Include the queries that did not work too, commented out, if you want partial credit on a stuck question.
- `hw_03_explainer.md`: the markdown explainer you produced with AI help.

One submission per student. No zip files, no PDFs.

## Grading

Lab 3 grading is generous and so is this. A submission with 8 working queries that validate against the Excel summary, plus a substantive explainer that shows you understood what you wrote, earns full credit. Missing queries, queries that do not run, or an explainer that is clearly the model's first draft and not your own thinking will lose marks. There are no point breakdowns on the individual questions. Submit the full set or do not submit.

## FAQ and gotchas

**My WHERE clause on `balance` throws an error.** SQLite will not let you filter on a column you just computed in the same SELECT. Wrap HW-04 in a CTE and put the `WHERE balance > 0` in the outer query. That is HW-05.

**My invoice count is 18,666 instead of 20,015.** You used an INNER JOIN to payments. 1,349 invoices have no payment row at all. Use LEFT JOIN, then wrap the `total_paid` column in `COALESCE(total_paid, 0)` so the arithmetic works.

**My aging buckets are off by one day.** Use `julianday('2026-04-30') - julianday(due_date)` and bucket on that integer. The cutoff date is 2026-04-30 for everything in this week. Do not use `CURRENT_DATE`. The data is historical.

**My distinct customer count is 1,499, not 1,500.** Check whether you have a stray WHERE clause filtering out a customer with only voided invoices. HW-02 is unfiltered. Every customer with any invoice counts.

**My SQL total matches Excel to the dollar but my row count is off.** Two different bugs can produce the same total. Trust the row count. If HW-04 does not return exactly 20,015 rows, the query is wrong even if the dollars happen to tie out.
