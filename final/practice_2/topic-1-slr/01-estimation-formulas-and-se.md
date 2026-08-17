# Practice 01 (Topic 1) — Estimation Formulas & SD vs SE (computation)

*Gap-filler for Topic 1. Solutions: [`solutions/01-estimation-formulas-and-se-solutions.md`](solutions/01-estimation-formulas-and-se-solutions.md).
Companion to `../../practice/topic-1-slr/` (which covers the concepts).*

> **Exam-style.** Show key steps (70% procedure, 30% answer). Circle final numbers. Calculator allowed.

---

## Problem 1 (16 pts) — Building the fitted line from summary statistics

You study a fish's **weight** `Y` (kg) vs. its **length** `X` (cm). You are given only these five summary
statistics (no raw data, no `lm` output):

```
r (correlation X,Y) = 0.75      S_x (sd of X) = 3      S_y (sd of Y) = 12
x̄ = 8      ȳ = 40
```

**(a) (4 pts)** Use `β̂₁ = r · (S_y / S_x)` to compute the **slope**. Show the substitution and circle the
number. Then state, from the sign alone, the direction of the association.

**(b) (4 pts)** Use `β̂₀ = ȳ − β̂₁·x̄` to compute the **intercept**. Write the full fitted equation, then
explain in ≤ 25 words why the least-squares line is *guaranteed* to pass through the point `(x̄, ȳ)`.

**(c) (4 pts)** Compute **R²** from the information given (no RSS/TSS needed — use the SLR shortcut). State
in one sentence what it means here, and give the correlation-to-R² warning (why `r = 0.75` is **not** "75%
explained").

**(d) (4 pts)** Predict the average weight of a **10 cm** fish. Then: a classmate predicts for a **40 cm**
fish (the data ran 2–15 cm). Name the problem in one word and say why the number is untrustworthy.

---

## Problem 2 (15 pts) — SD vs SE vs RSE (the three "spreads")

**(a) (5 pts)** Define and distinguish, in one sentence each: (i) the **standard deviation (SD)** of the
errors `σ`; (ii) the **residual standard error (RSE)**; (iii) the **standard error (SE)** of a coefficient
`β̂₁`. Which two are *estimates*, and which one describes an **estimator** (a thing that varies across
samples) rather than the data?

**(b) (4 pts)** True/false, justify: **"The standard error of `β̂₁` measures how much the individual data
points scatter around the fitted line."** If false, which quantity *does* measure that?

**(c) (3 pts)** An `lm` fit reports `RSE (sigma) = 10` on `n = 100` observations. Using the fact that a
standard error shrinks like `1/√n`, explain what happens to `SE(β̂₁)` as `n → ∞`, and what happens to the
**RSE** as `n → ∞`. Why do they behave differently?

**(d) (3 pts)** The final-review sheet says `SE = σ̂/√n` while `SD` uses the true `σ`. In one sentence, state
the key conceptual difference: *what* does each one describe the spread **of**?
