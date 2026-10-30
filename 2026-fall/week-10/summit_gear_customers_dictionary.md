# Summit Gear customer accounts: data dictionary

`summit_gear_customers.csv` holds 2,200 business (B2B) customer accounts for Summit
Gear Co., a wholesale outdoor-equipment company. Each row is one account. The data is
synthetic teaching data, built to behave like a real receivables file.

This week you predict `days_to_pay`, how long an account takes to pay an invoice, from
the account's attributes. `defaulted` is Week 11's target. Ignore it this week.

## Columns

| Column | Type | Meaning |
|---|---|---|
| `customer_id` | text | Unique account ID. An identifier, not a predictor. |
| `region` | category | Sales region: Mountain North, Mountain Central, Desert Southwest. |
| `segment` | category | Account segment: Outdoor Retail, School District, Resort, Outfitter. |
| `industry` | category | Account industry (Retail, Hospitality, Education, and so on). |
| `tenure_months` | number (months) | Months the account has been active. |
| `credit_limit` | number ($) | The account's credit limit. |
| `avg_balance` | number ($) | Average outstanding balance. |
| `annual_spend` | number ($) | Total spend over the last 12 months. |
| `prior_late_count` | number (invoices) | Count of prior invoices the account paid late. |
| `days_since_last_order` | number (days) | Days since the account's most recent order. |
| `orders_per_year` | number (orders) | Orders the account places per year. |
| `discount_rate` | number (percent) | Average discount rate offered to the account. 3.5 means 3.5 percent. |
| `avg_order_value` | number ($) | Average dollar value per order. |
| `noise_a` | number | An auxiliary field from the data export. |
| `noise_b` | number | An auxiliary field from the data export. |
| `days_to_pay` | number (days) | **This week's target.** Days from invoice to payment. |
| `defaulted` | 0 or 1 | Week 11's target. Ignore it this week. |

## Notes

- The target is `days_to_pay`. The Lab 10 notebook starts from ten numeric candidate
  predictors: `credit_limit` through `noise_b` in the table above.
- `tenure_months` and the three category columns stay out of the lab, so everyone's
  first fit is the same model.
- Using a category column in a regression is optional this week. If you do, encode it
  as 0 or 1 dummy columns and leave one level out as the base case. Never feed it a
  1, 2, 3 code.
- Not every numeric column earns its place in the model. Deciding which ones do is part
  of the lab.
- `summit_gear_customers_with_ols.xlsx` is the same 2,200 rows in Excel, with two
  regressions already run in the Analysis ToolPak. The "Reduced Column OLS" tab is one
  pruned model: one size column plus the four payment-behavior columns. The "All Column
  OLS" tab also includes `tenure_months`, so its numbers will not match your Exercise 1
  fit exactly. It is optional, for reading a regression in Excel.
