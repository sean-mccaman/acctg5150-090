# Model definition sheet: a filled example

> This is a filled example on a different estimate at a different company. Use it to judge how much detail each field needs, then supply Summit Gear's own assumptions and sources. Your sheet is about Summit Gear's allowance for doubtful accounts, so these rows will not carry over.

Kettle Pass Apparel Co. is fictional. It is a small distributor that sells outdoor apparel (shells, base layers, fleece) to about 140 independent outdoor retailers in the Mountain West. It carries about 2,400 SKUs, one for each style, color and size, at average cost, about $6.2 million in total. Its fiscal year ends January 31, and its bank line of credit is secured by its inventory.

## 1. The question, and the decision it informs

<!-- table: widths=30,70 boldfirst -->
| Item | Answer |
|---|---|
| Model name | Kettle Pass reserve for excess and obsolete inventory |
| The question the model answers | How much of the cost of the inventory on hand at month-end will Kettle Pass not recover when the goods are sold or liquidated? |
| The decision it informs | The Controller books the reserve at each month-end close (debit cost of goods sold, credit the inventory reserve), and the merchandising manager decides which SKUs to mark down or send to the liquidator. |

## 2. Users

<!-- table: widths=14,22,18,18,28 boldfirst -->
| User | What they need from the model | Form of the number | How wrong is acceptable (a number) | Which direction of error hurts more, and what it costs |
|---|---|---|---|---|
| Controller | A supportable reserve to book at each month-end close | One booked amount each month-end | A supportable lower-of-cost-and-NRV estimate, with any difference above $20,000 from the independently reviewed calculation investigated before booking | Too low hurts more. Inventory and gross margin are overstated, and a year-end audit adjustment means re-sending the compliance certificate to the bank. Too high understates margin by the excess, which costs a conversation with the owners but no re-sent filing. |
| Merchandising manager | Which SKUs to mark down, bundle, or send to the liquidator this month | A list of SKUs, ranked by reserve dollars | Proposed, pending the merchandising manager's sign-off: at most 10 percent of the listed cost sells at full price within the next 90 days | Too high hurts more. A SKU listed by mistake gets a 30 percent markdown on goods that would have sold at full price. A missed SKU (too low) waits a month and loses about 2 points of liquidation value. |
| Bank collateral analyst | Eligible inventory net of the reserve, for the monthly borrowing base certificate | One net inventory figure each month, with the reserve on its own line | Within 2 percent of eligible inventory, about $110,000 | Too high on net eligible inventory (too low on the reserve) hurts more. It overstates borrowing capacity, and a field exam that finds it can cut the inventory advance rate from 50 to 40 percent, about $550,000 less available credit. Too low on net inventory (too high on the reserve) costs 50 cents of available credit for each dollar of excess reserve. |

## 3. Method

<!-- table: widths=35,65 -->
| Input | How it enters the calculation |
|---|---|
| Units on hand and average unit cost, by SKU | Extended cost is units on hand times average unit cost. |
| Average units sold per month | Net units sold in the trailing 6 months, divided by the months the SKU was available for sale in that window, counted from its first available date, with a partial month counted as a full month and the result capped at 6. |
| Months of supply and supply band | Units on hand divided by average units sold per month. The bands are under 6 months; 6 to under 12; 12 through 24; over 24; and no positive sales, which takes any SKU whose trailing net units sold are zero or negative, before any division. |
| Season code | Current, one season old, or two or more seasons old. With the supply band, it places the SKU in one of 15 grid cells. |
| Recovery rate by grid cell | Net proceeds over cost relieved for every unit that left inventory in the last 8 quarters from a SKU that sat in that cell at the prior month-end, with full-price, markdown and liquidation sales all included. The reserve rate is 1 minus the recovery rate, floored at 0. |
| Vendor status (current-conditions adjustment) | A SKU whose vendor has discontinued the style moves to the no-positive-sales band, whatever its months of supply. |
| **The calculation, in one line** | Reserve = the sum over SKUs of extended cost times the reserve rate for the SKU's grid cell. |

## 4. Data and reliability

<!-- table: widths=20,18,22,40 -->
| Input | Table | Column(s) | How completeness and accuracy are checked |
|---|---|---|---|
| Units on hand, average cost | `inventory_snapshot` | `sku`, `snapshot_date`, `qty_on_hand`, `avg_unit_cost` | The sum of `qty_on_hand` times `avg_unit_cost` ties to account 1400 Inventory in `gl_balances` at the same date, to the dollar. The SKU count matches the warehouse system's on-hand report. |
| Units sold; recoveries on full-price and markdown sales | `sales_lines` | `sku`, `ship_date`, `qty`, `net_amount`, `cost_relieved` | The monthly sums of `net_amount` and `cost_relieved` tie to accounts 4000 Sales and 5000 Cost of goods sold in `gl_balances`. Returns (negative `qty`) are kept, not dropped. |
| Season code, vendor status, first available date | `sku_master` | `sku`, `season_code`, `vendor_status`, `first_available_date` | An anti-join from `inventory_snapshot` returns no SKU missing from `sku_master`. Separately, grouping `sku_master` by `sku` returns exactly one row per SKU. The join keeps the snapshot's row count and extended-cost total. |
| Recoveries on liquidation | `liquidation_sales` | `sku`, `sale_date`, `qty`, `net_proceeds`, `cost_relieved` | The quarterly sum of `net_proceeds` ties to account 4050 Liquidation sales. Ten sales a quarter are recomputed from the liquidator's settlement statements. |
| The grid cell each sale came from | Proposed: `sku_class_history`, a dated record per SKU and month-end (no such table exists today; the Controller approves building it) | `snapshot_date`, `sku`, `supply_band`, `season_age_band`, `vendor_status_as_of`, matched on `sku` and the latest month-end strictly before the sale | Each included sale has one documented historical classification; today's `sku_master` attributes are never used for an old sale. Sales with no prior month-end (a SKU first stocked and sold in the same month) are reported separately and left out of the rates until their classification is supported. Counts, units, proceeds and cost reconcile before and after assignment. |

## 5. Assumptions

<!-- table: widths=55,45 -->
| Assumption | Source |
|---|---|
| Each grid cell's recovery history applies to the SKUs in that cell now. In the no-positive-sales band, 94 percent of SKUs over the last 8 quarters ended up liquidated and 6 percent sold at markdown, and both outcomes are in that band's rate. | Merchandising policy memo, March 2026, and the 8-quarter history in `sales_lines` and `liquidation_sales` |
| Recovery rates from the last 8 quarters hold for the current quarter. | The liquidator contract renewed in August 2025 on the same fee schedule. The back-test and the NRV check in field 6 test it. |
| SKUs are pooled by supply band and season code, not by vendor. | Pooling by vendor leaves most cells with fewer than 20 SKUs, which is too few for a stable rate. |
| `net_proceeds` is after the liquidator's 15 percent fee and freight, so no separate cost to sell is added for liquidated units. | Liquidator contract, schedule B, and three settlement statements traced to `liquidation_sales` |
| Inventory is carried at the lower of cost and net realizable value. | ASC 330-10-35-1B |

## 6. Validation

<!-- table: widths=45,25,30 -->
| Check | Date or snapshot it uses | What counts as passing |
|---|---|---|
| Back-test: rebuild the estimate from the inputs available on July 31, 2025. Track the units and cost held that day apart from later purchases (first in, first out within each SKU, for this test only), and compare the reserve with the cost those units did not recover through July 31, 2026. Units still on hand get their own NRV assessment and are reported as unresolved. The test needs a proposed inventory-movement extract (receipt, sale and return dates, quantities and costs), reconciled to the opening cohort before any outcome is used. | Snapshot 2025-07-31, outcomes through 2026-07-31 | The unrecovered cost on resolved units, plus the assessed shortfall on unresolved units, is between 85 and 115 percent of the modeled reserve, and the unresolved units are disclosed in the close memo. |
| NRV check: at each month-end, compare each pool's historical recovery rate with current expected selling prices and the liquidator's current quotes, less reasonably predictable disposal and transportation costs, expressed as a percent of the pool's cost so the two rates compare. | Each month-end, starting 2026-08-31 | The Controller documents the support for each pool's recovery rate before booking. A pool whose current evidence supports a different rate is revised; the review trigger decides which differences get a second look, and it never makes an unsupported rate acceptable. |
| Recompute 10 SKUs by hand from the source tables: the 5 largest reserves and 5 picked at random. | Each month-end run, starting 2026-08-31 | All 10 match the model to the dollar. |
| Control total: the model's extended cost equals account 1400. | Each month-end run | A difference of zero. |

## 7. Decision rule and refresh

<!-- table: widths=35,65 boldfirst -->
| Item | Answer |
|---|---|
| Management's review trigger: the result moves by more than | $40,000 from the prior month-end, or 10 percent, whichever is smaller |
| Who is told, and by when | The Controller and the merchandising manager, by business day 4 of close |
| What happens next | The Controller reviews the 20 SKUs that moved most before booking, and the close memo to the owners and the bank explains the move. |
| How often it runs | Every month-end, on business day 3 of close |
| Who owns it | The Controller. The senior accountant runs it and prepares the review. |

## 8. Not modeled, and why

<!-- table: widths=30,40,30 -->
| Item left out | Why it is left out | What would bring it in |
|---|---|---|
| Customer returns of seasonal goods after the season | Returns run under 1 percent of cost a year ($18,000 in fiscal 2025) and go back into stock at full value. | Returns above 3 percent of a season's shipments |
| Buy-back credits from three vendors | Credits are negotiated SKU by SKU and are not known until the vendor agrees, so they are booked when received. | A signed buy-back agreement with a stated rate |
| Weather and competitor pricing | Eight quarters hold only two winters, so the history cannot measure a weather effect, and no table records competitor prices. The Controller checks both against current selling-price evidence each month and records any remaining limitation in the close memo before relying on the reserve. | Current selling prices that the model's recovery rates no longer support, from either cause. |

## 9. AI use

<!-- table: widths=40,20,40 -->
| What an AI produced | Tool | How it was checked |
|---|---|---|
| The first draft of the SQL that computes months of supply | Claude | Recomputed 5 SKUs by hand in Excel. It divided by 6 months even for SKUs launched 2 months ago, so it now divides by the months available for sale, from `sku_master.first_available_date`. |
| A list of possible current-conditions adjustments | Claude | Kept vendor status, which the data supports. Assessed weather and competitor pricing for relevance, and field 8 records the result and what would bring them in. |

## 10. Prepared by, reviewed by, date, version

<!-- table: widths=30,30,20,20 -->
| Prepared by | Reviewed by | Date | Version |
|---|---|---|---|
| Senior accountant | Controller | 2026-08-14 | 1.3 |
