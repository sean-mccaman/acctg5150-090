# Summit Gear Schema + Lab Explainer — ACCTG 5150 Week 3
*Background reference for the Lab 3 and HW 3 work. Open this in another tab as you read the lab.*

For SQL syntax, see the [SQLite cheat sheet](https://github.com/sean-mccaman/acctg5150-090/blob/main/2026-summer/week-3/sqlite_cheatsheet.md) (also hosted as [HTML](https://seanmccaman.com/acctg5150/2026-summer/week-3/interactive/sqlite_cheatsheet.html)).

---

## 1. The dataset in one paragraph

Summit Gear Co. is a fictional wholesale outdoor-equipment distributor based in Salt Lake City, selling to four customer segments — Outdoor Retail, School District, Resort, and Outfitter. The AR dataset covers a 28-month window from **2024-01-01 to 2026-04-30** and lands in your hands as five tables: about 1,500 customers, roughly 20,000 invoices, and about 18,700 payments, plus two small lookup tables for terms and statuses. Each customer carries one of five payment profiles (PROMPT, STANDARD, SLOW, EPISODIC, RISKY) that governs how they pay over time, which is why the dataset has realistic-feeling rhythm rather than uniformly-late or uniformly-on-time payments. The job: read it, compute the AR aging report, and find the disagreements between the ERP's stored invoice status and what the payments actually do.

---

## 2. Schema diagram

```
                     ┌─────────────────────┐
                     │   invoice_terms     │   (4 rows — lookup)
                     │  ─────────────────  │
                     │  terms_id  (PK)     │◄──────┐
                     │  terms_name         │       │
                     │  net_days           │       │
                     └─────────────────────┘       │
                                                   │
                     ┌─────────────────────┐       │
                     │     customers       │       │
                     │  ─────────────────  │       │
                     │  customer_id  (PK)  │◄──┐   │
                     │  customer_name      │   │   │
                     │  city, state        │   │   │
                     │  segment            │   │   │
                     │  terms_id     (FK)  │───┼───┘
                     └─────────────────────┘   │
                                               │
                     ┌─────────────────────┐   │
                     │     invoices        │   │
                     │  ─────────────────  │   │
                     │  invoice_id   (PK)  │◄──┼───┐
                     │  customer_id  (FK)  │───┘   │
                     │  invoice_date       │       │
                     │  due_date           │       │
                     │  amount             │       │
                     │  status_id    (FK)  │───┐   │
                     └─────────────────────┘   │   │
                                               │   │
                     ┌─────────────────────┐   │   │
                     │  invoice_statuses   │   │   │
                     │  ─────────────────  │   │   │
                     │  status_id  (PK)    │◄──┘   │
                     │  status_name        │       │
                     │  description        │       │
                     └─────────────────────┘       │
                                                   │
                     ┌─────────────────────┐       │
                     │     payments        │       │
                     │  ─────────────────  │       │
                     │  payment_id   (PK)  │       │
                     │  invoice_id   (FK)  │───────┘
                     │  payment_date       │
                     │  amount             │
                     │  payment_source     │
                     └─────────────────────┘
```

In words:
- A **customer** has one **terms** code (`customers.terms_id` → `invoice_terms.terms_id`)
- An **invoice** has one **customer** (`invoices.customer_id` → `customers.customer_id`) and one stored **status** (`invoices.status_id` → `invoice_statuses.status_id`)
- A **payment** is tied to one **invoice** (`payments.invoice_id` → `invoices.invoice_id`)
- Net terms are a *customer-level* attribute, not an invoice-level one. To find an invoice's terms, JOIN through `customers` to `invoice_terms`. See [Section 4](#4-key-relationships-to-know) below.

---

## 3. Each table in detail

### 3.1 `customers` — one row per customer

- **Grain:** one row per customer. ~1,500 rows.
- **PK:** `customer_id` (a TEXT code like `C-01000`)
- **FK:** `terms_id` → `invoice_terms.terms_id`

| Column | Type | Purpose |
|---|---|---|
| `customer_id` | TEXT (PK) | Stable customer code |
| `customer_name` | TEXT | Display name |
| `city` | TEXT | City |
| `state` | TEXT | Two-letter state code |
| `segment` | TEXT | One of: Outdoor Retail, School District, Resort, Outfitter |
| `terms_id` | INTEGER (FK) | The customer's standing payment terms |

Sample rows:

| customer_id | customer_name | city | state | segment | terms_id |
|---|---|---|---|---|---:|
| C-01000 | Ogden Valley Schools | Denver | CO | School District | 2 |
| C-01001 | Cottonwood Heights ISD | Casper | WY | School District | 2 |
| C-01002 | Uinta Highline Outfitters | Logan | UT | Outfitter | 2 |

### 3.2 `invoices` — one row per invoice

- **Grain:** one row per invoice issued. ~20,000 rows.
- **PK:** `invoice_id` (TEXT, e.g. `INV-2024-000001`)
- **FKs:** `customer_id` → `customers.customer_id`; `status_id` → `invoice_statuses.status_id`

| Column | Type | Purpose |
|---|---|---|
| `invoice_id` | TEXT (PK) | Stable invoice code |
| `customer_id` | TEXT (FK) | Who was billed |
| `invoice_date` | DATE | When the invoice was issued (YYYY-MM-DD) |
| `due_date` | DATE | When payment is contractually due |
| `amount` | NUMERIC | Invoice amount, in dollars |
| `status_id` | INTEGER (FK) | The ERP's *stored* status — set by hand, not always correct |

Sample rows:

| invoice_id | customer_id | invoice_date | due_date | amount | status_id |
|---|---|---|---|---:|---:|
| INV-2024-000001 | C-01000 | 2024-02-02 | 2024-03-03 | 8087.55 | 3 |
| INV-2024-000002 | C-01000 | 2024-09-25 | 2024-10-25 | 7578.30 | 3 |
| INV-2025-000004 | C-01000 | 2025-03-27 | 2025-04-26 | 8981.53 | 3 |

### 3.3 `payments` — one row per payment

- **Grain:** one row per payment. ~18,700 rows.
- **PK:** `payment_id` (TEXT, e.g. `PAY-0000001`)
- **FK:** `invoice_id` → `invoices.invoice_id`

| Column | Type | Purpose |
|---|---|---|
| `payment_id` | TEXT (PK) | Stable payment code |
| `invoice_id` | TEXT (FK) | Which invoice this payment is applied to |
| `payment_date` | DATE | When the payment was received (YYYY-MM-DD) |
| `amount` | NUMERIC | Payment amount, in dollars |
| `payment_source` | TEXT | Channel — ACH, Wire, Check, etc. |

Sample rows:

| payment_id | invoice_id | payment_date | amount | payment_source |
|---|---|---|---:|---|
| PAY-0018550 | INV-2025-018884 | 2026-03-16 | 6904.66 | ACH |
| PAY-0005682 | INV-2026-005764 | 2026-04-24 | 12529.07 | Wire |
| PAY-0017967 | INV-2024-018288 | 2024-08-21 | 12081.97 | ACH |

Most invoices have exactly one payment row. A few have zero (unpaid), one has two (split payment), 100 have an underpayment (payment < amount), and 60 have an overpayment (payment > amount). Detail in [Section 5](#5-seeded-edge-cases).

### 3.4 `invoice_terms` — lookup, 4 rows

- **Grain:** one row per terms code.
- **PK:** `terms_id`

| Column | Type | Purpose |
|---|---|---|
| `terms_id` | INTEGER (PK) | Numeric code |
| `terms_name` | TEXT | Display name |
| `net_days` | INTEGER | Days from invoice date to due date |

Full contents:

| terms_id | terms_name | net_days |
|---:|---|---:|
| 1 | Net 15 | 15 |
| 2 | Net 30 | 30 |
| 3 | Net 45 | 45 |
| 4 | Due on Receipt | 0 |

### 3.5 `invoice_statuses` — lookup, 4 rows

- **Grain:** one row per stored status.
- **PK:** `status_id`

| Column | Type | Purpose |
|---|---|---|
| `status_id` | INTEGER (PK) | Numeric code |
| `status_name` | TEXT | Display name |
| `description` | TEXT | Brief description |

Full contents:

| status_id | status_name | description |
|---:|---|---|
| 1 | Open | Issued; payment not yet fully received. |
| 2 | Partial | Issued; some payment received but balance remains. |
| 3 | Paid | Issued; total payment received meets invoice amount. |
| 4 | Void | Issued then cancelled; not a live receivable. |

Key point: this is the *stored* status — what someone in accounting flipped a flag to. It is not always correct. The disagreements between this stored status and the payment-derived state are the discrepancy hunt in Lab Part 5.

---

## 4. Key relationships to know

Three relationships drive every multi-table query in the lab and homework.

**Invoice → customer (direct).** `invoices.customer_id` → `customers.customer_id`. Used in every customer-rollup query.

**Invoice → terms (through customer).** `invoices.customer_id` → `customers.customer_id`, then `customers.terms_id` → `invoice_terms.terms_id`. This is the trap. Net terms are a *customer-level* attribute, not an invoice-level one. A given customer always invoices on the same terms.

There is **no `terms_id` column on `invoices`**. Students often reach for `i.terms_id` and get `no such column`. The fix is to walk through `customers`:

```sql
SELECT i.invoice_id, t.terms_name
FROM invoices i
JOIN customers     c ON c.customer_id = i.customer_id
JOIN invoice_terms t ON t.terms_id    = c.terms_id;
```

This is the Lab Part 3.4 / Part 8.4 multi-table-JOIN exercise.

**Payment → invoice → customer.** `payments.invoice_id` → `invoices.invoice_id`, then `invoices.customer_id` → `customers.customer_id`. Used whenever you want to roll payments up to the customer (e.g. "total received from C-01000").

---

## 5. Seeded edge cases

The dataset is shaped to be boring to a CFO and pedagogically rich for a first-time SQL student. Six designed exceptions. Each is in the data on purpose — finding and explaining them is part of the lab.

| Case | Count | Where it lives | What it teaches |
|---|---:|---|---|
| Unpaid invoices (no payment row at all) | ~349 (~1.7%) | `invoices` with no matching `payments` | LEFT JOIN, aging buckets, customer rollup. Forces the "every invoice must appear" thinking. |
| Status discrepancies (stored ≠ derived) | ~198 (~1%) | `invoices.status_id` | Stored vs derived state. The controls beat — the disagreement is where the analyst earns their keep. |
| Underpayments | 100 | `payments` | Partial balance arithmetic. Payment is less than the invoice amount; balance is positive but small. Scoped to a customer's last invoice only. |
| Overpayments | 60 | `payments` | Credit balance. Payment exceeds the invoice amount; balance goes negative. |
| Split-payment invoice (one specific) | 1 (`INV-2024-018653`) | `payments` | Two payment rows for one invoice. Why `SUM(amount) GROUP BY invoice_id` matters — a `MAX` or `MIN` over payments would give the wrong number for this one. |
| Legit voids (no payment, real cancellation) | ~50 | `invoices.status_id = 4` | Real Void state — the invoice was cancelled. Must be excluded from aging; not a real receivable. |
| Lockbox orphan payments | 1–2 | `lockbox_feed_2026-05-20.json` (HW) | Cash-side LEFT JOIN skepticism. Lockbox payments whose `invoice_ref` matches no invoice in the system. **Not in lab — HW only.** |

The point is not that the dataset is dirty in some special way — it is that *every* real B2B AR dataset has cases like these. The lab gives you practice naming them.

---

## 6. As-of dates

| Date | Meaning |
|---|---|
| 2024-01-01 → 2026-04-30 | Invoice date range. No invoice in the base dataset is dated outside this window. |
| **2026-04-30** | The lab's primary as-of date. The aging report and the `vw_aging_current` view are built against this. |
| **2025-12-31** | The historical snapshot built in Lab Part 9.2 as `ar_aging_2025_12_31`. Demonstrates `CREATE TABLE AS SELECT` (frozen) vs `CREATE VIEW` (recomputed). |
| **2026-05-23** | The HW as-of date once the lockbox feed integrates. The lockbox JSON covers payments arriving 2026-05-01 through 2026-05-22. |

When you write a query that references an as-of date, hard-code the date string (`'2026-04-30'`) rather than using `date('now')`. That way the result is reproducible months later, when "now" is no longer the same day.

---

## 7. Where this schema is used in the lab

A quick map from each lab/HW deliverable to the tables it touches:

| Deliverable | Tables touched | Key shape |
|---|---|---|
| **Lab Part 3.1 — Cash application** | `payments` → `invoices` | LEFT JOIN payments, GROUP BY invoice_id, COALESCE(SUM, 0) |
| **Lab Part 3.3 — By customer segment** | `invoices` + `customers` | JOIN customers, GROUP BY segment |
| **Lab Part 3.4 — One named customer** | `invoices` + `customers` + `invoice_terms` + `invoice_statuses` | The multi-table-JOIN trap |
| **Lab Part 4 — AR aging** | `invoices` + `payments` + `invoice_statuses` | LEFT JOIN payments, filter Void, CASE WHEN bucketing |
| **Lab Part 5 — Discrepancy hunt** | `invoices` + `payments` + `invoice_statuses` | Compare stored status vs derived state; classify the disagreement |
| **Lab Part 8.4 — Four-table JOIN in SQL** | `invoices` + `customers` + `invoice_terms` + `invoice_statuses` | The same multi-table-JOIN, in SQL this time |
| **Lab Part 9.1 — Aging view** | `invoices` + `payments` + `invoice_statuses` | CTE-shaped CREATE VIEW with julianday() and CASE |
| **Lab Part 9.2 — Historical snapshot table** | Same as 9.1, but with `'2025-12-31'` | CREATE TABLE AS SELECT — frozen result |
| **HW Part 3 — Lockbox** | `payments` + new lockbox table + `invoices` | INSERT INTO from JSON; LEFT JOIN to find orphan payments |

If you can read the schema and write each of those JOIN/aggregate shapes, you have the SQL covered for Week 3.

---

## 8. Companion links

- **SQLite cheat sheet (Markdown):** <https://github.com/sean-mccaman/acctg5150-090/blob/main/2026-summer/week-3/sqlite_cheatsheet.md>
- **SQLite cheat sheet (HTML, with copy-paste buttons):** <https://seanmccaman.com/acctg5150/2026-summer/week-3/interactive/sqlite_cheatsheet.html>
- **Lab 3 page (Canvas-equivalent HTML):** <https://seanmccaman.com/acctg5150/2026-summer/week-3/lab_03_canvas_page.html>
- **Pre-lab SQL trainers:**
  - [SQL Fundamentals trainer](https://seanmccaman.com/acctg5150/2026-summer/week-3/interactive/sql_fundamentals_trainer.html) — SELECT / FROM / WHERE / ORDER BY / LIMIT
  - [Aggregate trainer](https://seanmccaman.com/acctg5150/2026-summer/week-3/interactive/aggregate_trainer.html) — GROUP BY, SUM, COUNT, AVG, HAVING
  - [JOIN trainer](https://seanmccaman.com/acctg5150/2026-summer/week-3/interactive/join_trainer.html) — INNER vs LEFT, the 1:n trap
  - [Aging builder](https://seanmccaman.com/acctg5150/2026-summer/week-3/interactive/aging_builder.html) — the headline; builds toward `vw_aging_current`
- **Lab spec template** (Part 2 deliverable starting point): <https://github.com/sean-mccaman/acctg5150-090/blob/main/2026-summer/week-3/lab_03_spec_template.md>
- **Vibe-code starter prompt** (Part 7): <https://github.com/sean-mccaman/acctg5150-090/blob/main/2026-summer/week-3/lab_03_starter_prompt.md>

If a link 404s, the artifact has not been deployed yet — check the lab page on Canvas for the current set.
