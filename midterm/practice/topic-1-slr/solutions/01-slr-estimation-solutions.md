# Solutions 01 — Simple Linear Regression: Estimation

*Questions: [`../01-slr-estimation.md`](../01-slr-estimation.md).*

---

**Q1.**
```
body_mass_g_i = b0 + b1 * flipper_length_mm_i + e_i
                ^intercept  ^slope               ^error
```
- **`b1`** (slope): the expected change in body mass (g) for a **1 mm increase** in flipper length —
  the "exchange rate" between flipper length and mass, on average.
- **`e`** (error): everything about a penguin's mass that flipper length does *not* explain (other
  variables + pure noise); it's why two penguins with the same flipper length can weigh differently.

---

**Q2.** `E[Y|X] = b0 + b1*X` is **the line** — the *average* of `Y` over all individuals at a given
`X` (smooth, no error term). `Y_i = b0 + b1*X_i + e_i` describes **one specific observation**, which
sits off the line by its error `e_i`. The line is the center of the cloud; individual points scatter
around it.

---

**Q3.** **False as stated.** Least squares minimizes the sum of **squared** vertical distances (the
sum of squared residuals), not the raw vertical distances. It *is* correct that the distances are
measured **vertically** (in the `Y` direction), because we're explaining `Y`. Corrected: "minimizes
the sum of the *squared* vertical distances."

---

**Q4.** Two reasons:
1. **Squaring removes signs** so positive and negative residuals don't cancel (raw signed residuals
   would sum to ~0 for any line through the mean, making them useless as a total-error measure).
2. **Squaring penalizes large misses disproportionately** — a residual of 4 contributes 16 while two
   residuals of 2 contribute only 8 — so the fit works hard to avoid big errors. (Absolute values
   fix the sign problem but don't punish big misses extra, and are harder to optimize analytically.)

---

**Q5.** Residual `= observed Y_i − fitted Y_i` (`= y_i − y_i_hat`), computed from the **sample**. It's
only a *stand-in* for the error because it's measured from the **estimated** line (`b0hat`, `b1hat`),
not the true population line (`b0`, `b1`); since our estimates aren't exactly the truth, the residual
isn't exactly `e_i`. It isn't generally 0 because individual points don't lie exactly on the fitted
line — only the *sum* (and mean) of residuals is 0 for the least-squares line.

---

**Q6.** **Correct:** "A one-year increase in education is **associated with** an expected increase of
about **\$0.75/hour** in wage, on average."
**Incorrect versions:**
- "Each extra year of education **causes** wages to rise by \$0.75." — asserts **causation** from
  observational data.
- "An extra year of education raises **your** wage by \$0.75." — describes an individual and implies
  causation; the model is about the **average**, and it's association only.

---

**Q7.** A correlation of 0.382 only says wage and education **move together**; it says nothing about
one *causing* the other. There could be confounders (e.g. family background driving both education
and wage), and the data are observational. Classic counter-example: **ice-cream sales and drowning
deaths** are strongly correlated, but neither causes the other — summer heat drives both.

---

**Q8.** (a) **Roles:** correlation is **symmetric** (no response/predictor — it just measures the
strength of linear association); regression is **asymmetric** (one response `Y`, one predictor `X`).
(b) **X:** correlation treats both variables as random/stochastic; regression treats **`X` as fixed
(non-stochastic)** and models `E[Y|X]`. **Sign:** in SLR the slope and the correlation always share
the **same sign** (both carry the sign of the covariance), so a positive `r` ⇒ a positive slope.

---

**Q9.** This is **extrapolation** — predicting outside the observed range of `X` (172–231 mm). It's
untrustworthy because we have no data out there and the true relationship could bend or break down
beyond what we saw. This is Box's *"all models are wrong, but some are useful"*: the line is a useful
**approximation within its range**, not a law of nature you can extend arbitrarily.

---

**Q10.**
(a) Fitted equation: `wage_hat = −0.746 + 0.750 * education`.
(b) At `education = 12`: `wage_hat = −0.746 + 0.750 × 12 = −0.746 + 9.00 = **8.25**` (≈ \$8.25/hour).
(c) The regression line gives `E[wage | education]` — the **average** wage over everyone with 12 years
of education. Individuals scatter above and below the line (that's the error term `e`), so any single
12-year person could earn well more or less than \$8.25; the model predicts the center of the cloud,
not one point.
