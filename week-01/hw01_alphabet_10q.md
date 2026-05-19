> **STATUS: archived reference doc.** The live source of truth for HW1 is now the Canvas quiz at <https://utah.instructure.com/courses/1284436/quizzes/4669761>. This file predates the quiz format and reflects an earlier Markdown-file-submission design. Compared to the live quiz: the cohort probe section has been deleted, sections renumbered (Pass 1 / Pass 2 / Reflection = 35 / 35 / 30 = 100), and Pass 2 now requires only `role_profile.md` + `about_me.md` (not `educational_success_criteria.md`). Use this file for design rationale and decisions; use the live quiz for what students actually see.

# HW1 — Alphabet Q1 2026 10-Q Investigation

**Course**: ACCTG 5150-090 — Accounting Analytics, Summer 2026
**Module**: Week 1 (Module ID 4391856)
**Group**: Homework
**Points**: 100
**Due**: Sunday, May 17, 11:59 PM Mountain Time
**Time estimate**: 60-90 minutes (real hands-on with two LLM sessions)
**Format**: Markdown file upload (`hw01_alphabet_10q.md`)
**Prerequisite**: Complete Lab 1 first. This homework references your Lab 1 profile documents.

---

## Assignment description (student-facing)

### What this is

A two-pass investigation of Alphabet's most recent quarterly filing
using your LLM. **Pass 1**: no profile context, no source document.
**Pass 2**: full profile context (your Lab 1 documents) plus the actual
10-Q as source material. Same four questions in both passes.

You will see, in your own work, what changes when you give an LLM real
context. This is the felt experience of the course's stated goal:
analytics has shifted from tool fluency to context engineering. You
cannot read about that; you have to do it.

### The source document

**Alphabet, Inc. Quarterly Report on Form 10-Q for the quarter ended
March 31, 2026** (Q1 calendar 2026).

- Alphabet investor relations: <https://abc.xyz/investor/>
- The direct SEC EDGAR link is in the Canvas module.
- This filing covers Alphabet's first calendar quarter of 2026.
  Revenue, segment mix (Google Services / Google Cloud / Other Bets),
  AI infrastructure capex commentary, and forward-looking statements
  are all substantive.
- Most current LLMs do not have this filing in their training data.
  That is the point: Pass 1 forces the model to either admit it does
  not know or to hallucinate. Either outcome is diagnostic.

### How to run the two passes

**Pass 1** — fresh LLM session, no uploads:

1. Open a new conversation with your chosen LLM.
2. Do NOT upload any documents from Lab 1.
3. Do NOT upload the 10-Q.
4. Ask each of the four questions in Section 2 below.
5. Capture verbatim: your prompt, the LLM's response, and your
   verification against the actual 10-Q (which you can read in your
   browser at <https://abc.xyz/investor/> or via the SEC EDGAR link).

**Between passes** — download the 10-Q PDF from Alphabet's investor
relations page or SEC EDGAR. Save it locally so you can upload it in
Pass 2.

**Pass 2** — fresh LLM session, full context uploaded:

1. Open a NEW conversation with the same LLM.
2. Upload (or paste) your `role_profile.md` and `about_me.md` from Lab 1.
   Do NOT upload `educational_success_criteria.md` — that file is for
   personal study sessions (NotebookLM, dedicated learning chats), not
   assignment sessions; it doesn't help the LLM analyze the 10-Q.
3. Upload the Alphabet Q1 2026 10-Q PDF.
4. Ask the LLM to use these documents as standing context.
5. Ask the same four questions. Same verbatim capture.

If your LLM tool does not accept file uploads, paste the contents
inline. Note in your submission which approach you used.

### Required submission structure

Submit one Markdown file named **`hw01_alphabet_10q.md`** with these
four sections in this order:

```md
# HW1 — Alphabet Q1 2026 10-Q Investigation
**Your name** | **Date completed**

## 1. Quick cohort probe

- Primary spreadsheet I use most: [Excel / Sheets / Both / Neither]
- Operating system: [Windows / Mac / Linux / ChromeOS]
- Have you read a 10-Q or 10-K before this course? [Yes / No / A long time ago]
- AI tool used for this homework: [ChatGPT / Claude / Gemini / Copilot / Cursor / Other:____]
- Does your AI tool accept file uploads? [Yes / No / Not sure]

## 2. Pass 1 — No profile, no source document

I asked these questions to a fresh LLM session with NO uploaded
documents (no Lab 1 profile, no 10-Q).

### Q1. Total revenue
**Prompt:** [paste verbatim]
**LLM response:** [paste verbatim, or summarize if very long with a note]
**Verification against the actual 10-Q:** [matched / partial / missed; what you found]

### Q2. Segment operating income (Google Services, Google Cloud, Other Bets)
**Prompt:**
**LLM response:**
**Verification:**

### Q3. Cash from operations vs net income for the quarter
**Prompt:**
**LLM response:**
**Verification:**

### Q4. MD&A summary (3-5 bullet points)
**Prompt:**
**LLM response:**
**Verification:**

## 3. Pass 2 — Profile context + source document

I downloaded the 10-Q PDF, opened a NEW LLM session, and provided my
Lab 1 profile documents (`role_profile.md` and `about_me.md`) PLUS the
10-Q PDF as context. (`educational_success_criteria.md` is for personal
study sessions, not assignment sessions, so I did NOT upload it for HW1.)

(Note: if my AI tool does not accept PDF uploads, I pasted the
relevant sections inline and noted that here.)

### Q1. Total revenue
**Prompt:**
**LLM response:**
**Verification:**

### Q2. Segment operating income
**Prompt:**
**LLM response:**
**Verification:**

### Q3. Cash from operations vs net income
**Prompt:**
**LLM response:**
**Verification:**

### Q4. MD&A summary
**Prompt:**
**LLM response:**
**Verification:**

## 4. Reflection

1. **Biggest difference between Pass 1 and Pass 2.** Which question
   showed the largest shift? Quote a relevant phrase from each pass.
2. **Was the role-anchored output more useful for your chosen role?**
   Yes or no, and why. Either answer is valid; specificity matters.
3. **What would you change in `role_profile.md` or `about_me.md`** based
   on what you saw in Pass 2? Suggest one specific edit.
4. **Of your three content-bearing Lab 1 artifacts, which do you expect
   to revise during the term, and why?** `educational_success_criteria.md`
   is designed for ongoing revision; the question is whether
   `role_profile.md` or `about_me.md` surprised you in Pass 2 in a way
   that makes you want to update them too.
5. **Best prompts.** Paste 4-8 verbatim prompts from this homework
   that produced your best results, with one sentence each on why
   they worked.
```

### Grading (100 pts)

| Section | Points | Criteria |
|---|---:|---|
| 1. Cohort probe | 10 | All five fields answered honestly. |
| 2. Pass 1 (no context) | 35 | All four questions: prompt + LLM response + verification documented. Verification reflects an honest read of the 10-Q. |
| 3. Pass 2 (with context) | 35 | Same four questions repeated with profile + source. Documentation as honest and specific as Pass 1. |
| 4. Reflection | 20 | All five items answered with specificity, including verbatim prompts. Generic reflection without prompt examples earns partial credit. |

---

## Build notes for the instructor

- **Submission**: Canvas file upload assignment; accept `.md` extension
  only. Reject other formats with a brief feedback note.
- **Auto-grade**: completion-based with rubric check on the submitted
  file structure. AI-assisted grading per the syllabus AI-Grading
  Disclosure may be used for the reflection section.
- **Visibility**: ungraded individual responses; aggregate Section 1
  (cohort probe) and share back in Week 2. **Do NOT share aggregated
  Sections 2-4** — those are personal reflections and prompt captures.
- **Canvas description**: include both the Alphabet investor relations
  URL (`https://abc.xyz/investor/`) and the direct SEC EDGAR link for
  the Q1 2026 10-Q. Suggested CTA: *"Complete Lab 1 first. Read this
  assignment in full before starting. Estimated 60-90 minutes
  hands-on."*

## Decisions made (flag if any are wrong)

1. **Single Markdown file submission**, not a Canvas New Quiz with
   twelve essay fields. Markdown matches the Lab 1 deliverable pattern,
   gives the student a reusable artifact, and is easier to audit at
   scale than scattered quiz responses.
2. **Source: Alphabet Q1 2026 10-Q (calendar Q1, quarter ended
   March 31, 2026, filed late April 2026).** Recent filing outside the
   training cutoff for most major LLMs as of course launch. Alphabet
   is a household-name tech company with a distinctive accounting
   profile (segment reporting, deferred revenue, stock-based
   compensation, AI infrastructure capex) — pedagogically richer than
   a retailer for this cohort.
3. **Four questions per pass, eight LLM interactions total.** Enough
   data points for a meaningful comparison without overwhelming the
   homework. The questions span revenue (income statement), segment
   reporting, cash flow vs accrual (cash flow statement), and MD&A
   (narrative).
4. **Pass 1 = no profile, no source.** The "naive LLM" baseline. Most
   students will see hallucinations or confidently wrong answers.
   That is the point — feeling what bad context produces.
5. **Pass 2 = profile + source.** Maximum context. Students should see
   the difference dramatically. The reflection's job is to tease apart
   which part of the context contributed what.
6. **Reflection includes the "which artifacts will you revise" SRL
   question** (per the educational best-practices subagent finding).
   Surfaces students' early intuitions about why the three Lab 1
   artifacts are separate files and gives them ownership of the
   revisability heuristic.
7. **Cohort probe stays minimal (5 items).** Enough for pacing data.
   The thicker tools/skills diagnostic was retired when `about_me.md`
   Section 2 absorbed concrete technical skills as a Lab 1 deliverable.
8. **Pass 1 deliberately runs before students download the 10-Q.**
   This is a pedagogical choice. Many students would otherwise default
   to uploading the document in both passes. Forcing the document-less
   Pass 1 makes the value of source context dramatic and undeniable.
