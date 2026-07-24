# Practice 04 (Topic 3) — Worksheet 03: Model Assumptions via Simulation

*Topic 3 (assumptions, diagnostics, multicollinearity, causality). Source: `worksheets/worksheet_03.ipynb`.
Solutions: [`solutions/04-worksheet3-assumptions-sim-solutions.md`](solutions/04-worksheet3-assumptions-sim-solutions.md).*

Worksheet 03 studies assumption violations by **simulating data from a known mechanism** (so the true
`b`'s are known) and breaking one assumption at a time.

---

## Warm-up true/false (justify each)

**Q1 [TF].** The hypothesis tests reported by `lm()` are valid **only if** the errors are (exactly)
Normally distributed.

**Q2 [TF].** In linear regression, multicollinearity refers to the correlation between each **input
variable and the response** variable.

**Q3 [TF].** Under multicollinearity it can be difficult to determine how the collinear variables are
**separately** associated with the response.

**Q4 [TF].** Multicollinearity **inflates** the estimated standard errors of the LS estimators.

**Q5 [TF].** The assumption that all error terms have the **same variance does not affect** the
estimator of the standard error of the LS estimators.

---

## Understanding the simulation approach

**Q6 [SA].** Why does the worksheet use **simulated** data (with known true `b0, b1, b2`) to study
assumption violations, rather than a real dataset? What can you check with simulated data that you
cannot with real data?

**Q7 [SA].** In the **benchmark** model (all assumptions satisfied), the estimates come out within
about 2 SE of the true parameters and the 95% CIs contain the true values. Even so, the worksheet notes
a correctly-built 95% CI *can* miss the truth. In roughly what fraction of samples, and why is that not
a failure of the method?

---

## Consequences of each violation

**Q8 [SA].** Data are simulated with **heteroscedasticity** (`Var(e_i) = X_i1^4`) and then fit with
`lm()` ignoring it. What happens to (a) the **point estimates** and (b) the **standard errors / CIs /
p-values**? How would you **detect** heteroscedasticity from a plot?

**Q9 [SA].** Data are simulated with **non-Normal (Uniform) errors**. Why is this generally the
**least damaging** violation for inference, and which two plots diagnose it?

**Q10 [SA].** To study **multicollinearity**, the worksheet generates `X1, X2` with correlation
`rho = 0.95` vs. `rho = 0.001`, fits the model **1000 times**, and compares the histograms of `b1_hat`.
(a) What is different about the two histograms? (b) What does that show about multicollinearity's
effect? (c) Why is this **not** bootstrapping?

---

## Whose job & causality

**Q11 [SA].** `lm()` reports SEs and p-values assuming a `t`-Student (≈ Normal) sampling distribution.
Whose responsibility is it to check that the model assumptions actually hold, and how is that done?

**Q12 [SA].** The worksheet states that the goal of generative modelling is usually to make a **causal**
claim, but that we often can't. In an **observational** study, what blocks the causal claim, and what
kind of study would license one?
