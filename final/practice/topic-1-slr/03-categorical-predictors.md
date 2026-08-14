# Practice 03 (Topic 1) — Categorical Predictors

*Topic 1 → Topic 2 bridge. Solutions:
[`solutions/03-categorical-predictors-solutions.md`](solutions/03-categorical-predictors-solutions.md).*

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Circle
> final numeric answers and respect the word limits.

---

## Problem 1 (16 pts) — A two-level factor (penguin sex)

Consider `lm(body_mass_g ~ sex)` on the penguins, where `sex` has levels `female` and `male`. R fits
```
body_mass = b0 + b1 * sexmale + e
```
and reports a coefficient named `sexmale` (and no `sexfemale`).

**(a) (4 pts)** You cannot put `sex = "male"/"female"` directly into a regression equation. Explain the
**dummy variable** trick, and state the general rule for how many dummies a categorical variable with
`L` levels needs.

**(b) (4 pts)** In this output, which level is the **reference**, why did R pick it, and how many dummy
variables did it create for this 2-level factor?

**(c) (4 pts)** (i) Write out what the model predicts for **females** and for **males** separately, and
state in words what `b0`, `b1`, and `b0 + b1` each represent. (ii) "Here `b0` and `b1` are a geometric
intercept and slope of a fitted line." True or false? Explain what they actually are.

**(d) (4 pts)** Testing `H0: b1 = 0` in `lm(wage ~ sex)` is equivalent to a well-known STAT 201 test.
Which one? Explain *why* they are the same thing, and what "equivalent" was shown to mean in class (which
two numbers matched?).

---

## Problem 2 (15 pts) — Many-level factors (state, occupation)

`lm(TARGET_deathRate ~ state)`, with **Alabama** as the reference, gives intercept `192.73` and
`stateCalifornia = −34.63`.

**(a) (5 pts)** (i) Interpret `stateCalifornia` in one sentence. (ii) What is the mean death rate in
California? (show the calculation). (iii) If you instead fit `lm(TARGET_deathRate ~ 0 + state)`, what
would the `stateCalifornia` coefficient equal, and why?

**(b) (3 pts)** By default R makes the first alphabetical level the reference. Give one reason you might
override this with `relevel()`, and name a situation where the choice of reference changes the
*coefficients* but **not** the model's predictions or overall fit.

**(c) (3 pts)** A categorical variable `region` has **4 levels**. In `lm(Y ~ region)`, how many
coefficients (including the intercept) does the model estimate? Show how you get the number.

**(d) (4 pts)** Explain why fitting `lm(wage ~ occupation)`, where `occupation` is stored as the numbers
`1..6`, gives a *wrong* model, and how `factor(occupation)` fixes it. What does the single slope in the
un-factored version even mean?
