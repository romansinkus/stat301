# Solutions 04 (Topic 3) — Worksheet 03: Model Assumptions via Simulation

*Questions: [`../04-worksheet3-assumptions-sim.md`](../04-worksheet3-assumptions-sim.md).*

> Marking scheme: **70% for correct procedures, 30% for correct answers.**

---

## Problem 1 — Warm-up and the simulation method

**(a)** (i) **False.** `lm()`'s tests are valid if the errors are Normal **or** — thanks to the **CLT** —
if the sample size is large enough (and errors are "nice"); exact Normality is not required.
(ii) **False.** Multicollinearity is correlation **among the input variables (predictors)** — not between
an input and the response.
(iii) **True.** When predictors carry overlapping information, the model cannot cleanly attribute `Y`'s
variation to one versus another, so their **individual** associations are hard to isolate.
(iv) **True.** Collinearity **inflates the SEs** of the affected LS estimators (widening CIs, making
coefficients harder to declare significant).
(v) **False.** The usual SE formula **assumes** a single constant `σ²`; if equal variance fails, the SE
estimator is **wrong/biased** — so the assumption very much *does* affect it. (Point estimates
unaffected; SEs are.)

**(b)** With **simulated** data you **know the true parameters** and the true data-generating process, so
you can directly check whether the estimates/CIs recover the truth and *see* exactly what a violation
breaks. With **real** data the true `b`'s are unknown and the data usually contain several unknown
problems at once, so you cannot isolate a single violation or grade the estimator against truth.

**(c)** About **5%** of samples (for a 95% CI). That is not a failure — it is the **definition**: "95%
confidence" means across many samples, 95% of the intervals contain the truth and **5% do not**. Any
single interval either contains the true value or not; the guarantee is about the long-run procedure.

**(d)** It is **your (the analyst's) job** to check the assumptions — `lm()` just assumes them and reports
numbers regardless. You check with **diagnostic plots**: residuals-vs-fitted (linearity + equal
variance), Q-Q plot / histogram of residuals (normality), and reasoning from the **study design**
(independence). Some assumptions may need a **domain expert**.

---

## Problem 2 — Consequences of each violation

**(a)** (i) The **point estimates stay approximately unbiased** — still close to the true `b0, b1, b2`.
(ii) The **standard errors are wrong**, so the **CIs and p-values are invalid**. (iii) **Detect** with a
**residuals-vs-fitted plot** — a **funnel/fan** shape (spread changing with fitted value) signals
heteroscedasticity; constant spread is what you want.

**(b)** Non-Normality is least damaging because, with a **large sample the CLT** makes the estimators'
sampling distributions approximately Normal (and `t`) anyway, so inference stays approximately valid;
**bootstrapping** is another rescue. Diagnose with a **Q-Q plot** of the residuals (points off the
diagonal = non-Normal) and a **histogram** of the residuals.

**(c)** (i) The `rho = 0.95` histogram of `b1_hat` is **much wider** (more spread) than the `rho = 0.001`
one; both are centered near the true value. (ii) It shows multicollinearity **inflates the variance/SE**
of the estimator — less precise coefficients — without biasing the center. (iii) It is **repeated
sampling from a known population** (1000 fresh simulated datasets), whereas bootstrapping resamples
**with replacement from a single observed sample**.

**(d)** In an **observational** study, **confounders** (and reverse causality/selection) create
associations that are not causal, and you generally **cannot rule them out**, so only association can be
claimed. A **randomized experiment** would license a causal claim, because randomization balances
confounders — **observed and unobserved** — across treatment groups on average.
