# Topic 1: Simple Linear Regression (SLR)

Consolidated notes drawn from the lecture slides (`topic1_..._part1/2.pdf`), the
in-class activities (`activity1.ipynb`, `activity2.ipynb`), and personal notes.

> "Essentially, all models are wrong, but some are useful." — George E. P. Box
> All models in this course are approximations of reality; none will be *true*, but
> hopefully they are still useful.

---

## 1. Relations between variables

STAT 201 mostly estimated/tested **one parameter** of a population (an average income, a
median diameter). STAT 301 studies how one variable **relates to** other variables —
explanatory and predictive modelling.

**Deterministic relation** — the value of one variable is *entirely* determined by another.
No uncertainty.
- Einstein's mass–energy: `E = m·c²`
- Circle area–radius: `A = πr²`

**Stochastic relation** — the outcome of a given input *cannot* be precisely predicted.
There is **uncertainty**, due to other variables not being considered or noise.
- Height vs. weight — taller people tend to weigh more, but with considerable variability.
- Home price vs. square footage.

A stochastic relation includes a **random error term** (ε):
`Weight = β₀ + β₁·Height + ε`
This lets two people with the same height have different weights.

**Our focus is exclusively on stochastic relations.**

### Shape of a relation
Categorized by the form of the model equation:
- Linear: `Weight = β₀ + β₁·Height + ε`
- Quadratic: `A = π·r²`
- Exponential: `N = N₀·e^(−λt)·ε`

---

## 2. Terminology

| Response (Y) | Predictor (X) |
|---|---|
| output variable | feature |
| ~~dependent variable~~ (avoid!) | input variable |
| | covariate |
| | regressor |
| | ~~independent variable~~ (avoid!) |

- The **response** is the variable we're interested in (trying to predict/explain).
- `Xᵢ`, `Yᵢ` = values of X and Y for observation `i`. Think of `n` pairs:
  `(X₁,Y₁), (X₂,Y₂), …, (Xₙ,Yₙ)`.
- The explanatory variable **X is assumed to be fixed** (non-stochastic) for each individual.

---

## 3. The model

The model relating X and Y is the equation of a line **plus an error term**:

```
Yᵢ = β₀ + β₁·Xᵢ + εᵢ
     ▲     ▲        ▲
 intercept slope  error term
```

- **Intercept (β₀):** the value of Y when X = 0 (where the line crosses the Y-axis).
- **Slope (β₁):** how much Y changes for a one-unit increase in X. `β₁ = Δy/Δx`.
- **Error (εᵢ):** captures the variability in the response *not* explained by the model —
  everything the model does not.

### The model as a conditional expectation
The regression line is the **conditional average of Y for a given X**:

```
E[Y | X] = β₀ + β₁·X          ← the regression line (average Y at each X)
Yᵢ = β₀ + β₁·Xᵢ + εᵢ           ← a specific point, off the line (note the error term)
```

So `β₀ + β₁·Xᵢ` is the regression line `E[Y|Xᵢ]`, and adding `εᵢ` gives the actual point `Yᵢ`.

Example: for `Weight = −166 + 140·Height + ε`, a 1.63 m person has
`Weight = 62.2 + ε`. We expect **on average** 62.2 kg; individuals scatter around it. The
line gives the **mean** weight of people of a given height.

### The random errors
We treat `εᵢ` as a random variable:
- **Distribution:** assumed **Normal**.
- **Mean:** safely assumed to be **0**.
- **Variance:** unknown, denoted **σ²** (assumed constant across all errors, and errors
  uncorrelated — "homoscedastic").

### Interpretation of β₀ and β₁
- **Slope:** a 1-unit increase in X is *associated with* an expected change of β₁ in Y.
  Associated with — **not the cause of**.
- **Intercept:** average value of Y when X = 0. Usually we don't care much about it.

> ⚠️ **Association is not causality.** We generally **cannot** conclude that a change in X
> *causes* a change in Y. Causality requires more than a good model. With observational
> data we can only study associations, not cause/effect.

---

## 4. Fitting = estimation (Least Squares)

We never know the true β₀, β₁ — they are population parameters. We **estimate** them from a
sample, producing `β̂₀` and `β̂₁`.

- **Population regression:** `Yᵢ = β₀ + β₁·X + εᵢ`
- **Sample regression:** `Ŷᵢ = β̂₀ + β̂₁·X + eᵢ`
- Note `eᵢ ≠ εᵢ` because `β̂₀ ≠ β₀` and `β̂₁ ≠ β₁`. (This is the residual vs. error-term
  distinction — see Questions.)

**Least Squares** chooses β̂₀, β̂₁ to **minimize the Sum of Squared Errors (residuals)**:
minimize `Σ(yᵢ − (β̂₀ + β̂₁·xᵢ))²`. Solve `dQ/dβ₀ = 0` and `dQ/dβ₁ = 0`.

Estimators (you do **not** need to memorize these):
```
β̂₁ = Σ(Xᵢ − X̄)(Yᵢ − Ȳ) / Σ(Xᵢ − X̄)²
β̂₀ = Ȳ − β̂₁·X̄
```

Relationship to correlation: `β̂₁ = r · (s_y / s_x)`. A positive correlation ⟹ positive slope.

**In R:** fit with `lm()`.
```r
model <- lm(y ~ x, data = df)
```

---

## 5. Inference for the coefficients

**Inference** = generalizing from a single sample to the larger population.

Since `β̂₀`, `β̂₁` are statistics computed from the sample, they are **random variables** with
a **sampling distribution**. Different samples ⟹ different estimates. The spread of an
estimator across samples is its **standard error (SE)** — the SD of its sampling distribution.

- **SD vs SE:** `SD(ȳ) = σ/√n` uses the true σ; `SE(ȳ) = σ̂/√n` uses the estimate. SE is an
  *estimate* of the SD (because σ is unknown).

Sampling distributions (assuming Normal, uncorrelated, equal-variance errors):
```
β̂₀ ~ N(β₀, [SE(β̂₀)]²)
β̂₁ ~ N(β₁, [SE(β̂₁)]²)
```
`σ²` is unknown and estimated from the residuals: `σ̂² = Σeᵢ² / (n−2)`.

**You need two things for inference:** (1) an unbiased estimate, and (2) its uncertainty (SE).
*Unbiased* means `E(β̂₁) = β₁` — the estimate is right on average.

### How do we get the sampling distribution / SE?
Two routes:
1. **Theoretical result** — this is what `lm` does. Requires assumptions (Normal errors, etc.).
2. **Bootstrapping** — resample; no formula/assumptions needed (see §8).

> Course note: "Just use Z instead of worrying about the t-distribution." The exact theory
> uses `t_{n−2}`, but for our purposes the Normal approximation is fine.

---

## 6. Two forms of inference

### (a) Confidence interval for β₁
```
CI(β₁, 1−α) = β̂₁ ± t*_{1−α/2} · SE(β̂₁)
```
95% is most common. Interpretation: we're 95% confident the true β₁ lies in the interval;
across repeated samples, 95% of such intervals would cover the true value.

### (b) Hypothesis test
In SLR the "status quo" is **the absence of a relationship** between response and predictor.
Testing whether X and Y are linearly related is equivalent to:
```
H₀: β₁ = 0   vs.   H₁: β₁ ≠ 0     (default; α often = 0.05)
```
(Change H₁ to one-sided if β₁ cannot be positive/negative.) Note: separate tests exist for
each parameter (intercept and slope).

Test statistic / null model:
```
T = (β̂₁ − 0) / SE(β̂₁) ~ t_{n−2}
```
**Reject H₀ if p-value < α.**

### The p-value
The probability of observing a test statistic **at least as extreme** as the one obtained,
**assuming H₀ is true**. The **smaller the p-value, the stronger the evidence against H₀.**
- It is **NOT** the probability that H₀ is true (it's computed *assuming* H₀).
- "Fail to reject" ≠ "H₀ is true" — we never *prove* H₀; we only reject or fail to reject.
- Statistical significance ≠ practical importance.

### CI ⟺ hypothesis test
> A 95% CI for β₁ that **covers 0** is *equivalent to* **failing to reject H₀** at the 5% level.

Equivalently: |Z| > 1.96 (⟺ p < 0.05) ⟺ the 95% CI excludes 0 ⟺ statistically significant.
At exactly Z = 1.96 / p = 0.05, 0 sits on the boundary of the CI.

---

## 7. R workflow — two parallel paths

**Don't mix these two in one pipe.** (Hard-won lesson — see the debugging log at the bottom.)

### Theory-based path: `lm()` + `broom`
```r
library(broom); library(moderndive)
model <- lm(y ~ x, data = df)

tidy(model, conf.int = TRUE)   # coefficient table: term, estimate, std.error,
                               #   statistic, p.value, conf.low, conf.high
glance(model)                  # one-row model summary (R², sigma, AIC, …)
augment(model)                 # data + .fitted, .resid per observation
confint(model, level = 0.95)   # CI for each coefficient
```
- `tidy()` must be given a **model object**, not a data frame. Feeding it a data frame calls
  the deprecated `tidy.data.frame` method, which crashes on non-numeric columns.
- `moderndive::get_regression_table(model)` is a friendly wrapper around
  `tidy(model, conf.int = TRUE)`.
- `get_correlation(formula = y ~ x)` / base `cor(df$y, df$x)` for the correlation coefficient.

### Simulation-based path: `infer`
A fixed sequence of verbs (`specify → hypothesize → generate → calculate`):
```r
library(infer)
boot_dist <- df %>%
  specify(formula = y ~ x) %>%          # declare model (NOT lm())
  generate(reps = 15000, type = "bootstrap") %>%
  calculate(stat = "slope")

boot_dist %>% get_ci(type = "percentile", level = 0.95)
boot_dist %>% visualize()               # for plotting; not geom_histogram() directly
```
- Use `specify()`, **not** `lm()`, at the top — `generate()` needs a data frame to resample.
- `hypothesize()` is only needed for hypothesis tests, not for a bootstrap CI.

---

## 8. Bootstrap

**Bootstrapping** = sampling **with replacement** from the original sample to build an
empirical sampling distribution. The original sample stands in for the unknown population.
Works for **any sample size and any distribution**, no matter how complicated the estimate.

- It's the "advil" of statistics — no formula, no assumptions; always gives *a* CI.
- Trade-off: the CI may be **wider** than the theory-based one. If you want the narrowest CI
  (and assumptions hold), the formula is better.
- Use the bootstrap when a formula is hard/unavailable: SE of a **correlation r**, SE of a
  **median**, etc. (For a sample mean, `SE(ȳ) = s/√n` — a formula exists.)
- **Number of replicates B:** more reps ⟹ smoother approximated sampling distribution.
  `B ≥ 100` is typically enough; much larger needs real compute.

> NOTE: taking *many fresh samples from the full dataset* is **not** bootstrapping — that
> draws new data from the population. Bootstrapping resamples the **one** sample you have.
> In practice you only ever have one sample.

### Two ways to build a bootstrap CI
- **Standard-error (normal) method:** use the bootstrap estimates to approximate the SE,
  then `estimate ± 1.96·SE`. Assumes the bootstrap distribution is ~symmetric/normal.
- **Percentile method:** take the empirical **quantiles** of the bootstrap estimates directly
  (e.g. 2.5th and 97.5th for 95%). No shape assumption; can be asymmetric.

```r
# Percentile method (manual, from a table of bootstrap estimates)
summarise(avg      = mean(value),
          lower_ci = quantile(value, 0.025),
          upper_ci = quantile(value, 0.975))
```
⚠️ When `value` is already a **bootstrap distribution of a statistic**, `sd(value)` *is* the
SE — do **not** divide by √n again.

---

## 9. Categorical covariates (a bridge to the t-test)

A predictor can be **categorical**. To put a category in an equation, encode it as a **dummy
variable**. For 2 categories you need only **1** dummy:
```
sexᵢ = 0 if female, 1 if male
body_mass_gᵢ = β₀ + β₁·sexᵢ + εᵢ
```
There is no line here — `sex` is only 0 or 1. The model reduces to two group means:
```
body_mass_gᵢ = β₀ + εᵢ            if female (reference level)
             = β₀ + β₁ + εᵢ        if male
```
So:
- **β₀** = average response of the **reference** group (female).
- **β₁** = the **difference** in means.
- **β₀ + β₁** = average response of the other group (male).

Testing `H₀: β₁ = 0` (means are equal) is **equivalent to a two-sample t-test** (with
`var.equal = TRUE`). The `lm` slope estimate = the difference `estimate1 − estimate2`, and the
statistics/p-values match.

In R, just make the variable a **factor** and `lm` builds the dummies and names the level:
```r
df %>% mutate(sex = as_factor(sex))
lm(body_mass_g ~ sex, data = df)      # term "sexmale" is β₁
```

---

## 10. Two important cautions

**Regression vs. correlation analysis:**
- *Correlation analysis* — strength of linear association between two variables; **no**
  response/covariate distinction; **both** variables assumed stochastic.
- *Linear regression* — estimates the conditional **average** of the response given the
  covariate; the covariate is assumed **non-stochastic**; one variable is response, the other
  covariate.
- Consequence: the regression of Y on X is **not** the same as the regression of X on Y.
  (`y = β₀ + β₁x` rearranges to `x = −β₀/β₁ + (1/β₁)y` — different line.)

**The range problem:** the linear model assumes linearity between X and E[Y|X], which may
hold only over **part** of the data range. Be cautious **extrapolating** beyond the observed
range of X — the relationship can differ substantially there.

---

## 11. Worked examples

### Wage vs. Education (activity 1 — `wage.txt`)
- Scatterplot shows a **weak but positive** linear relationship.
- `get_correlation(wage ~ education)` ≈ **0.382** — weak, positive; consistent with the plot.
  (`cor()` gives the same value.) Correlation ≠ causation.
- `lm(wage ~ education)` gives a positive slope ≈ **0.750** — consistent with A & B.

### Wage vs. Education — inference (activity 2)
- p-value for the `education` slope ≈ **0** < 0.05 ⟹ relationship is **statistically
  significant**.
- 95% CI for β₁ ≈ **(0.596, 0.905)** — excludes 0 ⟹ reject H₀ (significant at 5%),
  consistent with the p-value.
- Z-statistic ≈ 9.53 > 1.96 and p ≈ 0 ⟺ CI excludes 0. All three tell the same story.

### Penguins (slides — `body_mass_g ~ flipper_length_mm`)
- `confint()`: 95% CI for the flipper slope ≈ **(47.12, 53.18)** g per mm.
- `tidy(conf.int = TRUE)`: slope estimate ≈ 50.15, p ≈ 0 ⟹ reject `H₀: β₁ = 0`.
- Bootstrap percentile CI for the slope ≈ **(47.28, 53.10)** — close to the theory CI.
- `body_mass_g ~ sex`: intercept 3862.27 (female avg), `sexmale` 683.41 (difference) ⟹
  male avg = 4545.68; matches a two-sample t-test exactly.

---

## 12. Worksheet 01 — Generative Modelling (cancer-mortality case study)

Worksheet 01 ("Introduction to Generative Modelling") walks the whole SLR pipeline on the
`US_cancer_data` dataset. This is the case study behind the `US_cancer_sample250` /
`lm_boot250` / `boot_SLR_CIs` code.

### Framing: the three aspects of linear models
Linear regression is a **generative model** — it approximates the underlying mechanism that
generated the data. Research focuses on three intimately-connected aspects:
- **Estimation:** estimate the true (unknown) relation between response and inputs.
- **Inference:** use the model to infer information about that unknown relation.
- **Prediction:** use the model to predict the response for *new* observations.

("*Simple*" in SLR means **one** input variable — not that it's easy.)

### The dataset & question
`US_cancer_data` — cancer mortality and demographics for US counties (n = 3047).
- `TARGET_deathRate` — cancer deaths per 100,000 (2010–2016 avg) → **response (Y)**
- `povertyPercent` — % of county population in poverty → **input (X)**
- `PctPrivateCoverage` — % with private health coverage

Model: `TARGET_deathRate = β₀ + β₁·povertyPercent + ε`. The scatterplot shows a **positive**
association. Since this is **observational** data, the SLR describes **association, not
causation** — so the correct slope interpretation is *"a one-unit increase in poverty % is
**associated with** a 1.52 increase in mortality"* (not "causes", not "the effect of").

### Part I — Estimation
- Choosing the "best" line = the line that **minimizes the distance of points to the line**,
  where distance is the **vertical** gap (the residual — we're explaining Y). ⟹ **Least Squares**.
- Fit with `lm(formula = TARGET_deathRate ~ povertyPercent, data = US_cancer_sample250)`.
- **`lm` formula helpers:**
  - `lm(y ~ ., data = df)` — use **all** other columns as predictors.
  - `lm(y ~ x - 1, data = df)` — force intercept = 0. **Never do this** unless you know why.
- Draw the fitted line with `geom_smooth(method = "lm", se = FALSE)`.
- **Inference/estimation vs. prediction:** "Is there an association across *all* counties?" →
  inference/estimation. "A new county has 14% poverty — what mortality do we expect?" →
  **prediction**.

### Part II — Inference
- **Estimators are random variables.** `β̂₀`, `β̂₁` depend on the sample, so different samples
  give different estimates (the worksheet builds a `many_SLR` table by drawing several fresh
  samples). ⚠️ Drawing multiple fresh samples from the full dataset is a **pedagogical**
  exercise and is **NOT bootstrapping** (bootstrapping resamples the *one* sample, with
  replacement). In practice you only ever have one sample.
- **Standard error** = SD of that sampling distribution; get it two ways — (1) theoretical
  result (`lm`), or (2) bootstrapping.
- `tidy(SLR_cancer_sample250)` → the coefficient table (`term, estimate, std.error,
  statistic, p.value`); `mutate_if(is.numeric, round, 2)` to tidy the display.

**Hypothesis test (careful with hats!):**
- Correct null is about the **population parameter**: `H₀: β₁ = 0` (**not** `β̂₁ = 0`).
- For a *positive* association, the alternative is one-sided: `H₁: β₁ > 0`.
- **p-value MCQ (worksheet's own emphasis):** the only correct statement is *"the p-value is
  **not** the probability that the null hypothesis is true."* It is **not** the probability H₁
  is false, **not** a measure of effect size/importance, and **not** "the probability the
  effect was produced by random chance alone."
- Decision: smaller p ⟹ stronger evidence against H₀; reject when p < α. Here p is
  effectively 0 ⟹ **reject H₀**: poverty % is statistically associated with mortality.
- ⚠️ Aside flagged in the worksheet: the "**crisis of p-values**" (see the *Nature* article and
  ASA statement) — p-values are widely misused.

**Confidence interval:**
- `SLR_cancer_sample250 %>% tidy(conf.int = TRUE)` → asymptotic 95% CI per coefficient.
- ⚠️ Interpretation caveat: once computed from the data, **nothing is random** — the interval
  either covers the true value or it doesn't. The "95%" refers to the *procedure* across
  repeated samples, not a probability for this one interval.

### Sampling distribution via bootstrapping ("case bootstrapping")
Steps: (1) resample with replacement to get B samples of size n; (2) fit the SLR on each;
(3) the B estimates approximate the sampling distribution (and give its mean & SE).

Two ways to generate the bootstrap estimates:
```r
# (a) base R — replicate + lm + extract coefficients
set.seed(123); n <- 250; B <- 1000
lm_boot250 <- replicate(B, {
  sample_n(US_cancer_sample250, size = n, replace = TRUE) %>%
    lm(formula = TARGET_deathRate ~ povertyPercent, data = .) %>% .$coef
})
lm_boot250 <- data.frame(boot_intercept = lm_boot250[1, ], boot_slope = lm_boot250[2, ])

# (b) infer — one slope statistic per replicate
bootstrap_slope_infer <- US_cancer_sample250 %>%
  specify(formula = TARGET_deathRate ~ povertyPercent) %>%
  generate(reps = 1000, type = "bootstrap") %>%
  calculate(stat = "slope")           # columns: replicate, stat
```
(Same seed ≠ identical results across the two methods — they resample differently.)
Visualize with a histogram of `boot_slope`, or `bootstrap_slope_infer %>% visualize()`.

**Does sample size matter?** Bootstrapping from n = 250, 500, 1500: the bootstrap sampling
distribution of the slope gets **tighter as n increases** (its center stays roughly the
same). Larger samples ⟹ less estimator variability ⟹ narrower intervals.

### Bootstrap percentile CI (Question 7.3 — the one debugged earlier)
```r
boot_SLR_CIs <- lm_boot250 %>%
  pivot_longer(cols = contains('boot'), names_prefix = 'boot_', names_to = 'statistic') %>%
  group_by(statistic) %>%
  summarise(avg      = mean(value),
            lower_ci = quantile(value, 0.025),
            upper_ci = quantile(value, 0.975))   # 4 cols: statistic, avg, lower_ci, upper_ci

# infer equivalent:
percentile_ci <- bootstrap_slope_infer %>%
  get_confidence_interval(type = "percentile", level = 0.95)
bootstrap_slope_infer %>% visualize() + shade_confidence_interval(endpoints = percentile_ci)
```
The worksheet **explicitly asks for the percentile method** — hence `quantile()`, not
`mean ± 1.96·sd`. (See the debugging appendix for every trap this question triggered.)

---

## 13. Tutorial 01 — EDA + SLR (California Schools case study)

Tutorial 01 covers the same learning objectives as the worksheet but on a different dataset,
and adds a proper **Exploratory Data Analysis (EDA)** workflow up front.

### Warm-up fundamentals (T/F)
- The variable being *explained* (e.g. a newborn's birth weight) is the **response**. ✓
- SLR is **not** an exact linear function — `Yᵢ = β₀ + β₁Xᵢ` (without ε) is **false**; the
  model always includes the error term `+ εᵢ`.
- The error term `εᵢ` **does** contain relevant info from explanatory variables *not* in the
  model (plus noise). ✓
- The population coefficient `β₁` is **not** known — it must be estimated. ✓

### The dataset
`CASchools` from the **`AER`** package (Applied Econometrics with R) — 420 California K–6/K–8
school districts, 1998–99. Treated as a *random sample*. Variables used:
- `grades` — factor (grade span) · `income` — avg district income ($000s) ·
  `english` — % English learners · `read` — avg reading test score.
**Question:** is school performance (`read`) associated with family `income`?

### EDA workflow (from *The Art of Data Science*, Peng & Matsui)
Data-science work is not linear — it proceeds in **epicycles**. Checklist:
1. Formulate your question · 2. Read your data · 3. Check the packaging ·
4. Look at the top and bottom · 5. Check your "n"s.

```r
data(CASchools)
caschools <- CASchools %>% select(grades, income, english, read) %>%
  mutate_if(is.numeric, round, 2)

str(caschools)                 # check packaging (types, structure)
caschools %>% head(n = 3); caschools %>% tail(n = 3)
dim(caschools)                 # dimensions

# summary stats: reshape to long, then group + summarise
caschools_long <- caschools %>% select(-grades) %>%
  gather(factor_key = TRUE, key = 'variable')     # (older tidyr verb for pivot_longer)
caschools_long %>% group_by(variable) %>%
  summarise(mean = mean(value), sd = sd(value), max = max(value), min = min(value))
```

**`ggpairs()`** (from **`GGally`**) — a scatterplot-matrix that auto-picks plot types:
distributions on the diagonal, pairwise relationships off-diagonal. Preferred over base
`pairs()` (shows distributions, correlations, and handles categorical vars). *Caveat:* not
ideal when there are too many variables.

```r
caschools %>% ggpairs(progress = FALSE)
```
From the EDA: `income` is **right-skewed**.

### Fitting the SLR
Key nuance: `read` vs. `income` is **positive but not perfectly linear** across the full
range — yet an SLR is still a **useful first approximation** (ties back to the *range problem*,
§10).

```r
caschools_SLR <- lm(read ~ income, data = caschools)
caschools_SLR_results <- tidy(caschools_SLR, conf.int = TRUE) %>%   # conf.level = 0.95 default
  mutate_if(is.numeric, round, 2)
# scatterplot + fitted line
ggplot(caschools, aes(x = income, y = read)) +
  geom_point() + geom_smooth(method = "lm", se = FALSE, linewidth = 1.5)
```
Slope interpretation (association, not cause): *an increase in average district income is
associated with an increase in average district reading score.*

### Inference
- At α = 0.05, `income` **is** statistically associated with `read` (p < 0.05).
- The p-values from `lm` come from **classical theoretical approximations** — not bootstrap.
- The relevant **sampling distribution** is the distribution of **β̂₁** (the *estimator* of the
  slope) — not of Y, X, or the true β₁.

### Bootstrap + percentile CIs (visualized with vertical lines)
```r
set.seed(123); n <- 420; B <- 10000        # n = nrow(caschools); B large ⟹ slow
lm_boot <- replicate(B, {
  sample_n(caschools, size = n, replace = TRUE) %>%
    lm(formula = read ~ income, data = .) %>% .$coef
})
lm_boot <- data.frame(boot_intercept = lm_boot[1, ], boot_slope = lm_boot[2, ])

# 95% percentile CI for the slope, drawn as vlines on the histogram
ggplot(lm_boot, aes(x = boot_slope)) +
  geom_histogram(bins = 30, color = 'white') +
  geom_vline(aes(xintercept = quantile(boot_slope, 0.025)), col = 'blue', linewidth = 1) +
  geom_vline(aes(xintercept = quantile(boot_slope, 0.975)), col = 'blue', linewidth = 1)
```
- To bootstrap the **intercept** instead, use the `boot_intercept` column the same way.
- For a **90%** CI, use the `0.05` / `0.95` quantiles (not `0.025`/`0.975`).

> Gotcha: the tutorial wrote `tidy(caschools_SLR, conf.int = 0.95)`. That happens to work only
> because `0.95` is truthy for the `conf.int` (logical) flag — the confidence *level* argument
> is actually `conf.level`, which defaults to 0.95. Prefer `tidy(model, conf.int = TRUE)` (and
> `conf.level = 0.90` when you want a different level).

---

## Questions / TODO

- **Why is the residual different from the error term?**
  The error term `εᵢ = Yᵢ − (β₀ + β₁Xᵢ)` uses the **true, unknown** population line; the
  residual `eᵢ = Yᵢ − (β̂₀ + β̂₁Xᵢ)` uses the **estimated** line from our sample. They differ
  because `β̂ ≠ β`. We never observe εᵢ; we only compute eᵢ.
- Relationship between the two-sample t-test and regression — see §9 (resolved: identical when
  the covariate is a 2-level dummy with equal variances).
- Iterative algorithms / model families (Frequentist likelihood vs. Bayesian), MCMC, EM,
  CLT — flagged in personal notes as later/aside topics; not core to Topic 1.

### Clicker questions
- *Positive correlation ⟹ positive regression slope?* **TRUE** — `β̂₁ = r·(s_y/s_x)`.
- *Higher correlation ⟹ larger slope?* Poorly-designed question (slope also depends on
  `s_y/s_x`, not correlation alone).
- *Regression of Y on X = regression of X on Y?* **FALSE** (see §10).

---

## Appendix — debugging lessons (from working the exercises)

- `tidy()` needs a **model**, not a data frame; and don't call it twice in a pipe.
- `infer` starts with `specify()`, not `lm()`; `generate()` needs a data frame, not an `lm`
  object (a list) — otherwise `rep_sample_n()` errors with "`tbl` must be 'data.frame'".
- `1.96(…)` is not multiplication — R reads it as calling `1.96` as a function
  ("attempt to apply non-function"). Write `1.96 * (…)`.
- Inside `summarise()`, don't restate the grouping column (`statistic = statistic`) — it
  returns the whole group vector and re-expands the rows. The `group_by` key is kept
  automatically.
- When the worksheet says **percentile method**, use `quantile(value, 0.025/0.975)`, not
  `mean ± 1.96·sd`.
