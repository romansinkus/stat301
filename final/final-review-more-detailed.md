# Final Review — Detailed (slide-by-slide, with added depth)

*A slide-by-slide transcription of the professor's **`slides/final-review.pdf`** (34 slides), each
expanded with **"🔍 More detail"** — the stuff that's implied, adjacent, or a known exam trap but **not
written on the slide itself.** The review deck only covers **post-midterm** material (Topics 4–9); pair
this with [`final-review-notes.md`](final-review-notes.md) (the annotated-slide traps) and
[`master_notes.md`](master_notes.md).*

---

## Slides 1–3 — Exam logistics

**On the slides:**
- **Wednesday, August 19, 2026, 3:30–5:40pm (130 min), Life Building 2302**, in person. Then ≤ 20 min
  (5:40–6:00) to upload a **single PDF** to Canvas ("Final Exam Solutions upload here").
- Format **similar to the midterm**. Write on the exam paper (scan) or on laptop, then upload.
- **Cumulative**, all term, but **more weight on post-midterm** material.
- **Closed book/notes**, but **two letter-size sheets (both sides, written or typed)**.
- **Internet/Canvas only at the very end** (for uploading). **Simple calculator** required.
- This review **only covers post-midterm**; review pre-midterm yourself. **R code isn't tested directly —
  but you must read R outputs.** Picture ID checked.

**🔍 More detail:**
- **Two sheets vs. the midterm's one** — use the extra sheet for the post-midterm density (the 3-scale
  logistic table, overdispersion workflow, deviance/F/χ² mapping, LASSO, CIP-vs-PI).
- **"Written answers only, no MCQ"** — 70% of marks are for **procedure/showing steps**, 30% for the final
  answer. Circle final numbers; state interpretations in full sentences with the exact words ("associated
  with", "log-odds" vs "odds" vs "probability", "holding constant").
- **"Read R outputs"** means: `tidy()`/`summary()` coefficient tables (est, SE, z/t, p, CI),
  `glance()` (R², adj R², sigma, F, AIC, deviance), `anova()` (F-test / χ² deviance test), VIF/GVIF,
  residual & Q-Q plots, LASSO coefficient paths, CV curves, and `predict()` CI/PI output.

---

## Slide 4 — Post-midterm roadmap

**On the slide:** Logistic regression · Poisson regression · Model diagnostics & evaluation · Variable
selection (stepwise, LASSO) · Post-inference, Prediction uncertainty.

**🔍 More detail:** the spine that ties it together is the **GLM** (slide 14): every model is
`g(E[Y]) = β0 + β1x1 + … + βpxp`. The response type picks the link `g`. Everything after (goodness of fit,
selection, prediction) is the *same* set of questions asked for each model type.

---

## Slide 5 — Logistic: three equivalent forms

**On the slide:** a logistic model for a **binary response**, written three equivalent ways:
- **log-odds:** `log( P(Y=1)/(1−P(Y=1)) ) = β0 + β1x1 + … + βpxp`
- **odds:** `P(Y=1)/(1−P(Y=1)) = e^β0 · e^β1x1 ··· e^βpxp`
- **probability:** `P(Y=1) = exp(β0+…)/(1 + exp(β0+…))`

`P(Y=1)/(1−P(Y=1))` is the **odds of "Y=1"**.

**🔍 More detail:**
- These are the **three scales** you interpret on: **log-odds** (additive `+`, where the model is linear),
  **odds** (multiplicative `×`, from `exp`-ing coefficients → odds ratios), and **probability** (the
  S-curve, for prediction of a specific case).
- **There is NO `+ e` error term** in these equations — they define the mean (`P(Y=1)`) *exactly*. The
  randomness lives in the **Bernoulli coin flip** of `Y` given `p`, not in an additive noise term. (Common
  exam trap: writing `logit = β0+β1x+e`.)
- **Prediction by hand (likely exam task):** compute the linear predictor `L = β̂0+β̂1x`, then
  `p = e^L/(1+e^L)`; as a classifier, threshold at 0.5.
- **Why go through the logit?** A probability is trapped in (0,1); a straight line isn't. The logit
  stretches (0,1) onto the whole real line so a linear predictor is valid.

---

## Slide 6 — Logistic assumptions & Bernoulli moments

**On the slide:** (1) `Y` takes two values (0/1); (2) `Y` follows **Binomial/Bernoulli**; (3) the data are
**independent**. For Bernoulli: `E(Y) = P(Y=1)` and `Var(Y) = E(Y)(1−E(Y))` — "**very different from a
normal distribution where mean and variance are un-related.**"

**🔍 More detail:**
- The line "mean and variance are *related*" is the **conceptual seed of overdispersion** (slides 9–10):
  because `Var` is *locked* to the mean by the distribution, there's no free `σ²` knob — so the data can
  have *more* spread than `E(Y)(1−E(Y))` allows.
- **This is why linear regression has `+e` and logistic doesn't:** Normal has a *separate* variance
  parameter `σ²` (mean and variance unrelated → additive noise); Bernoulli has *one* parameter `p` (mean
  fixes variance → no separate noise term).
- **Independence comes from the study design**, not a plot (clustering / repeated measures break it).
- **Bernoulli = Binomial with n = 1** (flagged on the annotated slides).

---

## Slide 7 — Logistic: estimation & coefficient interpretation

**On the slide:** estimates via **maximum likelihood** through an **iterative algorithm** (so it *may not
converge*). `βj` interprets as: **log-odds** of "Y=1" in an **additive model**, or **odds** of "Y=1" via
`e^βj` in a **multiplicative model** (odds *ratio* for a binary predictor). Interactions & categorical
predictors: same as MLR.

**🔍 More detail:**
- **MLE vs least squares:** `lm` uses **least squares (closed-form)**; `glm` uses **MLE (iterative, Fisher
  scoring)**. They *coincide* only for Normal errors — which is why "linear regression is a GLM fit by
  MLE" isn't a contradiction.
- **`glm()` raw coefficients = log-odds; `exponentiate = TRUE` → odds ratios** (estimate + CI only, **not**
  the SE).
- **Percent change from an odds ratio (recurring trap):** `OR > 1` → increase `= (OR−1)×100`; `OR < 1` →
  decrease `= (1−OR)×100`. Never multiply the raw OR by 100. Watch decimals: OR `1.008` = **0.8%** up, not
  8%.
- **Additive vs interaction:** additive = **parallel** on the log-odds scale (a constant gap, "holding
  constant" is legal); interaction = the effect of one predictor **depends on** another → you **cannot**
  say "holding the other constant," and a main-effect odds ratio applies to the **reference group only**.

---

## Slide 8 — Logistic: inference & residuals

**On the slide:** inference on `βj` uses a **normal distribution (CLT)**. **Residuals** exist but use
**Pearson** or **deviance** residuals (because mean and variance are related); residual plots are **less
useful** than for linear models. The more important diagnostic is **overdispersion**.

**🔍 More detail:**
- **GLM inference uses `z` (Wald), linear uses `t`.** Same statistic `β̂/SE`, different reference
  distribution. GLM has no separate `σ²` to estimate → straight to Normal; but it's a **large-sample**
  (asymptotic MLE) result, so inference is **approximate**, whereas linear's `t` is **exact** under Normal
  errors. Equivalence: **|z|>1.96 ⟺ CI excludes 0 (log-odds) / 1 (odds) ⟺ p<0.05.**
- **Why the raw residual plot is useless:** with 0/1 `Y`, residuals collapse onto **two lines** (`−p̂` and
  `1−p̂`), and the variance `p(1−p)` changes with `p` *by design* — so non-constant spread is expected, not
  a flaw. Hence Pearson/deviance residuals or **binned** residual plots.

---

## Slides 9–10 — Overdispersion (logistic) & the dispersion parameter

**On the slides:** **over-dispersion** = the data's variance exceeds the Bernoulli/Binomial value:
`Var(Y) > E(Y)(1−E(Y))`. Then the assumed distribution doesn't hold, and **R's estimates and SEs are not
correct** (they're computed under the assumed distribution). Fix by introducing a **dispersion parameter
η**: `Var(Y) = η·E(Y)(1−E(Y))`. If the Binomial holds, `η = 1`. Use **`quasibinomial`** in R to estimate
`η`; if `η` is far from 1, use the quasibinomial results.

**🔍 More detail:**
- **Overdispersion damages SEs/p-values, NOT the point estimates** — the coefficients come from the *mean
  structure*, which is untouched; the SEs are computed from the *assumed variance*, which is too small.
  Quasibinomial keeps the estimates and **multiplies SEs by √η**.
- **Individual (n=1) logistic basically can't overdisperse** — a single 0/1 outcome's variance is locked
  at `p(1−p)`. Overdispersion appears only with **grouped/binomial data** (successes-out-of-n, hidden
  heterogeneity) or **correlated/clustered** data. This is why it's the "**sometimes**" case for logistic.
- **`η < 1` = under-dispersion** (safe direction — SEs slightly conservative); **`η ≫ 1`** is dangerous
  (SEs too small → false significance).
- **Workflow:** fit plain → refit quasi, read `η` → keep plain if `η ≈ 1`, keep quasi if `η ≫ 1`. (Note:
  quasi is *not* a real distribution → no AIC/likelihood-ratio test; that's the cost.)

---

## Slide 11 — Poisson: model & assumptions

**On the slide:** for **count responses**. Additive: `log(E(Y)) = β0+β1x1+…+βpxp`; multiplicative:
`E(Y) = e^β0 e^β1x1 ··· e^βpxp`. Assumptions: (1) `Y` is a count; (2) `Y ~ Poisson`; (3) independent.

**🔍 More detail:**
- **The log link guarantees `E(Y) > 0`** (since `e^anything > 0`) — cures the "linear regression predicts
  negative counts" problem.
- **`factor()` gotcha (flagged trap):** a categorical stored as numbers (season 1–4, or `workingday` if
  multi-level) must be `as.factor()` — otherwise R fits ONE continuous slope instead of `c−1` dummies.
  Check the tidy table shows the dummy rows.
- **Two example count responses** (exam sometimes asks): goals scored per game, machine failures per week.

---

## Slide 12 — Poisson: interpretation, inference, residuals

**On the slide:** `βj` measures association with the **log mean count** (additive) or **mean count**
(multiplicative). Inference like logistic (Normal, via CLT). Residual diagnostics via **Pearson/deviance**
residuals.

**🔍 More detail:**
- **Always say "mean/expected count"** — a rate ratio `e^βj` multiplies the **mean** count, not "the number
  of" events.
- **Rate ratio** = Poisson's analog of the odds ratio: `e^βj` = multiplicative effect on the mean. Percent
  change uses the same `(RR−1)×100` / `(1−RR)×100` rules.
- **Prediction by hand:** `λ̂ = e^(β̂0+β̂1x)`; if the mean is 40 now, one unit up is `40 × e^β1` (a
  *multiply*, because coefficients act on the log-mean).

---

## Slide 13 — Poisson: mean = variance & overdispersion

**On the slide:** if Poisson holds, `Var(Y) = E(Y) = e^(β0+…)`. If the observed variance is larger
(`Var(Y) = η E(Y)`, `η > 1`), you have **overdispersion** — use **`quasipoisson`**. Overdispersion is
**more common in Poisson than logistic**, and is **more important than residual plots**.

**🔍 More detail:**
- **Why Poisson usually overdisperses but logistic often not:** `Var = λ` is one rigid knob real counts
  routinely break (clustering, bursts, unmodeled predictors), and a count is *unbounded* (infinite room to
  overshoot its mean); a 0/1 outcome is *bounded* and variance-locked, so it rarely overdisperses.
- **A single "safe big η" isn't the goal — calibration is.** Under-estimating η → false significance;
  over-estimating → CIs so wide you can't detect real effects (no power). That's why R **estimates** η from
  the data rather than assuming it.
- **Course numbers:** Bikeshare quasipoisson `η ≈ 90.6` (severe → true variance ~90× assumed → keep quasi,
  SEs ×√90.6 ≈ 9.5); Titanic logistic `η ≈ 0.98` (≈1 → no fix).

---

## Slide 14 — The GLM unification

**On the slide:** all three models are a **generalized linear model**: `g(E(Y)) = β0+β1x1+…+βpxp`, where
`g` is the **link function** and `L = β0+…+βpxp` is the **linear predictor**. The link depends on the
response: **linear** `g(y)=y` (identity); **logistic** `g(y)=log(y/(1−y))` (logit); **Poisson**
`g(y)=log(y)` (log).

**🔍 More detail:**
- **The response type sets the model** (a flagged fact): continuous+Normal → `lm`; binary → logistic
  (logit); count → Poisson (log).
- **`predict()` scale trap:** `type="link"` (default) returns the **linear predictor** (log-odds /
  log-mean); `type="response"` returns the **probability / mean count**. (`augment()$.fitted` = link scale;
  `fitted()` = response scale.)
- The GLM view is *why* Topics 6 (linear GoF) and 7 (GLM GoF) are parallel: same questions, different
  link → different fit measure (RSS ↔ deviance) and test (F ↔ χ²).

---

## Slide 15 — Two questions for any model

**On the slide:** for any regression model, consider **goodness-of-fit** (how well it fits) and
**model/variable selection** (which predictors to include).

**🔍 More detail:** these map to Topics 6–7 (goodness of fit) and Topic 8 (selection). Keep them separate:
*descriptive* fit (R², deviance) vs. *inferential* comparison (F-test, χ² deviance test) vs. *selection*
(AIC, LASSO).

---

## Slide 16 — Variance decomposition (linear)

**On the slide:** for linear models, `TSS = ESS + RSS`, i.e.
`Σ(yᵢ−ȳ)² = Σ(ŷᵢ−ȳ)² + Σ(yᵢ−ŷᵢ)²`. TSS = total variation, ESS = explained by the model, RSS = noise.

**🔍 More detail:**
- **The decomposition holds ONLY with (1) an intercept and (2) an LS fit.** It **breaks for GLMs** (MLE),
  which is exactly why they need deviance instead (Topic 7).
- **LS minimizes RSS** (⇒ maximizes ESS and R², since TSS is fixed by the data).
- Everything is computed from the **sample** (`yᵢ`, `ŷᵢ`, `ȳ`) — no population parameters needed. `ȳ` is the
  **null (intercept-only) model's prediction**.

---

## Slide 17 — R² and AIC

**On the slide:** `R² = ESS/TSS = 1 − RSS/TSS` = proportion of total variation explained; larger is
preferred. **AIC** is another criterion; **smaller AIC** is preferred.

**🔍 More detail:**
- **In SLR, `R² = r²`** (square of the correlation). Given a correlation, **square it**: `r = 0.3` →
  R² = 0.09 (9%), *not* 30%.
- **Three critical R² caveats:** (1) computed **in-sample** (says nothing out-of-sample); (2) it is **NOT a
  significance test** — it has **no known distribution**, so no p-value (the F-test is R² repackaged into
  something with the F-distribution); (3) it **always increases** with any predictor (even useless) → can't
  compare different-sized models. Hence adjusted R² (next slide).
- **Chasing R² → 1 is overfitting** (fitting the irreducible noise `e`); a low R² (protein~mRNA ≈ 0.09) can
  still be an honest, useful model in noisy observational data.

---

## Slide 18 — Adjusted R²

**On the slide:** R² favors larger models, but we prefer **parsimonious** models. **adjusted R² =
1 − [RSS/(n−p−1)] / [TSS/(n−1)]**, where `p` = # predictors. Use it to compare models.

**🔍 More detail:**
- The `n−p−1` divisor **penalizes extra variables**: a useless predictor lowers RSS only slightly but costs
  a degree of freedom, so adjusted R² can **go down**. That's what makes it fair across different sizes
  (unlike raw R²).
- Analogy: raw R² = extra credit for *attempting* anything; adjusted R² = a grader who **deducts for
  busywork**. Adjusted R² exists **only for linear models** (there's no adjusted R² for GLMs — that's
  deviance/AIC's job).

---

## Slides 19–20 — RSE and MSE

**On the slides:** **RSE = √(RSS/(n−p−1))**, a good estimate of the error variance in `y=β0+β1x+e`,
`e ~ N(0,σ²)` (slide writes "σ̂² = RSE"). **MSE = (1/n)Σ(yᵢ−ŷᵢ)²** measures how close fitted values are to
observed; smaller = better fit.

**🔍 More detail:**
- **Careful with the slide's `σ̂² = RSE`:** RSE **is `σ̂`** — it estimates `σ`, the *standard deviation* of
  the errors (the professor's own trap sheet says "RSE = σ̂ = `sigma` in `glance`"). So `σ̂ = RSE` and
  `σ̂² = RSE²`. RSE is on the scale of `Y`; the *variance* is its square.
- **Don't confuse RSE with the SE of a coefficient:** RSE = spread of the **data/errors** around the line;
  `SE(β̂)` = spread of the **estimator** across samples. As `n→∞`, `SE(β̂)→0` but **RSE stays put** (it
  estimates irreducible noise).
- **Training vs testing MSE:** training MSE uses the fitting data (optimistic); **testing MSE** on
  held-out data is the honest measure of out-of-sample prediction.

---

## Slide 21 — Three GoF metrics + the need for a test

**On the slide:** **adjusted R², RSE, and MSE** measure GoF for MLR. We pick large adj R² / small RSE-MSE,
**but** the chosen model may or may not be **significantly** better — that needs a **hypothesis test
(F-test or χ²-test).**

**🔍 More detail:** this is the key **descriptive vs. inferential** split. A number being bigger/smaller
(descriptive) is not the same as "significantly better" (a test with a p-value). The next slides give the
tests: **F for linear, χ² deviance for GLMs.**

---

## Slides 22–23 — The F-test for nested linear models

**On the slides:** hypothesis testing compares **nested models**. Model I (`q` predictors) nested in Model
II (`p` predictors, `p>q`). Test `H0: β_{q+1}=…=β_p = 0`. Statistic:
`F = [(RSS_I − RSS_II)/(p−q)] / [RSS_II/(n−p−1)]`, compared to `F(p−q, n−p−1)`. Done in R.

**🔍 More detail:**
- **"Nested" is required** — the small model's predictors must be a **subset** of the big model's;
  otherwise `RSS_I − RSS_II` isn't a clean "effect of dropping these terms" and the F-distribution doesn't
  apply.
- **R commands:** `glance(model)` gives the model-vs-null F (reduced = intercept-only); `anova(reduced,
  full)` compares any nested pair.
- **`F = t²`** for a single predictor (same p-value); linear GoF test = **F**, GLM = **χ²**.
- **The punchline trap:** a significant F means the bigger model **fits significantly better** — it does
  **NOT** mean "we can predict Y well," nor that a *specific* predictor of interest drives Y.

---

## Slides 24–25 — The deviance test for nested GLMs

**On the slides:** for logistic/Poisson, compare nested models with the **deviance** ("a generalization of
RSS"; lower = better fit) via the **deviance test** (χ²). Model I nested in Model II; `H0: β_{q+1}=…=β_p=0`;
**statistic = Deviance(I) − Deviance(II)**, compared to `χ²(p−q)`. Done in R.

**🔍 More detail:**
- **R command:** `anova(reduced, full, test = "Chisq")`. **`glm` prints a null deviance** (intercept-only)
  and a **residual deviance** (your model); the drop = evidence the predictors help.
- **Why not the F-test?** The F rests on the LS sum-of-squares decomposition, which doesn't hold for MLE
  fits. Deviance (likelihood-based) replaces RSS; the **workflow is identical** (fit reduced vs full,
  compare, reject if the improvement is significant).
- **Large-sample caveat:** the χ² reference is an approximation — distrust it with small `n` or sparse/rare
  events.
- **A perfect (saturated) fit is bad** — it fits noise (overfitting); you want good-but-not-perfect.

---

## Slide 26 — AIC and BIC

**On the slide:** **AIC = goodness-of-fit + penalty for # predictors**; smaller is better; picks a model
that fits well without too many predictors. **BIC** is similar.

**🔍 More detail:**
- **AIC works for BOTH linear and GLMs** (it's likelihood-based) — it's the single criterion that bridges
  the F-world and the deviance-world. (`AIC = −2·logLik + 2·k`.)
- **BIC penalizes size more heavily** (penalty grows with `log n`), so it favors **smaller** models than
  AIC.
- AIC is what **`step()`** optimizes. Unlike the F/χ² tests, AIC/adjusted-R² let you compare models that
  **aren't nested**.

---

## Slide 27 — Stepwise selection

**On the slide:** **stepwise** selection is **forward** (start null, add predictors one at a time by AIC),
**backward** (start full, delete one at a time by AIC), or both.

**🔍 More detail:**
- **`drop1`/`add1`** = one-move what-if tables (remove/add each single variable); **`step()`** = the full
  automated loop. Both work on `lm` **and** `glm`.
- Stepwise is **greedy** — the *order* variables enter matters and it can miss the best subset; and it's
  **all-or-nothing** (a variable is fully in or fully out). Its post-selection p-values suffer
  double-dipping (slide 31).

---

## Slides 28–29 — LASSO (regularization)

**On the slides:** stepwise is all-or-nothing (coef 0 or not). Can we **shrink smoothly**? **LASSO** (least
absolute shrinkage and selection operator) is such a **regularized** method. It penalizes coefficient size:
minimize **`RSS + λ Σ|βj|`**. At `λ=0` → least squares. As `λ` grows, coefficients shrink and some become
**exactly 0** (removed). Choose `λ` by **cross-validation** (minimize MSE).

**🔍 More detail:**
- **LASSO = L1 penalty (`Σ|βj|`) → can hit exactly 0 → selects variables.** **Ridge = L2 penalty (`Σβj²`)
  → shrinks smoothly but never to 0 → never selects.** (`glmnet`: `alpha=1` LASSO, `alpha=0` ridge.)
- **Standardize predictors first** — the penalty is on coefficient *size*, which depends on units; without
  standardizing, selection reflects units, not importance.
- **Bias–variance:** LASSO deliberately **biases** estimates to cut variance (`MSE = Variance + Bias²`);
  worth it especially when **`p` is large relative to `n`**.
- **CV reading:** `lambda.min` = min CV error; **`lambda.1se`** = largest `λ` within 1 SE of the min
  (simpler model, usually preferred). CV splits the **training** data (k-fold, usually k=10) — it does
  **not** touch the real test set.

---

## Slide 30 — LASSO is biased → select then re-fit

**On the slide:** LASSO builds strong **predictive** models, but its estimates `β̂j` are **biased**
(`E[β̂j] ≠ βj`). Solution: use LASSO to **select** predictors, then use **least squares** for **inference**.

**🔍 More detail:**
- This is **postLASSO**. But the fix only works **honestly if selection and inference use different data**
  — re-fitting OLS on the LASSO-selected variables *on the same data* still double-dips (next slide). LASSO
  coefficients are biased, so **never report LASSO coefficients for inference**.

---

## Slide 31 — Post-inference / double-dipping

**On the slide:** using the **same data** to select predictors *and* do inference → **inflated Type I
error** (the **post-inference problem**). Fix: **split the data** — one part to select, the other for
inference.

**🔍 More detail:**
- **The "two dips":** (1) peek at the data to pick "significant" variables, (2) test those same variables
  on the same data → the p-values are no longer valid (you already used the data to choose what to test).
  A simulation with all true `β = 0` shows the Type I error rate blows past 5%; **splitting restores it.**
- **Careful:** the slide ties this to "cross-validation," but the specific remedy is **sample splitting**
  (a selection set + an inference set). CV is the related idea of repeated splitting used for *tuning* `λ`.
- **Broader takeaway (flagged trap):** select-then-infer on the same data is invalid; LASSO coefficients
  are biased so don't use them for inference; rejecting the null doesn't prove your predictor of interest
  drives `Y`.

---

## Slide 32 — Prediction uncertainty

**On the slide:** a predicted `ŷᵢ` has **two sources of uncertainty**: the usual **sample-to-sample
variation** (in the estimated line), and the **error term `e`** in the linear model. This is **prediction
uncertainty.**

**🔍 More detail:**
- The two sources map to the two intervals: the **Confidence Interval for the Prediction (CIP)** targets
  the **average** `E[Y|X]` — only estimation uncertainty; the **Prediction Interval (PI)** targets a
  **single actual** `Y` — estimation **plus** the irreducible `e`. So the **PI is always wider**.
- **Language:** CIP uses **"confidence"** (target is a fixed number, `E[Y|X]`); PI uses **"probability"**
  (target is a random variable, an individual `Y`). `predict(interval="confidence")` vs
  `predict(interval="prediction")`.
- **Band shape:** both bands are **narrowest at `x̄`** and **flare** as `X` moves away (uncertainty grows
  with `(X−x̄)`). The `geom_smooth(se=TRUE)` shaded band is the **CIP** (mean line), **not** where 95% of
  points fall — that's the PI.
- **Extrapolation** far from the data makes both the point estimate *and* the interval width untrustworthy.

---

## Slides 33–34 — Closing

**On the slides:** questions on Piazza or office hour **Tuesday, August 19 [sic], 2–3pm via Zoom**. "Thank
you! See you Wednesday, August 19."

**🔍 More detail:** the office-hour date on the slide reads "Tuesday, August 19," but **Aug 19 is the
Wednesday exam day** — the office hour is almost certainly **Tuesday, August 18** (the day before).
Confirm on Canvas/Piazza if you plan to attend.

---

## One-page mental map (the whole post-midterm in a breath)

1. **GLM** `g(E[Y]) = β0+β1x…` unifies everything; the **response** picks the link (identity / logit /
   log).
2. **Logistic** (binary): 3 scales (log-odds/odds/prob), odds ratios, no `+e`, z-inference, residual plots
   useless → watch **overdispersion** (`quasibinomial`, but rare for individual data).
3. **Poisson** (count): rate ratios, log link (no negatives), `mean = variance` → **usually
   overdispersed** (`quasipoisson`).
4. **Goodness of fit:** linear → `TSS=ESS+RSS`, R²/adjR²/RSE/MSE, **F-test**; GLM → **deviance**, **χ²
   test**; **AIC** bridges both. R² isn't a test; a significant test ≠ good prediction.
5. **Selection:** stepwise (greedy, AIC) vs **LASSO** (L1, shrinks to 0, standardize, tune `λ` by CV);
   ridge never selects.
6. **Post-inference:** select-then-test on the same data inflates Type I error → **split the data**.
7. **Prediction uncertainty:** **CIP** (mean, narrower, "confidence") vs **PI** (individual, wider,
   "probability"); bands pinch at `x̄`.
