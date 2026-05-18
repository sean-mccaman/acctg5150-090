# ACCTG 5150-090 — Course Data

Public datasets and assets for **ACCTG 5150-090 — Accounting Analytics**
(Summer 2026), University of Utah, David Eccles School of Business.

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
