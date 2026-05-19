# Example Managing-Up Document

*Also known as "How to Work With Me." A worked example of a managing-up document, written by your instructor. You will write your own — for your audit senior, your manager, your stakeholder, or your direct report — using this as the model.*

Use this as a working reference for how to communicate with me (the instructor), Sean McCaman, and how to create higher quality deliverables.

## If You Only Do Five Things

Whether you use an LLM or not, the checklist below is the core. If you are using an [LLM](#llm), give it the assignment prompt, rubric, and the relevant parts of this document, and ask it to review your draft against the checklist.

For every deliverable:

1. **Lead with the point.** State the conclusion before the supporting detail.[^bluf]
2. **Make every number [traceable](#traceable).** Source, calculation, or assumption should be findable.
3. **Pick consistent terms and stick to them.** Pick one term per concept and use it everywhere.
4. **Match the format to the deliverable type.** A chart, slide, report, model, and code project are not the same. Use the right checklist below.
5. **Proofread before submitting.** Typos and inconsistency have a meaningful impact on reader trust.[^typos]

## What This Is

This document explains how I tend to read, review, and give feedback on student work. It is not a replacement for the [course syllabus](https://utah.instructure.com/courses/1284436/assignments/syllabus) (Canvas login required), assignment instructions, rubric, or course policies. Use those first. Use this as a practical guide for making your work clearer, easier to evaluate, and more useful to your audience.

The deeper skill this guide is practicing is constraint definition: being clear about requirements and expectations. Analytics used to be "how well do you know Tableau or Excel." It is increasingly "who can write the best prompt with the best context." The tool fluency still matters; the leverage now comes from the constraint-definition layer above the tool. Clearer constraints produce better work, whether the producer is an LLM, a teammate, or yourself.

These are my preferences as one instructor working in financial technology. My perspective skews toward fintech roles, data engineering, and finance/accounting automation; other industries, classes, and reviewers will weight things differently. Treat the standards in this document as practical guidance for working with me, not as universal rules.

Note on professional context: most production AI use in accounting now happens on enterprise-controlled platforms — in-house LLMs at firms like KPMG and Deloitte, sanctioned agentic workflows, Microsoft Copilot deployments. The principles in this document are tool-agnostic; the specific platform you use professionally will vary by employer, but the skill of defining good constraints transfers.

If you are using an [LLM](#llm), reference this document — or just the relevant excerpts — as a standing guide. Give the LLM the current assignment instructions, rubric, and the specific deliverable you want reviewed. Good context is targeted context.

## Who I Am

- **Contact:** sean.m@utah.edu. <!-- ferpa-ok: instructor's own published contact info -->

- I am an Adjunct Instructor at the University of Utah.
- I am a Senior Director of Data Science and Data Engineering, reporting to the CFO at PayIt.
- I have 15 years of professional experience.
- My background is in data, analytics, and finance.
- I work primarily in Python, PHP, SQL, and Big Data tools such as Snowflake, Databricks, and BigQuery.
- I am comfortable reading charts, tables, spreadsheets, models, code, and technical explanations.
- What I love most professionally is helping people push their boundaries of understanding and creativity in pursuit of innovation.
- I have used LLMs daily since December 2022 and have built large-scale projects with Claude, Codex, Cursor, and Gemini. My current AI work focuses on agentic software development, AI-assisted workflows, and practical machine learning applications for finance and fintech teams.

## What I Value

- Clarity.
- Simplicity.
- Consistency.

Clarity is kindness. When you make your work easy to follow, you are respecting the time, attention, and decision-making responsibility of your reader.

## What Good Work Looks Like to Me

- **Lead with the point:** Make it clear what I am looking at and why it matters.
- **Readable numbers:** Use appropriate rounding, labels, and units.
- **No unnecessary clutter:** Keep only what helps me understand your work.
- **Consistent presentation:** Use consistent terminology, formatting, and structure throughout.
- **[Traceable](#traceable) logic:** Make it easy for me to follow the source, method, and conclusion.
- **Your understanding of the topic:** My goal is to empower your learning and growth. When you can demonstrate a simple explanation, it conveys your understanding of the material.

## What Usually Draws Feedback

I am usually reacting to something that makes the work harder to trust or harder to understand. These are fixable communication or analytical issues.

- **Untraceable numbers:** Conclusions that do not make the source, calculation, or assumption clear.
- **Polish without clarity:** Visual effects or complex layouts that make the answer harder to understand.
- **Inconsistency:** Mixed chart formatting, headers that move around, distracting fonts, or different terms for the same metric. For example, two charts on the same page that represent the same population but use different colors.
- **Wrong chart for the question:** A chart type that does not match the data or the point being made.

## How to Get Moving Fast

- **Start with the deliverable type:** Decide whether you are producing a chart, table, slide deck, written analysis, spreadsheet, model, notebook, or code project.
- **Read the instructions first:** Review the assignment prompt, rubric, and any examples before asking an LLM for help.
- **Ask what decision the work supports:** If you cannot name the decision, question, or learning objective, the output will probably drift.
- **Draft the answer first:** Write the main takeaway in one sentence before polishing the format.
- **Use an LLM as a reviewer:** Ask it to check clarity, source [traceability](#traceable), assumptions, bias, and [reproducibility](#reproducibility) before you submit.
- **Verify before trusting the LLM:** If an LLM helped produce the work, make sure you can reproduce or explain the important numbers yourself.
- **Tighten one pass at a time:** First check correctness, then clarity, then formatting.

## How to Build Your Own Managing-Up Document

The same pattern adapts to any working relationship: your audit senior, your manager, a stakeholder you support, a direct report you manage, a peer team you collaborate with. The relationships differ; the document structure does not. You define who they are, what they value, what you can offer, and how you want to be evaluated.

Good source material includes the job description, performance criteria, prior feedback you have received, formal style guides of your firm or industry (e.g., Big Four work-paper conventions, GAAP presentation rules, internal style guides), and any public artifacts (LinkedIn profiles, internal bios, published deliverables) that show what your audience prioritizes.

Use a prompt like this:

```text
Read the attached job description, performance criteria, prior feedback (if any), and any public artifacts about my [audit senior / manager / stakeholder / direct report]. Build a concise managing-up document for this relationship that explains:

1. What this person appears to value in the work I produce.
2. What strong work likely looks like to them.
3. What mistakes are likely to draw critical feedback.
4. What checklist I should run on my own deliverables before sending.
5. What deliverable-specific checks apply to writing, slides, charts, spreadsheets, models, code, or other outputs I will produce.

Write it in a calm, professional tone. Do not invent private information. Separate evidence from interpretation.
```

Once you have a draft, refine it against the real interactions you have. The document is most useful when it captures what you have actually observed, not what you initially guessed. Treat it as a living artifact — review and update it every few months.

This same pattern can also adapt to other classes (instructor as audience, syllabus as job description, rubric as performance criteria). The structure carries.

## Skill-Ready Checklist

"[Skill-ready](#skill-ready-checklist)" means the checklist is structured so a person or an LLM can apply it directly without further translation. Use it before submitting a chart, table, document, slide deck, spreadsheet, model, notebook, or code-based deliverable. A reviewer or LLM can mark each relevant item as `[OK]`, `[WARN]`, or `[FIX]`, then give brief evidence and a suggested improvement.

### Applies to Every Deliverable

- [ ] **Review the full deliverable:** Read the work all the way through before submitting it.
- [ ] **Understand the deliverable:** If any part is unclear, ask an LLM to explain the component parts, then verify the explanation.
- [ ] **Lead with the point:** Make the main conclusion easy to find without requiring narration.
- [ ] **Use concise language:** Say the most important thing with the fewest useful words.
- [ ] **Use consistent terms:** Do not switch between terms like "revenue," "sales," and "net revenue" unless they mean different things.
- [ ] **Define important terms:** Explain terms that could be interpreted more than one way.
- [ ] **Cite the source:** Make the source file, workbook, dataset, system, or code path easy to find.
- [ ] **Make the logic [traceable](#traceable):** Show enough method, formula, or reasoning that I can tell how you got the answer.
- [ ] **Check [reproducibility](#reproducibility):** Confirm the work can be re-run or independently recreated from the provided source, formula, or code.
- [ ] **Check risk level:** Identify whether the work could influence serious decisions such as layoffs, acquisitions, audits, grades, contracts, or compliance.
- [ ] **Match rigor to risk:** Use extra care when a small error could create a large consequence.
- [ ] **Check for bias:** Look for confirmation bias, selection bias, survivorship bias, anchoring, recency bias, and motivated reasoning.[^biases]
- [ ] **Separate facts from opinion:** Make it clear when you are reporting evidence versus giving a recommendation.
- [ ] **Proofread carefully:** Fix typos in titles, headers, labels, body text, comments, and footnotes.

### Charts and Tables

- [ ] **Use a specific title:** Tell me what I am looking at immediately, such as "Revenue by Quarter, FY2024 (USD millions)."
- [ ] **Choose the right chart type:** Match the chart type to the data and the question being answered.[^charts]
- [ ] **Remove [chartjunk](#chartjunk):** Delete or mute unnecessary gridlines, redundant legends, heavy borders, 3D effects, drop shadows, and decorative elements.
- [ ] **Use meaningful precision:** Match decimals to what the underlying number can realistically support.
- [ ] **Label units:** Make units visible in the title, axis, column header, subtitle, or note.
- [ ] **Use readable axes:** Keep only the axis lines, labels, and gridlines that improve readability.
- [ ] **Use color intentionally:** Use color to direct attention, not to decorate.
- [ ] **Check accessibility:** Confirm the chart still works in grayscale and is readable for color-blind viewers.
- [ ] **Align tables cleanly:** Right-align numbers, left-align text, and center headers only when it improves readability.
- [ ] **Avoid mystery numbers:** Make every key number [traceable](#traceable) to a source, calculation, or assumption.

### Slides and Presentations

- [ ] **Use consistent placement:** Keep titles, charts, labels, and page numbers in consistent positions across slides.
- [ ] **Use consistent typography:** Keep font sizes, styles, and emphasis patterns consistent.[^slides]
- [ ] **Run the [rapid slide cycle](#rapid-slide-cycle):** Scroll quickly through the slides while letting your eyes relax; fix anything that jumps around.
- [ ] **Keep one idea per slide:** Do not force the audience to untangle multiple unrelated points.
- [ ] **Make the slide stand alone:** Assume the slide may be read without live narration.
- [ ] **Use footnotes for context:** Use footnotes to explain assumptions, confidence level, risk, or exceptions.

### Written Analysis and Reports

- [ ] **Start with the answer:** Put the conclusion or recommendation before the supporting detail.[^bluf]
- [ ] **Explain why it matters:** Connect the analysis to the decision, risk, or business question.
- [ ] **Use headings as signposts:** Make the structure easy to scan.
- [ ] **Keep paragraphs tight:** Break up dense blocks of text.
- [ ] **Support claims with evidence:** Do not make strong claims without data, citation, or reasoning.
- [ ] **Preserve nuance:** Call out limitations, uncertainty, or assumptions that affect interpretation.

### Spreadsheets, Models, and Data Workbooks

- [ ] **Separate inputs, calculations, and outputs:** Make it clear which cells are raw data, formulas, assumptions, and final results.
- [ ] **Label assumptions:** Put assumptions where reviewers can find them.
- [ ] **Use consistent formulas:** Avoid unexplained formula changes across similar rows or columns.
- [ ] **Check totals and [tie-outs](#tie-out):** Reconcile totals to the source or explain the difference.
- [ ] **Avoid hardcoded surprises:** Flag hardcoded values that are not obvious assumptions.[^spreadsheets]
- [ ] **Make refresh steps clear:** Document how to update the workbook or model with new data.
- [ ] **Protect important formulas:** Reduce the chance that a reviewer or user accidentally overwrites logic.

### Code-Based Deliverables

- [ ] **State the purpose:** Make the code's job clear in the README, docstring, notebook title, or top-level comment.
- [ ] **Make setup [reproducible](#reproducibility):** Include dependencies, environment assumptions, and run commands.
- [ ] **Prefer clear names:** Use names that explain what variables, functions, files, and outputs represent.
- [ ] **Keep logic organized:** Break work into small functions or sections that each do one clear job.
- [ ] **Explain why, not what:** Use comments for decisions, assumptions, edge cases, and non-obvious tradeoffs.
- [ ] **Validate inputs:** Check that required files, columns, parameters, or configuration values are present before relying on them.
- [ ] **Handle errors clearly:** Fail with messages that help someone fix the problem.
- [ ] **Test important behavior:** Include focused checks for calculations, transformations, edge cases, and expected outputs.
- [ ] **Avoid hidden state:** Do not depend on unstated local files, manual steps, notebook cell order, or machine-specific paths.
- [ ] **Write safe outputs:** Use clear output paths and avoid overwriting important files without making that behavior obvious.
- [ ] **Keep data private:** Do not include private data, credentials, tokens, student records, or sensitive business data in code, logs, examples, or commits.
- [ ] **Confirm lint and formatting:** Run the available formatter, linter, or notebook cleanup step before submitting.

## Final Principle

[AI](#ai) is a powerful collaborator, and learning to use it well is part of this course. There is no expectation that you start out expert. The students who get the most out of these tools are the ones who stay curious, keep their own thinking in the lead, and check the work before trusting it.

An LLM can help you reach a finished product faster, but the final submission still carries your name. Whether you send an email, post a Slack message, submit in Canvas, or deliver code, you are responsible for the quality, accuracy, and judgment behind it. Wherever you are with these tools, you are in the right place.

Clear thinking shows up as clear output. If your analysis is solid but the chart, table, document, slide deck, spreadsheet, or code hides it, much of the value is lost on the audience.

## Fair Use

You are welcome to copy, adapt, and reuse this document for your own classes, teams, or projects. Please include attribution when you do.

Suggested attribution:

```text
Adapted from "Example Managing-Up Document" by Sean McCaman, University of Utah.
```

## Definitions

A few terms used above, in case any of them are new. They are listed alphabetically. Click any linked term in the body of this document to jump back here.

- <a id="ai"></a>**AI (artificial intelligence):** A broad term for systems that perform tasks typically associated with human thinking, such as reasoning, language, and pattern recognition. In this course, you may work with AI through LLMs, neural networks, unsupervised learning, and other machine learning methods.
- <a id="chartjunk"></a>**Chartjunk:** Visual elements in a chart that do not add information, such as heavy gridlines, drop shadows, 3D effects, or decorative graphics. The term comes from Edward Tufte's work on data visualization. See [Chartjunk on Wikipedia](https://en.wikipedia.org/wiki/Chartjunk) for background.
- <a id="llm"></a>**LLM (large language model):** A specific kind of AI tool that takes a prompt and produces text in response. Examples include ChatGPT, Claude, Gemini, and Copilot.
- <a id="rapid-slide-cycle"></a>**Rapid slide cycle:** Scrolling quickly through a slide deck while letting your eyes relax, looking for anything that jumps around — placement, font size, color, alignment. Inconsistencies are easier to spot at speed than slide by slide.
- <a id="reproducibility"></a>**Reproducibility:** Someone else can re-run or recreate your work from the source files, formulas, or code you provided. Without it, your numbers are hard to trust.
- <a id="skill-ready-checklist"></a>**Skill-ready checklist:** A checklist written so a person or an LLM can apply it directly without needing further translation or interpretation.
- <a id="tie-out"></a>**Tie-out:** A check that two numbers that should match actually match — e.g., a model total reconciled to its source data, or a row-by-row sum reconciled to a column total. If they don't match, you either find the error or document the difference.
- <a id="traceable"></a>**Traceable:** A number, claim, or conclusion is traceable when I can find the source, calculation, or assumption behind it without having to ask. The opposite is a "mystery number" — visible result, hidden origin.

[^bluf]: On readers: Weinreich et al. (2008) found people consume ~20% of words on a typical page and abandon nearly half of new pages within 12 seconds. On LLMs: Liu et al. (2024) document a U-shaped attention curve where models reliably attend to information at the start and end of context but miss content buried in the middle.

[^biases]: The heuristics-and-biases literature was launched by Tversky & Kahneman (1974). For systematic coverage of all six biases listed, see Gilovich, Griffin, & Kahneman (2002).

[^charts]: Saket, Endert, & Demiralp (2019) found chart effectiveness varies significantly across analytical tasks, supporting the principle of matching chart type to the question being answered.

[^slides]: Kosslyn et al. (2012) found that arbitrary typographic mixing and unsignalled visual changes are widespread slide-design failures, violating principles of discriminability and informative change.

[^spreadsheets]: Panko (1998) summarizes field audits showing approximately 88% of operational spreadsheets contain errors. Embedded constants inside formulas are a commonly flagged finding in EUC audit guidance.

[^typos]: Witchel et al. (2020) found spelling errors produced an 8.86-point trustworthiness penalty (out of 100) in randomized reading experiments; Cox, Cox, & Cox (2017) replicated this finding for online reviewer credibility.

## References

Sources backing claims made in this document.

- Cox, D., Cox, J. G., & Cox, A. D. (2017). To err is human? How typographical and orthographical errors affect perceptions of online reviewers. *Computers in Human Behavior, 75*, 245–253. https://doi.org/10.1016/j.chb.2017.05.008
- Gilovich, T., Griffin, D., & Kahneman, D. (Eds.). (2002). *Heuristics and biases: The psychology of intuitive judgment*. Cambridge University Press.
- Kosslyn, S. M., Kievit, R. A., Russell, A. G., & Shephard, J. M. (2012). PowerPoint® presentation flaws and failures: A psychological analysis. *Frontiers in Psychology, 3*, 230. https://doi.org/10.3389/fpsyg.2012.00230
- Liu, N. F., Lin, K., Hewitt, J., Paranjape, A., Bevilacqua, M., Petroni, F., & Liang, P. (2024). Lost in the middle: How language models use long contexts. *Transactions of the Association for Computational Linguistics, 12*, 157–173. https://doi.org/10.1162/tacl_a_00638
- Panko, R. R. (1998). What we know about spreadsheet errors. *Journal of End User Computing, 10*(2), 15–21.
- Saket, B., Endert, A., & Demiralp, Ç. (2019). Task-based effectiveness of basic visualizations. *IEEE Transactions on Visualization and Computer Graphics, 25*(7), 2505–2512. https://doi.org/10.1109/TVCG.2018.2829750
- Tversky, A., & Kahneman, D. (1974). Judgment under uncertainty: Heuristics and biases. *Science, 185*(4157), 1124–1131. https://doi.org/10.1126/science.185.4157.1124
- Weinreich, H., Obendorf, H., Herder, E., & Mayer, M. (2008). Not quite the average: An empirical study of web use. *ACM Transactions on the Web, 2*(1), Article 5. https://doi.org/10.1145/1326561.1326566
- Witchel, H. J., Thompson, G. A., Jones, C. I., Westling, C. E. I., Romero, J., Nicotra, A., Maag, B., & Critchley, H. D. (2020). Spelling errors and shouting capitalization lead to additive penalties to trustworthiness of online health information: Randomized experiment with laypersons. *Journal of Medical Internet Research, 22*(6), e15171. https://doi.org/10.2196/15171

## Last Updated

This document was last updated 5/11/2026 and is intended for use with the University of Utah course ACCTG 5150 - 090.
