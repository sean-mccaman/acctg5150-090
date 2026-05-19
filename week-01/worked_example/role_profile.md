# Role Profile

## 1. Role overview

- [ ] Auditor (external audit, Big Four or regional firm)
- [ ] In-house accountant (corporate finance, controller, FP&A, internal audit)
- [ ] Tax specialist (public accounting tax practice, corporate tax)
- [ ] Government accountant (federal, state, local, GAO, IRS)
- [x] Other: **Industry data professional in fintech, with finance/CFO adjacency**

**What this role does and who it serves:** This role sits between accounting, data engineering, and product. The work is primarily building data infrastructure that finance teams rely on — reconciliation pipelines, automated reporting, predictive cash-flow models, AI-assisted close processes. The audience is the CFO and finance team (decision-makers), product engineering (build partners), and external auditors (during quarterly close). It's "Other" relative to the four canonical tracks because the deliverables aren't audit memos, tax returns, financial statements, or in-house controllership work — they're data systems and the analyses those systems produce. Accounting fluency matters because the consumers of the work are accountants and the constraints (GAAP timing, auditability, materiality) come from the accounting world.

## 2. Communication norms for this role

- **CFO-level updates:** one-page exec summaries; lead with the decision the data supports; charts only if a number alone won't carry the message
- **Cross-functional with engineering:** technical specs in markdown, architecture diagrams, SQL or Python excerpts; comments explain the why, code shows the how
- **Audit and external review:** documented data lineage; reproducible queries; assumptions called out
- **Internal data team:** runbooks for production pipelines; postmortems after incidents; office-hours-style Slack threads for ad-hoc questions
- **Common framing:** every artifact has a one-line "what decision this supports" framing at the top. If it can't justify that line, it gets cut.

## 3. What this role values

- **Traceability** — every number tied to a source query, a source file, or a documented assumption. No mystery numbers.
- **Reproducibility** — anyone on the team can re-run the analysis from the artifact alone, without my desk
- **Automation over heroics** — work that runs on a schedule beats work that requires a person at 11pm on quarter-end
- **Concise framing** — exec time is the scarcest resource; the work earns attention by being short and clear, not long and exhaustive
- **Honest uncertainty** — confidence intervals, assumption documentation, and "I don't know yet" are professional standards, not weaknesses
- **Code review as quality control** — analyses ship after another engineer has read the code, not after the analyst is satisfied

## 4. Visual and format identity for this role

- **Chart palette:** small (2-4 colors), one labeled as emphasis. Default to a darker primary (`#BE0000`) plus a contrast highlight for the "look here" series. Avoid rainbow palettes; gray-out the non-emphasis series.
- **Font for documents:** system default sans-serif (Helvetica or Arial). Code in Menlo or Consolas.
- **Font for slides:** same as documents. Slides aren't where personality lives in this role.
- **Hyperlink convention:** colored (`#BE0000`), underlined. Treat links as referenceable evidence, not decoration.
- **Document length conventions:** one-page exec summaries (CFO); 5-10 page technical specs (engineering); runbooks as long as they need to be (operations).

**Why these conventions fit:** the audience is reading on laptops and phones, often in low-attention moments between meetings. The work earns trust by being legible and professional, not by being designed.

## 5. How an LLM should respond when serving this role

- Default to SQL and Python examples for data manipulation. Pandas dialect for analysis; Snowflake or BigQuery dialect for warehouse work — specify which.
- Cite the source dataset, table, or filing for any claimed number. If you don't have a source, say so.
- Format comparisons as tables when there are 3+ options to weigh.
- Show your math when arithmetic is involved. I'll check it.
- When asked for an exec summary, lead with the one-sentence takeaway. Detail follows.
- If a question has a "depends on" answer, spell out the cases — don't hedge into mush.

## 6. Validate it — interrogate this role profile

Once Sections 1-5 are drafted, paste this file back to your LLM with the prompt below.

> *"Read the role profile above and ask me 5 questions about whether this profile coherently describes the role I picked. Focus on places where the role's communication norms, values, format identity, or LLM directives feel generic, contradictory, or copied from a different role. End with one specific edit you'd recommend."*

Iterate the file based on what surfaces. The point is to confirm the role is described tightly enough that an LLM responding under this profile would behave noticeably differently than an LLM responding under a different role's profile. If the answers feel interchangeable across roles, the file isn't doing its job yet.
