# Practice 01 (Topic 1) — Simple Linear Regression: Estimation

*Topic 1 (SLR). Solutions: [`solutions/01-slr-estimation-solutions.md`](solutions/01-slr-estimation-solutions.md).*

> **Exam-style.** Written short answer only. **Show the key steps** — the real marking scheme is
> **70% for correct procedure, 30% for the correct answer.** Circle final numeric answers, and respect
> the stated word limits. A simple calculator is allowed.

---

## Problem 1 (17 pts) — Penguin body mass

You study the relationship between a penguin's **body mass** (`y`, in grams) and its **flipper length**
(`x`, in mm), based on a sample of 342 penguins whose flipper lengths range from **172 mm to 231 mm**.
Fitting `lm(body_mass_g ~ flipper_length_mm)` gives the following estimates (standard errors):

```
                 estimate   std. error
(Intercept)      -5780.83     305.81
flipper_length      49.69       0.86
```

**(a) (5 pts)** Write the SLR model for this study and label each of the three components `b0`, `b1`,
`e`. In one sentence each, say what `b1` and `e` represent. Then explain the difference between the two
equations below — which one is "the line," and which describes a single observation?

```
E[Y | X] = b0 + b1*X          Y_i = b0 + b1*X_i + e_i
```

**(b) (4 pts)** (i) "Least squares chooses the line that minimizes the sum of the *vertical* distances
from each point to the line." True or false? Correct it if it is wrong. (ii) Give **two** distinct
reasons least squares **squares** the residuals rather than using their raw signed values.

**(c) (4 pts)** Define the **residual** for observation `i` (give the formula). Then explain in no more
than 30 words why a residual is only a *stand-in* for the true error `e_i`, and why it is not generally
exactly 0.

**(d) (4 pts)** A classmate uses this fitted model to predict the mass of a penguin with a **500 mm**
flipper. Name the problem, explain in one sentence why the prediction is untrustworthy, and relate it to
George Box's aphorism.

---

## Problem 2 (18 pts) — Wage and education

You study **hourly wage** (`y`, in \$/hour) and **education** (`x`, in years) on a sample of workers.
`get_regression_table()` for `lm(wage ~ education)` reports:

```
term          estimate   std_error
(Intercept)     -0.746
education        0.750       0.079
```

The correlation between `wage` and `education` is `r ≈ 0.382`.

**(a) (5 pts)** (i) Write the fitted regression equation. (ii) Use it to predict the average wage for
someone with **12 years** of education (show the calculation and circle the answer). (iii) Explain in
less than 30 words why this number is an *average*, not a guarantee for any single person.

**(b) (5 pts)** (i) Write the **correct** one-sentence interpretation of the `education` slope `0.750`.
(ii) Then write **two** *incorrect* versions that would lose marks, and say what is wrong with each.

**(c) (4 pts)** A classmate says: "The correlation `r ≈ 0.382` proves that getting more education
*causes* higher wages." Respond in 2–3 sentences, using a concrete counter-example to make your point.

**(d) (4 pts)** Contrast **correlation analysis** with **linear regression** on two points: (i) whether
the two variables play symmetric or asymmetric roles, and (ii) how each treats `X` (random vs. fixed).
Then state how the **sign** of the correlation relates to the sign of the regression slope.
