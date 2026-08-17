# Solutions — Practice 01 (Topic 8): Reading LASSO Plots

## Problem 1

**(a)** At `log λ = −3`, nonzero coefficients: **x1, x2, x3** → **3 predictors selected** (x4, x5 are 0). A
coefficient at exactly **0** means LASSO has **dropped that variable** (performed selection). LASSO can do
this because its **L1 penalty** has a corner at 0 that pins coefficients exactly to 0; ridge's **L2**
penalty shrinks smoothly toward 0 but **never reaches it**, so ridge never selects.

**(b)** Drop-out order as `λ` grows: **x5 and x4 first** (gone by `log λ = −3`), then **x3** (gone by
`log λ = −1`), then **x2, x1 last** (gone only by `log λ = +1`). The variables that survive longest (**x1,
x2**) carry the **strongest signal**; the first to die (x4, x5) are the weakest.

**(c)** `λ = 0` removes the penalty entirely, recovering the **ordinary least-squares** fit — hence the
near-OLS values at `log λ = −6`. Moving rightward (larger λ) **increases bias** (coefficients shrink away
from their OLS values) but **decreases variance** (estimates get more stable) — the bias–variance
trade-off.

**(d)** LASSO penalizes the **size** of coefficients, and a coefficient's size depends on its variable's
**units**. `x1` (rooms, ~1–8) and `x2` (area, ~50–300 m²) live on wildly different scales, so without
standardizing, the penalty would unfairly hammer the small-unit variable (rooms) and spare the large-unit
one (area) — selection would reflect **units, not importance**. Standardizing puts all predictors on equal
footing.

## Problem 2

**(a)** At small `λ` (left), the model is barely penalized → **high variance** (overfitting) → high CV
MSE. As `λ` grows, variance falls faster than bias rises, so MSE **drops** to a minimum. Past the optimum,
`λ` is so large that **bias** dominates (too much shrinkage, underfitting) and MSE **rises** again — the
classic `Variance + Bias²` U.

**(b)** **`lambda.min`** = the λ at the CV-MSE **minimum**: `log λ = −2`, keeping **6 variables**.
**`lambda.1se`** = the **largest** λ whose CV error is within **1 SE** of that minimum: `log λ = −1`,
keeping **4 variables**. Prefer `lambda.1se` because it gives the **simplest model statistically
indistinguishable** from the best one — more regularization, fewer variables, less overfitting, at no
real cost in CV error.

**(c)** Cross-validation splits the **training data** into `k` folds, rotating which fold is the
validation set, so λ is tuned **without ever looking at the real test set** (which stays sealed for the
final honest evaluation). Procedure: **`k`-fold CV**, usually **`k = 10`**.

**(d)** Zero variables selected = the **intercept-only / null model** (predicts the mean for everyone).
