# Practice 01 (Topic 8) — Reading LASSO Coefficient-Path & Cross-Validation Plots

*Gap-filler for Topic 8. Solutions: [`solutions/01-reading-lasso-plots-solutions.md`](solutions/01-reading-lasso-plots-solutions.md).
Companion to `../../practice/topic-8-model-selection/` (LASSO/ridge concepts, double-dipping). The README
says you must be able to read **LASSO paths and CV plots** — this set drills exactly that.*

> **Exam-style.** Show key steps (70% procedure, 30% answer). Circle final answers.

---

## Problem 1 (15 pts) — The coefficient path

A LASSO fit reports the coefficient values at four penalty levels (a text version of the
`plot(glmnet_fit)` path; `λ` increases left → right):

```
                log λ = −6    log λ = −3    log λ = −1    log λ = +1
x1 (rooms)         2.0           1.6           0.9           0
x2 (area)          1.5           1.0           0.3           0
x3 (age)           0.8           0.4           0             0
x4 (dist_bus)      0.3           0             0             0
x5 (lot_slope)     0.1           0             0             0
```

**(a) (4 pts)** How many predictors are **selected** (nonzero) at `log λ = −3`? List them. What does a
coefficient hitting **exactly 0** signify, and why can LASSO do this while ridge cannot?

**(b) (4 pts)** As `λ` grows, in what **order** do the variables drop out? What does the drop-out order
suggest about which predictors carry the strongest signal?

**(c) (4 pts)** At `log λ = −6` the estimates are close to the ordinary least-squares fit. Explain why —
what does `λ = 0` recover, and what is happening to **bias** and **variance** as you move rightward
(larger λ)?

**(d) (3 pts)** Why must the predictors be **standardized** before fitting LASSO? Use `x1` (rooms) and `x2`
(area, in m²) to explain what would go wrong otherwise.

---

## Problem 2 (14 pts) — The cross-validation plot

`cv.glmnet` produces this CV-error curve (a text version of `plot(cv_fit)`):

```
log λ:        −6     −4     −2     −1      0     +1
CV MSE:        25     22     18    18.5    21     26
# nonzero:     12     10      6      4      2      0
```

The minimum CV MSE is at `log λ = −2`; the CV error at `log λ = −1` is within **one standard error** of that
minimum.

**(a) (4 pts)** Explain the **U-shape** of this curve. Why does MSE fall then rise as `λ` increases — tie
it to `MSE = Variance + Bias²`.

**(b) (5 pts)** Identify **`lambda.min`** and **`lambda.1se`** from the table (give the `log λ` and the
number of variables each keeps). What is the rationale for preferring `lambda.1se` in practice?

**(c) (3 pts)** What does cross-validation split, and why does it **not** touch the real held-out test set?
Name the procedure (`k`-fold) and the usual `k`.

**(d) (2 pts)** At `log λ = +1`, zero variables are selected. What model is that equivalent to?
