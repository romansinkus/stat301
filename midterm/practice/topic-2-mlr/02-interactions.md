# Practice 05 — Interaction Models

*Topic 2 (Interactions). Solutions: [`solutions/02-interactions-solutions.md`](solutions/02-interactions-solutions.md).*

---

**Q1 [SA].** What does an **interaction term** let a model do that an additive model cannot? Answer
in terms of the geometry of the two group lines.

---

**Q2 [SA].** For `Y = b0 + b1*D + b2*X + b3*(D*X)` with `D` a 2-level dummy (reference = group 0),
write the equation of each group's line, then fill in the meaning of all four coefficients:

| Coef | Meaning |
| --- | --- |
| `b0` | ? |
| `b1` | ? |
| `b2` | ? |
| `b3` | ? |

---

**Q3 [SA].** In the model above, what is the **slope of the line for group 1** (the non-reference
group), in terms of the coefficients? Explain why it isn't just `b2`.

---

**Q4 [SA].** A very common exam mistake: reading the continuous main-effect coefficient (`b2`) as
"the slope of `X`." Why is that wrong in an interaction model? What *is* `b2` the slope of?

---

**Q5 [SA].** The interaction row tests `H0: b3 = 0`. State in plain words what this null hypothesis
claims about the two groups. If you *fail to reject* it (large p-value), which simpler model is
justified?

---

**Q6 [SA].** In-class Activity 4A, `lm(wage ~ education*sex)` gave the `education:sex` term a p-value
of `0.273`. Interpret this fully: does the education–wage relationship depend on sex? Which model
would you report, and why?

---

**Q7 [CALC].** For `lm(wage ~ education * sex)` (female = reference) suppose the table shows:
`(Intercept) = 5.0`, `education = 0.60`, `sexmale = 1.2`, `education:sexmale = 0.15`.
Write the fitted line for **females** and the fitted line for **males** (intercept and slope for
each).

---

**Q8 [TF].** "In an interaction model you can interpret each coefficient by holding the other
variables constant at any value, just like in an additive model." True or false? Justify.

---

**Q9 [CALC].** A 3-level categorical interacted with one continuous predictor adds how many
*interaction* coefficients? Show the rule you use.

---

**Q10 [SA].** Explain the claim "an interaction model is two SLRs in one." Why does the reference
group's slope from the interaction model exactly match the slope you'd get by fitting an SLR on only
that group's rows?
