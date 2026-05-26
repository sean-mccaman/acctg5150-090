# Lab 3 Spec — Summit Gear AR: From Tables to Aging Report

`This is worth 15 points. Write this BEFORE you start the Colab workbook — it is the Setup deliverable that scaffolds everything else.`

---

## File manifest

`The four files your Lab 3 work produces. All four go to the Lab 3 quiz with plain filenames (no university ID or personal info — Canvas attaches identity automatically).`

- [ ] `lab_03_spec.md`
- [ ] `lab_03.xlsx`
- [ ] `lab_03.ipynb`
- [ ] `lab_03_explainer.html`

---

## References

`URLs you'll need while working through the lab. If you paste a GitHub "blob" URL into Gemini, ChatGPT, or another AI tool and it cannot fetch the file, use the "raw" URL instead — that serves the file as plain text and works in every tool.`

### Lab walkthrough and pre-lab tools (hosted on seanmccaman.com)

- Lab 3 walkthrough page: <https://seanmccaman.com/acctg5150/2026-summer/week-3/lab/lab_03_canvas_page.html>
- Week 3 index (all the week's resources): <https://seanmccaman.com/acctg5150/2026-summer/week-3/>
- Pre-lab SQL trainers (sqlbolt-style — type SQL, run it, get feedback):
  - SQL Fundamentals: <https://seanmccaman.com/acctg5150/2026-summer/week-3/interactive/sql_fundamentals_trainer.html>
  - JOIN trainer (walk this **before** the Aggregate trainer): <https://seanmccaman.com/acctg5150/2026-summer/week-3/interactive/join_trainer.html>
  - Aggregate trainer: <https://seanmccaman.com/acctg5150/2026-summer/week-3/interactive/aggregate_trainer.html>
  - Aging Builder: <https://seanmccaman.com/acctg5150/2026-summer/week-3/interactive/aging_builder.html>
- Excel Concepts trainer (SUMIFS at scale, XLOOKUP, IFS, cutoff cell): <https://seanmccaman.com/acctg5150/2026-summer/week-3/interactive/excel_concepts_trainer.html>
- SQLite cheat sheet (HTML, in-browser): <https://seanmccaman.com/acctg5150/2026-summer/week-3/interactive/sqlite_cheatsheet.html>
- Pandas chart trainer (optional, Python charts via Pyodide): <https://seanmccaman.com/acctg5150/2026-summer/week-3/interactive/pandas_chart_trainer.html>

### Spec, prompt, and reference docs (GitHub)

*Blob URL = renders in your browser. Raw URL = plain text that AI tools can always fetch.*

- Lab 3 starter prompt (the LLM prompt for Part 6):
  - Blob: <https://github.com/sean-mccaman/acctg5150-090/blob/main/2026-summer/week-3/lab_03_starter_prompt.md>
  - Raw: <https://raw.githubusercontent.com/sean-mccaman/acctg5150-090/main/2026-summer/week-3/lab_03_starter_prompt.md>
- Schema and lab explainer (ERD + per-table walkthrough + deliverable map):
  - Blob: <https://github.com/sean-mccaman/acctg5150-090/blob/main/2026-summer/week-3/schema_and_lab_explainer.md>
  - Raw: <https://raw.githubusercontent.com/sean-mccaman/acctg5150-090/main/2026-summer/week-3/schema_and_lab_explainer.md>
- SQLite cheat sheet (Markdown, paste-into-LLM friendly):
  - Blob: <https://github.com/sean-mccaman/acctg5150-090/blob/main/2026-summer/week-3/sqlite_cheatsheet.md>
  - Raw: <https://raw.githubusercontent.com/sean-mccaman/acctg5150-090/main/2026-summer/week-3/sqlite_cheatsheet.md>
- HW 3 spec (the lockbox homework that picks up where this lab ends):
  - Blob: <https://github.com/sean-mccaman/acctg5150-090/blob/main/2026-summer/week-3/hw_03_lockbox_and_reusability.md>
  - Raw: <https://raw.githubusercontent.com/sean-mccaman/acctg5150-090/main/2026-summer/week-3/hw_03_lockbox_and_reusability.md>
- This spec template (the file you're filling in):
  - Blob: <https://github.com/sean-mccaman/acctg5150-090/blob/main/2026-summer/week-3/lab_03_spec_template.md>
  - Raw: <https://raw.githubusercontent.com/sean-mccaman/acctg5150-090/main/2026-summer/week-3/lab_03_spec_template.md>

### Datasets — raw URLs (what your Excel and your Colab notebook fetch directly)

- **Excel template workbook** (download and open in Excel — this is where Parts 1–5 happen): <https://raw.githubusercontent.com/sean-mccaman/acctg5150-090/main/2026-summer/week-3/data/lab_03_template.xlsx>
- **SQLite database** (your Colab notebook downloads this in Part 6): <https://raw.githubusercontent.com/sean-mccaman/acctg5150-090/main/2026-summer/week-3/data/summit_gear.sqlite>
- **CSVs**, one per table — alternative to the SQLite if you prefer reading CSVs:
  - customers.csv: <https://raw.githubusercontent.com/sean-mccaman/acctg5150-090/main/2026-summer/week-3/data/customers.csv>
  - invoices.csv: <https://raw.githubusercontent.com/sean-mccaman/acctg5150-090/main/2026-summer/week-3/data/invoices.csv>
  - payments.csv: <https://raw.githubusercontent.com/sean-mccaman/acctg5150-090/main/2026-summer/week-3/data/payments.csv>
  - invoice_terms.csv: <https://raw.githubusercontent.com/sean-mccaman/acctg5150-090/main/2026-summer/week-3/data/invoice_terms.csv>
  - invoice_statuses.csv: <https://raw.githubusercontent.com/sean-mccaman/acctg5150-090/main/2026-summer/week-3/data/invoice_statuses.csv>
- **Lockbox feed JSON** (HW 3 only, ignore for the lab): <https://raw.githubusercontent.com/sean-mccaman/acctg5150-090/main/2026-summer/week-3/data/lockbox_feed_2026-05-20.json>

---

## Build Requirements:

`Provide a high level description of our goal here - below build requirements. Typically 2-3 sentences`

### Data sources

`You will be using a sqllite database {URL}. It works best when you describe the shape of the tables. If you are using codex, or another on device llm, you can ask it to connect to the sqllite database and explore the tables. You could also use the five csvs`





**Primary as-of date for this lab: 4/30/2026



`Note: terms_id lives on customers, not on invoices. To find an invoice's terms you have to JOIN through customers — three tables to answer one question.`

### Definitions

- Paid To Date:
- Aging: Days from due date to cut off date
- Invoice Status: An invoice is deemed to be aging if it still has an overdue balance



### Analyses

`What you'll compute, in order. Be specific. No vague verbs ("analyze", "look at") — name the SQL or Excel construct.`

| # | Analysis | Tool | Construct |
|---|---|---|---|
| Part 2.1 | Cash application — paid_to_date per invoice | Excel | |
| Part 2.2 | Days past due + aging bucket per invoice | Excel | |
| Part 2.3 | Customer-name / segment / terms-name / status-name lookups | Excel | |
| Part 3 | AR aging pivot — two snapshots (current + 2025-12-31) | Excel | |
| Part 4 | Discrepancy hunt — stored vs derived status, three categories | Excel | |
| Part 5 | One aging bar chart | Excel | |
| Part 6 | Vibe-code the Colab notebook scaffolding | Colab + LLM | |
| Part 7.1 | Cash application — recreated in SQL | Colab/SQL | |
| Part 7.2 | Q1 2026 total | Colab/SQL | |
| Part 7.3 | Total by customer segment | Colab/SQL | |
| Part 7.4 | One named customer (chained joins) | Colab/SQL | |
| Part 7.5 | Top 10 customers | Colab/SQL | |
| Part 7.6 | Stored status distribution | Colab/SQL | |
| Part 8 | Prompt an LLM to write the HTML explainer | LLM | |

---

### Edge cases

`An edge case is an uncommon problem. Could an invoice have more than 1 payment (1:n). Could an invoice be paid and voided? Could the status of an invoice not match the payment? Can someone overpay an invoice? The analysis in here is unlikely to be impacted`



---

### Expected output

`Specific deliverables, in your own words. "The right answer" beats "a report."`

- [ ] The Excel workbook with all nine analytical columns populated, two pivots (aging + discrepancies + top-10 lives in the SQL side), one bar chart, both aging snapshots, and the discrepancy categorization.
- [ ] The Colab notebook with the six SQL analyses (Parts 7.1–7.6).
- [ ] The LLM-generated HTML explainer — opened in your browser to verify before upload.

---

## Review/Acceptance Criteria:

`How a reviewer - or you - confirms the setup work is complete before submission. Keep this standard: all four files exist with correct plain filenames, the workbook and notebook outputs match the expected analyses, and all self-assessment gate checks are [OK] or have clear fix plans.`

## Self-assessment

`Run through this list before you submit any of the four files. Mark [OK], [WARN], or [FIX].`

### Submission gate checklist

- [ ] **SG-01 Filenames correct.** All four uploads use plain names (`lab_03_spec.md`, `lab_03.xlsx`, `lab_03.ipynb`, `lab_03_explainer.html`). No name, no uID, no extra suffix.
- [ ] **SG-02 Spec is filled in (this document).** Every section above has substantive content — not just placeholders.
- [ ] **SG-03 Cutoff cell drives the workbook.** Every analytical column on `invoices` references `cutoff!$B$1`. Spot-check three cells; none should contain the literal `2026-04-30`.
- [ ] **SG-04 Both aging snapshots present.** The `aging_summary` sheet shows the live pivot at the current cutoff AND a value-frozen 2025-12-31 snapshot below it.
- [ ] **SG-05 Discrepancy hunt names three categories.** The `discrepancies` pivot surfaces all three categories with counts and dollars. Your bullets in the quiz name the most concerning category with a ★.
- [ ] **SG-06 Explainer opened in browser.** You double-clicked the LLM-generated `lab_03_explainer.html` and read every section in your web browser. It actually covers your Lab 3 work (not generic SQL examples).
- [ ] **SG-07 Bullet items filled in.** Three quiz items (Discrepancy issues, Excel vs SQL, Prompting takeaways) all have bulleted answers — no prose paragraphs.

### Blocking issues (if any)
- [ ] Issue 1:
- [ ] Issue 2:

### Final decision
- [ ] Ready to submit
- [ ] Not ready — fixes required

---

## How this specification is graded

`How this spec is graded (15 of 100 pts for the lab as a whole):`

`- Build Requirements sections are filled in with real specifics (not placeholders) - 10 pts`
`- Edge cases section is named correctly and handled concretely - 3 pts`
`- Self-assessment is honestly completed - 2 pts`

`The full lab rubric is on the lab walkthrough page under "Grading rubric" - single source of truth.`
