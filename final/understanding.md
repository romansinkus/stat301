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

## Topic 1: Simple Linear Regression

⚪ Not covered in our conversations yet.

---

## Topics 2–3, 5+

⚪ Not covered yet.
