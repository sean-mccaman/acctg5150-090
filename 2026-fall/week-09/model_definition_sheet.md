# Model definition sheet

Fill this in before anyone builds the model. Each cell should be something a reviewer can check, such as a number, a table and column, a date, or a role. A line or two per cell is usually enough, and the sheet is usually three to five pages filled in.

Homework 9 uses this sheet for Summit Gear's allowance for doubtful accounts, so the three users below are already named. On another model, replace them with that model's users.

## 1. The question, and the decision it informs

*One sentence each. The decision names who acts on the number and what they do with it.*

<!-- table: widths=30,70 boldfirst -->
| Item | Your answer |
|---|---|
| Model name | |
| The question the model answers | |
| The decision it informs | |

## 2. Users

*One row per user. The form of the number is, for example, one booked amount, a list of accounts, or a documented calculation someone else can test. The tolerance is a number. The case gives you the audit senior's $25,000 investigation threshold, which the auditor sets independently. Propose the Controller's and the credit manager's tolerances yourself, label each one as a proposal, and say what it measures, because a dollar tolerance, a share of missed loss dollars, and an investigation threshold are not always the same measure. Do not present a proposal as a fact from the data.*

<!-- table: widths=14,22,18,18,28 boldfirst -->
| User | What they need from the model | Form of the number | How wrong is acceptable (a number) | Which direction of error hurts more, and what it costs |
|---|---|---|---|---|
| Controller | | | | |
| Credit manager | | | | |
| Audit senior | | | | |

## 3. Method

*Name each input and how it enters the number, for example open dollars by aging bucket times a loss rate, plus a current-conditions adjustment.*

<!-- table: widths=35,65 -->
| Input | How it enters the calculation |
|---|---|
| | |
| | |
| | |
| | |
| **The calculation, in one line** | |

## 4. Data and reliability

*Every input from field 3 gets a row. A check is something you can run and get a yes or a no, such as a tie to the general ledger, a row count, or a control total. If no table holds an input yet, name the source and the control you propose, and label the row Proposed.*

<!-- table: widths=22,18,20,40 -->
| Input | Table | Column(s) | How completeness and accuracy are checked |
|---|---|---|---|
| | | | |
| | | | |
| | | | |
| | | | |

## 5. Assumptions

*Each assumption gets its source, such as a policy, a memo, a standard, or a test you ran on the data. The write-off policy, the lookback window, and how customers are pooled are all assumptions.*

<!-- table: widths=55,45 -->
| Assumption | Source |
|---|---|
| | |
| | |
| | |
| | |

## 6. Validation

*How you will know the number is right before anyone books it. Include a back-test against a dated snapshot and a recompute.*

<!-- table: widths=45,25,30 -->
| Check | Date or snapshot it uses | What counts as passing |
|---|---|---|
| | | |
| | | |
| | | |

## 7. Decision rule and refresh

*The trigger is a number management sets for its own review. It is not the auditor's threshold, which the auditor sets independently. The owner is a role that can act, not "the team".*

<!-- table: widths=35,65 boldfirst -->
| Item | Your answer |
|---|---|
| Management's review trigger: the result moves by more than | |
| Who is told, and by when | |
| What happens next | |
| How often it runs | |
| Who owns it | |

## 8. Not modeled, and why

*At least one specific item, with the reason it is left out.*

<!-- table: widths=30,40,30 -->
| Item left out | Why it is left out | What would bring it in |
|---|---|---|
| | | |
| | | |

## 9. AI use

*What an AI produced and how you checked it. If you used none, say so in one row.*

<!-- table: widths=40,20,40 -->
| What an AI produced | Tool | How you checked it |
|---|---|---|
| | | |
| | | |

## 10. Prepared by, reviewed by, date, version

*Prepared by is you. Reviewed by is the role that signs off.*

<!-- table: widths=30,30,20,20 -->
| Prepared by | Reviewed by | Date | Version |
|---|---|---|---|
| | | | |

## Before you hand it over

Homework 9 grades the sheet on these seven checks. Each is a yes or a no, and a check that covers several rows passes only when every row meets it. A check passes only when the statement is specific and technically consistent with the model and the accounting requirements.

1. Each user's "how wrong is acceptable" is a number, in dollars or percent. A clearly labeled proposal counts.
2. Each user's row names which direction of error hurts more, too high or too low, and what that direction costs them.
3. Every input in the method names the table and the column it comes from, or a proposed source and control, clearly labeled as proposed.
4. Every data source has a concrete check of its completeness or accuracy, such as a tie to the general ledger, a row count, or a control total.
5. The validation plan includes a back-test against a dated snapshot.
6. The decision rule states the number that triggers it and names who owns it.
7. At least one item is listed as not modeled, with the reason it is left out.
