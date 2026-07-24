# STAT 301 — Midterm Practice Questions

Practice sets **organized by topic** (Topic 1 / Topic 2 / Topic 3), built from the
[midterm study guide](../master.md), the in-class activities (wage data), the tutorials (CASchools
data), and the worksheets (US cancer + simulated data). **Interpretation is the priority in this
course**, so most questions ask you to *explain what a result means* in plain language, not just
compute a number.

> **Exam logistics (from `mt-info.md` + the review slides).** Thursday **July 23, 2026, 3:45–4:45pm
> (60 min)**, in person in **ESB1012**, hard copies distributed; then 15 min to upload a single PDF to
> Canvas (`LastName-FirstName.pdf`). **Written answers only — there are NO multiple-choice questions.**
> The focus is **understanding + critical thinking**, not tedious computation: interpret R outputs,
> say what model components mean, and explain concepts *in the context of the given dataset*. **R code
> is not directly tested**, but you must understand the R outputs shown in lectures/assignments.
> There will be **some simple calculations — bring a simple calculator.** **Closed book/notes**, but
> you may bring **one letter-size sheet (both sides, written or typed).** Covers everything through the
> **Tuesday July 21 review class.**
>
> **Marking: 70% for correct *procedure/key steps*, 30% for the correct answer** — so *always show your
> reasoning*, and for word answers **write clearly**. These practice sets are therefore all written
> short-answer (no MC), matching the real format.

## How to use this

1. Attempt a file **without** the solutions open. Write full sentences for interpretation
   questions — the exam grades wording (e.g. "associated with" vs. "causes").
2. **Show your key steps**, not just the final answer — that's 70% of the marks. Practice writing the
   reasoning the way you'd hand it in.
3. Check against the matching file in that folder's `solutions/` subfolder.
4. Re-do any question you missed a week later.

## Folder structure (organized by topic)

Each topic folder has its own `solutions/` subfolder. The [`mock-exam/`](mock-exam/) is a cumulative,
deliberately mixed paper for the final dry run.

### [`topic-1-slr/`](topic-1-slr/) — Simple Linear Regression

| File | Covers |
| --- | --- |
| `01-slr-estimation.md` | Least squares, correlation, residuals vs. errors, association ≠ causation |
| `02-slr-inference.md` | SE, sampling distribution, tests, CIs, bootstrapping, p-value literacy |
| `03-categorical-predictors.md` | Dummy variables, 2-level = t-test, reference levels |
| `04-tutorial-caschools-slr.md` | Tutorial 01: generative modelling, EDA, SLR + inference + bootstrap |

### [`topic-2-mlr/`](topic-2-mlr/) — Multiple Linear Regression

| File | Covers |
| --- | --- |
| `01-mlr-additive-anova.md` | Additive MLR, k-level categoricals, ANOVA |
| `02-interactions.md` | Interaction models, reading slopes, slope gaps |
| `03-tutorial-caschools-mlr.md` | Tutorial 02: additive vs. interaction on `grades`, statistical vs. practical significance |

### [`topic-3-diagnostics-causality/`](topic-3-diagnostics-causality/) — Diagnostics, Multicollinearity & Causality

| File | Covers |
| --- | --- |
| `01-diagnostics-line.md` | LINE assumptions, residual/QQ plots, transformations |
| `02-multicollinearity.md` | Collinearity, VIF/GVIF, consequences, fixes |
| `03-causality-designs.md` | Confounding, Simpson's, experiments vs. observation |
| `04-worksheet3-assumptions-sim.md` | Worksheet 03: assumption violations via simulation |
| `05-tutorial3-multicollinearity-causality.md` | Tutorial 03: VIF detect-and-fix workflow + the TikTok confounding sim |

### [`mock-exam/`](mock-exam/) — cumulative

| File | Covers |
| --- | --- |
| `practice-exam.md` | Timed comprehensive practice exam spanning all three topics |

## Question-type legend

*(No multiple choice — the real exam has none, so every question here is written short-answer.)*

- **[TF]** true/false — **always justify** in one or two sentences (a bare T/F earns little)
- **[SA]** short answer / interpretation — explain in words, showing your reasoning
- **[CODE-read]** *read/interpret* R output or formula notation (never write code) — recognize what
  `lm(y ~ x*z)`, `factor()`, `anova()`, and a `get_regression_table()` table express
- **[CALC]** small hand calculation (calculator allowed) — **show the steps**

*Numbers in these questions are realistic but sometimes invented for practice — focus on the
reasoning, not memorizing the digits.*
