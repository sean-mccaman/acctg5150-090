# Lab 02 Spec, Data Cleaning

`In your own words, what is the goal of this lab? If it is not jumping out at you, run the Lab 2 page through an LLM and ask for a short summary.`

`Save your work. Make your own copy of this template before you start, and save it somewhere you control rather than only in a browser tab. You will upload the finished document to the Lab 2 quiz and also hand its text to the AI, so keep it where you can get to it. Delete each backtick guidance line once you have read it.`

## File manifest

`The files your Lab 2 work produces. The four marked "upload" go to the Lab 2 quiz. The two CSVs are written by your script and are what you use to check it.`

- [ ] lab_02_spec.md, this specification *(upload)*
- [ ] Part 1 workbook, `.xlsx`, your by-hand cleaned workbook *(upload)*
- [ ] lab_02_analysis.py or lab_02_analysis.ipynb, the script the AI builds from this spec *(upload)*
- [ ] lab_02_explainer.html, the Part 3 explainer *(upload)*
- [ ] lab_02_cleaned.csv, the cleaned dataset, written by the script
- [ ] lab_02_user_counts.csv, the per-user count, written by the script

Name each uploaded file so it starts with your university ID, like
`u1234567_lab_02_spec.md`. <!-- ferpa-ok: not a real uID, it is the placeholder in the student-facing file-naming example -->

## Build Requirements

`The precise instructions an AI will follow to clean the file. Write the four parts below. Be specific, and avoid vague verbs like "clean it up" or "fix the data". This is the part of the specification graded on precision.`

### Input

`What the file is, where it is, and what is wrong with it. State the encoding you found in Part 1. Name the ten columns. List the defects: the report header, the two-line column header, the page-break rows, the quoted and spaced Amount values, and the non-printing character in the ID column.`

### Operations

`The cleaning and analysis steps, in order. Do not write this from memory. Describe to an LLM, in plain words, every step you took by hand in Part 1, ask it to turn your description into a numbered list, then correct anything it got wrong or left out. Cover: load the file with the right encoding; skip the report header and the upper header line; promote the complete header row; drop the page-break rows; fix the Amount column; strip the non-printing character out of the ID column; count the journal entries per user.`

### Edge cases

`The specific traps, named exactly, and what should happen for each: the encoding; the two-line header, saying which line to keep; the page-break rows, meaning the ==== and PAGE lines; the quoted and spaced Amount values; the non-printing character in the ID column.`

### Expected output

`This part is filled in for you. Keep the paragraph below as the Expected output of your specification.`

The script prints a descriptive summary, covering the total number of journal
entries, the number of distinct users, the number of distinct accounts, and the
count of journal entries per user. It writes two files: `lab_02_cleaned.csv`
(the cleaned ten-column dataset) and `lab_02_user_counts.csv` (the per-user
count).

## Review and Acceptance Criteria

`How a reviewer, or you, confirms the work is correct. This part is filled in for you. Keep the paragraph below.`

The per-user counts the script produces match the result you built by hand in
Part 1, and `lab_02_cleaned.csv` passes the Lab 2 Output Validator with no
issues.

## How this specification is graded

`The specification is worth 15 of the 100 points in Lab 2, graded separately from the rest of the lab because it is the one piece judged on precision. This rubric is fixed. Check your specification against it before you submit.`

| Criterion | Pts |
|---|--:|
| Input names the file, states its encoding, and lists every defect, precisely | 4 |
| Operations are all present and in the right order | 4 |
| Edge cases are each named, with what the script should do about them | 4 |
| Expected output and Review and Acceptance are both stated, and the whole spec is specific with no vague verbs | 3 |
| **Total** | **15** |

## Self-assessment

`Run this section like a pre-submission system check. Mark each item [OK], [WARN], or [FIX], and include short evidence.`

### Submission Gate Checklist

- [ ] **SG-01 File Availability [OK/WARN/FIX]:** Every file in the manifest is produced, the four upload files are submitted to the Lab 2 quiz, and each is named with my university ID.
  - Evidence:
- [ ] **SG-02 Specification Complete [OK/WARN/FIX]:** Input, Operations, and Edge cases are all filled in, specific, in order, with no vague verbs.
  - Evidence:
- [ ] **SG-03 Output Matches the By-Hand Result [OK/WARN/FIX]:** The script's per-user count matches the count I produced by hand in Part 1.
  - Evidence:
- [ ] **SG-04 Validator Clean [OK/WARN/FIX]:** The Lab 2 Output Validator reports no issues on `lab_02_cleaned.csv`.
  - Evidence:
- [ ] **SG-05 File Extensions [OK/WARN/FIX]:** Each file uses the correct extension (`.md`, `.xlsx`, `.py` or `.ipynb`, `.csv`, `.html`), and the `.md` and `.py` files open as plain text.
  - Evidence:

**Blocking Issues (if any):**
- [ ] Issue 1:
- [ ] Issue 2:

**Final Gate Decision:**
- [ ] Ready to submit
- [ ] Not ready, fixes required
