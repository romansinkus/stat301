# Solutions 01 (Topic 1) — Simple Linear Regression: Estimation

*Questions: [`../01-slr-estimation.md`](../01-slr-estimation.md).*

> Marking scheme: **70% for correct procedures, 30% for correct answers.**

---

## Problem 1 — Penguin body mass

**(a)** Model:
```
body_mass_g_i = b0 + b1 * flipper_length_mm_i + e_i
                ^intercept  ^slope               ^error
```
- **`b1`** (slope): the expected change in body mass (about **+49.69 g**) for a **1 mm increase** in
  flipper length — the average "exchange rate" between flipper length and mass.
- **`e`** (error): everything about a penguin's mass that flipper length does *not* explain (other
  variables + pure noise); it is why two penguins with the same flipper length can weigh differently.

`E[Y|X] = b0 + b1*X` is **the line** — the *average* body mass over all penguins at a given flipper
length (smooth, no error term). `Y_i = b0 + b1*X_i + e_i` describes **one specific penguin**, sitting
off the line by its error `e_i`. The line is the center of the cloud; points scatter around it.

**(b)** (i) **False as stated.** Least squares minimizes the sum of **squared** vertical distances (the
residual sum of squares), not the raw distances. It *is* correct that the distances are measured
**vertically** (in the `Y` direction), because we are explaining `Y`. Corrected: "…minimizes the sum of
the **squared** vertical distances."
(ii) Two reasons to square: **(1)** squaring **removes signs** so positive and negative residuals do not
cancel (raw signed residuals sum to ~0 for any line through the mean, making them useless as a total-
error measure); **(2)** squaring **penalizes large misses disproportionately** (a residual of 4
contributes 16, while two residuals of 2 contribute only 8), so the fit works hard to avoid big errors.

**(c)** Residual `= observed − fitted = y_i − ŷ_i`, computed from the **sample**. It is only a stand-in
for `e_i` because it is measured from the **estimated** line (`b̂0, b̂1`), not the true population line
(`b0, b1`); since the estimates are not exactly the truth, the residual is not exactly `e_i`. It is not
generally 0 because points do not lie exactly on the fitted line — only the *sum* of residuals is 0.

**(d)** This is **extrapolation** — predicting outside the observed range of `X` (172–231 mm). It is
untrustworthy because we have no data out there and the relationship could bend or break down beyond
what we observed. This is Box's *"all models are wrong, but some are useful"*: the line is a useful
**approximation within its range**, not a law you can extend arbitrarily.

---

## Problem 2 — Wage and education

**(a)** (i) `ŵage = −0.746 + 0.750 × education`.
(ii) At `education = 12`: `ŵage = −0.746 + 0.750 × 12 = −0.746 + 9.00 =` **`8.25`** (≈ \$8.25/hour).
(iii) The line gives `E[wage | education]` — the **average** wage over everyone with 12 years of
education. Individuals scatter above and below the line (the error `e`), so any single person could earn
well more or less; the model predicts the center of the cloud, not one point.

**(b)** (i) **Correct:** "A one-year increase in education is **associated with** an expected increase of
about **\$0.75/hour** in wage, on average."
(ii) **Incorrect versions:**
- "Each extra year of education **causes** wages to rise by \$0.75." — asserts **causation** from
  observational data.
- "An extra year of education raises **your** wage by \$0.75." — describes an **individual** and implies
  causation; the model is about the **average**, and the claim is association only.
- *(Also wrong: reversing the roles — "a \$0.75 wage increase is associated with 1 more year of
  education." The regression of wage on education is not symmetric.)*

**(c)** A correlation of 0.382 only says wage and education **move together**; it says nothing about one
*causing* the other. The data are observational and there may be **confounders** (e.g. family background
driving both education and wage). Classic counter-example: **ice-cream sales and drowning deaths** are
strongly correlated, but neither causes the other — summer heat drives both.

**(d)** (i) **Roles:** correlation is **symmetric** (no response/predictor — it just measures the
strength of linear association); regression is **asymmetric** (one response `Y`, one predictor `X`).
(ii) **X:** correlation treats **both** variables as random; regression treats **`X` as fixed
(non-stochastic)** and models `E[Y|X]`. **Sign:** in SLR the slope and the correlation always share the
**same sign**, so a positive `r` ⇒ a positive slope.
