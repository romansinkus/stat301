# Practice 03 (Topic 2) — Tutorial 02: MLR with Categorical Input & Interactions (CASchools)

*Topic 2 (MLR + interactions). Source: `tutorials/tutorial_02.ipynb`.
Solutions: [`solutions/03-tutorial-caschools-mlr-solutions.md`](solutions/03-tutorial-caschools-mlr-solutions.md).*

Dataset: **CASchools** — `read` vs `income` (\$1000s) and `grades` (2 levels: `KK-06`, `KK-08`).

---

**Q1 [SA].** `grades` is a 2-level factor with baseline `KK-06`. In `lm(read ~ income + grades)`, how
many dummy variables does `lm()` create, and what must be true of the `grades` column for `lm()` to
dummy-code it at all?

---

**Q2 [SA].** In the **additive** model `lm(read ~ income + grades)` the `income` coefficient is
`≈ 1.93`. (a) Interpret it, including the "holding constant" clause. (b) Geometrically, what do the two
school types' fitted lines look like, and what forces that shape?

---

**Q3 [CALC].** In the **interaction** model `lm(read ~ income * grades)` (KK-06 = reference) the table
shows `income = 2.02` and `income:gradesKK-08 = −0.11`. (a) What is the fitted **slope** for KK-06
schools? (b) For KK-08 schools? (c) What does the `−0.11` by itself represent?

---

**Q4 [SA].** How many coefficients does `lm(read ~ income * grades)` estimate, and what does each of the
two fitted lines look like (same/different slope, same/different intercept)?

---

**Q5 [SA].** The interaction term `income:gradesKK-08` has `p ≈ 0.68` at `alpha = 0.10`. State the
conclusion about whether the income–reading relationship **differs by grade span**, and which model
you would report and why.

---

**Q6 [SA] (the Q2.7 punchline).** If you fit a **separate SLR** using only KK-06 districts, its `income`
slope equals the interaction model's `income` coefficient exactly. Explain why. Then explain why the
KK-08-only SLR slope equals `income + income:gradesKK-08`, **not** `income:gradesKK-08` alone.

---

**Q7 [SA].** Explain the difference between **statistical significance** and **practical
significance**, and give a scenario where a coefficient is statistically significant but not
practically significant.
