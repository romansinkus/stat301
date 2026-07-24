# Solutions 04 (Topic 3) — Worksheet 03: Model Assumptions via Simulation

*Questions: [`../04-worksheet3-assumptions-sim.md`](../04-worksheet3-assumptions-sim.md).*

---

## Warm-up true/false

**Q1.** **False.** `lm()`'s tests are valid if the errors are Normal **or** — thanks to the **CLT** —
if the sample size is large enough (and errors are "nice"). Exact Normality is not required.

**Q2.** **False.** Multicollinearity is correlation **among the input variables (predictors)** — not
between an input and the response. (Predictors being related to the response is the whole point of a
model; that's not collinearity.)

**Q3.** **True.** When predictors carry overlapping information, the model can't cleanly attribute
`Y`'s variation to one versus another, so their **individual** associations become hard to isolate.

**Q4.** **True.** Collinearity **inflates the SEs** of the affected LS estimators (widening CIs, making
their coefficients harder to declare significant).

**Q5.** **False.** The usual SE formula **assumes** a single constant variance `sigma^2`. If that
equal-variance assumption fails (heteroscedasticity), the SE estimator is **wrong/biased** — so the
assumption very much *does* affect it. (The point estimates `b_hat` are unaffected; the SEs are.)

---

## Understanding the simulation approach

**Q6.** With **simulated** data you **know the true parameters** and the true data-generating process,
so you can directly check whether the estimates/CIs recover the truth and *see* exactly what a
violation breaks. With **real** data the true `b`'s are unknown and the data usually contain several
unknown problems at once, so you can't isolate a single violation or grade the estimator against truth.

**Q7.** About **5%** of samples (for a 95% CI). That's not a failure — it's the **definition**: "95%
confidence" means that *across many samples*, 95% of the intervals contain the truth and **5% don't**.
Any single interval either contains the true value or not; the guarantee is about the long-run
procedure.

---

## Consequences of each violation

**Q8.** (a) The **point estimates stay approximately unbiased** — still close to the true
`b0, b1, b2`. (b) The **standard errors are wrong**, so the **CIs and p-values are invalid** (not
trustworthy). **Detect:** a **residuals-vs-fitted plot** — a **funnel/fan** shape (spread changing with
fitted value) signals heteroscedasticity; constant spread is what you want.

**Q9.** Non-Normality is least damaging because, with a **large sample, the CLT** makes the sampling
distributions of the estimators approximately Normal (and `t`) anyway, so inference stays approximately
valid; **bootstrapping** is another rescue. Diagnose with a **Q-Q plot** of the residuals (points off
the diagonal = non-Normal) and a **histogram** of the residuals.

**Q10.** (a) The `rho = 0.95` histogram of `b1_hat` is **much wider** (more spread) than the
`rho = 0.001` one; both are centered near the true value. (b) It shows multicollinearity **inflates the
variance/SE** of the estimator — less precise coefficients — without biasing the center. (c) It's
**repeated sampling from a known population** (1000 fresh simulated datasets), whereas bootstrapping
resamples **with replacement from a single observed sample**.

---

## Whose job & causality

**Q11.** It is **your (the analyst's) job** to check the assumptions — `lm()` just assumes them and
reports numbers regardless. You check with **diagnostic plots**: residuals-vs-fitted (linearity +
equal variance), Q-Q plot / histogram of residuals (normality), and reasoning from the **study design**
(independence). As ISL notes, this is "as much an art as a science," and some assumptions may need a
**domain expert**.

**Q12.** In an **observational** study, **confounders** (and reverse causality/selection) create
associations that aren't causal, and you generally **can't rule them out**, so only association can be
claimed. A **randomized experiment** would license a causal claim, because randomization balances
confounders — **observed and unobserved** — across treatment groups on average.
