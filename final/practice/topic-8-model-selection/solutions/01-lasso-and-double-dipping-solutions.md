# Solutions 01 (Topic 8) — Model Selection (Regularization & Post-Inference)

*Questions: [`../01-lasso-and-double-dipping.md`](../01-lasso-and-double-dipping.md).*

> Marking scheme: **70% for correct procedures, 30% for correct answers.**

---

## Problem 1 — Stepwise vs. regularization; ridge vs. LASSO

**(a)** (i) Stepwise adds/removes variables one at a time, so the result **depends on the order** in which
variables enter — it can miss the best subset (greedy, not exhaustive). (ii) A variable is either **fully
in or fully out**: its coefficient **jumps** discretely from `0` to some value in a single step.
**Regularization** instead shrinks coefficients **continuously** toward 0 by adding a penalty, so
selection happens *smoothly* rather than in all-or-nothing jumps.

**(b)** Minimize `Σ(Yᵢ − b0 − Xᵢ·b)² + λ·penalty(b)` = **(usual least-squares fit)** + **(penalty that
shrinks the coefficients)**. `λ ≥ 0` controls **how much shrinkage**: larger `λ` ⇒ stronger penalty ⇒ more
shrinkage toward 0.

**(c)**

| Method | Penalty | Norm | Shrinks to exactly 0? | Selects variables? |
| --- | --- | --- | --- | --- |
| Ridge | `λ·Σbⱼ²` | L2 (squared) | **No** (never quite 0) | **No** |
| LASSO | `λ·Σ|bⱼ|` | L1 (absolute) | **Yes** | **Yes** (selects + trains at once) |

The course focuses on **LASSO** = **L**east **A**bsolute **S**hrinkage **a**nd **S**election **O**perator.

---

## Problem 2 — Tuning λ and the bias–variance trade-off

**(a)** (i) At **`λ = 0`** there is no penalty, so the objective is just RSS — you **get back the ordinary
least-squares estimates**. (ii) As `λ` grows, coefficients shrink; **LASSO drives them to *exactly 0* one
by one** (a coefficient of 0 means the variable is **dropped** — that is how it selects). **Ridge** shrinks
toward 0 but **never reaches it** (the L2 penalty's gradient vanishes near 0), so every variable stays in.

**(b)** Choose `λ` by **cross-validation** (`cv.glmnet()`), picking the `λ` that **minimizes the estimated
test MSE**. CV splits the **training** data into internal train/validation folds, so it estimates
out-of-sample error **without touching the real test set**. It reports two choices: **`lambda.min`** = the
`λ` with the **smallest CV MSE**; **`lambda.1se`** = the **largest** `λ` whose CV MSE is still **within 1
standard error** of the minimum ⇒ **more shrinkage / a simpler model** at almost no cost in error.

**(c)** Shrinkage biases coefficients toward 0, but **`MSE = Variance + Bias²`**, and shrinkage **buys a
large reduction in variance** for a **small** increase in bias — so total MSE (prediction error) **goes
down**. We accept bias because LASSO is built for **prediction**, not unbiased interpretation. It shines
especially in **high-dimensional** problems where **`p >> n`** (more predictors than observations), where
ordinary LS is unstable or undefined. Inputs must be **standardized** because the penalty depends on
coefficient **size**, which depends on each variable's scale — otherwise variables in large units would be
unfairly penalized less (`glmnet` standardizes by default).

---

## Problem 3 — Double-dipping / post-inference

**(a)** **Double-dipping** = using the **same data twice** — first to **select** which variables enter the
model, then to **test/estimate** those same variables. The two "dips" are **selection** and **inference**
on one dataset. Because selection cherry-picks variables that look good **in this sample**, the follow-up
inference is **over-optimistic**: the **Type I error rate is inflated** (you reject true nulls far more
than the nominal 5%), so the p-values are not trustworthy.

**(b)** (i) Generate data where **all true coefficients are 0** — so the **intercept-only model is
genuinely correct** and **no** variable should look significant. (ii) On each of ~1000 simulated datasets:
**forward-select** up to 3 variables using **adjusted R²**, then run an **F-test** on the selected model
using the **same** data. (iii) Punchline: the F-test **wrongly rejects H0 in a large fraction** of
datasets — the Type I error rate is **badly inflated** (should be ~5%, comes out much higher), because
selecting on the data inflated adj R², which then fooled the test. **The fix — split the data** (select on
one part, test on a separate part) **restores the Type I error to ~5%.**

**(c)** **False.** It is true that **postLASSO** — refitting ordinary LS on the LASSO-**selected**
variables — gives **unbiased** coefficients (it removes the shrinkage bias). **But** you **still cannot
report valid inference from the same data**, because the variables were **selected using that data** — the
same double-dipping sin, and it still inflates the Type I error. For valid postLASSO inference you must
**split the data** (select on one part, infer on another).

**(d)** **Takeaway:** you **cannot select variables and do valid inference on the same data** (selection
inflates significance). **Remedy:** **split the data** — select the model on one part and fit/test it on a
separate, untouched part.
