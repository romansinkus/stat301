# Practice 01 (Topic 6) — Goodness of Fit for Linear Models (R², Adjusted R², F-test)

*Topic 6. Solutions: [`solutions/01-r2-anova-ftest-solutions.md`](solutions/01-r2-anova-ftest-solutions.md).
Course case study: predicting protein from mRNA.*

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Circle
> final numeric answers, and respect any word limits. A simple calculator is allowed.

---

## Problem 1 (16 pts) — The variance decomposition and R²

**(a) (3 pts)** What is the **null model** (a.k.a. intercept-only model)? What single number is its
prediction for **every** observation, and what question are we really asking when we compare a fitted
model to it?

**(b) (5 pts)** Define **TSS**, **ESS**, and **RSS** in words and with their formulas. State the
decomposition that ties them together and the two conditions under which it holds. Which quantity does
least squares minimize?

**(c) (4 pts)** A model has `TSS = 500` and `RSS = 455`. (i) Compute `ESS`. (ii) Compute `R²` two ways
(`1 − RSS/TSS` and `ESS/TSS`) and confirm they agree. (iii) State in one sentence what this `R²` means.

**(d) (4 pts)** In an SLR, the correlation between `X` and `Y` is `r = 0.3`. What is `R²`, and what is the
verbal interpretation? Is a low `R²` like this necessarily a "bad" or useless model? Explain in the
context of noisy observational data.

---

## Problem 2 (15 pts) — R²'s caveats, adjusted R², RSE/MSE, AIC

**(a) (4 pts)** Give the **three critical caveats** about `R²` from the notes: (i) what data is it
computed on; (ii) can you use it as a significance **test**; (iii) what happens to `R²` when you add a
predictor — even a useless one — and what does that imply about comparing models of different sizes?

**(b) (4 pts)** Write the formula for **adjusted R²** and explain the role of the `n − p − 1` divisor. Why
can adjusted R² **decrease** when R² cannot, and which one should you use to compare models with different
numbers of predictors?

**(c) (4 pts)** Define **RSE** and **MSE**. What does RSE estimate, and what is the crucial difference
between **training MSE** and **testing MSE** — which one honestly measures prediction quality, and why?

**(d) (3 pts)** One line each: what is **AIC**, and how does it (like adjusted R²) let you compare models
of different sizes? Which direction is better (larger or smaller AIC)? How does BIC differ?

---

## Problem 3 (16 pts) — The F-test

`glance(model)` reports `r.squared = 0.62`, `adj.r.squared = 0.58`, `sigma = 4.1`, `statistic = 15.3`,
`p.value = 2e-08`.

**(a) (4 pts)** (i) What is `sigma`? (ii) What test is the `statistic`/`p.value` here, and what is its null
hypothesis (be specific about the reduced model)? (iii) State the conclusion.

**(b) (4 pts)** For the **F-test**, distinguish **Case A** (model vs. the null) from **Case B** (a nested
pair). For each, write the null hypothesis in words and name the R function you would use. What does
"**nested**" mean, and why is it required?

**(c) (4 pts)** The protein~mRNA study found that adding `gene` to `prot ~ mrna` gave a significant F-test
(`F = 9.9`, `p = 0.001`). A student concludes "so mRNA predicts protein well." Give the **two** things a
significant F-test does **not** establish, and explain what actually carried the signal here.

**(d) (4 pts)** Contrast the **t-test** on a single coefficient with the **F-test**. (i) How many
coefficients does each test at once? (ii) For the t-test, are the other variables in or out of the model?
(iii) What is special about the case `p = 1` (one predictor) — how do `F` and `t` relate?
