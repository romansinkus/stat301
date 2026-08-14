# Practice 04 (Topic 3) — Worksheet 03: Model Assumptions via Simulation

*Topic 3 (assumptions, diagnostics, multicollinearity, causality). Source: `worksheets/worksheet_03.ipynb`.
Solutions: [`solutions/04-worksheet3-assumptions-sim-solutions.md`](solutions/04-worksheet3-assumptions-sim-solutions.md).*

Worksheet 03 studies assumption violations by **simulating data from a known mechanism** (so the true
`b`'s are known) and breaking one assumption at a time.

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Justify
> every true/false. Where a question says *sketch*, label both axes.

---

## Problem 1 (15 pts) — Warm-up and the simulation method

**(a) (5 pts)** True or false (justify each in one sentence):
(i) The hypothesis tests reported by `lm()` are valid **only if** the errors are (exactly) Normally
distributed.
(ii) In linear regression, multicollinearity refers to the correlation between each **input variable and
the response**.
(iii) Under multicollinearity it can be difficult to determine how the collinear variables are
**separately** associated with the response.
(iv) Multicollinearity **inflates** the estimated standard errors of the LS estimators.
(v) The assumption that all error terms have the **same variance does not affect** the estimator of the
standard error of the LS estimators.

**(b) (4 pts)** Why does the worksheet use **simulated** data (with known true `b0, b1, b2`) to study
assumption violations, rather than a real dataset? What can you check with simulated data that you cannot
with real data?

**(c) (3 pts)** In the **benchmark** model (all assumptions satisfied), the 95% CIs contain the true
values — yet the worksheet notes a correctly-built 95% CI *can* miss the truth. In roughly what fraction
of samples, and why is that not a failure of the method?

**(d) (3 pts)** `lm()` reports SEs and p-values assuming a `t`-Student (≈ Normal) sampling distribution.
Whose responsibility is it to check that the model assumptions actually hold, and how is that done?

---

## Problem 2 (16 pts) — Consequences of each violation

**(a) (5 pts)** Data are simulated with **heteroscedasticity** (`Var(e_i) = X_i1^4`) and then fit with
`lm()` ignoring it. What happens to (i) the **point estimates** and (ii) the **standard errors / CIs /
p-values**? (iii) How would you **detect** heteroscedasticity from a plot?

**(b) (4 pts)** Data are simulated with **non-Normal (Uniform) errors**. Why is this generally the
**least damaging** violation for inference, and which two plots diagnose it?

**(c) (4 pts)** To study **multicollinearity**, the worksheet generates `X1, X2` with correlation
`rho = 0.95` vs. `rho = 0.001`, fits the model **1000 times**, and compares the histograms of `b1_hat`.
(i) What is different about the two histograms? (ii) What does that show about multicollinearity's
effect? (iii) Why is this **not** bootstrapping?

**(d) (3 pts)** The worksheet states the goal of generative modelling is usually a **causal** claim, but
that we often cannot make one. In an **observational** study, what blocks the causal claim, and what kind
of study would license one?
