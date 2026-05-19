# Lab 01 Spec

This submission delivers the three Lab 1 profile files (`lab01_spec.md`, `role_profile.md`, `about_me.md`) for the "Other" accounting route — specifically, an industry data professional in fintech with finance/CFO adjacency.

## File manifest

- [x] lab01_spec.md
- [x] role_profile.md
- [x] about_me.md

(All files are Markdown, `.md` extension, plain text.)

## Build Requirements

The three files together form a profile that future LLM sessions can use as standing context. Each does a different job:

- `role_profile.md` describes the **role construct** I'm tracking toward — communication norms, values, format identity, and LLM behavior directives. It's intentionally swappable. In later weeks I expect to compare this profile against alternate role profiles and watch how the same prompt produces different output.
- `about_me.md` describes **me as a student** — background, career picture, current skills, learning goals, the questions I'm carrying, and the behavior table that shapes how the LLM tutors me.
- `lab01_spec.md` is this file: the spec-doc pattern that captures what I committed to deliver and how I'd grade it.

For the "Other" route specifically, my customization shows up in `role_profile.md` Section 1 (one sentence explaining why this work doesn't fit the four canonical tracks) and in `role_profile.md` Section 5 (LLM directives specific to a data-engineering-meets-finance context — SQL/Python defaults, source-dataset citation, table-formatted comparisons).

## Review/Acceptance Criteria

A reviewer (or an LLM running a check) should confirm:

- All three files exist with the correct filenames, are valid Markdown, and contain every section the templates specify
- `role_profile.md` is role-construct only — no personal student content has bled in
- `about_me.md` Section 2 (career picture) includes the one-sentence link to the role in `role_profile.md` Section 1
- `about_me.md` Section 5 (learning goals) references the current skills in Section 3, so the gap between today and end-of-term is visible
- `about_me.md` Section 7 (behavior table) has at least 5 rows and is specific enough to actually shape LLM responses
- Both forcing-function sections (`role_profile.md` Section 6 and `about_me.md` Section 8) are populated with the prompt block and iteration instruction
- Tone is consistent across files: no emojis, no exclamation marks, em dashes used sparingly, contractions OK, neutral formality

## How I would grade this submission

| Criterion | Pts |
|---|---:|
| Specificity in `role_profile.md` (concrete role conventions, not generic ones) | 25 |
| Specificity in `about_me.md` current skills and learning goals (visible today-to-goal gap) | 25 |
| Career picture in `about_me.md` Section 2 is concrete enough to grade alignment against later | 15 |
| Behavior table in `about_me.md` Section 7 is usable, not aspirational | 15 |
| Forcing-function sections completed (`role_profile.md` §6, `about_me.md` §8) | 10 |
| Markdown formatting and proofread | 10 |
| **Total** | **100** |

Math: 25 + 25 + 15 + 15 + 10 + 10 = 100.

## Self-Assessment

### Submission Gate Checklist

- [x] **SG-01 File Availability [OK]:** All three files (`lab01_spec.md`, `role_profile.md`, `about_me.md`) are created and saved in the submission folder.
  - Evidence: Folder listing shows three `.md` files at the expected names; total size ~12 KB.
- [x] **SG-02 Managing-Up Coverage [OK]:** I evaluated this submission against `Example_Managing_Up_Doc.md`. The "lead with the point," "consistent terms," "make logic traceable," and "match format to deliverable type" principles are visible across all three files.
  - Evidence: Each file's intro states the file's purpose in one sentence; "role_profile" and "about_me" are used consistently as terms; the rubric in this file shows traceable point math; per-file format conventions match the role's expectations.
- [x] **SG-03 File Extension Validation [OK]:** All three submissions are `.md` and render cleanly in a Markdown preview.
  - Evidence: Tested in VS Code preview; tables, code blocks, headings, and the behavior table render correctly.
- [x] **SG-04 File Completion [OK]:** Every required section is filled, including the forcing-function sections.
  - Evidence: `role_profile.md` Sections 1-6 populated; `about_me.md` Sections 1-8 populated; no `[Write here]` placeholders remain in either file.
- [x] **SG-05 Grade Estimate [OK]:** I rated this submission against the rubric above. Self-estimate: 100/100.
  - Evidence: Each rubric criterion is satisfied with concrete content — role_profile is role-construct only (no personal bleed); about_me Section 5 references Section 3 with parenthetical "Today:" gaps; the behavior table has 7 specific rows including the verification row; both forcing-function sections are populated. The behavior table will get more rows as I use the file in HW1; that's iteration, not a gap against the rubric.

**Blocking Issues:** None.

**Final Gate Decision:**
- [x] Ready to submit
- [ ] Not ready - fixes required
