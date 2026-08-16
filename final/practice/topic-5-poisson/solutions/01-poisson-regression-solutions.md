# Solutions 01 (Topic 5) — Poisson Regression (count response)

*Questions: [`../01-poisson-regression.md`](../01-poisson-regression.md).*

> Marking scheme: **70% for correct procedures, 30% for correct answers.**

---

## Problem 1 — Why Poisson, and the model

**(a)** Poisson regression is for a **count** response — non-negative integers 0, 1, 2, … Examples: number
of emails received per day; number of goals scored in a match; number of earthquakes per year in a region.

**(b)** (1) **Range problem** — counts are `≥ 0`, but a straight line predicts **negative** counts. (2)
**Non-constant variance** — the Poisson distribution has **mean equal to variance**:
`λ = E[Y|X] = Var(Y|X)`. So anything that shifts the mean **also shifts the variance**; larger predicted
counts are automatically more variable. That violates the **Equal-variance (E)** assumption, which
requires constant `σ²`.

**(c)** **Mean form:** `E[Y|X] = λ = e^(b0 + b1X)` (always positive). **Log-mean form:**
`log(λ) = b0 + b1X` ← **the linear one** (log = canonical link). The **log link cures the range problem**
because exponentiating the linear predictor gives `λ = e^(…)`, always **positive** whatever the linear
part equals — so predicted mean counts can never go negative.

**(d)** Start from `log λ_t = b0 + b1·temp` (all else held constant). At `temp + 1`:
`log λ_(t+1) = b0 + b1·(temp+1) = b0 + b1·temp + b1`. Subtract: `log λ_(t+1) − log λ_t = b1`, i.e.
`log(λ_(t+1)/λ_t) = b1`, so `λ_(t+1)/λ_t = e^b1` ⇒ **`λ_(t+1) = e^b1 · λ_t`**. Increasing `temp` by 1
**multiplies** the mean by `e^b1` — a multiplicative (not additive) effect.

---

## Problem 2 — Interpreting a Bikeshare Poisson fit

**(a)** (i) "A 1-unit increase in `temp` is associated with a **+2.688 change in the log-mean** number of
bikers, holding other predictors constant." (ii) `e^2.688 ≈ 14.7`: "a 1-unit increase in `temp`
**multiplies the mean count** of bikers by **14.7**." (iii) `40 × 14.7 =` **588** bikers (the effect is
multiplicative). *(The large ratio reflects `temp` being on a normalized/small scale — focus on the
reasoning.)*

**(b)** (i) `season2`: `e^0.063 ≈ 1.065` → **+6.5%** vs. season 1. `season3`: `e^(−0.141) ≈ 0.868` →
**−13.2%** vs. season 1. (ii) **Season 2** is higher than season 1; **season 3** is lower. (iii) "The mean
number of bikers in **season 3** is about **86.8% of** (i.e. **13.2% lower than**) the mean in season 1,
holding the other predictors constant."

**(c)** **False.** R only builds dummy variables out of **factors**. `season` is stored as the **numbers**
1,2,3,4, so `glm` silently treats it as **continuous** and fits **one meaningless slope on the codes**
(pretending season 4 is "twice" season 2). You must `mutate(season = as.factor(season))` **before**
fitting to get proper `season2, season3, season4` dummies. (`workingday` is genuinely binary 0/1, so a
single slope there is fine, but factoring it is clearer.)

**(d)** (i) Working-day `temp` rate ratio `= e^(b_temp + b_int) = e^b_temp · e^b_int = 14.7 × 0.483 ≈`
**7.11**. (ii) Temperature increases ridership in **both** groups, but the effect is **weaker on working
days** (~7.1) than on non-working days (~14.7) — warm weather boosts leisure/weekend riding more than
commuting. The effect of `temp` **depends on** whether it is a working day (the interaction), so you
cannot quote a single temperature effect. 

---

## Problem 3 — Overdispersion and inference

**(a)** (i) Logistic → **odds ratio**; Poisson → **rate ratio** (ratio of mean counts). (ii) Logistic
`Var(Y|X) = p(1−p)`; Poisson `Var(Y|X) = λ`. (iii) **Poisson usually** shows overdispersion; **logistic
only sometimes**. (Both share: no error term, MLE, Wald inference, `factor()` your categoricals,
exponentiate for a multiplicative interpretation.)

**(b)** Poisson forces `Var(Y|X) = λ` (mean = variance) — a very rigid constraint. Real count data almost
always has **extra variability** (unmodeled heterogeneity, clustering, etc.), so the actual variance
exceeds the mean, producing **overdispersion**. Logistic's `Var = p(1−p)` is a milder constraint, so it is
violated **less often**.

**(c)** (i) A dispersion of **≈ 90.6** (vs. the ideal ≈ 1) signals **severe overdispersion** — the plain
Poisson's "mean = variance" clearly fails. (ii) The **SEs and p-values** become untrustworthy (too small
⇒ over-optimistic significance); the **coefficient point estimates are unaffected**. (iii) Refitting with
`family = quasipoisson` **re-estimates the dispersion and inflates the SEs**, leaving the estimates
unchanged. Contrast: Titanic logistic dispersion ≈ **0.98** ≈ 1 is what "no overdispersion" looks like;
Bikeshare's 90.6 is a serious violation.

**(d)** Inference uses the **Wald statistic** `z = b̂ / SE(b̂)`, compared to the **standard Normal
`N(0,1)`**, justified by the **CLT / large-sample theory** (GLM estimates are approximately Normal for
large `n`). Equivalence (5% level): **`|z| > 1.96` ⇔ the 95% CI excludes 0 (rate-ratio CI excludes 1) ⇔
`p < 0.05`** ⇒ reject `H0: β = 0`.
