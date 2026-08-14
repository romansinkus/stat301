# Practice 02 (Topic 2) — Interaction Models

*Topic 2 (Interactions). Solutions: [`solutions/02-interactions-solutions.md`](solutions/02-interactions-solutions.md).*

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Circle
> final numeric answers and respect the word limits.

---

## Problem 1 (16 pts) — Anatomy of an interaction model

Consider `Y = b0 + b1*D + b2*X + b3*(D*X)`, where `D` is a 2-level dummy (reference = group 0) and `X`
is continuous.

**(a) (4 pts)** (i) What does the **interaction term** let this model do that an additive model cannot?
Answer in terms of the geometry of the two group lines. (ii) Fill in the meaning of all four
coefficients:

| Coef | Meaning |
| --- | --- |
| `b0` | ? |
| `b1` | ? |
| `b2` | ? |
| `b3` | ? |

**(b) (4 pts)** (i) What is the **slope of the line for group 1** (the non-reference group), in terms of
the coefficients? Explain why it is not just `b2`. (ii) A common mistake reads `b2` as "the slope of
`X`." Why is that wrong here, and what *is* `b2` the slope of?

**(c) (4 pts)** "In an interaction model you can interpret each coefficient by holding the other
variables constant at *any* value, just like in an additive model." True or false? Justify.

**(d) (4 pts)** Explain the claim "an interaction model is two SLRs in one." Why does the reference
group's slope from the interaction model exactly match the slope you would get by fitting an SLR on only
that group's rows?

---

## Problem 2 (16 pts) — `wage ~ education * sex`

`lm(wage ~ education * sex)` (female = reference) gives the table below; the `education:sexmale` term has
`p_value = 0.273`.

```
term                 estimate
(Intercept)            5.00
education              0.60
sexmale                1.20
education:sexmale      0.15
```

**(a) (4 pts)** The interaction row tests `H0: b3 = 0`. (i) State in plain words what this null claims
about the two groups. (ii) If you *fail to reject* it (large p-value), which simpler model is justified?

**(b) (4 pts)** Interpret the `p = 0.273` fully: does the education–wage relationship depend on sex?
Which model would you report, and why?

**(c) (5 pts)** Write the fitted line for **females** and the fitted line for **males** (give the
intercept and slope for each; show the arithmetic).

**(d) (3 pts)** A 3-level categorical interacted with one continuous predictor adds how many
*interaction* coefficients? Show the rule you use.
