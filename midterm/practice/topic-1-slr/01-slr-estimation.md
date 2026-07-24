# Practice 01 — Simple Linear Regression: Estimation

*Topic 1 (SLR). Solutions: [`solutions/01-slr-estimation-solutions.md`](solutions/01-slr-estimation-solutions.md).*

---

**Q1 [SA].** Write the SLR model for predicting a penguin's `body_mass_g` from its
`flipper_length_mm`, and label each of the three components (`b0`, `b1`, `e`). In one sentence
each, say what `b1` and `e` represent

A: body_mass_g = b0 + b1*flipper_length_mm + e. b0 is the intercept which does not really have any real world significance. b1 is the slope -> this indicates how much the body mass in grams changes for each change in flipper length (mm). The e indicates the error.

---

**Q2 [SA].** Explain the difference between these two equations. Which one is "the line," and which
describes a single observation?

```
E[Y | X] = b0 + b1*X
Y_i      = b0 + b1*X_i + e_i
```

A: y_i is a single observation since it indicates some prediction i. 

---

**Q3 [TF].** "Least squares chooses the line that minimizes the sum of the *vertical* distances from
each point to the line." True or false? Justify, and correct it if it's wrong.

---

**Q4 [SA].** Why does least squares **square** the residuals instead of, say, using their absolute
values or their raw signed values? Give two distinct reasons. 

A: Magnify large errors and 

---

**Q5 [SA].** Define the **residual** for observation `i` in a fitted model (give the formula). Then
explain in one or two sentences why a residual is only a *stand-in* for the true error term `e_i`, and
why it is not generally exactly 0.

A: residual = y_i - y_hat_i. Not a stand-in for true error term e_i since it describes the gap from the fitted line, not the true line.

---

**Q6 [SA].** For the wage data, `lm(wage ~ education)` gives an `education` estimate of `0.750`.
Write the **correct** one-sentence interpretation of this slope. Then write two *incorrect*
versions that would lose marks, and say what's wrong with each.

A: An increase in education by 1 is associated with an increase in wage by 0.750.

Incorrect: in increase in education CAUSES....

Incorrect: in increase in wage by 1 is asociated with an increase in eduction by 0.750

---

**Q7 [SA].** The correlation between `wage` and `education` is `r ≈ 0.382`. A classmate says: "That
proves getting more education *causes* higher wages." Respond in 2–3 sentences, using a concrete
counter-example of the general principle.

A: weakly correlated and cannot prove causation

---

**Q8 [SA].** Contrast **correlation analysis** with **linear regression** on two points: (a) whether
the two variables play symmetric or asymmetric roles, and (b) how each treats `X` (random vs. fixed).
Also state how the *sign* of the correlation relates to the sign of the regression slope.

A: correlation analysis is symmetric, linear regression is not symmetric.

---

**Q9 [SA].** You fit `lm(body_mass_g ~ flipper_length_mm)` on penguins with flippers ranging
172–231 mm. Your friend uses it to predict the mass of a penguin with a 500 mm flipper. Name the
problem, and explain in one sentence why the prediction is untrustworthy. Then relate it to George
Box's aphorism.

---

**Q10 [CODE-read].** A `get_regression_table()` output for `lm(wage ~ education)` shows
`(Intercept) = −0.746` and `education = 0.750`. (a) Write the fitted regression equation.
(b) Use it to predict the average wage for someone with **12 years** of education. (c) Explain why
this number is an *average*, not a guarantee for any single person with 12 years of education.


y = -0.746 + 0.750X

y = -0.746 + 0.750(12) = 8.254

This is an average because it doesn't account for the error
