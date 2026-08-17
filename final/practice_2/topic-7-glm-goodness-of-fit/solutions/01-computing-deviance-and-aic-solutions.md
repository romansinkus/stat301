# Solutions — Practice 01 (Topic 7): Computing Deviance & AIC

## Problem 1

**(a)** **Null deviance** → the **intercept-only** model (no predictors). **Residual deviance** → your
**fitted** model (with all predictors). Deviance is the GLM analog of **RSS** — a likelihood-based measure
of *unexplained misfit* (smaller = better fit).

**(b)** (i) Deviance drop = `900.0 − 750.0 = **150.0**`. (ii) df = `199 − 195 = **4**` (= number of
predictors added). (iii) `150.0 ≫ χ²₄ = 9.49`, so **reject H0** → the model fits significantly better than
the null. *(This is the GLM version of the model-vs-null F-test.)*

**(c)** McFadden pseudo-R² = `1 − 750/900 = 1 − 0.833 = **0.167**`. Interpretation: the predictors reduce
the deviance (misfit) by ~17% relative to the null model. It's **not** the linear R² because there's no
`TSS = ESS + RSS` decomposition for MLE fits — deviance isn't "variance," so it's an *analogy* to
"proportion explained," not a literal variance share.

**(d)** A saturated model has one parameter per data point — it fits the **noise**, not just the signal
(overfitting), so it predicts terribly on new data. You want good-but-not-perfect fit.

## Problem 2

**(a)** (i) Deviance drop = `780.0 − 750.0 = **30.0**`. (ii) `d = 197 − 195 = **2**`. (iii) `30.0 ≫ χ²₂ =
5.99` → **reject H0**: the extra block of predictors **significantly improves** the model. R command:
**`anova(reduced, full, test = "Chisq")`**.

**(b)** AIC picks the **full** model (764 < 790, smaller is better) — **agrees** with the deviance test.
Raw deviance *always* drops as you add predictors (like R²), so it can't compare different sizes; **AIC
adds a size penalty** (AIC = −2·logLik + 2·#params), so it only rewards predictors that improve fit *enough
to justify their cost*.

**(c)** The F-test rests on the LS **sum-of-squares** decomposition, which doesn't hold for MLE-fit GLMs.
It's replaced by the **χ² deviance test** (deviance drop vs. χ² with `d` df). What stays the same: the
**workflow** — fit reduced vs. full, compare via `anova()`, reject if the improvement is significant.

**(d)** "Large-sample" means the χ² reference distribution is only an **approximation** that's accurate when
`n` is big; with **small samples** (or very rare events / sparse cells in logistic), the χ² p-value can be
unreliable, so you'd distrust it there.
