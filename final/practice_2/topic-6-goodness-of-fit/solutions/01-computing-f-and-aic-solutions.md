# Solutions — Practice 01 (Topic 6): Computing F & Model Selection

## Problem 1

**(a)** `k = p − q = 4 − 2 = 2` extra predictors. Degrees of freedom: **df₁ = k = 2**,
**df₂ = n − p − 1 = 100 − 4 − 1 = 95**.
`F = [(500 − 400)/2] / [400/95] = [100/2] / [4.2105] = 50 / 4.2105 = **11.88**`.
R function: **`anova(reduced, full)`** (Case B — any nested pair). *(Big RSS drop → big F → small p.)*

**(b)** `F = [0.60/4] / [(1 − 0.60)/(100 − 4 − 1)] = [0.15] / [0.40/95] = 0.15 / 0.004211 = **35.63**`.
This is the **`statistic`** field in `glance(model)` (the model-vs-intercept-only F). *(Its reduced model
is always the null.)*

**(c)** Rejecting `H0` says the **full model fits significantly better than the reduced one** — at least
one of the extra predictors has a nonzero coefficient. It does **not** establish that you can *predict Y
well*, nor that any *particular* predictor of interest carries the signal (in protein~mRNA, the model
became significant because `gene`, not mRNA, did the work). Significance ≠ good prediction ≠ a specific
predictor mattering.

**(d)** The F-test compares `RSS_reduced` vs. `RSS_full` assuming the reduced model is the full model with
some coefficients set to 0 — that only makes sense if the reduced predictors are a **subset** of the full
ones (**nested**). If they aren't nested, `RSS_reduced − RSS_full` isn't a clean "effect of dropping these
`k` terms," the df aren't defined, and the F-distribution doesn't apply.

## Problem 2

**(a)** `F = t² = 3.5² = **12.25**`. When `p = 1`, "does this one predictor help?" (the t-test on its
coefficient) and "does the model beat the null?" (the F-test) are the **same hypothesis** `H0: b1 = 0`, so
the tests coincide and `F = t²` with an identical p-value.

**(b)** (i) **AIC prefers model B** (smallest AIC = 512; **smaller is better**). (ii) Raw **R²** always
increases with more predictors (0.55 → 0.60 → 0.62), so it would wrongly favor the biggest model C — it
can't penalize size, so it can't compare different-sized models. (iii) Adding predictors 5–8 (B→C) raised
R² only trivially (0.60 → 0.62) while adding complexity; AIC "sees" this because its **size penalty**
outweighs the tiny fit gain, so AIC *rose* (512 → 518) — overfitting flagged.

**(c)** **AIC** = (goodness of fit, via −2·log-likelihood) + (penalty for # parameters); smaller = better.
**BIC** is the same idea with a **heavier** size penalty (penalty grows with `log n`), so it favors
*smaller* models. **`step()`** optimizes **AIC** by default.
