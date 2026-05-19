# About Me

## 1. Background and experiences

I came up through data engineering and analytics, mostly in fintech and government-tech-adjacent companies. Currently Senior Director of Data Science and Data Engineering at PayIt, reporting to the CFO. Fifteen years of professional experience, the last seven leading teams that build automation around finance functions — close processes, revenue-recognition reconciliation, customer-payment lifecycle reporting. Adjunct at the U of U Eccles School; this is the second time I'm teaching ACCTG 5150.

The persona for this profile is "industry data professional taking my own course" — I'm filling these out as I'd want a student to fill them out, which means writing about myself as if I were learning the material rather than teaching it.

## 2. Career picture (3-5 year horizon)

- **Target role / title:** Continuing in director-level data science / data engineering leadership; eventually moving toward VP of Data or CTO at a fintech with strong finance-team partnership. Possibly a founding role at the AI-tooling-meets-accounting-workflow intersection.
- **Target employer type:** Fintech, government-tech, or finance-automation startup at growth stage. 50-500 people, post-product-market-fit, with a CFO who treats the data team as a partner instead of a service desk.
- **Credentials you're working toward:** None. I'm not chasing CPA or CFA. My credentialing path is shipping things and writing about them.
- **Why this picture fits the role I picked in role_profile.md:** The "Other — industry data with finance adjacency" route is the role I already inhabit; the picture is about where I take that role next.
- **What I'm still figuring out:** Whether I stay on the build-and-lead track at increasing scale, or pivot to founding something narrow at the AI-plus-accounting intersection. The instructor work is partly an experiment in whether teaching that intersection is itself a leverage point.

## 3. Current technical skills

> *Persona note: this is the skill list of a working data professional with fifteen years of experience. It is NOT the bar for this course. Your version should be honest about what you've actually used — including "class only," "tried once for a project," and "never used." The structure (tool: depth — what I do with it) is what to model; the depth is mine, not yours.*

- **Excel / Google Sheets:** Pivot tables, INDEX/MATCH, SUMIFS, basic Power Query for data shaping. I rarely build complex models in Excel — I push them to Python or SQL once they outgrow a single sheet.
- **Python:** Daily user. pandas for analysis, FastAPI and Flask for services, SQLAlchemy for database work. I write production scripts, deploy to Kubernetes, review code from my team.
- **R:** Read-only. I can interpret R in research papers but I don't write it.
- **SQL:** Daily user. Window functions, CTEs, query optimization, both BigQuery and Snowflake dialects. I work upstream of dbt models more often than I write them.
- **Tableau:** Rarely use directly. My team builds dashboards in Looker; I review them.
- **Power BI:** Never used.
- **Other:** Snowflake, Databricks, BigQuery (daily); dbt, Airflow, Dagster (working knowledge); LLMs (Claude, Codex, Cursor, Gemini) — daily since December 2022.

## 4. How I learn and what makes concepts stick

I learn by reading the documentation first, then building the smallest version of the thing that produces a real result. I prefer technical depth over surface coverage — I'd rather understand one thing well enough to teach it than have shallow exposure to ten things. Concepts stick when I can re-derive them from first principles, not just recall them. Worked examples land harder than abstract explanations; analogies are useful for orientation, but I distrust them past the orientation phase.

## 5. What I want to learn this term

(Persona note: writing as if I were a student in my own course — these are things I'd want to sharpen by end of term, not things I already know.)

- **Goal 1:** Build a forecast workflow in Python that ingests a CSV of quarterly financials, runs a seasonal decomposition, and produces a one-page exec summary chart — without searching syntax. (Today: I write production Python but rarely use statsmodels, Prophet, or seasonal decomposition directly.)
- **Goal 2:** Articulate the trade-offs between different LLM context strategies for accounting-adjacent work in language a non-technical finance partner can follow. (Today: I can do the work, but my explanations to non-technical partners are still too jargon-loaded.)
- **Goal 3 (optional):** Read three SEC filings end to end and produce a written comparison of how each handles segment reporting. (Today: I read filings opportunistically but rarely structure the comparison in writing.)

## 6. Questions I would like answered

- *"How are auditors actually using AI in the field right now — what's adopted, what's resisted, and why?"*
- *"When does it make sense for a finance team to build custom LLM tooling vs use off-the-shelf platforms like Microsoft Copilot or KPMG's internal tools?"*
- *"What patterns do undergrads pick up first when learning to use LLMs for analysis, and which of those patterns generalize to professional work?"*
- *"How are firms structuring 'AI-assisted' grading, review, and audit workflows so the human stays accountable?"*

## 7. What I want this file to help with

When you upload this file to your LLM (ChatGPT, Claude, Gemini, NotebookLM), it reads instructions for HOW to help me. Use the table below.

| When I... | I want the LLM to... |
|---|---|
| Am stuck on a problem | Ask me one clarifying question before giving the answer |
| Get an error message | Help me debug step by step, not just give the fix |
| Don't understand a concept | Explain it with a fintech or finance-team example, not a generic one |
| Get a number or fact from the LLM | Show its work and tell me how to verify it against the source |
| Am tempted to copy-paste an answer | Make me explain my reasoning first |
| Am writing for a CFO or exec | Cut anything that doesn't earn its place; lead with the decision |
| Notice the LLM hedging | Push back — name the cases instead of softening into mush |

The LLM follows these instructions in every future session where I upload this file. I'll add rows over the term as I notice patterns I want the LLM to encourage or interrupt.

## 8. Validate it — interrogate your own work

Once Sections 1-7 are drafted, paste this file back to your LLM with the prompt below.

> *"Read the about-me profile above and ask me 5 questions about my skill claims, my career picture, my learning goals, the questions I'm carrying, and the entries in my behavior table. Focus on places where my answers are vague, generic, or might not match the role I picked in role_profile.md. End with one specific edit you'd recommend."*

Answer in your own voice. Iterate the file based on what surfaces. The point is to discover where the reasoning is thin — not to defend every choice.
