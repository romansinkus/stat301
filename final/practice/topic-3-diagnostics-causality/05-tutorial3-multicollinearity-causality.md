# Practice 05 (Topic 3) — Tutorial 03: Multicollinearity Workflow & Causality

*Topic 3 (multicollinearity + causality). Source: `tutorials/tutorial_03.ipynb`. Solutions:
[`solutions/05-tutorial3-multicollinearity-causality-solutions.md`](solutions/05-tutorial3-multicollinearity-causality-solutions.md).*

Part 1 uses **CASchools** (response `score` = avg of math & read); Part 2 is the **TikTok ad**
confounding simulation.

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Circle
> final numeric answers and respect the word limits.

---

## Problem 1 (15 pts) — Multicollinearity in practice (CASchools)

Only `lunch` had a VIF above 5 (≈ 5.7); it also sat in the most-correlated pair (`calworks`–`lunch`,
`r = 0.74`). The tutorial drops `lunch`.

**(a) (4 pts)** Describe the full **detect-and-fix workflow** for multicollinearity, from visualizing
correlations to confirming the fix. Name the two visual tools and the numeric one.

**(b) (4 pts)** VIF is computed with `car::vif()` on `lm(score ~ ., data = CASchools_dat)`. (i) What does
the `.` in the formula mean? (ii) What VIF value indicates *no* multicollinearity, and what thresholds
flag a problem? (iii) State the **rule** used to decide *which* variable of a correlated pair to drop.

**(c) (4 pts)** (i) After removing `lunch`, the tutorial notes the **coefficients of other variables
changed** — which ones changed the most, and why those specifically? (ii) "After removing `lunch`, the
standard errors of **all** remaining input variables decreased." True or false? Explain what actually
happens to the SEs and why.

**(d) (3 pts)** How do you decide, from the before/after VIF tables, whether dropping `lunch` **solved**
the multicollinearity problem?

---

## Problem 2 (16 pts) — Causality & confounders (TikTok simulation)

The three fitted models gave these ad-effect estimates (true effect = **+8 seconds**):

| Model | Estimate |
| --- | --- |
| `lm(y_obs ~ x_self_choice)` (naive) | 9.83 |
| `lm(y_obs ~ x_self_choice + athlete)` (adjusted) | 7.92 |
| `lm(y_exp ~ x_randomized)` (experiment) | 8.03 |

**(a) (4 pts)** (i) Identify the **response `Y`**, the **treatment `X`**, and the **confounder `C`**, and
state the two conditions that make `athlete` a confounder. (ii) Why use a **simulation** (1,000,000
customers with set means) instead of real data — what does knowing the true effect (+8) let you do?

**(b) (5 pts)** (i) Which estimate is **biased**, in which **direction**, and **why**? (ii) What do the
other two estimates show?

**(c) (4 pts)** Explain the **two ways** to deal with a confounder demonstrated here (adjustment vs.
randomization); state the key **limitation** of adjustment and the key **advantage** of randomization.
The experiment recovered the true +8 **without `athlete` in the model at all** — explain how that is
possible.

**(d) (3 pts)** A colleague says: "We ran the observational regression and adjusted for `athlete`, so our
estimate is now causal and unbiased." Give the important **caveat** to that claim.
