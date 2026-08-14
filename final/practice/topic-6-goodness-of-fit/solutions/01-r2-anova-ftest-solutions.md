# Solutions 01 (Topic 6) — Goodness of Fit for Linear Models (R², Adjusted R², F-test)

*Questions: [`../01-r2-anova-ftest.md`](../01-r2-anova-ftest.md).*

> Marking scheme: **70% for correct procedures, 30% for correct answers.**

---

## Problem 1 — The variance decomposition and R²

**(a)** The **null model** is `Y = b0 + e` — **no predictors**. Its prediction for every observation is
the **sample mean `ȳ`**. Comparing a fitted model to it asks: **"does using `X` beat simply predicting the
average?"** (does `ŷ`, an estimate of `E[Y|X]`, beat `ȳ`, an estimate of `E[Y]`?).

**(b)**
- **TSS** `= Σ(yᵢ − ȳ)²` — **total** variation in `Y` (residuals from the null model).
- **ESS** `= Σ(ŷᵢ − ȳ)²` — variation the model **explains** (fitted values vs. the mean).
- **RSS** `= Σ(yᵢ − ŷᵢ)²` — variation the model **misses** (the quantity **least squares minimizes**).

Decomposition: **`TSS = ESS + RSS`**, which holds when the model has an **intercept** and is fit by
**least squares**. A good model makes ESS large and RSS small.

**(c)** (i) `ESS = TSS − RSS = 500 − 455 =` **45**. (ii) `1 − RSS/TSS = 1 − 455/500 =` **0.09**;
`ESS/TSS = 45/500 =` **0.09** — they agree. (iii) "The model explains about **9%** of the total variation
in `Y`."

**(d)** In SLR, `R² = r² = 0.3² =` **0.09** → the model explains **9%** of the variation in `Y`. This is
**not necessarily useless**: in noisy **observational** data even 9–20% can be meaningful, and a real
association can have low `R²` simply because many other factors (in the error term) also drive `Y`. Low
`R²` limits *predictive* tightness but does not make the estimated association wrong or uninteresting.

---

## Problem 2 — R²'s caveats, adjusted R², RSE/MSE, AIC

**(a)** (i) `R²` is computed **in-sample (on the training data)** — it says nothing about **out-of-sample**
prediction. (ii) **No** — `R²` is **not a test**; it has **no known sampling distribution**, so you cannot
use it to declare one model "significantly" better. (iii) `R²` **always increases (never decreases)** when
you add a predictor, even an irrelevant one — so a bigger `R²` alone does not mean a better model, and
`R²` **cannot fairly compare models of different sizes** (it tempts overfitting).

**(b)** `adj R² = 1 − [RSS/(n − p − 1)] / [TSS/(n − 1)]`, where `p` = number of covariates (excluding the
intercept). The `n − p − 1` divisor **penalizes extra variables**: each added predictor costs a degree of
freedom, so if it only trims RSS a little, `RSS/(n−p−1)` can **rise**, making adj R² **fall**. Plain R²
cannot fall because it ignores the df cost. **Use adjusted R² to compare models of different sizes.**

**(c)** **RSE (Residual Standard Error)** `= √(RSS/(n − p − 1))` (the `sigma` in `glance()`) — it
**estimates `σ = √Var(e)`**, the size of the irreducible error, and underlies the coefficient SEs.
**MSE** `= (1/n)Σ(yᵢ − ŷᵢ)²`. **Training MSE** uses the data the model was fit on; **testing MSE** uses
**new/held-out** data. **Testing MSE** honestly measures prediction quality, because training MSE is
optimistically biased — the model was tuned to fit *that* data.

**(d)** **AIC** `= (goodness of fit) + (penalty for model size)`; like adjusted R², the size penalty lets
it trade fit against complexity, so it can compare models of **different sizes**. **Smaller AIC = better.**
**BIC** is the same idea with a **heavier** penalty on size (so it favors **smaller** models than AIC).

---

## Problem 3 — The F-test

**(a)** (i) `sigma` = the **residual standard error (RSE)** = `√(RSS/(n−p−1))`, an estimate of the error
SD `σ`. (ii) It is the **overall F-test**, comparing the full model to the **intercept-only (null)**
model; `H0: all slope coefficients = 0` simultaneously (the predictors as a group add nothing). (iii)
`p = 2e-08` is tiny ⇒ **reject H0** — the model as a whole explains significantly more than the mean alone.

**(b)** **Case A** — full vs. the **null (intercept-only)** model: `H0:` *none* of the predictors help
(all slopes = 0 at once); read from **`glance(model)`**. **Case B** — a **nested pair** (reduced ⊂ full):
`H0:` the **extra block** of variables adds nothing (the extra coefficients are all 0); use
**`anova(reduced, full)`**. "**Nested**" means the reduced model's predictors are a **subset** of the
full's. It is required because the F-statistic compares `RSS_reduced − RSS_full`, which is only a
meaningful "improvement from the extra terms" when one model is contained in the other.

**(c)** A significant F-test does **not** establish: (1) that we can **predict `Y` well** — model
significance ≠ good prediction; (2) that a **specific predictor** (here `mRNA`) is useful — the F-test is
about the block/model as a whole. What actually carried the signal was **`gene`**, not `mRNA`: adding
`gene` is what made the bigger model significant, so the significance says nothing good about mRNA's
predictive value.

**(d)** (i) The **t-test** tests **one** coefficient (`βj = 0`); the **F-test** tests **several**
simultaneously (a block, or the whole model). (ii) For the t-test, **the other variables stay in the
model** — it asks "does *this* variable add anything **given the rest**?" (iii) With **`p = 1`** the two
hypotheses are identical and **`F = t²`** with the same p-value.
