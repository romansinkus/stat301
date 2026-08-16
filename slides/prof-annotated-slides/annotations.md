# Professor's annotated-slides — transcribed reference

A faithful summary of the instructor's **handwritten red annotations** on the marked lecture
PDFs in this folder, so you can reference them without re-opening the (large) PDFs. Organized by
topic → marked file. "Q:/A:" are the professor's own questions and answers written in the margins.

A shorter, exam-focused distillation lives in `final/master_notes.md` ("PROFESSOR'S ANNOTATED
SLIDES" section) and `final/final-review-notes.md`. This file is the fuller, page-aware record.

> Note: **Topic 9 (Prediction Uncertainty) has no marked slides** in this set. The annotated decks
> cover Topics 1–8 only.

---

## Topic 1 — Simple Linear Regression

### `topic1-1-marked.pdf` (SLR: model, estimation)
- **Stochastic-relation scatter:** the professor drew a too-steep line and labelled it "**wrong**", then
  wrote `R²=0.4` / "40%" — a fitted line can be judged good/bad, and R²=0.4 means 40% of the variance in
  the response is explained. Scribbled "IQ", "EQ?" = other omitted factors.
- **Error-term slide:** `y=f(x) → y=β₀+β₁x`, labelled "**simplest**". `ε` = "uncertainty."
  **Q: Why do we FIRST consider a linear relationship? A: it's the simplest.**
- **Terminology:** `Y` = "variable of interest, e.g. grade; depends on the study objective." OK names for
  `X`: covariate / feature / input.
- **Specification:** the data are "a sample of size n"; `X` is "**not random** / assumed to be fixed."
- **Model components:** `Yᵢ` is random; `εᵢ` is random = "the variation in Y that cannot be explained by X."
- **Fitting (the derivation logic):** "You have DATA first, then find a line closest to ALL data points.
  How? **Minimize `Σᵢ(yᵢ − (β₀+β₁xᵢ))²`.** Then set `∂Q/∂β₀=0`, `∂Q/∂β₁=0`, solve." → `β̂₀, β̂₁` are
  **estimates**, NOT the true values (true values are never known).
- **Random errors:** `εᵢ ~ Normal`, mean 0 ("safely assumed" ⇒ unbiased), variance `σ²` unknown.
  **Two starred points every estimate has:** (1) unbiased, `E(β̂₁)=β₁`; (2) uncertainty (SE), true `β₁`
  in `β̂₁ ± 1.96·SE(β̂₁)`.
- **Conditional expectation:** `E[Y|X]=β₀+β₁X` with X fixed. **Q: Does it still hold for a different dataset?**
  (the generalization question that motivates inference).
- **Population vs sample:** professor **crossed out the `+ε̂`** in the sample line — the fitted line
  `Ŷ=β̂₀+β̂₁X` has **no error term**; the residual `eᵢ` is separate, and `eᵢ ≠ εᵢ` because `β̂ ≠ β`.
- **Slope–correlation link (written twice):** **`β̂₁ = r · (S_y/S_x)`**, `r` = correlation between X and Y,
  `S_y, S_x` = sample SDs (>0). ⇒ sign of slope = sign of correlation.
- **Inference for β̂₀:** "Inference = can we **generalize** results from one dataset to a larger population?
  Two approaches: (1) CI for β₀, (2) hypothesis test for β₀." SE formulas are "derived based on the
  assumptions" (uncorrelated, equal-variance errors); `β̂₀ ~ N` (normal).
- **CI slide:** `t*_{1−α/2} ≈ 1.96 ≈ 2` when `α=0.05`; CIs assume `ε` normally distributed.
  **Q: What if the normal assumption doesn't hold? A: bootstrap.**

### `topic1-2-marked.pdf` (Inference in SLR)
- **SD vs SE (big circled Q):** `SD(β̂)=σ/√n` (true σ); `SE(β̂)=σ̂/√n` (estimate; σ unknown). **SE = the
  estimated SD of the estimator.**
- **Sampling-distribution intuition (Strathcona houses, samples of 1000 from a 27,699-row population):**
  fit SLR repeatedly → `β̂₁` = 2.618, 3.017, 2.448, … "**Q: which one is best? A: we don't know.**"
  `SE(β̂₁)` = SD of these repeated-sample slopes = `√( 1/(k−1) Σ(β̂₁ᵢ − β̄₁)² )`. City analogy: Vancouver
  β̂₁=2.3, Toronto 2.1, ….
- **Two ways to get the SE from one sample:** (1) theoretical formula (`lm`), (2) bootstrap.
- **CORRECTION:** taking new samples from the full dataset is **NOT bootstrapping** — bootstrap resamples
  the ONE observed sample **with replacement**; it does not draw fresh data from the population.
- **The statistic:** `T = (β̂₁−0)/SE(β̂₁) ~ N(0,1)` under H₀ (finite n: `t(n−2)`; `t(n)→N(0,1)` as n→∞).
  Worked: `T = 2.618/0.059 = 44.514`. Test: **H₀: β₁=0 = "no linear relationship"**, H₁: β₁≠0.
  Worked 95% CI: `2.618 ± 1.96×0.059`.
- **CI ⇄ test duality (boxed):** "**the 95% CI of β₁ covers 0 ⟺ fail to reject H₀ at the 5% level.**"
- **Classical CI:** `estimate ± t*_{α/2, n−k}·SE`, `k` = # regression parameters (df = n−k). If errors are
  normal with σ *known*, use `z_{α/2}` instead of `t`.
- **CI misinterpretation (underlined "misunderstandings"):** once a 95% CI is computed, nothing is random —
  it either covers the truth or it doesn't; the 95% describes the procedure across many samples.
- **Bootstrap procedure:** (1) treat the observed sample as an estimate of the population; (2) resample it
  WITH replacement, same size n; (3) repeat B times (100/1000/10000). "Population : sample :: sample :
  bootstrap sample." Bootstrap SE = SD of the B bootstrap estimates; 95% CI = `β̂₁ ± 1.96·SE`;
  `Z = β̂₁/SE ~ N(0,1)`. Some SEs (median, correlation) have no formula → must bootstrap.
- **Bootstrap CI methods:** (1) SE method `β̂₁ ± z*·SE*`; (2) **Percentile method** = the 2.5th and 97.5th
  percentiles of the bootstrap estimates → `(a,b)`. Reject at 5% iff `(a,b)` excludes 0.

---

## Topic 2 — Multiple Linear Regression

### `topic2-1-marked.pdf` (categorical inputs & additive MLR)
- **c-level categorical ⇒ c−1 dummies;** the reference level is "**hidden**" (coded 0 in every dummy,
  chosen alphabetically → "Indiana"). `βⱼ = E(Y|level) − E(Y|reference)`; `β₀` = mean of the reference.
  The β's here are **NOT** slopes/intercepts even though R labels them so.
- **WHY LINEAR FIRST — the first-order Taylor argument (answers the Topic-1 open Q):** for any smooth `f`,
  `f(x) ≈ f(x₀) + f'(x₀)·x + (higher-order remainder)`. The linear model IS this first-order Taylor
  approximation; it needs `f` smooth (`f'` exists). A kink / non-smooth relation breaks it.
- **Additive model** `y=β₀+β₁x₁+β₂x₂+ε` has 3 coefficients but describes **2 parallel lines** (common slope).
- **SE column** = "the accuracy of the estimate," marked "**most important**."

### `topic2-2-marked.pdf` (interactions)
- **Profile plot (before/after treatment × gender sketch):** lines **parallel ⇒ NO interaction** (the effect
  of one variable doesn't depend on the other); lines **non-parallel / crossing ⇒ interaction** present.
- **Testing interaction:** `H₀: β₃=0` (none) vs `H₁: β₃≠0`; `Z = β̂₃/SE(β̂₃) ~ N(0,1)`. **Power caveat:** a
  *weak* real interaction ⇒ small Z ⇒ large p-value ⇒ fail to reject even though it exists. Worked example:
  interaction p=0.306 > 0.05 ⇒ weak ⇒ remove the interaction term.
- **COMMON MISTAKE (underlined):** in a model WITH interaction you **cannot** interpret a coefficient
  "holding the others constant" — that's additive-only. "We test you only on the interaction types covered
  in lecture" (one continuous × one categorical).

---

## Topic 3 — Diagnostics, multicollinearity & causality

### `topic3-1-marked.pdf` (LINE diagnostics + multicollinearity)
- **Residual-plot mechanics:** fitted `ŷᵢ = β̂₀+β̂₁x₁ᵢ+β̂₂x₂ᵢ` (no error term); residual `rᵢ = yᵢ−ŷᵢ`. Plot
  residuals vs fitted. Good fit ⇒ scatter around `Y=0`, **no pattern**; a curve ⇒ non-linearity, a funnel ⇒
  non-constant variance.
- **"Linear" = linear in the parameters, not in the predictors.** `income²`, `log X`, `√X` are fine
  covariates; LS works identically, only interpretation changes. Fix non-linearity by adding
  transformations/interactions, then re-check the residual plot.
- **Independence (I):** judged from the **study design**, not a plot. Violations: temporal data, repeated
  measurements (longitudinal) — "your homework scores aren't independent." If violated → SEs biased → CIs
  & tests **invalid** → use time-series / longitudinal methods (out of scope).
- **Equal variance (E):** `Var(εᵢ)=σ²` constant (= `Var(Yᵢ)`). Funnel ⇒ heteroscedasticity. Fix by
  transforming the **response** (√Y or log Y). `log(Y)=β₀+β₁X ⟺ Y=e^{β₀+β₁X}·e^ε` (multiplicative model).
- **Normality (N):** least-severe violation. Q-Q plot: points on a straight line = normal. Large n (CLT) or
  bootstrap rescue it. Normal errors ⇒ `E[Y|X]` provably linear.
- **Multicollinearity:** strong association among **2+** covariates. Perfect collinearity (income vs
  income×1000) ⇒ R returns **NA** (infinitely many models with the same SSR). Consequence: **inflates SEs ⇒
  inflates p-values ⇒ CIs wider ⇒ harder to reject H₀.** Pairwise correlation is **not enough** (misses
  >2-variable collinearity).
- **VIF (concrete):** guideline `> 5` or `> 10` = problematic ("**this is a guideline**"). For categorical
  covariates use the **generalized VIF** — R's `GVIF^(1/(2·Df))` column; compare it to `√5 ≈ 2.23` or
  `√10 ≈ 3.16` (or square it and compare to 5/10). `Df = #categories − 1`. Fix: drop or combine collinear
  variables (removing `species` made all GVIF < √5 → problem gone).

### `topic3-2-marked.pdf` (causality & designs)
- "X causes Y" **≠** "X and Y are associated"; regression finds only association. Three ways association
  misleads: **reverse causality**, **Simpson's paradox** (correlation sign *flips* within strata — UC
  Berkeley admissions), **confounding** (a C causing both X and Y; lifestyle → smoking and → cancer).
- Causal inference depends on (1) how data were collected (experimental vs observational) and (2) the
  method; **randomization eliminates confounders.**
- **CRD** (completely randomized, the simplest): balances **observed AND unobserved** confounders on average
  ⇒ **gold standard.** **RBD** (randomized block): homogeneous blocks (identical except treatment) remove
  nuisance variation; balances **only observed** confounders. Blocking ⇒ **smaller SD ⇒ smaller SE ⇒ smaller
  p-value ⇒ more power.** Observational: treatments not controlled; unobserved confounders remain ⇒ causal
  effects can't be established naively.

---

## Topic 4 — Logistic Regression

### `topic4-1-marked.pdf` (estimation & interpretation)
- **KEY PRINCIPLE (boxed):** the **model type is set by the RESPONSE, not the predictors.** Linear assumes a
  continuous, normal response; binary → logistic; count → Poisson.
- **GLM unified form:** `h(E(Yᵢ)) = β₀+β₁X₁+…` (the "link of the conditional expectation = the linear part").
  Identity link `h(X)=X` ⇒ linear model; logit link `h(X)=log(X/(1−X))` ⇒ logistic. **No error term.**
- **Bernoulli:** `Y∈{0,1}`, `P(Y=1)=p` — a special case of Binomial with n=1.
- **`glm` = MLE (maximum likelihood); `lm` = least squares.** They coincide for normal errors. Logistic MLE
  has no closed form ⇒ iterative ("# Fisher scoring iterations"). `family=binomial` for logistic,
  `family=gaussian` (default) for linear. R's output notes "dispersion taken to be 1" (φ=1 assumption).
- **Three scales (Titanic `fare`, β̂₁=0.0152):** log-odds +0.0152 per $1; odds ×`e^0.0152=1.015` (+1.5%);
  probability `p=e^{β₀+β₁x}/(1+e^{β₀+β₁x})` (nonlinear). Exponentiate coefficients to read odds/odds-ratios.
- **Complementary-outcome trick:** flip the sign. `e^β̂₁=e^{−2.514}=0.081` = odds_male/odds_female of
  *surviving* ⇒ males' odds of *dying* = `e^{+2.514}=12.35×` those of females.
- **% change in odds = `(e^β − 1)×100%`;** `e^β` = the multiplicative factor.
- **Additive logistic** (equal log-odds slope, different intercepts): probability curves are **NOT parallel**
  (they diverge/compress near 0 and 1).
- **Interaction logistic:** cannot say "holding the other constant"; split into two curves; with exponentiated
  coefficients you **multiply** (`e^{β₀+β₁}=e^{β₀}·e^{β₁}`). Example interaction `sexmale:fare` p=0.050.
- **GLM inference = Wald, uses `z` (Normal), NOT `t`:** `Z=(β̂ⱼ−0)/SE(β̂ⱼ) ~ N(0,1)` approximately (large-n,
  via CLT + MLE asymptotics `√n(β̂−β)→N(0, I⁻¹(β))`). `CI = β̂ⱼ ± z_{α/2}·SE`.
- **Summary of interpretation:** raw coefficients (log-odds model) = log-odds of reference / difference of
  log-odds / change in log-odds per unit; exponentiated (odds model) = odds of reference / **odds ratio** /
  multiplicative change in odds.

### `topic4-2-marked.pdf` (fitted values, residuals, overdispersion)
- **WHICH-SCALE R gotchas:** `predict(type="link")` = LOG-ODDS (default), `type="response")` = PROBABILITIES.
  `augment()` adds `.fitted` = LOG-ODDS, but `model$fitted` / `fitted(model)` = PROBABILITIES. Worked:
  male, fare $7.25 → log-odds −1.696 → `p = e^{−1.696}/(1+e^{−1.696}) = 0.155`.
- **Why the residual plot is useless:** raw residual `rᵢ=yᵢ−p̂ᵢ` takes only two values (−p̂ᵢ or 1−p̂ᵢ) ⇒ two
  straight lines; and `Var(Yᵢ)=pᵢ(1−pᵢ)` isn't constant. **Pearson residual = `(yᵢ−p̂ᵢ)/√(p̂ᵢ(1−p̂ᵢ))`** is
  more reliable but still not fixable for binary data ⇒ use a **binned residual plot.**
- **Overdispersion (the key GLM diagnostic):** binomial assumes `Var(Y)=p(1−p)`, φ=1. Model `Var(Y)=φ·p(1−p)`
  and estimate φ via `family=quasibinomial`: **φ=1 correct, φ>1 over-, φ<1 under-dispersion.** It corrects
  the SEs and affects the **SEs, not the point estimates.** Worked: `φ̂=0.98 ≈ 1` ⇒ binomial holds, inference valid.

---

## Topic 5 — Poisson Regression (`topic5-marked.pdf`)
- **Poisson:** `P(Y=k)=e^{−λ}λ^k/k!`, k=0,1,2,…; **`E(Y)=Var(Y)=λ`** (mean equals variance — the defining
  property). Model `log(λᵢ)=β₀+β₁X₁+…` (log link, canonical); `λ=e^{linear}`. Models the log of the mean
  counts; no error term.
- **FACTOR GOTCHA (starred "if this isn't true the results are WRONG!") — applies to logistic/Poisson/linear:**
  a categorical variable stored as a **number** (season 1/2/3/4) is treated by `glm`/`lm` as **continuous**
  and gets ONE coefficient — wrong. `as.factor()` it so R makes `c−1` dummies (season2/3/4, season1 reference).
  Always check the tidy table shows the expected number of dummy rows.
- **Two scales (same logic as logistic):** raw β = change in **log-mean counts** (iClicker trap: "the mean
  decreases 0.036" is FALSE — it's the *log*-mean); exponentiated `e^β` = mean-count **ratio/factor**,
  `(e^β−1)×100%` = % change. (`e^2.688=14.703` = factor 14.7; `e^0.063=1.065` = +6.5%.)
- **Inference = Wald `z`** (same as logistic). **Residuals:** raw not comparable ⇒ use Pearson `(yᵢ−λ̂ᵢ)/√λ̂ᵢ`.
- **Overdispersion — Poisson USUALLY over-disperses** (real count variance exceeds its mean). Fit
  `family=quasipoisson` and read φ̂. Worked: **`φ̂ ≈ 90.6 ≫ 1` ⇒ SERIOUS overdispersion, Poisson invalid**
  (contrast the logistic `φ̂≈0.98`). φ affects SEs, not estimates.

---

## Topic 6 — Goodness of Fit (linear models)

### `topic6-1-marked.pdf` (R², metrics)
- **Three sums of squares:** `ESS=Σ(ŷᵢ−ȳ)²` = variation **explained**; `RSS=Σ(yᵢ−ŷᵢ)²` = residual/noise
  (not explained); `TSS=Σ(yᵢ−ȳ)²` = **total** = residuals of the null (intercept-only) model, and ÷(n−1)
  estimates `Var(Y)`. **Decomposition `TSS=ESS+RSS` holds ONLY with LS + intercept.** Null prediction = ȳ.
- **`R² = ESS/TSS = 1−RSS/TSS`** = proportion of total variation explained; in [0,1]; = square of the
  multiple correlation.
- **Four problems with R² (the *why* behind Adj R² and the F-test):** (1) no hypothesis test (unknown
  distribution); (2) in-sample only; (3) no out-of-sample sense; (4) **always increases when you add any
  variable ⇒ can't compare nested models.**
- **`Adj R² = 1 − [RSS/(n−p−1)] / [TSS/(n−1)]`** (`p` = # covariates excluding intercept) penalizes large p.
- **`RSE = √(RSS/(n−p−1)) = σ̂`** = estimate of the error SD (`Var(ε)=σ²`); the `sigma` column in `glance`.
  Smaller = better. `AIC = fit + penalty` for large model — pick the **smallest** AIC (BIC analogous).
- **MSE = `(1/n)Σ(yᵢ−ŷᵢ)²`;** Training MSE (in-sample, from `.resid`) vs Testing MSE (new data, out-of-sample).

### `topic6-2-marked.pdf` (nested-model F-test)
- **Case A (full vs null, `glance`):** `H₀: β₁=…=βₚ=0` ("none significant") vs `H₁`: at least one ≠ 0.
  `F = [(RSS_red−RSS_full)/p] / [RSS_full/(n−p−1)] ~ F(p, n−p−1)`. glance's reduced model is always the null.
- **Case B (any nested pair, `anova(reduced, full)`):** `k=p−q` added; `H₀: β_{q+1}=…=βₚ=0` ("extras not
  needed"). `F = [(RSS_red−RSS_full)/k] / [RSS_full/(n−p−1)] ~ F(k, n−p−1)`. Table cols: Res.Df, RSS, Df,
  Sum of Sq, F, Pr(>F).
- **t-test vs F-test:** t-test (`lm`) tests **one** coefficient with others present; F-test (`glance`) tests
  **all** at once (all-vs-nothing). **For a single predictor, `F = t²`** and the p-values match. Both rely
  on normality / large-sample approximation.
- **Caveat (IMPORTANT):** rejecting H₀ (model beats null) does **not** prove your predictor of interest drives
  Y — another variable may matter as much or more.
- Foreshadow: using F/t-tests to select then refit reuses the data ⇒ post-inference / double-dipping (Topic 8).

---

## Topic 7 — Goodness of Fit for GLMs (`topic7-marked.pdf`)
- R²/RSE/MSE/F don't carry over (all built on `yᵢ−ŷᵢ`, for normal responses). For non-normal responses use
  the **deviance**.
- **Deviance = `2 × (logLik_saturated − logLik_estimated)`** (saturated/perfect model fits the data exactly).
  It **generalizes RSS** — for a normal-error linear model, deviance ∝ RSS. **Lower deviance = better fit.**
  "Null deviance" = deviance of the intercept-only model.
- **Deviance test for nested GLMs (the GLM analog of the F-test):** `H₀`: the two nested models are equally
  good vs `H₁`: the larger is better. Deviance difference ~ **χ²(d)** under H₀, `d` = difference in # of
  predictors. Run with `anova(reduced, full, test="Chisq")`. **Linear ⇒ F (exact under normality); GLM ⇒ χ²
  (large-sample only).**

---

## Topic 8 — Model Selection

### `topic8-1-marked.pdf` (regularization)
- **Stepwise** = greedy, order-dependent, variables fully in/out (coefficient jumps 0 → 83.88).
  **Regularization** shrinks **smoothly**: minimize **penalized RSS** `Σ(Yᵢ−β₀−Xᵢβ)² + λ·penalty`.
  **Ridge = L2 (`λΣβⱼ²`), Lasso = L1 (`λΣ|βⱼ|`).**
- **λ = penalty parameter:** `λ=0` ⇒ ordinary LS (unbiased); larger λ ⇒ more shrinkage. Tune λ to minimize
  test MSE via k-fold cross-validation.
- **Lasso vs Ridge (key contrast):** **LASSO can shrink coefficients exactly to 0 ⇒ variable selection**
  (simultaneously selects and trains); **Ridge never reaches 0 ⇒ no selection** (targets multicollinearity).
  Geometry: constraint region is a **diamond** for Lasso (`|β₁|+|β₂|≤s`, corners on axes ⇒ sparsity) vs a
  **circle** for Ridge (`β₁²+β₂²≤s`). Ridge = Hoerl & Kennard 1970; Lasso = Tibshirani 1996 (good for p≫n).
- **Bias–variance tradeoff (derived):** shrinkage **biases** the estimates (`E(β̃)≠β`) but lowers variance;
  accept bias for prediction performance. `MSE(β̃) = Var(β̃) + bias²`.
- **Always standardize the inputs** before regularizing (penalty depends on coefficient size); `glmnet` does
  by default.
- **In `glmnet`:** pass a **matrix** of inputs + a response vector; **`alpha=1` = LASSO, `alpha=0` = Ridge**
  (between = Elastic Net). Fits over a grid of λ.
- **Reading the `cv.glmnet` plot:** y = CV test MSE, x = log(λ); the **top axis = # of non-zero coefficients**
  (predictors selected) at each λ. **`lambda.min`** = minimum CV-MSE; **`lambda.1se`** = largest λ whose MSE
  is within 1 SE of the minimum (a simpler, more-penalized model at low cost). `coef(cv, s="lambda.min")`;
  a `.` = a variable shrunk to exactly 0. Predict: `predict(cv, newx=X_test, s="lambda.min")`.
- **LASSO must NOT be used for inference** — its coefficients are **biased** (sampling distribution centred
  off the true β).

### `topic8-2-marked.pdf` (post-selection inference / double-dipping)
- **The post-inference problem ("bad idea"):** if you use the data to **select** a model you cannot reuse the
  **same** data for valid inference (the data is "double-dipped").
- **Simulation proof:** generate Y and 10 covariates with **all true β = 0** (so the intercept-only null
  should win). n=100, replicate 1000×; each time forward-select ≤3 variables by Adj R², then run the F/t-test
  on the selected model with the same data. **Result: many replicates reject H₀ (e.g. p=0.032, p=0.00299) —
  the type I error is inflated far above 5%.**
- **Fix:** split/partition the data — select the model on one part, do inference on a held-out part.
