# Role Profile

`This file describes a role construct, not a person. You build one in Lab 1 for the accounting route you're tracking toward — but the file itself is meant to be swappable. Future weeks will provide alternate role_profile files (auditor, tax specialist, in-house, government) so you can swap them in and watch how the same prompt produces different LLM output. The point of this file is to demonstrate that role context shifts everything.`

`Six sections total. Sections 1-5 describe the role; Section 6 is the validate-it forcing function. Aim for 1-2 pages when rendered.`

---

## 1. Role overview

`Pick one route, then write 2-3 sentences describing what this role does and who it serves. Stay role-construct focused — your personal reasons for picking it belong in about_me.md Section 2 (Career picture).`

- [ ] Auditor (external audit, Big Four or regional firm)
- [ ] In-house accountant (corporate finance, controller, FP&A, internal audit)
- [ ] Tax specialist (public accounting tax practice, corporate tax)
- [ ] Government accountant (federal, state, local, GAO, IRS)
- [ ] Other: ____________

**What this role does and who it serves:**

[Write 2-3 sentences here.]

---

## 2. Communication norms for this role

`What does day-to-day written and spoken communication look like for someone in this role? Who are the typical audiences (audit partner? CFO? client engagement letter recipient? IRS examiner?)? What document types and format conventions matter (work-paper format vs FP&A deck vs tax memo vs audit findings letter)?`

`Not sure? Ask your LLM: "What does day-to-day communication look like for a [your chosen role]? Give me 5 specific document types this person produces in a week and who the audience is for each."`

[Write 4-8 sentences or bullets.]

---

## 3. What this role values

`The work standards and quality bar this role is held to. Different from generic "be clear" — these are role-specific. Examples: an auditor values traceability of every number to a source document. A tax specialist values precision in citation of code sections. An FP&A analyst values fast, decision-ready summaries. List 4-6 things this role specifically values, in this role's language.`

-
-
-
-

---

## 4. Visual and format identity for this role

`What deliverables look like in this role. In most professional contexts the employer dictates this (Big Four firms have strict branding, SEC filings have presentation conventions, government has GAO style guides). Capture what the conventions are.`

- **Chart palette** (typical colors, what carries emphasis):
- **Font for documents:**
- **Font for slides** (often the same):
- **Hyperlink convention** (underlined, colored, both, none):
- **Document length conventions** (1-page memos, 30-page work papers, etc.):

**One sentence on why these conventions fit this role:**

[Write here.]

---

## 5. How an LLM should respond when serving this role

`Concrete directives you'd give an LLM that's been told "respond as if you're supporting an auditor / tax specialist / FP&A analyst." Aim for 4-6 directives. These are role-specific — they should differ noticeably from what an LLM would default to without role context.`

`Examples for an auditor: "Always cite the GAAP source." "Format outputs as work-paper-style tables." "Treat all numbers as if they may end up in a 10-K."`

`Examples for FP&A: "Default to month-over-month and year-over-year comparisons." "Round to nearest thousand for slides; full precision for the model." "Lead with the trend, then the drivers."`

-
-
-
-

---

## 6. Validate it — interrogate this role profile

`Once Sections 1-5 are drafted, paste this file back to your LLM with the prompt below.`

> *"Read the role profile above and ask me 5 questions about whether this profile coherently describes the role I picked. Focus on places where the role's communication norms, values, format identity, or LLM directives feel generic, contradictory, or copied from a different role. End with one specific edit you'd recommend."*

`Iterate the file based on what surfaces. The point is to confirm the role is described tightly enough that an LLM responding under this profile would behave noticeably differently than an LLM responding under a different role's profile. If the answers feel interchangeable across roles, the file isn't doing its job yet.`
