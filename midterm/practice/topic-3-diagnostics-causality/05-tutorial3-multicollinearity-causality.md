# Practice 05 (Topic 3) — Tutorial 03: Multicollinearity Workflow & Causality

*Topic 3 (multicollinearity + causality). Source: `tutorials/tutorial_03.ipynb`.
Solutions: [`solutions/05-tutorial3-multicollinearity-causality-solutions.md`](solutions/05-tutorial3-multicollinearity-causality-solutions.md).*

Part 1 uses **CASchools** (response `score` = avg of math & read); Part 2 is the **TikTok ad** confounding
simulation.

---

## Part 1 — Multicollinearity in practice

**Q1 [SA].** Describe the full **detect-and-fix workflow** for multicollinearity the tutorial follows,
from visualizing correlations to confirming the fix. Name the two visual tools and the numeric one.

---

**Q2 [SA].** `VIF` is computed with `car::vif()` on `lm(score ~ ., data = CASchools_dat)`. (a) What does
the `.` in the formula mean? (b) What VIF value indicates *no* multicollinearity, and what rule-of-thumb
thresholds flag a problem?

---

**Q3 [SA].** Only `lunch` had a VIF above 5 (≈ 5.7). It also sat in the most-correlated pair
(`calworks`–`lunch`, r = 0.74). The tutorial drops `lunch`. Explain the **rule** used to decide *which*
variable of a correlated pair to drop.

---

**Q4 [SA].** After removing `lunch`, all VIFs fell below ~2. But the tutorial also notes the **coefficients
of other variables changed.** Which variables' coefficients changed the *most*, and why those ones
specifically?

---

**Q5 [TF].** "After removing the collinear variable `lunch`, the standard errors of **all** remaining
input variables decreased." True or false? Explain what actually happens to the SEs and why.

---

**Q6 [SA].** How do you decide, from the before/after VIF tables, whether dropping `lunch` **solved** the
multicollinearity problem?

---

## Part 2 — Causality & confounders (TikTok simulation)

**Q7 [SA].** In the ad study, identify the **response `Y`**, the **treatment `X`**, and the **confounder
`C`**. State the two conditions that make `athlete` a confounder of the ad→dwell-time relationship.

---

**Q8 [SA].** Why does the tutorial use a **simulation** (1,000,000 customers with set means) instead of
real data? What does knowing the true effect (**+8 seconds**) let you do?

---

**Q9 [CALC/SA].** The three fitted models gave these ad-effect estimates:

| Model | Estimate |
| --- | --- |
| `lm(y_obs ~ x_self_choice)` (naive) | 9.83 |
| `lm(y_obs ~ x_self_choice + athlete)` (adjusted) | 7.92 |
| `lm(y_exp ~ x_randomized)` (experiment) | 8.03 |

(a) Which estimate is **biased**, in which **direction**, and **why**? (b) What do the other two show?

---

**Q10 [SA].** Explain the **two ways** to deal with a confounder demonstrated here (adjustment vs.
randomization). State the key **limitation** of the adjustment approach and the key **advantage** of
randomization.

---

**Q11 [SA].** The randomized experiment recovered the true +8 **without `athlete` in the model at all.**
Explain how that's possible — what does random assignment do to the confounder?

---

**Q12 [SA].** A colleague says: "We ran the observational regression and adjusted for `athlete`, so our
estimate is now causal and unbiased." Give the important **caveat** to that claim.
