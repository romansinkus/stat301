# Practice 01 (Topic 3) — Assumptions & Diagnostics (LINE)

*Topic 3 (Diagnostics). Solutions: [`solutions/01-diagnostics-line-solutions.md`](solutions/01-diagnostics-line-solutions.md).*

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Where a
> question says *sketch*, clearly label the x-axis and y-axis of your plot.

---

## Problem 1 (16 pts) — The LINE assumptions and their consequences

**(a) (4 pts)** Write out the **LINE** acronym: name each assumption and state it in one sentence.

**(b) (4 pts)** "The assumption that all the error terms have the same variance does **not** affect the
estimator of the standard error of the LS estimators." True or false? Justify (be clear about what
happens to the *point estimates* vs. the *SEs*).

**(c) (4 pts)** For each of **L**, **I**, and **E**, name the consequence of violating it. Which two
specifically break your standard errors (and therefore your CIs and p-values)?

**(d) (4 pts)** (i) Why is **Normality** described as the "least severe" of the four violations? Name the
two things that rescue your inference when errors are not Normal. (ii) When is the **Independence**
assumption most likely to fail? Give two data situations, and explain why you often assess independence
from the **study design** rather than a plot.

---

## Problem 2 (16 pts) — Reading diagnostic plots

The additive wage model's **residuals-vs-fitted** plot shows a clear **funnel** (spread widens as fitted
values increase), and its **Q-Q plot** drifts off the diagonal at the tails.

**(a) (4 pts)** Explain *why* residuals are the right thing to plot (what do they contain?), and describe
what the residuals-vs-fitted plot should look like if the model is good.

**(b) (5 pts)** (i) The funnel: which LINE assumption is violated, what is the technical name for this
problem, and what does the plot look like when the assumption *holds*? (ii) A *different* model,
`read ~ income`, instead shows a curved (U-shaped) residuals-vs-fitted plot. Which assumption is
violated, propose a fix, and explain why adding an `income^2` term still counts as a **linear**
regression.

**(c) (4 pts)** (i) Which plot diagnoses the **Normality** assumption, and what does a "good" version
look like versus a violation? (ii) The wage model funnels **and** its Q-Q plot drifts. Name both
violations, and explain why refitting with `log(wage)` addresses *both* at once.

**(d) (3 pts)** Complete the diagnostic table — for each assumption, name the plot you would inspect and
the *bad* pattern that signals a violation:

| Assumption | Plot to inspect | 'Bad' pattern that signals a violation |
| --- | --- | --- |
| **L** (linearity) | ? | ? |
| **E** (equal variance) | ? | ? |
| **N** (normality) | ? | ? |
