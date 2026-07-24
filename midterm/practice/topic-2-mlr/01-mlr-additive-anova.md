# Practice 04 — Additive MLR, k-Level Categoricals & ANOVA

*Topic 2 (MLR). Solutions: [`solutions/01-mlr-additive-anova-solutions.md`](solutions/01-mlr-additive-anova-solutions.md).*

---

**Q1 [TF].** "Multiple linear regression and multivariate linear regression are two names for the
same thing." True or false? Justify, and state what is *always* true about the response `Y` in this
course.

---

**Q2 [SA].** In the additive model `Y = b0 + b1*stateWashington + b2*povertyPercent + e` (Indiana =
reference), this is "secretly two parallel lines." Write the equation of each line and say what
`b0`, `b1`, and `b2` represent geometrically.

---

**Q3 [SA].** State the **additive assumption** in words. Then explain the special property that makes
additive-model coefficients easy to interpret — the phrase involving "holding the other variables
constant" — and why the phrase "at any value" applies here but *not* in an interaction model.

---

**Q4 [SA].** In-class Activity 3: going from `lm(wage ~ education)` to `lm(wage ~ education + sex)`,
the education CI barely moved from `(0.596, 0.905)` to `(0.600, 0.902)`. What does this *small*
change tell you about the relationship between `education` and `sex`? What would a *large* change
have implied?

---

**Q5 [SA].** A predictor's coefficient often **changes** between its SLR and an MLR that includes
other predictors (e.g. `PctPrivateCoverage` alone vs. with `povertyPercent`). Explain *why*, using
the idea of an omitted variable being "dumped into the error term."

---

**Q6 [SA].** Define what `anova(model)` tests for a k-level categorical predictor. Write the null and
alternative hypotheses in words, and contrast it with what the individual coefficient t-tests test.

---

**Q7 [SA].** `anova(lm(wage ~ factor(occupation)))` returns `p ≈ 4.12e-21`. State the correct
conclusion. Be precise about what this *does* say (which groups differ?) and what it does **not** say
(does it identify which occupation is highest, or that *every* pair differs?).

---

**Q8 [SA].** Why not just look at the `k − 1` individual coefficient t-tests instead of running one
ANOVA F-test? Give the statistical reason ANOVA is preferred for the "does this variable matter at
all?" question.

---

**Q9 [CALC].** A model `Y = b0 + b1*D1 + b2*D2 + b3*X` has a 3-level categorical (`D1`, `D2`) plus one
continuous `X`, additive. (a) How many fitted lines does this describe? (b) Do they share a slope or
an intercept? (c) How many total coefficients (including intercept)?

---

**Q10 [SA].** Consider the additive model of `wage` on `education` (continuous), `occupation`
(6 levels, categorical), and `sex` (2 levels). (a) Write the model equation with named coefficients.
(b) How many coefficients does it estimate, including the intercept? (c) If you wanted a *single* test
of whether occupation matters overall, what would you compute, and what is its null hypothesis?
