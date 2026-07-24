# Solutions 05 — Interaction Models

*Questions: [`../02-interactions.md`](../02-interactions.md).*

---

**Q1.** An interaction term lets the **slope itself differ between groups** — the two group lines can
have **different slopes** (non-parallel), not just different intercepts. An additive model forces a
**common slope** (parallel lines), so it can't capture "the effect of `X` is steeper in one group."

---

**Q2.**
```
Group 0 (reference, D=0):  Y = b0 + b2*X                 → intercept b0,     slope b2
Group 1            (D=1):  Y = (b0+b1) + (b2+b3)*X        → intercept b0+b1,  slope b2+b3
```

| Coef | Meaning |
| --- | --- |
| `b0` | intercept of the **reference** line |
| `b1` | **difference in intercepts** (group 1 − reference) |
| `b2` | **slope of the reference line** |
| `b3` | **difference in slopes** (group 1 − reference) — the interaction |

---

**Q3.** The slope for group 1 is **`b2 + b3`** — you **add** the interaction coefficient `b3` to the
reference slope `b2`. It isn't just `b2` because `b2` is only the **reference group's** slope, and `b3`
is the *difference* in slopes; group 1's actual slope is the sum of the two.

---

**Q4.** In an interaction model `b2` is **only the reference group's slope**, not "the" slope for
everyone — the other group's slope is `b2 + b3`. Reading `b2` as the universal slope ignores that the
effect of `X` **depends on the group**, which is the whole point of adding the interaction.

---

**Q5.** `H0: b3 = 0` claims the two groups have the **same slope** — i.e. the association between `X`
and `Y` is **the same in both groups** (the lines are parallel). Failing to reject it (large p-value)
justifies the simpler **additive/parallel-lines model**.

---

**Q6.** `p = 0.273 > 0.05`, so we **fail to reject `H0: b3 = 0`** — there is **no evidence** that the
education–wage slope differs by sex. So the education–wage relationship **does not depend on sex**
(as far as the data show), and you'd report the simpler **additive model** `wage ~ education + sex`,
which is easier to interpret and not contradicted by the data.

---

**Q7.**
```
Female (reference):  intercept = 5.0,          slope = 0.60
Male:                intercept = 5.0 + 1.2 = 6.2,  slope = 0.60 + 0.15 = 0.75
```

---

**Q8.** **False.** In an interaction model the effect of one variable **depends on the value of the
other**, so you **cannot** say "holding the other constant at any value." Saying "holding all else
constant" (as if the value doesn't matter) is the classic flagged mistake — that phrasing is only
valid for **additive** models.

---

**Q9.** Interaction coefficients = (coefs of A) × (coefs of B). A 3-level categorical contributes
`3 − 1 = 2` dummies, times `1` for the continuous predictor = `2 × 1 =` **2 interaction terms**.

---

**Q10.** Fitting the interaction model on the full data reproduces the **same two lines** you'd get
by fitting a **separate SLR to each group's rows**. The reference group's rows have all dummies = 0,
so their fitted line uses only `b0` and `b2` — exactly the intercept and slope a reference-only SLR
would find. (The other group's line is `b0+b1` and `b2+b3`.) That's why it's "two SLRs in one."
