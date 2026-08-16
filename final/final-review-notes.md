# Final review — the professor's top exam traps & "gotchas"

Distilled from the red-pen annotations on the marked slides (full detail in
`master_notes.md` → "PROFESSOR'S ANNOTATED SLIDES"). These are the things the instructor
starred, corrected, or turned into questions — i.e. the likeliest exam hooks.

## Facts to memorize
- **CI ⇄ test:** the 95% CI for a coefficient **covers 0 ⟺ fail to reject `H₀: coef = 0` at 5%.**
- **SD vs SE:** `SE = σ̂/√n` (uses the estimate); `SD` uses the true σ. SE = *estimated* SD of the estimator.
- **Slope ⇄ correlation:** `β̂₁ = r · S_y/S_x` ⇒ sign of slope = sign of correlation.
- **Model type is set by the RESPONSE:** continuous+normal → `lm`; binary → logistic; count → Poisson.
- **`lm` = least squares, `glm` = maximum likelihood** (they agree for normal errors).
- **Linear inference uses `t` (df = n−k); GLM inference uses `z` (Wald).**
- **Poisson: `E(Y)=Var(Y)=λ`.** **Bernoulli = Binomial with n=1.**
- **Single predictor: F-test = t² (same p-value).** Linear GoF test = **F**; GLM GoF test = **χ² (deviance).**
- **RSE = σ̂** (`sigma` in `glance`). **`TSS=ESS+RSS` only with LS + intercept.**
- **glmnet: `alpha=1` = LASSO, `alpha=0` = Ridge.** LASSO → exact 0 (selects); Ridge → never 0.

## Traps that cost points
- **"Why linear?"** = it's the **first-order Taylor approximation** of a smooth function. "Linear" means
  **linear in the parameters**, so `X²`, `log X`, `√X` are still linear regression.
- **Interaction model:** you **cannot** say "holding the other variable constant" — that's additive-only.
- **GLM coefficient scale:** raw β is on the **log-odds** (logistic) / **log-mean** (Poisson) scale, not the
  probability / count scale. "The mean changes by β" is FALSE — it's the *log*-mean/log-odds.
- **`predict` scale:** `type="link"` = log-odds/log-mean (default); `type="response"` = probability/count.
  `augment()$.fitted` = link scale; `fitted()` = response scale.
- **Numeric categorical:** a category coded as a number (season 1–4) must be `as.factor()` or R fits it as
  ONE continuous coefficient → wrong. Check the tidy table shows `c−1` dummy rows.
- **Multiple samples ≠ bootstrap.** Bootstrap resamples the ONE sample **with replacement**.
- **R² always increases** with more variables ⇒ can't compare nested models (use Adj R² / F-test).
- **Select-then-infer on the same data = invalid** (post-inference / double-dipping ⇒ inflated type I error);
  LASSO coefficients are **biased** so don't use LASSO for inference.
- **Rejecting the null** (model beats intercept-only) does **not** prove your predictor of interest drives Y.
- **CI misread:** a computed 95% CI does not "contain the truth with 95% probability" — the 95% is about the
  procedure across samples.

## Diagnostics quick-reference
- **Residual plot:** scatter around `Y=0`, no pattern = good; curve = non-linear; funnel = heteroscedastic.
- **Independence** comes from the **design** (temporal / repeated measures break it → SEs biased → CIs invalid).
- **Multicollinearity:** can involve **>2** variables; perfect collinearity → NA in R; inflates SEs/p-values.
  **VIF > 5–10 is a guideline;** for categoricals use **GVIF^(1/(2·Df))** vs √5 (≈2.23) / √10 (≈3.16).
- **Overdispersion** (logistic/Poisson): fit `quasibinomial`/`quasipoisson`, read φ̂ — **≈1 fine, ≫1 bad**
  (Poisson usually over-disperses; φ affects **SEs, not estimates**). Logistic residual plot is useless →
  use Pearson residuals / binned plot.

## Causality
- Association ≠ causation. Watch **reverse causality**, **Simpson's paradox** (sign flips within strata),
  **confounding** (C causes both X and Y).
- **CRD** balances observed **and unobserved** confounders (gold standard); **RBD** balances only observed
  but **blocking → smaller SE → more power**; observational studies can't establish causation naively.
