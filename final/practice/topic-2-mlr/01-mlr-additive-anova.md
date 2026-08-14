# Practice 01 (Topic 2) — Additive MLR, k-Level Categoricals & ANOVA

*Topic 2 (MLR). Solutions:
[`solutions/01-mlr-additive-anova-solutions.md`](solutions/01-mlr-additive-anova-solutions.md).*

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Circle
> final numeric answers and respect the word limits.

---

## Problem 1 (15 pts) — Additive MLR: two parallel lines

Consider the additive model, fit on cancer-registry data (Indiana = reference):
```
Y = b0 + b1*stateWashington + b2*povertyPercent + e
```
where `Y` is the cancer death rate.

**(a) (3 pts)** "Multiple linear regression and multivariate linear regression are two names for the
same thing." True or false? Justify, and state what is *always* true about the response `Y` in this
course.

**(b) (4 pts)** This additive model is "secretly two parallel lines." Write the equation of each line
(Indiana, Washington) and say what `b0`, `b1`, and `b2` represent geometrically.

**(c) (4 pts)** State the **additive assumption** in words. Then explain the special property that makes
additive coefficients easy to interpret — the "holding the other variables constant" phrase — and why
"at any value" applies here but **not** in an interaction model.

**(d) (4 pts)** (i) Going from `lm(wage ~ education)` to `lm(wage ~ education + sex)`, the `education` CI
barely moved, from `(0.596, 0.905)` to `(0.600, 0.902)`. What does this *small* change tell you about
the relationship between `education` and `sex`, and what would a *large* change have implied? (ii) In
≤ 30 words, explain *why* a coefficient can change between its SLR and an MLR, using the idea of an
omitted variable being "dumped into the error term."

---

## Problem 2 (16 pts) — ANOVA for a categorical predictor

Consider the additive model of `wage` on `education` (continuous), `occupation` (6 levels), and `sex`
(2 levels). `anova(lm(wage ~ factor(occupation)))` returns `p ≈ 4.12e-21`.

**(a) (4 pts)** (i) Define what `anova(model)` tests for a k-level categorical predictor — write `H0`
and `H1` in words, and contrast with what the individual coefficient t-tests test. (ii) Why is the ANOVA
F-test preferred over just scanning the `k − 1` individual t-tests for the "does this variable matter at
all?" question?

**(b) (4 pts)** State the correct conclusion from `p ≈ 4.12e-21`. Be precise about what it **does** say
(which groups differ?) and what it does **not** say (does it identify which occupation is highest, or
that *every* pair differs?).

**(c) (3 pts)** A model `Y = b0 + b1*D1 + b2*D2 + b3*X` has a 3-level categorical (`D1`, `D2`) plus one
continuous `X`, additive. (i) How many fitted lines does this describe? (ii) Do they share a slope or an
intercept? (iii) How many total coefficients (including the intercept)?

**(d) (5 pts)** For the additive model of `wage` on `education`, `occupation` (6 levels), and `sex`
(2 levels): (i) write the model equation with named coefficients; (ii) how many coefficients does it
estimate, including the intercept? (iii) if you wanted a *single* test of whether occupation matters
overall, what would you compute, and what is its null hypothesis?
