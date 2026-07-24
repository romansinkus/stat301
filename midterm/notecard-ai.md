# Notecard (one letter-size sheet, front + back)

*Copy-paste the sections below into your physical cheat sheet, organized as **Topic 1 / Topic 2 /
Topic 3 / General**. Dense on purpose — trim what you know cold. Exam is written-answer, closed-book
except this sheet; **show key steps (70% of marks).** Inference uses the **standard Normal (z)** (t ≈ Normal).*

---

# TOPIC 1 — SIMPLE LINEAR REGRESSION

## T1.1 — The model
- Regression models the **average of Y given X**: `E[Y|X] = b0 + b1*X` (the line = conditional mean).
  One observation: `Y_i = b0 + b1*X_i + e_i` (off the line by error `e_i`).
- **b1** = expected change in Y per **+1 X**; **b0** = mean Y at X=0. Interpret with **"associated with"**
  (never "causes"/"effect of" on observational data).
- Fitted line valid only **within the observed range of X** (no extrapolation).

## T1.2 — Least squares & residuals
- **LS:** choose `b`'s to minimize **SSR = Σ(y_i − ŷ_i)²** (squared **vertical** distances; squaring
  removes signs + punishes big misses).
- **Error `e_i`** = true, population, unknowable (omitted variables + noise).
  **Residual `= y_i − ŷ_i`** = sample, observable, stand-in for `e_i`. Differ because `b_hat ≠ b`.

## T1.3 — Inference (SE, tests, CIs)
- **SE(b_hat)** = SD of the sampling distribution of `b_hat` = sample-to-sample **wobble of the estimate**
  (NOT the scatter of points around the line).
- **Sampling distribution** = distribution of **b_hat** (the estimator) — not of Y, true b, or X.
- **Test** `H0: b1=0` vs `H1: b1≠0`: **z = b_hat / SE**, compare to standard Normal.
- **THE EQUIVALENCE (5%):** 95% CI excludes 0 ⇔ **|z| > 1.96** ⇔ **p < 0.05** ⇒ reject H0.
- **CI** `b_hat ± 1.96·SE`. Correct reading: *"across many samples, 95% of such intervals contain the
  true b"* — NOT "95% probability the truth is in this fixed interval."
- **p-value:** small p = **strong evidence** vs H0, NOT a big effect, NOT P(H0 true). Report "< 0.001".

## T1.4 — Bootstrap
- Resample your one sample **with replacement**, **same size n**, refit many times (e.g. B=10 000);
  spread ≈ sampling distribution. **Percentile CI:** 2.5/97.5% (95%), 5/95% (90%).
- For **non-Normal errors / small n** ⇒ more reliable SEs. Must be **with replacement** (not fresh
  population samples).

---

# TOPIC 2 — MULTIPLE LINEAR REGRESSION

## T2.1 — Form & categoricals
- `Y = b0 + b1*X1 + ... + bp*Xp + e`. Y **always continuous**; predictors continuous or categorical.
- Factor with **L levels ⇒ L−1 dummies**; left-out = **reference** (default first alphabetically;
  `relevel()` to change). Must be a **factor** or `lm` won't dummy-code (`factor()`).
- **k-level categorical:** `b0`= reference mean; each `b`= that level **minus reference**.
- MLR coefficient = effect **"holding the other predictors constant."**

## T2.2 — ANOVA
- **`anova(model)`** = one **joint F-test** for a whole categorical variable (or interaction block):
  `H0: all group means equal` vs `H1: at least one differs`. Small p ⇒ variable associated with Y
  (doesn't say *which* pair — use the coefficient table).

## T2.3 — Additive vs. Interaction (interpretation)

| Model | Form | Coefficients |
| --- | --- | --- |
| Additive (cat+cont) | `Y=b0+b1D+b2X` | **parallel lines**: `b0`=ref intercept, `b1`=intercept gap, `b2`=**common slope** |
| Interaction (cat×cont) | `Y=b0+b1D+b2X+b3DX` | `b2`=**ref slope**, `b3`=**slope gap**, other slope=**b2+b3**; non-parallel |

- **Additive** ⇒ "holding constant" holds at *any* value. **Interaction** ⇒ **cannot** say "holding
  constant"; effect of X **depends on the group**.
- Interaction adds coefs = (coefs A)×(coefs B). 2-level cat × continuous ⇒ +1 coef.
- Interaction row tests `H0: b3=0` = "**same slope** both groups." Fail to reject ⇒ use **additive** model.
- Main continuous coef = **reference group's slope only** (other = b2+b3). Interaction = **two SLRs in one**.

---

# TOPIC 3 — DIAGNOSTICS, MULTICOLLINEARITY & CAUSALITY

## T3.1 — LINE assumptions

| | Assumption | Diagnose | If violated |
| --- | --- | --- | --- |
| **L** | E[Y\|X] linear (in parameters) | residuals-vs-fitted: want no pattern | model misspecified/dubious |
| **I** | errors independent | study design / residual runs | **SEs biased ⇒ CIs & tests invalid** |
| **N** | errors Normal | Q-Q plot (on diagonal); histogram | **least severe** — CLT / bootstrap save you |
| **E** | equal variance (homoscedastic) | residuals-vs-fitted: **funnel = bad** | **SEs wrong ⇒ CIs & p invalid** |

- Point estimates stay OK under I/E/N; it's the **SEs** that break (**I & E**).
- **Fixes:** `X²`/`log` predictor for L; **transform Y (`log Y`,`√Y`)**/WLS for E; transforms/CLT/bootstrap
  for N; time-series methods for I. "Linear" = linear **in the parameters** (`X²` still linear regression).
  `lm` assumes assumptions — **checking them is YOUR job.**

## T3.2 — Multicollinearity
- **Def:** predictors correlated **with each other** (NOT with Y) ⇒ overlapping info ⇒ can't isolate
  individual effects. Perfect ⇒ `NA` coef. Can involve a **combination** of several predictors.
- **Consequence:** **inflates SEs** ⇒ wider CIs, harder to reject H0. Estimates ~unbiased, R² can stay high.
- **Diagnose:** pairwise corr (not enough) + **VIF** (=1 none; >5 or 10 concerning). Categorical ⇒ **GVIF**:
  compare **`GVIF^(1/(2·Df))`** to `√5≈2.23` / `√10≈3.16`.
- **Workflow:** `ggpairs`/heatmap → `lm(y~.)` → `car::vif()` → drop **higher-VIF** var of **most-correlated
  pair** → recheck VIF.
- **Fixes:** **drop** or **combine**. Dropping one **shifts its correlated partners' coefficients** &
  lowers their p (SE relief); unrelated vars' SEs can *rise*.

## T3.3 — Causality & study designs
- Causal claim depends on **(1) how data collected** + **(2) methods.**
- Threats: **confounder** `C` (`C→X`, `C→Y`), **reverse causality**, **Simpson's paradox** (assoc flips
  within subgroups; UC Berkeley 1973).
- **Observational** ⇒ association only. **Randomized experiment** ⇒ causation (balances **observed AND
  unobserved** confounders).
- **CRD** = randomize freely (gold standard, balances unobserved). **RBD** = block on known nuisance,
  randomize within blocks (balances **observed only**).
- **Two confounder fixes:** (1) **adjust** — put it in the model; works **only if known & measured**.
  (2) **Randomize** — balances **all** confounders, even unknown (no need to model). *Adjust fixes the
  ones you know; randomize fixes them all.* (Obs. alt: **stratify** within confounder subgroups.)

---

# GENERAL (cross-cutting)

## G.1 — Framing
- **Generative modelling:** the regression **approximates the mechanism that generated the data**; the
  `b`'s are unknown true parameters we estimate. SLR = MLR with p=1. (Multiple ≠ Multivariate.)
- **Fixed vs random:** predictors `X` and parameters `b` are **fixed**; only `Y` and `e` are random.
- **Association ≠ causation** (see T3.3). "All models are wrong, but some are useful."

## G.2 — Reading R output & significance
- `estimate`=effect size · `std_error`=wobble · `statistic`=est/SE · `p_value`=evidence ·
  `lower/upper_ci`=CI. (`get_regression_table()` shows 95% CI by default; `tidy()` similar.)
- **Statistical vs practical significance:** statistical = effect ≠ 0 (evidence); practical = **big enough
  to matter** (magnitude). Big n ⇒ tiny effects can be significant. Read **both**.

## G.3 — Worked numbers (quick recall)
- Wage `wage~education`: slope ≈ 0.750, CI (0.596, 0.905), p≈0. `+sex` (additive) ⇒ CI barely moves.
  `education*sex` interaction p≈0.273 ⇒ no slope difference.
- CASchools `read~income`: slope ≈ 1.94, CI (1.75, 2.13). Additive `+grades`: income ≈ 1.93. Interaction
  `*grades`: KK-06 slope 2.02, `income:gradesKK-08` = −0.11 ⇒ KK-08 slope 1.91, p≈0.68 (NS).
- TikTok sim (true = 8): naive `y_obs~x_self_choice` = **9.83** (inflated), adjusted `+athlete` = **7.92**,
  randomized `y_exp~x_randomized` = **8.03**. athlete coef ≈ +5.
- Multicollinearity (CASchools): only `lunch` VIF>5 (5.7); drop it ⇒ all VIF <2.

## G.4 — Common traps
- "causes"/"effect of" on observational data; SE = point scatter; "95% probability truth in this interval";
  main continuous coef = everyone's slope in an interaction; p-value = effect size or P(H0);
  multicollinearity = corr with response (it's **among predictors**); equal-variance "doesn't affect SE"
  (it does); "adjusting for a confounder makes it causal" (only if ALL confounders measured); "dropping a
  collinear var lowers ALL SEs" (only the collinear partners').
