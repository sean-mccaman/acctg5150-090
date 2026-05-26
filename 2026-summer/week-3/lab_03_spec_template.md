# Lab 3 Spec — Summit Gear AR: From Tables to Aging Report

`Worth 15 points. Write this BEFORE you start the workbook — it is the Setup deliverable that scaffolds everything else. Save your filled-in copy as lab_03_spec.md (plain filename — no name or uID prefix) and upload to the Lab 3 quiz. Delete each backtick guidance line once you've read it.`

`Your spec is graded on PRECISION — specific tables, specific columns, specific edge cases. "Get the data and make a report" is generic; specifics win.`

---

## 1. File manifest

`The four files your Lab 3 work produces. All four go to the Lab 3 quiz with plain filenames (no university ID or personal info — Canvas attaches identity automatically).`

- [ ] `lab_03_spec.md` — this specification (the file you're writing right now) *(upload)*
- [ ] `lab_03.xlsx` — the Excel workbook (Parts 1–6) *(upload)*
- [ ] `lab_03.ipynb` — the Colab notebook (Parts 7–9) *(upload)*
- [ ] `lab_03_explainer.html` — the Part 10 explainer covering SQL and Python *(upload)*

---

## 2. Data sources

`The five Summit Gear AR tables you'll query in both Excel and SQL. For each, name the grain (one row per WHAT?), the primary key, and the foreign-key relationship to the other tables. Pull this from the lab page's "Dataset" section if you have not opened the workbook yet.`

| Table | Grain (one row per ___) | Primary key | Foreign keys |
|---|---|---|---|
| `customers` | | | |
| `invoices` | | | |
| `payments` | | | |
| `invoice_terms` | | | |
| `invoice_statuses` | | | |

**Primary as-of date for this lab:** ____________

**Historical snapshot date (Part 9.2):** ____________

`Note: terms_id lives on customers, not on invoices. To find an invoice's terms you have to JOIN through customers — three tables to answer one question.`

---

## 3. Analyses

`What you'll compute, in order. Be specific. No vague verbs ("analyze", "look at") — name the SQL or Excel construct.`

| # | Analysis | Tool | Construct |
|---|---|---|---|
| Part 2.1 | Cash application — paid_to_date per invoice | Excel | |
| Part 2.2 | Days past due + aging bucket per invoice | Excel | |
| Part 2.3 | Customer-name / segment / terms-name / status-name lookups | Excel | |
| Part 3 | AR aging pivot — two snapshots (current + 2025-12-31) | Excel | |
| Part 4 | Discrepancy hunt — stored vs derived status, three categories | Excel | |
| Part 5 | Top 10 customers by open balance | Excel | |
| Part 6 | Three bar charts (aging, top 10, discrepancies) | Excel | |
| Part 7 | Vibe-code the Colab notebook scaffolding | Colab + LLM | |
| Part 8.1 | Cash application — recreated in SQL | Colab/SQL | |
| Part 8.2 | Q1 2026 total | Colab/SQL | |
| Part 8.3 | Total by customer segment | Colab/SQL | |
| Part 8.4 | One named customer (chained joins) | Colab/SQL | |
| Part 8.5 | Top 10 customers | Colab/SQL | |
| Part 8.6 | Stored status distribution | Colab/SQL | |
| Part 9.1 | `vw_aging_current` — CTE-based VIEW | Colab/SQL | |
| Part 9.2 | `ar_aging_2025_12_31` — frozen snapshot table | Colab/SQL | |

---

## 4. Edge cases

`The traps the data contains. Name each one and how you'll handle it. If you don't know yet, leave a note ("will discover in Part X") — and update this section when you do.`

- [ ] **Voided invoices** — what stored status flags them, and how you exclude them from the aging report:
- [ ] **The one split-payment invoice** — what happens when you SUM payments without grouping by invoice_id:
- [ ] **Discrepancy category — Paid-but-not** — stored = ___, derived = ___, what it means:
- [ ] **Discrepancy category — Open-but-paid** — stored = ___, derived = ___, what it means:
- [ ] **Discrepancy category — Void-with-payment** — stored = ___, derived = ___, what it means:
- [ ] **The 1:n trap in Part 8.1** — what happens to `SUM(amount)` if you JOIN payments naively:
- [ ] **The cross-tool variance line in Part 9.1** — what number must equal what other number, to the cent:

---

## 5. Expected output

`Specific deliverables, in your own words. "The right answer" beats "a report."`

- [ ] The Excel workbook with all nine analytical columns populated, three pivots, three charts, both aging snapshots, and the discrepancy categorization.
- [ ] The Colab notebook with the six SQL analyses, the aging view, the frozen snapshot table, and the cross-tool variance line.
- [ ] The HTML explainer covering the six SQL keywords and the three Python patterns — opened in your browser to verify before upload.
- [ ] The cross-tool variance: SQL aging total vs Excel aging total = ___ (target: zero variance to the cent).

---

## 6. Self-assessment

`Run through this list before you submit any of the four files. Mark [OK], [WARN], or [FIX].`

### Submission gate checklist

- [ ] **SG-01 Filenames correct.** All four uploads use plain names (`lab_03_spec.md`, `lab_03.xlsx`, `lab_03.ipynb`, `lab_03_explainer.html`). No name, no uID, no extra suffix.
- [ ] **SG-02 Spec is filled in (this document).** Every section above has substantive content — not just placeholders.
- [ ] **SG-03 Cutoff cell drives the workbook.** Every analytical column on `invoices` references `cutoff!$B$1`. Spot-check three cells; none should contain the literal `2026-04-30`.
- [ ] **SG-04 Both aging snapshots present.** The `aging_summary` sheet shows the live pivot at the current cutoff AND a value-frozen 2025-12-31 snapshot below it.
- [ ] **SG-05 Discrepancy hunt names three categories.** The `discrepancies` pivot surfaces all three categories with counts and dollars. Your bullets in the quiz name the most concerning category with a ★.
- [ ] **SG-06 Cross-tool verification.** Your Part 9.1 `vw_aging_current` rollup total matches your Excel Part 3 aging pivot total, to the cent. You report the variance (or "exact match, zero variance") in a Markdown cell.
- [ ] **SG-07 Explainer opened in browser.** You double-clicked `lab_03_explainer.html` and read every section in your web browser before uploading. Every "Your explanation" block has been replaced.

### Blocking issues (if any)
- [ ] Issue 1:
- [ ] Issue 2:

### Final decision
- [ ] Ready to submit
- [ ] Not ready — fixes required

---

`How this spec is graded (15 of 100 pts for the lab as a whole):`

`- Sections 1–5 filled in with real specifics (not placeholders) — 10 pts`
`- Edge cases section (§4) named correctly — 3 pts`
`- Self-assessment (§6) honestly completed — 2 pts`

`The full lab rubric is on the lab walkthrough page under "Grading rubric" — single source of truth.`
