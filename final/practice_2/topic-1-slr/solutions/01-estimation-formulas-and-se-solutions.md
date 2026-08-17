# Solutions — Practice 01 (Topic 1): Estimation Formulas & SD vs SE

> Marking: **70% procedure, 30% answer.** Show substitutions.

## Problem 1

**(a)** `β̂₁ = r·(S_y/S_x) = 0.75 × (12/3) = 0.75 × 4 = **3**` (kg per cm). Sign is **positive** →
longer fish are associated with **higher** weight. *(3 pts substitution, 1 pt direction.)*

**(b)** `β̂₀ = ȳ − β̂₁·x̄ = 40 − 3×8 = 40 − 24 = **16**`. Fitted equation: **`ŷ = 16 + 3·X`**.
It passes through `(x̄, ȳ) = (8, 40)` because the intercept formula is *derived* by forcing the line
through the mean point — least squares always makes the residuals sum to zero, which pins the line to
`(x̄, ȳ)`. *(Check: 16 + 3×8 = 40 ✓.)*

**(c)** SLR shortcut: `R² = r² = 0.75² = **0.5625 ≈ 56.25%**`. Meaning: the model explains ~56% of the
variation in fish weight. **Warning:** you must *square* `r` — `r = 0.75` is **not** "75% explained"; the
explained fraction is `r² = 56%`. (A moderate correlation explains less than it sounds.)

**(d)** At `X = 10`: `ŷ = 16 + 3×10 = **46 kg**`. For `X = 40`: the word is **extrapolation** — 40 cm is
far outside the training range (2–15 cm), so the linear relationship is unverified there and the
prediction is untrustworthy (the true relationship could bend). *(2 pts prediction, 2 pts extrapolation.)*

## Problem 2

**(a)**
- (i) **SD of errors `σ`** — the true spread of the noise `e` around the regression line (how far a
  typical observation sits from `E[Y|X]`); describes the **data-generating process**.
- (ii) **RSE** = `√(RSS/(n−p−1))` = `σ̂` — the **estimate** of that `σ` from the residuals.
- (iii) **SE(`β̂₁`)** — the estimated **standard deviation of the slope estimator** across hypothetical
  repeated samples; describes how much `β̂₁` itself would bounce around, not how the data scatter.

Estimates: **RSE and SE** (both have hats). The one describing an **estimator** (not the data) is the
**SE of `β̂₁`**. *(σ is the true parameter; RSE estimates σ; SE estimates the estimator's SD.)*

**(b)** **False.** The scatter of individual points around the line is measured by **`σ` (estimated by the
RSE)**, not by `SE(β̂₁)`. `SE(β̂₁)` measures how much the *fitted slope* would vary if you re-collected the
sample. (They're related — `SE(β̂₁) = σ̂ / (S_x·√(n−1))`-ish — but they answer different questions.)

**(c)** `SE(β̂₁)` shrinks toward **0** as `n → ∞` (more data → you pin down the slope ever more precisely,
`∝ 1/√n`). The **RSE stays put** — it estimates `σ`, the *irreducible* noise, which is a fixed property of
the world and does **not** vanish with more data. Different because one describes **estimation
uncertainty** (shrinks with n) and the other describes **irreducible spread** (fixed). *(This is the same
"two uncertainties" split as in logistic regression.)*

**(d)** **SD** describes the spread of the **data / errors** (the true variability in the population);
**SE** describes the spread of an **estimator** (a statistic like `β̂₁` or `ȳ`) across samples. `SE =
σ̂/√n` gets *smaller* with more data; the SD does not. One is about the world, the other about how well
you've measured it.
