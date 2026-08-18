# Understanding Tracker

A living record of how well I understand each topic, updated as we work through
things together. Ask me later: *"what am I strong on?"*, *"what should I review?"*

**Legend:** 🟢 solid · 🟡 shaky / needs a nudge · 🔴 weak / revisit · ⚪ not covered yet

---

## Topic 4: Logistic Regression & the GLM Bridge

### 🟢 Strong

- **Why logistic regression has no error term `e`.** Worked from confused →
  solid. Understands that `logit(p) = b0 + b1x` is *exact* (no `+ e`) because the
  left side is a computed probability, not an observed noisy data point.
- **Where the randomness lives (Bernoulli "coin flip").** Got it via the
  weather-forecast / marble-bag analogy. Nailed the summary himself: *"`e` means
  sometimes above/below the line; Bernoulli means sometimes yes, sometimes no."*
- **Two kinds of uncertainty.** Sharp intuition — spotted on his own that "70%,
  but realistically 65–75%" is a *separate* uncertainty. Correctly separates
  irreducible noise (coin flip / `e`) from estimation uncertainty (confidence
  interval, from SEs of coefficients).
- **`e` in linear regression = irreducible noise, not the CI.** Understood the
  parallel: `e` is the linear-model analog of the coin flip.
- **Linear regression is a GLM** (identity link = "do nothing"). Understood.
- **MLE vs least squares.** Understands they *coincide* for Normal errors (LS is
  the special-case shortcut of MLE), and that this is why "LinReg is a GLM fit by
  MLE" isn't a contradiction. Asked genuinely sharp probing questions here.
- **LS is not iterative for linear regression** (closed-form formula from
  "slope = 0"), but **MLE is iterative for logistic** (no closed form → Fisher
  scoring). Understands iteration is caused by the math being unsolvable in closed
  form, not by MLE vs LS itself.
- **`glm()` output scales.** Raw coefficients = log-odds (default);
  `exponentiate = TRUE` → odds *ratios* (learned the odds vs odds-ratio
  distinction); `predict(type="response")` → probability.
- **log-odds is additive (+), odds is multiplicative (×).** Solid, and connects it
  to why we model on the log-odds scale (a straight line is additive).
- **Which scale for which job.** Worked out on his own that *coefficient*
  interpretation uses log-odds/odds (the effect is constant there) while
  *probability* is for predicting a specific case. Understands the reason: the
  effect on probability isn't constant (S-curve), so there's no single number to
  quote — hence coefficients live on log-odds/odds.

### 🟡 Watch / recently corrected

- **Interpretation wording.** Tends to drop **"is associated with"** (writes
  "results in" → causal) and **"holding [other var] constant."** Reminded on 2a-i.
  Knows the fix now but should build the habit.
- **Odds ratio is multiplicative, not additive.** Initially wrote "+0.015 in the
  odds." Worked through why "1.5% increase" ≠ "+0.015" (percent scales with current
  odds; they only match when odds = 1). Understood after discussion.

- **Significance on the odds-ratio scale.** 2d-iii: correctly said `fare` is
  significant because its CI excludes **1** (the no-effect value on the odds scale;
  = 0 on log-odds).
- **Additive vs interaction on probability curves (3a).** Solid: parallel on
  log-odds, non-parallel (but non-crossing) on probability because the S-curve
  squashes equal log-odds gaps unequally. Also grasped that *crossing* (not merely
  non-parallel) is what would signal interaction.
- **Logistic residual plot uselessness (3c).** Reasoned out both reasons himself
  via Socratic prompts: residuals collapse onto **2 lines** (`−p̂`, `1−p̂`) because
  `Y` is 0/1; and variance `p(1−p)` changes with `p` by design so non-constant
  spread is expected, not a flaw. Knew the "instead" (overdispersion / binned
  Pearson) already.
- **Overdispersion (3d).** Solid: def `Var(Y) > p(1−p)`; damages **SEs not point
  estimates**; detect+fix both via `quasibinomial` dispersion (≈1 fine, >1 bad);
  Titanic 0.98 → no problem.

### 🔴 Needs practice — recurring weak spot

- **Percent change from an odds ratio (subtract 1 / subtract from 1).** Made this
  error **twice**:
  - 2b-i: read OR `0.081` as "19% lower" — should be `(1 − 0.081) = 91.9%` lower.
  - 2b-ii: wrote "1235% increase" for OR `12.35` — should be
    `(12.35 − 1) × 100 = 1135%` (forgot to subtract 1).
  - **Rule to drill:** OR > 1 → increase `= (OR − 1)×100`; OR < 1 → decrease
    `= (1 − OR)×100`. **Never** multiply the raw OR by 100.
- **Decimal place when converting odds ratios near 1 to percentages.** 2d-ii: read
  CI `(1.008, 1.015)` as "8% to 15%" instead of **0.8% to 1.5%**. `1.008` is 0.8%
  above 1, not 8%. Watch that `1.0xx` odds ratios → fractions of a percent.

### Conceptual questions raised (all resolved)

- Is there error *somewhere* in logistic regression? → Yes: the Bernoulli coin
  flip, not a `+ e` term.
- Isn't `logit = b0 + b1x + e`? → No, that equation is exact.
- Does `e` correspond to the CI in linear regression? → No, `e` is irreducible
  noise; the CI is separate estimation uncertainty.
- Can linear regression be a GLM? → Yes (identity link).
- If LinReg is a GLM, isn't "MLE not LS" a contradiction? → No, they coincide for
  Normal errors.
- Would MLE and LS differ on non-Normal data? → Only if you *assume* a non-Normal
  distribution; the identity is about the assumed distribution, not the true one.

---

## Topic 5: Poisson Regression & Overdispersion

### 🟢 Strong

- **Response type & why not linear.** Poisson = non-negative integer counts; linear
  fails on the range problem (predicts negatives) and the variance problem
  (`Var = λ = mean` breaks Equal-Variance / the "E" in LINE).
- **The two ratio scales (3a-i).** Exponentiating a GLM coefficient gives a
  multiplicative *ratio*: **odds ratio** (logistic, scales the odds) vs. **rate
  ratio** (Poisson, scales the mean count). Both from `exp()`; differ only in what
  they multiply.
- **`Var(Y|X)` contrast (3a-ii).** Logistic `p(1−p)`; Poisson `λ = E[Y|X]`. In both,
  variance is *locked to the mean* (not a free parameter) — that's *why*
  overdispersion is even possible.
- **Which overdisperses (3a-iii, 3b).** Poisson **usually**, logistic **sometimes**.
  Reason nailed after a long deep dive: `Var = λ` is one rigid knob real counts
  routinely break (clustering/bursts); `Var = p(1−p)` is *automatically locked* per
  individual 0/1 obs → can't overdisperse unless data is **grouped or correlated**.

### 🟢 Strong — overdispersion mechanism (deep-dived, moved 🔴→🟢)

- **"Variance is locked" = one-parameter distributions.** For a 0/1 outcome, mean
  (`p`) fixes the *entire* distribution, variance included (`Y²=Y` ⇒ `Var=p−p²`).
  For a count, mean fixes only the center; spread stays free, so Poisson *imposes*
  `Var=λ` as an extra bet reality often loses.
- **How logistic overdispersion actually arises.** Two routes: (1) **grouping /
  binomial** data (counts-out-of-`n`) where a shared `p` hides real heterogeneity;
  (2) **correlation/clustering** (families on the Titanic, repeated measures). Coin
  example: 10 flips/day, secret sunny(p=.9)/rainy(p=.1) days → same mean 5, variance
  ~16 not 2.5. Individual coins still locked; the *single-p, independent* assumption
  is what fails.
- **Individual vs grouped format.** Titanic/World-Cup style = one row per
  person, `n=1` → variance locked → basically **can't overdisperse** (φ≈1). Grouped
  (successes-out-of-n) or clustered → can. This is the "usually vs sometimes" split.
- **When you actually reach for quasibinomial.** Only grouped/proportion or
  clustered data (seed-plots, patients-in-hospitals). You *fit and check* φ̂: ≈1 →
  keep plain family; ≫1 → keep quasi (widens SEs). Titanic 0.98 / a World-Cup
  individual fit 0.83 → no problem, don't switch. Bikeshare Poisson 90.6 → switch.
- **φ < 1 = underdispersion** (safe direction: SEs slightly conservative); φ ≫ 1 is
  the dangerous one (SEs too small → false significance).
- **Overdispersion ≠ bad predictions.** Overdispersion is a *variance* problem (fix:
  quasi family). Getting predictions *wrong* is a *mean/accuracy* problem (fix:
  better predictors; diagnose via deviance/AUC/misclassification). The dispersion
  parameter watches spread, not correctness. Also distinct from irreducible coin-flip
  noise (a 70%-then-doesn't-score player is *not* a model error).
- **Why linear has `+e` but logistic/Poisson don't.** Normal has a *separate,
  additive* variance knob (`σ²`) → noise peels off as `+e`. Bernoulli/Poisson are
  *one-parameter* → setting the mean (`p`/`λ`) locks the variance; randomness is
  baked into the coin flip / count draw, not an additive term. Same "variance locked
  by mean" idea from the other side. Overdispersion can't exist in linear regression
  (its analog is heteroscedasticity — non-constant `σ²`, a *shape* not *magnitude*
  issue).

- **Poisson inference (3d).** Statistic = **Wald z = β̂/SE(β̂)**; reference dist =
  **standard Normal** (GLM uses z, linear uses t — because GLM has no separate σ² to
  estimate). Justified by **asymptotic normality of the MLE** (large-sample, so GLM
  inference is *approximate* vs. linear's *exact* t). Equivalence: **|z|>1.96 ⟺ 95%
  CI for β excludes 0 ⟺ p<0.05** (⟺ rate-ratio CI excludes 1). Inference is on the
  **β (log-mean) scale**; exponentiate only to *report* the rate ratio.
- **3c overdispersion read (φ ≈ 90.6).** (i) severe overdispersion, true variance
  ~90× assumed; (ii) SEs/p-values untrustworthy (too small → false significance),
  coefficients still valid (mean structure untouched); (iii) quasi-Poisson keeps
  estimates but multiplies SEs by **√φ** (~9.5×), vs. Titanic φ≈0.98 → √φ≈1 → no fix.
- **Plain family vs. quasi — the trade-off.** Plain binomial/Poisson is a *real
  distribution* (→ likelihood → AIC/BIC/LRT, simulation, prediction intervals,
  efficient when φ≈1); quasi is only a mean–variance spec (no likelihood → AIC=NA,
  no LRT) but gives honest SEs under overdispersion. Workflow: fit plain → check φ →
  switch to quasi only if φ ≫ 1.

### 🟡 Watch

- **Interaction rate ratios need a group tag (2d).** In an interaction model the
  main-effect ratio (`e^b_temp = 14.7`) applies to the **reference group only**
  (non-working days); working days = 14.7 × 0.483 ≈ 7.1. Must state the group — not
  "implied." Long confusion here, now resolved via the on/off-switch framing.
- **Always say "mean/expected count"** in Poisson interpretations (rate ratio
  multiplies the *mean*, not "the number of bikers").

---

## Topic 6: Goodness of Fit (linear / LS)

### 🟢 Strong

- **The null model & what GoF compares against (1a).** Null = intercept-only
  `Y=b0+e`, predicts the **sample mean `ȳ`** for everyone (it's the LS fit with no
  predictors). Comparing a model to it asks "does `X` explain variation `ȳ` alone
  can't — is it better than *nothing*?" Self-corrected the over-eager use of
  "significant" (that's the F-test's job, not R²'s — see below).
- **Nothing here is a population parameter.** Cleared up own worry: `ȳ`, `ŷᵢ`, `yᵢ`
  are all computed from the sample; SS formulas measure distances between known
  quantities, no population mean needed. `ŷ`↔`E[Y|X]`, `ȳ`↔`E[Y]` are both estimates.
- **Sums of squares (1b), plain-English.** TSS = total variation to explain; ESS =
  what the model explained; RSS = what it missed. `TSS = ESS + RSS` holds **only with
  (1) intercept + (2) LS fit**. **LS minimizes RSS** (⇒ maximizes ESS & R², since TSS
  fixed).
- **Decomposition breaks for GLMs.** Connected it himself: GLMs are MLE-fit, so the
  LS decomposition (and hence R²/adjR²/RSE/F-test) doesn't apply → that's exactly why
  Topic 7 exists (deviance replaces RSS, χ² test replaces F). Grasped Topic 6 = linear
  version, Topic 7 = parallel GLM version of the same story.
- **`r²` vs `R²`.** `r²` = squared correlation (pair of variables / SLR only); `R²` =
  `1−RSS/TSS` (any model). Equal in SLR (`R²=r²`); only `R²` survives into MLR.
- **Explain signal, not noise.** Understood that RSS→0 / R²→1 is *bad* (overfitting —
  fitting irreducible noise `e`); low R² (e.g. protein~mRNA 0.09) can be an honest
  useful model in noisy observational data.
- **R² has no distribution → not a test (2a-ii).** Deep-dived: a significance test
  needs a statistic with a *known distribution under H₀* to get a p-value (ties to the
  3d reference-distribution idea); R² is a descriptive 0–1 ratio with none, so it can
  only *describe*, not *test*. The F-test = R² repackaged (same RSS/TSS) into a form
  that follows the known F-distribution.
- **Three R² caveats (2a).** In-sample only (says nothing out-of-sample); not a test;
  always ↑ with any predictor (even useless) → use **adjusted R²** to compare sizes.

### 🟢 Strong — inference distributions (t vs z), deep-dived

- **Linear → t, GLM → z.** Same statistic (`β̂/SE`), different reference dist. Linear
  estimates a separate `σ²` → extra uncertainty → fatter-tailed **t** (df=n−k); GLM
  has no free `σ²` (variance locked to mean) → straight to **Normal z** (large-sample
  MLE result, so *approximate* vs linear's *exact*).
- **t vs Normal.** Same bell shape; t has **fatter tails** because it *estimates* σ
  (Normal assumes σ known). Small df → fat tails → bigger critical value (>1.96);
  df→∞ → t converges to Normal (crit → 1.96).
- **Distribution of DATA ≠ distribution for INFERENCE.** Sharp question. Data dist =
  shape of one `Y` (Normal/Bernoulli/Poisson); inference dist = sampling dist of an
  *estimate* (`β̂/SE`: t or z). Poisson data is nothing like Normal yet inference is z
  — because the CLT / MLE asymptotic normality makes *estimates* Normal even when raw
  data isn't.
- **Reference dist centered at 0 ≠ "β is usually 0."** It's the **null** ("no effect")
  yardstick — "if β were 0, how would z scatter?" — the hypothesis you test *against*,
  not a belief. Far-tail z → reject 0.

### 🔴 Weak — recurring "don't skip the transformation" family

- **Squaring `r` to get R² (1d).** Wrote `r=0.3 → R²=0.3`; correct is `R²=r²=0.09`.
  Same *cousin* as the Topic 4 odds-ratio arithmetic slip — a "forgot the
  transformation step" error. **Rule:** given a correlation, always **square it**;
  `r=0.3` explains only **9%**, not 30%.

### 🟢 Strong — what "statistically significant" actually means (deep-dived)

- **Core:** significant = "the pattern is too big to be a plausible fluke of random
  sampling." Because we have a *sample* (which wobbles), even a true no-effect world
  can throw up an apparent pattern by luck; significance asks whether the pattern is
  extreme enough to rule that out. Landed via the **coin analogy** (7/10 heads = not
  significant; 70/100 = significant; same proportion, sample size changes plausibility
  of "just chance").
- **Machinery:** assume the null → p-value = P(data this extreme | null true) → small
  p (<0.05) = surprising under no-effect → reject → significant. In regression:
  `z = β̂/SE` = "how many SEs from 0"; significance = estimate **relative to its
  noise**, not raw size.
- **Significant ≠ large/important** (evidence vs. effect size): tiny effects go
  significant with huge n; big effects can be non-significant with tiny n. Report both.
- **Why R²/AIC/RSE/MSE aren't significance:** descriptive numbers with **no null
  reference distribution** → no "how surprising by chance" probability → no p-value.
  Only a **test** (F/t/z/χ²) has a known null distribution, so only a test establishes
  significance. (This is why the F-test — not R² — answers "is the model real?")

### 🟡 Watch — wording

- Say **"variation in `Y`"** (the response), not "variance in the data," when
  interpreting R². Reserve **"significant"** for the F-test, not R²/descriptive
  comparisons.
- **F-test conclusion framing (3a-iii):** state the **decision** (reject, since
  p<0.05) → meaning (≥1 slope ≠ 0, model beats the intercept-only null) → caveats (not
  *which* predictor, not good prediction). Gave the *alternative* instead of a
  conclusion at first.

---

## Topic 7: Goodness of Fit for GLMs (Deviance)

### 🟢 Strong

- **Deviance = the GLM's misfit = "RSS for GLMs."** Solid after working the
  concept: deviance `= 2·(logLik_saturated − logLik_model)` = the log-likelihood
  **gap** between your model and the **saturated (perfect)** model (one parameter
  per data point, hits every obs exactly). Measures **distance FROM perfect**, so
  it's a *misfit* score → **lower = better**; deviance 0 = perfect fit. Corrected
  own earlier "deviance = how saturated a model is" (it's misfit, not saturation).
- **Null vs residual deviance (1b).** Null deviance = intercept-only model;
  residual deviance = fitted model. A big **drop** (residual ≪ null) *describes*
  how much the predictors improved fit — but that's **descriptive**, not
  significance (significance needs the χ² deviance test). Same descriptive-vs-
  significance split flagged repeatedly.
- **Saturated ≠ best (1c, overfitting).** A model through every point overfits —
  memorizes noise, perfect on training / bad on new data. Course prefers
  good-but-not-perfect. Named overfitting correctly after a nudge.
- **The deviance test (2a/2b).** Nested GLMs: H₀ = extra coefs all 0; statistic =
  **deviance drop** `= Dev(reduced) − Dev(full)` (always ≥ 0 — MLE can zero the
  extras, so reduced always has larger deviance); reference **χ²(d)**, d = number
  of extra coefficients (categorical adds L−1); `anova(reduced, full,
  test="Chisq")`; p<0.05 → keep bigger model. Worked the sign/naming carefully
  (statistic is the *drop*, not "residual − null"; "null deviance" is only the
  model-vs-null special case).
- **Deviance ↔ RSS parallel.** Locked the mapping: RSS↔deviance, RSS drop + F ↔
  deviance drop + χ², LS↔MLE. "Perfect fit = 0" on both.

### 🟢 Strong — why GLMs swap the whole LS toolkit (deep-dived, 2c/2d)

- **Why no F-test / no R² for GLMs.** The F-test rides on the RSS decomposition
  (TSS=ESS+RSS), which exists **only** because LS makes residuals orthogonal to
  fitted values (Pythagorean split). GLMs are **MLE-fit, not LS** → no RSS, no
  decomposition → no F, no R². Replacement: deviance + χ².
- **Why LS itself fails for GLMs (three reasons, deep-dived).** (1) a straight line
  is unbounded → predicts P>1 or negative counts (link function fixes this); (2) LS
  assumes one constant-width band (σ²) but GLM variance moves with the mean
  (p(1−p), λ) → LS mis-weights points → wrong SEs; (3) minimizing squared error
  **is** MLE *only* for Normal constant-variance noise — for Bernoulli/Poisson the
  likelihood is a different formula, so best-fit maximizes *that*, not squared
  error. **The one domino:** response no longer Normal-constant-variance → LS→MLE →
  RSS→deviance → F→χ². Started confused ("why can't we use LS"), ended solid.
- **Exact vs approximate (2c).** F-test is **exact** given Normality (holds at any
  n; weak spot = *violated assumptions*, not small n). Deviance χ² test is a
  **large-sample approximation** (weak spot = small n / sparse cells / fitted probs
  near 0 or 1). Same exact-vs-approximate split as **t (exact) vs z (approximate)**
  — exact tools travel together (t, F), approximate together (z, χ²).

### 🟡 Watch

- **AIC/BIC work for both** linear and GLM (likelihood-based) — the single
  criterion that crosses the divide. But **NA for quasi** families (no likelihood).
- Keep saying **"deviance drop"** for the statistic (not "residual − null
  deviance", which flips the sign and only names the model-vs-null case).

---

## Topic 8: Model Selection (Regularization & Post-Inference)

### 🟢 Strong

- **Stepwise limitations (1a).** (i) **Greedy/path-dependent**: adds/removes the
  single best variable by AIC each step and **never reconsiders**, so the entry
  *order* is locked in → can settle on a suboptimal subset and miss the best model.
  (ii) **All-or-nothing**: a variable is either out (coef=0) or in at its **full
  OLS size** — a hard binary. Regularization is **smooth**: λ continuously shrinks
  all coefficients toward 0 (LASSO to exactly 0) → more stable, explores the
  trade-off gradually.
- **Regularized objective (1b).** minimize **fit + λ·penalty**: `RSS + λ·Σ|βⱼ|`
  (LASSO). Fit term (RSS) wants to match data; penalty term (λΣ|β|) punishes big
  coefficients. λ = tuning knob for bias–variance: **λ=0 ⇒ ordinary LS** (objective
  = RSS); larger λ ⇒ more shrinkage (LASSO → exactly 0). Intercept **not** penalized.
  Understood the LHS is just the **objective function** (argmin over β), not a named
  identity like TSS=ESS+RSS.
- **Ridge vs LASSO (1c).** Ridge L2 (λΣβ²) shrinks but **never to exactly 0** →
  keeps all predictors, **no selection**. LASSO L1 (λΣ|β|) snaps coefficients to
  **exactly 0** → shrinks **and selects**. Caught own error (had Ridge "selects =
  YES"); locked that the last two table columns must match (NO/NO vs YES/YES).
- **Why Ridge can't zero (deep-dived).** Ridge penalty force = derivative 2λβ
  **fades to 0** as β→0 (β² smooth at 0) → only approaches 0 asymptotically. LASSO
  force = **constant λ** (|β| has a **kink at 0**) → strong enough to pin
  coefficients exactly at 0. Also got the geometry (L1 diamond corners on axes vs L2
  smooth circle). The corner = selection.
- **λ=0 anchor (2a-i).** λ=0 ⇒ penalty off ⇒ pure RSS ⇒ **ordinary least squares**
  (all predictors at full size, no shrinkage/selection). As λ climbs, coefficients
  move away from OLS values.

### 🟢 Strong — how λ is chosen (2b, long deep-dive, several misconceptions fixed)

- **Two-loop structure, fully grasped.** Outer loop = grid of λ's; inner loop =
  k folds. **Objective fits β (given λ); cross-validation picks λ.** Repeatedly
  self-corrected the trap of "pick λ by minimizing the objective" — that always
  gives λ=0 (objective monotonically ↑ with λ; penalty baked in → not comparable
  across λ).
- **The compared value = held-out MSE/RSS.** For fixed λ: fit on k−1 folds → use
  those **frozen** coefficients → compute **RSS on the held-out fold** → average
  over folds = that λ's **CV error**. Key: it's RSS on **held-out** data (not
  training → can rise again → real U-shaped minimum) with **no penalty term** (same
  yardstick for all λ). Pick smallest CV error.
- **CV folds ≠ real test set.** CV carves folds *within training*; the real test
  set is **untouched** during tuning (else optimistically biased) and used **once at
  the end**.
- **Frozen-vs-refit (the subtle part he flagged).** *During* CV the fold
  coefficients are **disposable** (fit on 4 folds, used frozen to score the 5th,
  discarded). *After* CV picks λ, **refit once on the full data** at that λ → those
  are the **final** coefficients. "Disposable measuring instruments vs keeper coefs."
- **lambda.min vs lambda.1se.** CV error has SE bars, so λ's near the min are
  statistically **tied**. `lambda.min` = lowest CV error; `lambda.1se` = **largest
  λ (simplest model) within 1 SE of the min** → parsimony at no real accuracy cost
  (course usually prefers it). Got it via the "two commutes, same time ±5 min, take
  the simpler route" analogy.
- **The λ grid.** Not arbitrary/not chosen by hand: `glmnet` computes **λ_max** from
  data (smallest λ that zeros every coef) → λ_min = small fraction of it (≈OLS) →
  ~100 **continuous, log-spaced** values between. λ's are **decimals, not integers**.

### 🟢 Strong — bias–variance & standardization (2c)

- **Why accept bias.** MSE = Variance + Bias². Shrinkage adds a little **bias** but
  sharply cuts **variance** (unpenalized coefs are unstable when predictors are
  many/correlated or n small) → total MSE **falls** → better on new data. Nailed the
  net-trade framing; added the *why variance drops* mechanism after a nudge.
- **Where LASSO shines: p ≈ n or p > n.** When p>n **OLS is undefined** (no unique
  solution); p≈n → OLS wildly high-variance. LASSO makes it **solvable** and selects
  a **sparse subset** (high-dimensional/genomics setting).
- **Standardize first.** L1 penalty punishes **large coefficients**, and coefficient
  size is set by each predictor's **arbitrary units** (small-scale predictor → big
  coef → penalized/dropped harder). Standardizing (mean 0, SD 1) makes coefficients
  comparable so the penalty reflects **true importance, not measurement scale**.
  Corrected own reversed direction (thought big-coef predictor "overpowers" and drops
  the small ones — actually the **big-coef** one is penalized/dropped more).

### 🟢 Strong — LASSO is not linear-only

- **Generalizes to GLMs.** Objective = **fit + λ·penalty** where "fit" swaps
  **RSS→deviance** (same Topic 7 domino): penalized logistic/Poisson via
  `glmnet(family="binomial"/"poisson", alpha=1)`; CV scored on held-out **deviance**.
  Connected himself: "fit" is generic *so the framework isn't linear-specific."

### 🟢 Strong — double-dipping / post-selection inference (Problem 3)

- **What double-dipping is (3a).** Using the **same data twice**: dip 1 = **select**
  variables, dip 2 = **test their significance / report p-values**. Selection
  cherry-picks predictors that look strong in *this* sample (some by **noise**), so
  same-data testing gives **artificially low p-values** → declares noise significant
  → **inflates Type I error (false-positive) rate** → inference **invalid**. Root
  cause: p-values pretend variables were chosen *independently* of the data, but
  selection already used it. Worked out the two dips himself via Socratic prompts.
- **The simulation (3b).** ~1000 datasets in a **pure null world (all true coefs =
  0)** → *any* "significant" flag is **provably a false positive**. Each dataset:
  select on the data → test significance on the **same** data → record if anything
  came out significant. **Punchline:** false-positive rate should be **α=5%** but
  double-dipping inflates it **far above 5%**. **Fix = data splitting** → back to the
  honest 5% (false positives still occur, but only at the α we set). Clarified
  1000 = **datasets/reps** (to estimate a *rate*), not observations; α vs
  confidence-level terminology (α=0.05, conf=0.95).
- **postLASSO caveat (3c).** postLASSO = LASSO to **select**, then refit the
  **unpenalized** model on survivors (**OLS** for linear, **MLE/log-likelihood** for
  GLMs) → removes **shrinkage** bias only. It does **NOT** fix **selection** bias
  (winner's curse — selected coefs biased away from 0), and same-data p-values are
  still double-dipping → invalid. postLASSO specifies only the **refit method, not
  held-out data** — two independent choices (OLS-refit fixes shrinkage; data-split
  fixes selection). Nailed the two-different-biases distinction after a deep-dive.
- **The clean workflow.** LASSO to **select** → unpenalized refit to **de-shrink** →
  on a **separate split** to make inference **valid**. Two fixes for two problems.
- **Overarching takeaway (3d).** Selection and inference **can't honestly share the
  same data**; remedy = **split the data** (select on one part, infer on another).
- **Generalizes to GLMs.** Whole double-dipping story is model-agnostic — for GLMs,
  postLASSO = refit unpenalized `glm()` by MLE, same-data z/deviance p-values still
  invalid.

---

## Topic 1: Simple Linear Regression

⚪ Not directly drilled yet (but many SLR ideas surfaced via Topic 6: `R²=r²`, the
null model, `ȳ` as the LS intercept-only fit, t-inference). Created `practice_2`
gap-drills for estimation formulas & SD-vs-SE.

---

## Topics 2–3

⚪ Not covered in conversation yet. `practice_2` gap-drills exist (MLR prediction &
practical significance; log-transformed model interpretation).

---

## Note: practice sets

Two practice folders exist: `practice/` (concepts, all 9 topics + mock exam) and
`practice_2/` (computation gaps: by-hand prediction for logistic/Poisson, computing
F/deviance, reading LASSO plots, CIP/PI band shape). Advised **against** a `practice_3`
— better to *do* existing sets, run the timed mock, and drill the 🔴 odds-ratio /
squaring arithmetic.
