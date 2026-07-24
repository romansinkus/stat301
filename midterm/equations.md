# Equations — STAT 301 Midterm

*Every equation you need for Topics 1–3, with what each is **for.** The exam is interpretation-heavy with
**simple calculations** (calculator allowed), so the ones you'll actually compute are flagged
**[CALC]**. Course convention: inference uses the **standard Normal (z ≈ 1.96)** since t ≈ Normal.*

---

## Notation key

| Symbol | Meaning |
|---|---|
| `Y`, `X` | response (continuous) and predictor |
| `β0, β1, …` | **true** (population) coefficients — unknown |
| `b̂0, b̂1, …` (or β̂) | **estimated** coefficients (from the sample) |
| `ε_i` (epsilon) | **error** term (true, unobservable) |
| `ê_i` | **residual** (observed − fitted) |
| `ŷ_i` | fitted / predicted value |
| `x̄, ȳ` | sample means · `s_x, s_y` | sample SDs |
| `n` | sample size · `k` | # coefficients (incl. intercept) · `p` | # predictors |
| `σ, σ²` | error SD / variance · `σ̂` | its estimate (residual standard error) |

---

# TOPIC 1 — SIMPLE LINEAR REGRESSION

## The model & the line
```
Population model:   Y_i = β0 + β1·X_i + ε_i
Regression line:    E[Y|X] = β0 + β1·X        (the conditional AVERAGE of Y)
Fitted line:        ŷ_i = b̂0 + b̂1·x_i         (uses estimated coefficients)
```
- **For:** the model is the assumed data-generating process; the line is the average of Y at each X; the
  fitted line is what `lm()` gives you.

## Residual  [CALC]
```
ê_i = y_i − ŷ_i = y_i − (b̂0 + b̂1·x_i)
```
- **For:** the vertical gap between an observed point and the fitted line. Observable stand-in for `ε_i`.

## Least squares (how the line is fit)
```
Minimize   SSR = Σ (y_i − ŷ_i)²      (sum of squared residuals; a.k.a. SSE / RSS)
```
- **For:** the criterion that defines the "best" line — smallest total squared vertical miss.

## LS estimators  [CALC]
```
b̂1 = Σ(x_i − x̄)(y_i − ȳ) / Σ(x_i − x̄)²        (slope)
b̂0 = ȳ − b̂1·x̄                                  (intercept)
b̂1 = r · (s_y / s_x)                            (slope ↔ correlation)
```
- **For:** computing the coefficients by hand if given sums/means. Note the slope shares the **sign of r**.

## Correlation coefficient  [CALC]
```
r = Σ(x_i − x̄)(y_i − ȳ) / √[ Σ(x_i − x̄)² · Σ(y_i − ȳ)² ]
  = cov(x, y) / (s_x · s_y)
```
- **For:** strength + direction of **linear** association, `−1 ≤ r ≤ 1`. (Tut 03 rule: `|r| > 0.6` = "high"
  for spotting multicollinearity.) `r ≈ 0` ⇒ no *linear* association (could still be nonlinear).

## Estimating the noise (residual standard error)
```
σ̂² = SSR / (n − k)      (for SLR, k = 2 ⇒ σ̂² = SSR/(n−2))
σ̂  = √(σ̂²)              (residual standard error)
```
- **For:** σ̂ estimates the scatter of points around the line; it feeds the SE below.

## Standard error of the slope
```
SE(b̂1) = σ̂ / √[ Σ(x_i − x̄)² ]
```
- **For:** the sample-to-sample **wobble of the estimate**. ↓ with more data / more X-spread; ↑ with more
  noise (σ̂). NOT the scatter of points (that's σ̂).

## Test statistic  [CALC]
```
z = (b̂1 − 0) / SE(b̂1) = b̂1 / SE(b̂1)     (test of H0: β1 = 0)
general:  z = (b̂ − β_null) / SE(b̂)
```
- **For:** how many SEs the estimate sits from the null value. **|z| > 1.96 ⇒ reject H0 at 5%.**
  (Strictly a t with n−k df; course uses Normal.)

## Confidence interval  [CALC]
```
b̂ ± z*·SE(b̂)      z* = 1.96 (95%),  1.645 (90%),  2.576 (99%)
Bootstrap CI:  [2.5th, 97.5th] percentiles of resampled estimates   (95%)
```
- **For:** a plausible range for the true parameter. CI excludes 0 ⇔ |z|>1.96 ⇔ p<0.05.

## (Optional) R² — goodness of fit
```
SST = Σ(y_i − ȳ)²   (total)      SSR = Σ(y_i − ŷ_i)²   (residual)
R² = 1 − SSR/SST     (fraction of variation in Y explained by the model)
```
- **For:** overall fit, `0 ≤ R² ≤ 1`. (Used inside VIF below.)

---

# TOPIC 2 — MULTIPLE LINEAR REGRESSION

## The model
```
Y = β0 + β1·X1 + β2·X2 + … + βp·Xp + ε
```
- **For:** many predictors (continuous and/or categorical). Fit by least squares (same SSR criterion).

## Counting  [CALC]
```
# dummies for an L-level categorical = L − 1
# interaction coefficients = (coefs of A) × (coefs of B)
degrees of freedom = n − k          (k = total coefficients incl. intercept)
```

## Two-level categorical  (D = 0/1 dummy)
```
Y = β0 + β1·D
   reference group (D=0):  mean = β0
   other group    (D=1):  mean = β0 + β1        (β1 = difference of means)
```

## Additive model (categorical + continuous) — PARALLEL lines
```
Y = β0 + β1·D + β2·X
   reference line (D=0):  Y = β0        + β2·X
   other line     (D=1):  Y = (β0+β1)   + β2·X
```
- β0 = ref intercept · β1 = intercept gap · **β2 = common slope (both groups).**

## Interaction model (categorical × continuous) — NON-parallel lines  [CALC]
```
Y = β0 + β1·D + β2·X + β3·(D·X)
   reference line (D=0):  Y = β0        + β2·X                 slope = β2
   other line     (D=1):  Y = (β0+β1)   + (β2+β3)·X            slope = β2 + β3
```
- β2 = **reference-group slope** · β3 = **slope gap** · other group's slope = **β2 + β3**
  · β1 = intercept gap.

## Prediction  [CALC]
```
ŷ = b̂0 + b̂1·x1 + b̂2·x2 + …        (plug in the X values; drop ε — it averages to 0)
```
- **For:** the predicted **average** Y at given X's. For a group line, use that group's intercept & slope.

---

# TOPIC 3 — ASSUMPTIONS, MULTICOLLINEARITY

## The LINE assumptions (stated about the errors)
```
L: E[Y|X] = β0 + β1·X        (mean is linear in the parameters; E[ε]=0)
I: ε_i are independent
N: ε_i ~ Normal
E: Var(ε_i) = σ²  for all i   (constant variance — homoscedasticity)
```
- **For:** the conditions inference relies on; check with residuals-vs-fitted (L, E) and Q-Q (N).

## Variance Inflation Factor  [CALC]
```
VIF_j = 1 / (1 − R²_j)
   R²_j = R² from regressing predictor X_j on ALL the other predictors
```
- **For:** how much predictor j's SE² is inflated by multicollinearity. **VIF > 5 (or 10) = concerning.**
  `VIF = 1` ⇒ no multicollinearity.

## Generalized VIF (for categorical predictors)  [CALC]
```
compare   GVIF^(1/(2·Df))   to   √5 ≈ 2.23   (or √10 ≈ 3.16)
equivalently: square that column and compare to 5 (or 10)
```
- **For:** the VIF analog when a predictor has multiple dummy columns (`Df` = its degrees of freedom).

---

# QUICK EXAM CALCULATIONS (the ones you'll actually do)

```
Predicted value:     ŷ = b̂0 + b̂1·x
Residual:            ê = y − ŷ
Test statistic:      z = b̂ / SE(b̂)          reject H0 if |z| > 1.96
Confidence interval: b̂ ± 1.96·SE(b̂)         significant if it excludes 0
Group slope (inter): β2 + β3                 (other group; reference = β2)
Group mean (2-lvl):  β0 (ref),  β0+β1 (other)
Dummies:             L − 1
VIF flag:            VIF > 5 (or 10)   |   GVIF^(1/(2Df)) > √5 ≈ 2.23
```

*Note: these are the equations the course actually uses. It emphasizes **interpretation** over derivation,
so you won't be asked to derive the LS formulas — but you should be able to **plug numbers into** the
boxed calculations above and **read what each equation means.***
