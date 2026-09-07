# Course Data: ACCTG 5150-090 (Summer 2026) and ACCTG 6155 (Fall 2026)

Public datasets, specs, and templates for **Accounting Analytics** at the
University of Utah, David Eccles School of Business. `2026-summer/` and the
top-level `week-NN/` folders belong to ACCTG 5150-090 (Summer 2026).
`2026-fall/` belongs to **ACCTG 6155** (Fall 2026, sections 001 and 002).

The data in this repository is **synthetic**. It contains no real or personally
identifiable information. It is public so that student lab scripts can read it
directly by URL — no download or upload step.

## Week 2 — Lab 2

`week-02/JEA Detail.txt` — a synthetic journal-entry detail export used in Lab 2.

Read it in pandas with its raw URL:

```python
import pandas as pd
url = "https://raw.githubusercontent.com/sean-mccaman/acctg5150-090/main/week-02/JEA%20Detail.txt"
df = pd.read_csv(url, sep="\t", encoding="utf-16", skiprows=9)
```

The file is UTF-16 encoded and tab-separated.

## Project 2 — Predicting Credit Default

`2026-summer/project-2/` — the consumer-lending credit-default dataset for Project 2.
29,881 account records, no personally identifiable information. See
[`ar_default_data_dictionary.md`](2026-summer/project-2/ar_default_data_dictionary.md)
for the full column reference.

- `ar_default_data.csv` — CSV, for pandas or Excel
- `ar_default.sqlite` — the same data as a SQLite database (table `accounts`)

Read it in pandas with its raw URL:

```python
import pandas as pd
url = "https://raw.githubusercontent.com/sean-mccaman/acctg5150-090/main/2026-summer/project-2/ar_default_data.csv"
df = pd.read_csv(url)
```
