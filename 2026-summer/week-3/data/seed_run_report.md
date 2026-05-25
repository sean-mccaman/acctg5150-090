# Summit Gear AR — Seed Run Report

- Seed: `20260523`
- Generated: 2026-05-23
- Date range: 2024-01-01 → 2026-04-30
- Lab as-of date: **2026-04-30**
- Lockbox arrival window: 2026-05-01 → 2026-05-22

## Top-line counts

| Table | Rows |
|---|---:|
| customers | 1,500 |
| invoices | 20,015 |
| payments (base) | 18,667 |
| lockbox payments | 1,002 |
| invoice_terms | 4 |
| invoice_statuses | 4 |

## Customer profile distribution

| Profile | Count | Share |
|---|---:|---:|
| PROMPT | 642 | 42.8% |
| STANDARD | 443 | 29.5% |
| SLOW | 210 | 14.0% |
| EPISODIC | 118 | 7.9% |
| RISKY | 87 | 5.8% |

## Segment distribution

| Segment | Count | Share |
|---|---:|---:|
| Outdoor Retail | 614 | 40.9% |
| School District | 367 | 24.5% |
| Resort | 310 | 20.7% |
| Outfitter | 209 | 13.9% |

## Terms distribution (customer-level)

| Terms | Count | Share |
|---|---:|---:|
| Net 15 | 175 | 11.7% |
| Net 30 | 818 | 54.5% |
| Net 45 | 428 | 28.5% |
| Due on Receipt | 79 | 5.3% |

## Invoice amount distribution

- min: $100.00
- max: $30,492.04
- mean: $5,341.79
- median: $4,377.36
- total: $106,915,884.57

## Stored status distribution (at lab as-of date)

| Status | Count |
|---|---:|
| Open    | 1,299 |
| Partial | 55 |
| Paid    | 18,545 |
| Void    | 116 |

## Edge cases injected

| Case | Count |
|---|---:|
| Unpaid invoices (no payment row at all) | 349 |
| Underpayments (last invoice only) | 100 |
| Overpayments | 60 |
| Split-payment invoice | INV-2024-018653 |
| Discrepancy: Paid-but-not | 66 |
| Discrepancy: Open-but-paid | 66 |
| Discrepancy: Void-with-payment | 66 |
| Legit voids (no payment, just cancelled) | 50 |
| Lockbox orphan payments (no matching invoice_id) | 2 |

## Customer-level shape

- Customers with at least one delinquent invoice as of 2026-04-30: **405** (27.0%)

## AR aging at lab as-of date (excluding voids)

| Bucket | Invoices | Dollars |
|---|---:|---:|
| Current | 571 | $2,915,107.00 |
| 1-30 | 200 | $1,035,162.35 |
| 31-60 | 92 | $425,693.26 |
| 61-90 | 86 | $493,706.36 |
| Over 90 | 405 | $2,506,106.38 |
| **Total** | **1,354** | **$7,375,775.35** |

## Lockbox feed shape

- File: `data/lockbox_feed_2026-05-20.json`
- Rows: 1,002
- Date range: 2026-05-01 → 2026-05-22
- Payment source: `Lockbox`
- Schema (deliberately different from `payments`):
  - `deposit_batch_id`, `bank_reference`, `received_date`, `branch_code`,
    `customer_account_token`, `invoice_ref`, `amount_cents`
- Orphan rows (invoice_ref not in invoices): 2

## Reproducibility

Re-running `python build_summit_gear.py --seed 20260523` from this commit reproduces every file byte-for-byte.