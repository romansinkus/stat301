# Practice 03 — Categorical Predictors

*Topic 1 → Topic 2 bridge. Solutions: [`solutions/03-categorical-predictors-solutions.md`](solutions/03-categorical-predictors-solutions.md).*

---

**Q1 [SA].** You can't put `sex = "male"/"female"` directly into a regression equation. Explain the
**dummy variable** trick, and state the general rule for how many dummies a categorical variable
with `L` levels needs.

---

**Q2 [SA].** In `lm(body_mass_g ~ sex)` on penguins, R reports a coefficient named `sexmale` (and no
`sexfemale`). Which level is the **reference**, why did R pick it, and how many dummy variables did it
create for this 2-level factor?

---

**Q3 [SA].** For `body_mass = b0 + b1*sexmale + e`, write out what the model predicts for females
and for males separately, then state in words what `b0`, `b1`, and `b0 + b1` each represent.

---

**Q4 [TF].** "In a 2-level categorical regression, `b0` and `b1` are a geometric intercept and slope
of a fitted line." True or false? Explain what they actually are.

---

**Q5 [SA].** Testing `H0: b1 = 0` in `lm(wage ~ sex)` is equivalent to a well-known STAT 201 test.
Which one? Explain *why* they're the same thing, and what "equivalent" was shown to mean in class
(what two numbers matched?).

---

**Q6 [CALC].** `lm(TARGET_deathRate ~ state)` (Alabama = reference) gives intercept `192.73` and
`stateCalifornia = −34.63`. (a) Interpret `stateCalifornia` in one sentence. (b) What is the mean
death rate in California? (c) If you instead fit `lm(TARGET_deathRate ~ 0 + state)`, what would the
`stateCalifornia` coefficient equal, and why?

---

**Q7 [SA].** By default R makes the **first alphabetical** level the reference. Give one reason you
might want to override this with `relevel()`, and name a situation where the choice of reference
changes the *coefficients* but not the *model's predictions or overall fit*.

---

**Q8 [CALC].** A categorical variable `region` has 4 levels. In `lm(Y ~ region)`, how many
coefficients (including the intercept) does the model estimate? Show how you get the number.

---

**Q9 [SA].** Explain why fitting `lm(wage ~ occupation)` where `occupation` is stored as the numbers
`1..6` gives a *wrong* model, and how `factor(occupation)` fixes it. What does the single slope in
the un-factored version even mean?
