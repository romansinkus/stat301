# STAT 301 — Tools & Equations Reference (cumulative, Topics 1–9)

*Every model, metric, test, interval, and diagnostic from the course, grouped by category. Plain-text
math (no LaTeX) so it prints clean on the CLI. Notation: β = true parameter, b̂ = estimate, e = error,
ŷ = fitted, ȳ = sample mean, n = #obs, k = #coefficients (incl. intercept), p = #predictors, σ = error
SD, r = correlation, λ = Poisson mean, φ = dispersion parameter.*

---

## 1. MODELS (the model equation + how it's fit)

| Tool | Full name | Equation | When to use | R command | vs. others |
|---|---|---|---|---|---|
| SLR | Simple Linear Regression | `E[Y\|X] = β0 + β1X`; obs `Y = β0+β1X+e` | 1 continuous predictor, continuous Y | `lm(y ~ x)` | MLR = many predictors |
| MLR (additive) | Multiple Linear Regression | `Y = β0+β1X1+…+βpXp+e` | 2+ predictors, effects don't interact → parallel lines | `lm(y ~ x1 + x2)` | interaction = non-parallel |
| Interaction model | — | `Y = β0+β1D+β2X+β3(D·X)+e` | one predictor's effect **depends on** another; ref slope β2, other β2+β3 | `lm(y ~ x * d)` | can't say "holding constant" |
| Logistic | Logistic Regression | `log(p/(1−p)) = β0+β1X`; `p = e^L/(1+e^L)` | **binary** 0/1 response | `glm(y ~ x, family=binomial)` | Poisson = counts |
| Poisson | Poisson Regression | `log(λ) = β0+β1X`; `λ = e^L` | **count** response (0,1,2,…) | `glm(y ~ x, family=poisson)` | logistic = binary |
| GLM | Generalized Linear Model | `g(E[Y]) = β0+β1X+…` (g = link) | umbrella: pick link by response type | `glm(…, family=…)` | linear = identity link |
| LASSO | Least Absolute Shrinkage & Selection Operator | min `RSS + λ·Σ\|βj\|` (L1) | selection + shrinkage; p large vs n; prediction | `glmnet(x, y, alpha=1)` | ridge never hits 0 |
| Ridge | Ridge Regression | min `RSS + λ·Σβj²` (L2) | shrinks all coefficients; multicollinearity remedy | `glmnet(x, y, alpha=0)` | LASSO selects, ridge doesn't |
| Stepwise | Stepwise Selection | greedy add/drop by AIC | quick variable search (forward/backward/both) | `step(model)` / `stepAIC()` | LASSO shrinks smoothly |

---

## 2. ESTIMATION METHODS (how coefficients are chosen)

| Tool | Full name | What it does | When | R command | vs. others |
|---|---|---|---|---|---|
| LS | Least Squares | pick b's to **minimize RSS** = `Σ(y−ŷ)²`; closed-form | linear models (`lm`) | `lm()` | = MLE for Normal errors |
| MLE | Maximum Likelihood Estimation | pick b's to **maximize likelihood**; iterative (may not converge) | GLMs (`glm`) | `glm()` | no closed form; LS special case |
| Bootstrap | Bootstrapping | **resample WITH replacement** (size n), refit many times → sampling dist. | non-Normal errors / small n / no SE formula (median, r) | `infer` / manual loop | theory-CI assumes a shape; bootstrap builds it |

---

## 3. GOODNESS-OF-FIT & ERROR METRICS

| Tool | Full name | Equation | When to use | R command | vs. others |
|---|---|---|---|---|---|
| RSS | Residual Sum of Squares (= SSE) | `Σ(yᵢ−ŷᵢ)²` | leftover error; what LS minimizes | — | sum (grows with n) |
| TSS | Total Sum of Squares | `Σ(yᵢ−ȳ)²` | total variation (null model) | — | `= ESS+RSS` (intercept+LS) |
| ESS | Explained Sum of Squares | `Σ(ŷᵢ−ȳ)²` | variation the model explains | — | — |
| R² | Coefficient of Determination | `1 − RSS/TSS = ESS/TSS` | % variation in Y explained; **linear only** | `glance()$r.squared` | `= r²` in SLR; always ↑ with predictors |
| adj R² | Adjusted R² | `1 − [RSS/(n−p−1)]/[TSS/(n−1)]` | **compare different-sized** linear models | `glance()$adj.r.squared` | can ↓ (penalizes size); linear only |
| RSE | Residual Standard Error (= σ̂) | `√(RSS/(n−p−1))` | estimates **σ**; feeds coefficient SEs; error size in Y's units | `glance()$sigma` | in Y units (has √); vs MSE = squared |
| MSE | Mean Squared Error | `(1/n)·Σ(yᵢ−ŷᵢ)²` | **prediction** quality; **test MSE** = honest | `mean((y−pred)^2)` | squared units; for model selection |
| Deviance | Deviance | `−2·(logLik_model − logLik_saturated)`; "RSS for GLMs" | GLM fit; null vs residual deviance | `glance()$deviance`, `$null.deviance` | lower = better; GLM analog of RSS |
| AIC | Akaike Information Criterion | `−2·logLik + 2k` | model selection; estimates out-of-sample error | `AIC()`, `glance()$AIC` | **works for linear + GLM**; smaller better |
| BIC | Bayesian Information Criterion | `−2·logLik + log(n)·k` | model selection, heavier penalty | `BIC()`, `glance()$BIC` | favors smaller models than AIC; NA for quasi |
| r | (Pearson) Correlation | `cov(x,y)/(sx·sy)`; range −1..1 | strength+direction of linear association (a pair) | `cor()`, `get_correlation()` | `R² = r²` in SLR; r has a sign |

---

## 4. HYPOTHESIS TESTS & INFERENCE STATISTICS

| Tool | Full name | Equation | When to use | R command | vs. others |
|---|---|---|---|---|---|
| t-test | coefficient t-test | `t = b̂/SE(b̂) ~ t(n−k)` | test one **linear** coefficient `H0: β=0` | `summary(lm)` | linear (estimates σ² → t) |
| z / Wald | Wald z-test | `z = b̂/SE(b̂) ~ N(0,1)` | test one **GLM** coefficient | `summary(glm)` / `tidy()` | GLM (no σ² → z); large-sample |
| F-test | F-test (nested) | `F = [(RSSr−RSSf)/k]/[RSSf/(n−p−1)] ~ F(k, n−p−1)` | compare **nested LINEAR** models | `anova(m1, m2)`; `glance()` vs null | `F = t²` when p=1; χ² for GLM |
| χ² deviance | Deviance test | `ΔDeviance ~ χ²(d)`, d = #extra params | compare **nested GLMs** | `anova(m1, m2, test="Chisq")` | GLM version of F-test; large-sample |
| ANOVA | Analysis of Variance (F-test) | overall F for a k-level factor | "does this categorical matter at all?" | `anova(lm(y ~ factor))` | doesn't say which group differs |
| CI | Confidence Interval (coefficient) | `b̂ ± 1.96·SE` (95%) | plausible range for true β | `confint(model)` | excludes 0 ⇔ significant |
| p-value | — | P(stat this extreme \| H0 true) | strength of evidence vs H0 | (in `summary`) | ≠ effect size; report "<0.001" |

**Equivalence (all one story at 5%):** `\|z\| or \|t\| > 1.96  ⇔  95% CI excludes 0  ⇔  p < 0.05` (⇔ odds/rate-ratio CI excludes **1**).

---

## 5. INTERVALS — prediction uncertainty

| Tool | Full name | Targets | Sources of uncertainty | Width | R command | Interpret with |
|---|---|---|---|---|---|---|
| CIP | Confidence Interval for the Prediction | the **average** `E[Y\|X]` | ONE (wobble in b̂) | narrower | `predict(m, interval="confidence")` | "**confidence**" (fixed target) |
| PI | Prediction Interval | an **actual new** `Y` | TWO (b̂ wobble **+** error e) | wider (`+σ²`) | `predict(m, interval="prediction")` | "**probability**" (random target) |
| Bootstrap CI | percentile CI | true parameter | resampling spread | data-driven | 2.5/97.5 percentiles of resamples | "confidence" |

**Both bands** are narrowest at `x̄`, flare at the extremes; `geom_smooth(se=TRUE)` draws the **CIP** band (not the PI). **PI ⊃ CIP always.**

---

## 6. DIAGNOSTICS

| Tool | Full name | What / equation | Checks | R command | Bad sign |
|---|---|---|---|---|---|
| Residual plot | residuals vs fitted | ê = y − ŷ vs ŷ | **L** (linearity) & **E** (equal var) | `plot(model, 1)` | curve (L), funnel (E) |
| Q-Q plot | Quantile–Quantile | residual quantiles vs Normal quantiles | **N** (normality) | `plot(model, 2)` | points off the diagonal |
| VIF | Variance Inflation Factor | `VIF_j = 1/(1−R²_j)` | multicollinearity (among predictors) | `vif(model)` | > 5 (or 10) |
| GVIF | Generalized VIF | compare `GVIF^(1/(2·Df))` to √5≈2.23 | multicollinearity for **categoricals** | `vif(model)` (car) | `GVIF^(1/2Df) > √5` |
| Dispersion φ | dispersion / overdispersion | `Var(Y) > mean-implied` (`p(1−p)` or `λ`) | over/under-dispersion | `glm(family=quasibinomial/quasipoisson)` | φ ≫ 1 (SEs too small) |
| LINE | Linearity/Independence/Normality/Equal-var | assumptions on e: `e ~ iid N(0,σ²)` | the linear-model assumptions | (plots + design) | I & E break SEs; L breaks model |

**Overdispersion fix:** refit `quasi…`, SEs get **×√φ** (φ≈1 → no change; Titanic 0.98, Bikeshare 90.6); **estimates unchanged**. Quasi has no likelihood → AIC = NA.

---

## 7. KEY EQUATIONS / QUANTITIES (the by-hand calc bank)

| Quantity | Equation | Notes |
|---|---|---|
| Slope | `b̂1 = r·(Sy/Sx) = Σ(x−x̄)(y−ȳ)/Σ(x−x̄)²` | sign(slope) = sign(r) |
| Intercept | `b̂0 = ȳ − b̂1·x̄` | line passes through (x̄, ȳ) |
| SE of slope | `SE(b̂1) = RSE/√Σ(x−x̄)²` | ↑ noise → ↑SE; ↑n or ↑X-spread → ↓SE |
| Noise estimate | `σ̂² = RSS/(n−k)` (SLR: n−2) | `σ̂ = RSE` |
| Degrees of freedom | `df = n − k` | divisor in σ̂²; sets t shape |
| # dummy variables | `L − 1` (L = #levels) | reference level dropped |
| # interaction coefs | (coefs of A) × (coefs of B) | e.g. 3-level × continuous = 2 |
| Predict (linear) | `ŷ = b̂0 + b̂1x1 + …` (drop e) | flag extrapolation outside data |

---

## 8. SCALE CONVERSIONS (GLM interpretation)

| From → To | Logistic (binary) | Poisson (count) |
|---|---|---|
| Linear predictor `L` | `L = b̂0+b̂1x+…` = **log-odds** | `L` = **log-mean** |
| Exponentiate `e^L` | **odds** `= p/(1−p)` | **mean** `λ` |
| Back to prediction | `p = e^L/(1+e^L)` (probability, S-curve) | `λ = e^L` (mean count) |
| Coefficient `e^β` | **odds ratio** | **rate ratio** |
| Percent change | `(e^β−1)·100` if OR>1; `(1−e^β)·100` if <1 | same rule on the mean count |
| Significance | CI excludes **0** (log-odds) ⇔ **1** (odds) | CI excludes 0 (log-mean) ⇔ 1 (rate) |
| `predict(type=)` | `"link"`=log-odds, `"response"`=probability | `"link"`=log-mean, `"response"`=count |

**Log-transformed linear models** (Topic 3 fix): `log(Y)~X` → +1 unit X ≈ `100·b %` change in Y (exact `(e^b−1)·100`); `Y~log(X)` → +1% X → `b/100` change in Y; `log(Y)~log(X)` → b = **elasticity** (+1% X → ~b% Y).

---

## 9. WHICH TOOL WHEN — quick decision guide

| Situation | Use |
|---|---|
| Continuous Y | linear regression (`lm`, LS) |
| Binary 0/1 Y | logistic (`glm binomial`) |
| Count Y | Poisson (`glm poisson`) |
| "Is one coefficient ≠ 0?" | t-test (linear) / z-Wald (GLM) |
| "Does this block of predictors help?" (linear) | F-test, `anova(m1,m2)` |
| "Does this block help?" (GLM) | χ² deviance test, `anova(…, test="Chisq")` |
| "Which categorical matters overall?" | ANOVA F-test |
| Compare models of different sizes | adj R² (linear) or **AIC/BIC** (both) |
| One model's fit (linear) | R², RSE | 
| One model's fit (GLM) | deviance, AIC |
| Pick variables / shrink coefficients | LASSO (selects) / ridge (shrinks) / stepwise |
| Tune λ | cross-validation (`cv.glmnet`) → `lambda.min` / `lambda.1se` |
| Select **and** infer | split the data (avoid double-dipping) |
| Predict the **average** at X | CIP (`interval="confidence"`) |
| Predict **one actual** Y at X | PI (`interval="prediction"`) |
| Check assumptions | residual plot (L,E), Q-Q (N), design (I), VIF (collinearity), dispersion (over/under) |
| Non-Normal errors / small n / no SE formula | bootstrap |
