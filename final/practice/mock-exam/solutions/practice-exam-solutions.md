# Solutions — Comprehensive Final Practice Exam (Topics 1–9)

*Questions: [`../practice-exam.md`](../practice-exam.md).*

> Marking scheme: **70% for correct procedures, 30% for correct answers.**

---

## Problem 1 — Linear regression on `homes`

**(a)** (i) "Holding waterfront status and neighbourhood constant, each additional square metre of area is
associated with about **\$2,450** more in price, on average." (ii) **Significant:** the 95% CI
`(2100, 2800)` **excludes 0** and `p ≈ 0 < 0.05` — equivalent statements. (iii) *Incorrect:* "each extra
m² **causes** the price to rise \$2,450" — asserts **causation** from observational data; we can only claim
**association**.

**(b)** (i) `ESS = TSS − RSS = 8.0e12 − 2.4e12 = 5.6e12`; `R² = 1 − RSS/TSS = 1 − 0.30 =` **0.70**.
(ii) "The model explains about **70%** of the total variation in price." (iii) (1) `R²` **always increases**
when you add a predictor (even a useless one), so a higher `R²` alone cannot justify adding one — use
**adjusted `R²`** (or AIC); (2) `R²` is **in-sample** and **not a significance test** (no sampling
distribution) — use an **F-test** to tell whether the extra predictor significantly helps.

**(c)** (i) `H0:` the coefficients on **waterfront and neighbourhood are all 0** (the extra block adds
nothing beyond `area`); `H1:` at least one is nonzero. (ii) The models must be **nested** — the reduced
model's predictors (`area`) are a **subset** of the full's. (iii) `p = 3e-06 < 0.05` ⇒ **reject H0**: the
extra variables **significantly improve the fit**. It does **not** prove the model **predicts well**, nor
that **every** added variable matters.

**(d)** **Significance** (small p / CI excludes 0) only says an effect **is not exactly 0** — it can be
tiny and useless. **Good prediction** is about out-of-sample error (test MSE / interval width).
**Causation** requires the **design** (randomization), not any p-value or `R²`. A result can be
significant yet predict poorly and imply nothing causal.

---

## Problem 2 — Logistic regression on `loans`

**(a)** (i) **No** — a GLM has **no additive error term `e`**; we model a *function of the conditional
expectation* (the log-odds) directly, and the randomness is carried by the Bernoulli distribution of `Y`.
Coefficients are estimated by **maximum likelihood (MLE)** via an **iterative algorithm** (Fisher
scoring); there is no closed form because the likelihood equations are nonlinear in the coefficients.
(ii) The **log-odds** scale.

**(b)** (i) (1) **Range:** a probability must stay in (0,1), but a linear predictor runs over all reals and
would predict impossible values; the log-odds is unbounded, so it can match the linear part. (2)
**Constant effect:** on the probability scale the effect of `X` is not constant (the S-curve flattens near
0 and 1), but on the log-odds scale it is a **constant slope**. **Yes**, we convert back to probability for
**prediction** (`p = e^L/(1+e^L)`); we just do not *model* on it. (ii) Odds ratio `= e^(−0.08) ≈ 0.923`;
percent change `= (0.923 − 1)×100 ≈` **−7.7%** — "each extra \$1000 of income is associated with about a
**7.7% decrease in the odds** of default." (iii) Compute the **log-odds** `L = b0 + b1·income` for that
borrower, then convert with `p = e^L / (1 + e^L)`.

**(c)** (i) **Yes** — in an **additive** logistic model the `income` slope (log-odds scale) is the **same
for owners and renters** (only the intercept differs), so a single "holding homeownership constant" income
effect exists and `e^b_income` applies to both. (ii) The homeowner income odds ratio is
`e^(b_income + b_interaction) = e^b_income · e^b_interaction` — a **product** because adding on the
**log-odds** scale becomes multiplying on the **odds** scale (`e^(a+b) = e^a·e^b`). (iii) **No.** An
additive logistic model is **parallel on the log-odds scale**, but the logit→probability S-curve
**squashes** those parallel lines, so the fitted **probability** curves look non-parallel even with no
interaction. Parallelness lives on the log-odds scale.

**(d)** (i) **No** `R²` — `R²`/adj `R²`/RSE/MSE/F-test are **linear-model only**. Use the **deviance**
(null vs. residual deviance) or **AIC**. For two nested logistic models the **deviance χ²-test** replaces
the F-test: statistic = the **difference in deviance**, `~ χ²(d)` with `d` = difference in number of
predictors; R command **`anova(reduced, full, test = "Chisq")`**. (ii) (1) The response is **0 or 1**, so
raw residuals collapse onto **two parallel lines** (`−p̂` and `1−p̂`) — not a model defect. (2) The
variance **`p(1−p)` is not constant**, so residuals are not comparable across observations. Rely on
**overdispersion** instead.

---

## Problem 3 — Poisson regression on `clinic`

**(a)** (i) "Holding age constant, having a chronic condition is associated with a **+0.55 change in the
log-mean** number of visits." (ii) `e^0.55 ≈ 1.73` → visits **× 1.73**, a **+73%** change. (iii)
`3 × 1.73 ≈` **5.2 visits** (multiplicative effect).

**(b)** (i) A dispersion of **6.4** (vs. ideal ≈ 1) indicates **overdispersion** — the Poisson
"mean = variance" assumption fails. It damages the **standard errors / p-values** (too small), **not** the
point estimates. (ii) Because the assumed distribution *fixes* the variance (Poisson `λ`), the model's
built-in dispersion is exactly 1. The dispersion parameter is the **ratio actual variance ÷ assumed
variance**, so **η = 1 means the data's spread matches the model's assumption**; η > 1 = overdispersion.

**(c)** R only builds dummy variables from **factors**. If `neighbourhood` is stored as numbers 1–4 and you
do not `factor()` it, `glm`/`lm` treats it as **continuous** and fits **one meaningless slope on the
codes** (pretending the categories are evenly spaced numeric values) instead of separate dummies.

**(d)** The linear predictor is additive: `log-mean = b0 + b1x1 + b2x2 + …`. **Exponentiating** to get the
mean turns sums into products because **`e^(a+b) = e^a · e^b`** — so each `e^bj` becomes a **multiplicative**
factor (rate ratio) on the count scale. Same model, two scales.

---

## Problem 4 — Model selection & prediction uncertainty (`homes`)

**(a)** (i) LASSO **shrinks coefficients continuously**, driving some to **exactly 0** (dropping them) — it
**selects variables smoothly** rather than in greedy all-or-nothing jumps, and selects + trains at once.
(ii) At **`λ = 0`** there is no penalty, so you get back the **ordinary least-squares** estimates. (iii)
`lambda.min` = the `λ` with the **smallest cross-validated MSE**; `lambda.1se` = the **largest** `λ` whose
CV MSE is still **within 1 SE** of the minimum. Prefer `lambda.1se` for a **simpler model / more
shrinkage** at almost no cost in predictive error.

**(b)** **`k`-fold CV:** split the training data into `k` equal folds, then `k` times train on `k−1` folds
and test on the held-out fold (every observation tested once), and average the `k` error estimates. In a
LASSO fit (`cv.glmnet`) it is used to **choose the penalty `λ`** (`lambda.min` or `lambda.1se`).

**(c)** (i) The **post-inference / double-dipping** problem — selecting and inferring on the **same data**;
the **Type I error rate is inflated** (you reject true nulls far more than the nominal 5%). (ii) The
simulation was rigged so **no variable truly matters** (`H0` is actually true), so a correct test should
reject only about **5%** of the time; rejecting *far more often* (many small p-values) means the procedure
is **flagging pure noise as significant** — inflated false positives. You want the rejection rate near
**5%**. (iii) **Split the data:** select the model on one part and fit/test it on a separate, untouched
part.

**(d)** (i) `(590k, 650k)` = **CIP** (`interval = "confidence"`); `(410k, 830k)` = **PI**
(`interval = "prediction"`) — the PI is wider. (ii) **CIP:** "With **95% confidence**, the **average** price
of 200 m² houses is between **\$590k and \$650k**." **PI:** "With **95% probability**, the price of **a
single** 200 m² house is between **\$410k and \$830k**." (iii) The client cares about **one actual house**,
so quote the **PI** — it includes the individual error `e`; the CIP would understate their uncertainty.

---

## Problem 5 — The unifying picture

**(a)** (i) Price → **linear regression** (`lm`, or `glm` `gaussian`), **identity** link. Default 0/1 →
**logistic** (`glm`, `binomial`), **logit** link. Visits (count) → **Poisson** (`glm`, `poisson`), **log**
link. (ii) All three are the **same linear predictor `b0 + b1X1 + …`**, wrapped in a **link function** of
`E[Y|X]`: identity (mean), logit (log-odds), log (log-mean). **What changes** is the scale of
interpretation (and that GLMs use MLE, have no `e`, and exponentiate to a multiplicative scale); **what
stays the same** is every structural skill — adding predictors, dummies, additive vs. interaction,
large-sample (Wald) inference.

**(b)** Both compare **nested** models by measuring how much fit improves when you add terms: the
**F-test** uses the drop in **RSS** (`~ F`) for **linear** models; the **deviance test** uses the drop in
**deviance** (`~ χ²`) for **GLMs** — same workflow (`anova(reduced, full, …)`), different fit measure and
reference distribution.

**(c)** (i) **CIP** predicts the **average** `E[Y|X]` (one source of uncertainty); **PI** predicts an
**actual new** `Y` (two sources: estimation **+** the individual error `e`). The **PI is wider**. (ii)
**False.** A GLM has no *additive* `e`, but there is still randomness — it is **built into the response's
distribution** (Bernoulli for logistic, Poisson for counts): `Y` is a random draw whose *mean* we model via
the link. GLMs are estimated by **maximum likelihood (MLE)**, not least squares.
