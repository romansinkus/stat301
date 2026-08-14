# Practice 03 (Topic 2) — Tutorial 02: MLR with Categorical Input & Interactions (CASchools)

*Topic 2 (MLR + interactions). Source: `tutorials/tutorial_02.ipynb`. Solutions:
[`solutions/03-tutorial-caschools-mlr-solutions.md`](solutions/03-tutorial-caschools-mlr-solutions.md).*

Dataset: **CASchools** — `read` vs `income` (\$1000s) and `grades` (2 levels: `KK-06`, `KK-08`).

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Circle
> final numeric answers and respect the word limits.

---

## Problem 1 (13 pts) — The additive model `read ~ income + grades`

In `lm(read ~ income + grades)` (baseline `KK-06`) the `income` coefficient is `≈ 1.93`.

**(a) (4 pts)** How many dummy variables does `lm()` create for `grades`, and what must be true of the
`grades` column for `lm()` to dummy-code it at all?

**(b) (5 pts)** (i) Interpret the `income` coefficient `1.93`, including the "holding constant" clause.
(ii) Geometrically, what do the two school types' fitted lines look like, and what forces that shape?

**(c) (4 pts)** Explain the difference between **statistical significance** and **practical
significance**, and give a scenario where an `income` coefficient is statistically significant but not
practically significant.

---

## Problem 2 (15 pts) — The interaction model `read ~ income * grades`

In `lm(read ~ income * grades)` (KK-06 = reference) the table shows `income = 2.02` and
`income:gradesKK-08 = −0.11`; the interaction term has `p ≈ 0.68` at `alpha = 0.10`.

**(a) (5 pts)** (i) What is the fitted **slope** for KK-06 schools? (ii) For KK-08 schools? (show the
arithmetic) (iii) What does the `−0.11` by itself represent?

**(b) (3 pts)** How many coefficients does `lm(read ~ income * grades)` estimate, and what do the two
fitted lines look like (same/different slope, same/different intercept)?

**(c) (3 pts)** State the conclusion about whether the income–reading relationship **differs by grade
span**, and which model you would report and why.

**(d) (4 pts)** If you fit a **separate SLR** using only KK-06 districts, its `income` slope equals the
interaction model's `income` coefficient exactly. Explain why. Then explain why the KK-08-only SLR slope
equals `income + income:gradesKK-08`, **not** `income:gradesKK-08` alone.
