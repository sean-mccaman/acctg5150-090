# Lab 3 — Colab Starter Prompt (guided vibe coding)

`This is the starter PROMPT you give an LLM to scaffold your Lab 3 Colab notebook. You are not going to type all the Python yourself — you are going to direct the LLM to build it, then verify what it built does what you asked. That is the Week 2 skill applied to a new task.`

`How to use this document:`
`  1. Open a new Colab notebook. Name it lab_03_<your-name>.ipynb.`
`  2. Open a new chat with your LLM of choice (Claude, ChatGPT, or Gemini all work).`
`  3. Paste the prompt below verbatim. Then add the four sections marked "YOU WRITE:" with content from your own work.`
`  4. The LLM will produce a sequence of Colab cells. Copy them into your notebook in order.`
`  5. Run each cell. When something fails, copy the error back to the LLM and ask it to fix.`

`Delete each backtick guidance line once you have read it. The blocks below are the prompt itself.`

---

## The prompt you paste into your LLM

```
You are pair-programming with me on a Google Colab notebook for an undergraduate
accounting analytics lab. I have a SQLite database of accounts receivable for a
fictional company called Summit Gear Co. I will be querying it in SQL. Your job
is to scaffold the notebook one cell at a time — give me each cell, wait for me
to run it, and only move on when I confirm it worked.

CONTEXT YOU NEED:

The database is at this URL (raw GitHub):
  https://raw.githubusercontent.com/sean-mccaman/acctg5150-090/main/2026-summer/week-3/data/summit_gear.sqlite

It contains five tables (you do not need to look these up — I will tell you):

  invoice_terms     (terms_id PK, terms_name, net_days)
  invoice_statuses  (status_id PK, status_name, description)
  customers         (customer_id PK, customer_name, city, state, segment,
                     terms_id FK -> invoice_terms)
  invoices          (invoice_id PK, customer_id FK -> customers,
                     invoice_date, due_date, amount, status_id FK -> invoice_statuses)
  payments          (payment_id PK, invoice_id FK -> invoices,
                     payment_date, amount, payment_source)

The lab "as-of" date is 2026-04-30. All base payments are dated on or before
that day.

WHAT I WANT THE NOTEBOOK TO DO, IN ORDER:

  1. Imports — sqlite3, pandas, matplotlib.pyplot, urllib.request, pathlib.
     Plus a one-line config that makes pandas show all columns when I print
     a DataFrame.

  2. Download summit_gear.sqlite from the URL above, only if the file is not
     already in the local directory. Print the file size in MB to confirm
     the download.

  3. Connect to the database with sqlite3.connect. Verify by reading the
     sqlite_master table and printing the list of table names.

  4. A clearly-labeled Markdown cell titled "Semantic layer" with a placeholder
     I will fill in by pasting my summit_gear_semantic_layer.md content.

  5. Five sampling cells, one per table. Each cell:
       - Runs SELECT * FROM <table> LIMIT 5 via pd.read_sql
       - Prints the result table's shape
       - Prints the dtypes
       - Displays the DataFrame
     Use a Markdown header above each cell that names the table.

  6. A section titled "Required queries (Lab Part 8)" — produce six EMPTY query
     cells, each with a leading Markdown cell that names the analysis the query
     should compute:
       6.1 Cash application — for every invoice, return invoice_id, amount, the
           total paid against it, and the open balance. LEFT JOIN payments,
           GROUP BY invoice. Show the first 20 rows.
       6.2 Total invoiced in Q1 2026 — single number.
       6.3 Total invoiced by customer segment — JOIN to customers, GROUP BY
           segment, order by total desc.
       6.4 All invoices for one named customer — pick a customer with at least
           10 invoices. Join in terms_name and status_name.
       6.5 Top 10 customers by total invoiced — GROUP BY customer, ORDER BY
           SUM DESC, LIMIT 10.
       6.6 Invoice count by stored status — GROUP BY status_name.
     Leave the SQL itself blank inside each query cell. I will write the SQL
     myself — you provide only the cell scaffolding and the comment block above
     each one with a hint. The hint is one sentence: name the relevant tables
     and the aggregate or join the query needs.

  7. A section titled "Aging view + historical snapshot (Lab Part 9)" with:
       7.1 A cell that DROP VIEWs vw_aging_current IF EXISTS, then CREATE VIEW
           with a CTE-based aging query. The query uses two CTEs (applied_as_of
           and balances), filters payment_date <= '2026-04-30', filters out
           Void invoices, and buckets by julianday()-difference into
           Current / 1-30 / 31-60 / 61-90 / Over 90. Provide the full SQL —
           this one I want written for me as a worked example so I can read
           and modify it.
       7.2 A cell that selects from the view and groups by aging_bucket to
           show totals.
       7.3 A cell that DROP TABLEs ar_aging_2025_12_31 IF EXISTS, then
           CREATE TABLE AS SELECT — same query as the view, but with
           '2025-12-31' as the as-of date. This time only stub the cell:
           give me the structure with a TODO comment where the SQL goes.
           I will write it.
       7.4 A Markdown cell with the reflection prompt: "Why is this a TABLE
           and not a VIEW?" — leave space for my answer.

  8. A final cell that closes the connection (conn.close()).

GROUND RULES:

  - One cell at a time. Wait for me to confirm before moving on.
  - Where I asked for a stub, do NOT fill in the SQL. The point is for me to
    write it.
  - Where I asked for a worked example (cell 7.1), give the full SQL.
  - When you hit a step that needs a value from me — for example, the name of
    the customer in 6.4 — ASK FIRST.
  - Comment cells so I understand what they do.
  - If I tell you a cell failed, debug from the error message I show you.
    Do not assume; ask if you do not have enough context.

YOU WRITE:
[Leave the LLM space here to acknowledge before producing Cell 1. Recommended:
ask it to summarize the plan back to you in one paragraph before it writes any
code. If its summary is wrong, correct it BEFORE it starts producing cells.]

YOU WRITE:
[After cell 7.1 — the worked aging view example — paste your own one-paragraph
answer to "what does this query do, in plain English?" The LLM will then know
how much you have understood before scaffolding the rest.]

YOU WRITE:
[Your name here, so the LLM knows whose file it is producing.]

YOU WRITE:
[Optional: your Week 1 about_me.md file pasted in, so the LLM knows what
explanation style works for you. Or: a one-sentence preference — "explain like
I have done one Excel pivot but no SQL" / "I have used SQL once or twice" /
etc.]
```

---

## What you actually submit

`Save your final notebook as lab_03_<your-name>.ipynb. Upload it to the Lab 3 quiz on Canvas alongside your Excel workbook, your semantic layer markdown, and your explainer HTML.`

`The grader is reading your notebook for what the queries DO, not for whether the LLM produced the scaffolding. The SQL in the query cells must be yours — that is the part you wrote.`

`If at any point the LLM produces SQL where the prompt asked for a stub, delete its SQL and write your own. Cite that you got LLM help in your Lab 3 explainer.`

---

## Troubleshooting

`If something goes wrong, the answer is rarely "ask the LLM to start over." The answer is to copy the exact error message and paste it back into the chat. Errors are how the LLM finds the bug.`

`Common gotchas, and what to copy back to the LLM:`

`- "no such table: <X>" — the database did not download or the connection points to the wrong file. Copy the error AND the output of cell 3 (the table-name listing).`

`- "near 'X': syntax error" — your SQL has a typo. Copy the error AND the cell with the bad SQL.`

`- "ambiguous column name" — your JOIN has two tables both named (say) status_id, and you need to disambiguate. Copy the query and tell the LLM to add table aliases.`

`- "no such function: julianday" — you are not on SQLite. (You should be.) Verify cell 3 says sqlite_master in the output.`

`- Notebook is slow / not responding — pandas pulled 18,000 payment rows into a DataFrame and the display is rendering. Add .head() or LIMIT to your query.`

---

## Why "guided vibe coding" instead of a starter notebook

`A starter notebook hands you the scaffolding. A starter PROMPT makes you direct the LLM to produce the scaffolding. Both end at the same place — but only the second one rehearses the skill the course is actually teaching: you spec the work, the AI builds it, you verify the result.`

`This is the Week 2 lesson applied to a new task. The prompt above is your specification. The notebook the LLM produces is the artifact. The SQL inside the query cells is yours.`
