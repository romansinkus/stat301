# Solutions 01 (Topic 7) — Goodness of Fit for GLMs (Deviance)

*Questions: [`../01-deviance-chisq.md`](../01-deviance-chisq.md).*

> Marking scheme: **70% for correct procedures, 30% for correct answers.**

---

## Problem 1 — The deviance concept

**(a)** (i) The key fact: **`R²`, adjusted `R²`, `RSE`, `MSE`, and the F-test are for LINEAR regression
only** — they **do not apply to logistic or Poisson regression**. For a GLM, compute the **deviance**
(and use a **deviance test** for nested models); AIC also works, being likelihood-based. (ii) The
**deviance** measures the gap between the **log-likelihood of your fitted model** and that of a "perfect"
model — the **saturated model**, which has **one parameter per observation** and fits the data **exactly**
(interpolates every point). It is the GLM's generalization of RSS. **Lower deviance = better fit.**

**(b)** **Null deviance** = the fit of the **intercept-only** model (no predictors). **Residual deviance**
= the fit of **your** model (with its predictors). If the residual deviance is much **smaller** than the
null deviance, your **predictors substantially improved the fit** over predicting a constant — the
analogue of a large drop from TSS to RSS in a linear model.

**(c)** **False.** The saturated model passing through every point has **overfit**: it has **memorized the
noise** in this particular sample, so it will make **large errors on a new sample** from the same
population. A perfect in-sample fit generalizes poorly. We deliberately prefer **good-but-not-perfect**
models that capture the signal without chasing noise.

**(d)** **Linear model:** RSS → **`R²` / adjusted `R²` / RSE / MSE** and the **F-test** for nested models.
**GLM (logistic/Poisson):** deviance → the **deviance χ²-test** for nested models. The single criterion
that works for **both** is **AIC** (likelihood-based, not tied to RSS).

---

## Problem 2 — The deviance test

**(a)** (i) `H0:` the two nested models are **equally good** (the extra coefficients add nothing) vs. `H1:`
the **larger model is better**. (ii) Test statistic = the **difference in deviance** between the two
models. (iii) Under `H0` it follows a **χ²(d)** distribution, where **`d` = the difference in the number of
predictors** between the two models. (iv) In R: **`anova(reduced, full, test = "Chisq")`**.

**(b)** (i) The **deviance drop of 18.7** is the improvement in fit (reduction in deviance = the χ²
statistic) from adding the extra terms to the reduced model. (ii) `d = 3` = the **number of extra
predictors** the full model has over the reduced (so the reference is χ²(3)). (iii) `p = 0.0003 < 0.05` ⇒
**reject H0** — the deviance drop is significantly larger than chance; the **larger model is justified**.

**(c)** "Large-sample" means the **χ² reference distribution is only an approximation**, reliable only when
the **sample size `n` is big** (and, for logistic/Poisson, when events are not too sparse). With a **small
`n`** (or very rare outcomes), the χ² p-value can be **inaccurate**, so you would distrust it and be
cautious about the conclusion.

**(d)** The F-test is a **linear-model tool** — built on RSS and an F distribution, which do not apply to
GLMs (no RSS/`σ²` in the same sense; estimation is by MLE). For GLMs you swap in the **deviance** as the
measure of fit and a **χ²** reference distribution instead of `F`. What **stays the same** is the
**workflow**: fit a reduced and a full **nested** model and compare with `anova(reduced, full, …)` — just
with `test = "Chisq"` and deviance rather than the F-statistic.
