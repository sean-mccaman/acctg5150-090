# Summit Gear customer accounts: data dictionary

`summit_gear_customers.csv` holds 2,200 business (B2B) customer accounts for Summit
Gear Co., a wholesale outdoor-equipment company. Each row is one account. The data is
synthetic teaching data, built to behave like a real receivables file. It is the same
file as Week 10, unchanged.

This week you predict `defaulted`, whether an account's receivable was written off, from
the account's attributes. `days_to_pay` was Week 10's target. It is known only after an
invoice is paid, so it is not a predictor this week.

## Timing

Every predictor is measured as of the start of the period: counts and limits on that date,
and averages and totals over the 12 months before it. `defaulted` records write-offs during
the period that follows. So a review list made at the start of the period can use every
predictor, and cannot use `defaulted` or `days_to_pay`.

## Columns

| Column | Type | Meaning |
|---|---|---|
| `customer_id` | text | Unique account ID. An identifier, not a predictor. |
| `region` | category | Sales region: Mountain North, Mountain Central, Desert Southwest. |
| `segment` | category | Account segment: Outdoor Retail, School District, Resort, Outfitter. |
| `industry` | category | Account industry (Retail, Hospitality, Public Sector, Recreation Services). Each segment maps to exactly one industry, so this column repeats `segment` under another name. |
| `tenure_months` | number (months) | Months the account has been active. |
| `credit_limit` | number ($) | The account's credit limit. |
| `avg_balance` | number ($) | Average outstanding balance over the 12 months before the period. |
| `annual_spend` | number ($) | Total spend over the 12 months before the period. |
| `prior_late_count` | number (invoices) | Count of invoices the account paid late before the period. |
| `days_since_last_order` | number (days) | Days from the account's most recent order to the start of the period. |
| `orders_per_year` | number (orders) | Orders the account placed over the 12 months before the period. |
| `discount_rate` | number (percent) | Average discount rate offered to the account over the 12 months before the period. 3.5 means 3.5%. |
| `avg_order_value` | number ($) | Average dollar value per order over the 12 months before the period. |
| `noise_a` | number | An auxiliary field from the data export. |
| `noise_b` | number | An auxiliary field from the data export. |
| `days_to_pay` | number (days) | Week 10's target. Days from invoice to payment. Known only after payment, so it is not a predictor this week. |
| `defaulted` | 0 or 1 | **This week's target.** 1 if the account's receivable was written off as uncollectible during the period. 0 if it was not written off in the period, which this course calls "did not default". Known only at the end of the period, so it is a target, never a predictor. |

## Notes

- About 20% of the accounts defaulted (438 of 2,200). That share is the base rate. Real
  write-off rates on business receivables are usually much lower; this table runs high so
  there are enough defaults to study.
- In Lab 11 you choose the predictors. The list must include `prior_late_count` and
  `discount_rate`, and may add any of the other eight numeric columns from `credit_limit`
  through `noise_b` and `segment`.
- Six columns stay out of the lab: `days_to_pay` (known only after payment), `industry`
  (it repeats `segment`), `customer_id` (an identifier), `tenure_months` and `region`
  (out in Week 10 too, so everyone works from the same candidate list) and `defaulted`
  (the target). The notebook says why if you try one.
- A category column goes into a model as 0 or 1 dummy columns, with one level left out
  as the base case. Never feed it a 1, 2, 3 code. In pandas,
  `pd.get_dummies(..., drop_first=True, dtype=float)` builds the dummies.
- A column being allowed does not mean it helps the model. Deciding which ones belong,
  and saying why, is part of the lab.
