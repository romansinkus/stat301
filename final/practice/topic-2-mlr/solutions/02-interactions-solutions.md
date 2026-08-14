# Solutions 02 (Topic 2) — Interaction Models

*Questions: [`../02-interactions.md`](../02-interactions.md).*

> Marking scheme: **70% for correct procedures, 30% for correct answers.**

---

## Problem 1 — Anatomy of an interaction model

**(a)** (i) An interaction term lets the **slope itself differ between groups** — the two group lines can
have **different slopes** (non-parallel), not just different intercepts. An additive model forces a
**common slope** (parallel lines), so it cannot capture "the effect of `X` is steeper in one group."
(ii)

| Coef | Meaning |
| --- | --- |
| `b0` | intercept of the **reference** line |
| `b1` | **difference in intercepts** (group 1 − reference) |
| `b2` | **slope of the reference line** |
| `b3` | **difference in slopes** (group 1 − reference) — the interaction |

```
Group 0 (reference, D=0):  Y = b0 + b2*X            → intercept b0,     slope b2
Group 1            (D=1):  Y = (b0+b1) + (b2+b3)*X  → intercept b0+b1,  slope b2+b3
```

**(b)** (i) The slope for group 1 is **`b2 + b3`** — you **add** the interaction `b3` to the reference
slope `b2`. It is not just `b2` because `b2` is only the **reference group's** slope, and `b3` is the
*difference* in slopes; group 1's actual slope is the sum. (ii) In an interaction model `b2` is **only
the reference group's slope**, not "the" slope for everyone — reading it as universal ignores that the
effect of `X` **depends on the group**, which is the whole point of the interaction.

**(c)** **False.** In an interaction model the effect of one variable **depends on the value of the
other**, so you **cannot** say "holding the other constant at any value." That phrasing (as if the value
does not matter) is valid only for **additive** models — this is the classic flagged mistake.

**(d)** Fitting the interaction model on the full data reproduces the **same two lines** you would get by
fitting a **separate SLR to each group's rows**. The reference group's rows have all dummies = 0, so
their fitted line uses only `b0` and `b2` — exactly the intercept and slope a reference-only SLR would
find. (The other group's line is `b0+b1` and `b2+b3`.) That is why it is "two SLRs in one."

---

## Problem 2 — `wage ~ education * sex`

**(a)** (i) `H0: b3 = 0` claims the two groups have the **same slope** — the association between
education and wage is **the same for both sexes** (the lines are parallel). (ii) Failing to reject it
justifies the simpler **additive / parallel-lines model** `wage ~ education + sex`.

**(b)** `p = 0.273 > 0.05` ⇒ **fail to reject `H0: b3 = 0`** — **no evidence** that the education–wage
slope differs by sex, so the relationship **does not depend on sex** (as far as the data show). Report
the simpler **additive model** `wage ~ education + sex`: it is easier to interpret and not contradicted
by the data.

**(c)**
```
Female (reference):  intercept = 5.0,             slope = 0.60
Male:                intercept = 5.0 + 1.2 = 6.2,  slope = 0.60 + 0.15 = 0.75
```

**(d)** Interaction coefficients = (coefs of A) × (coefs of B). A 3-level categorical contributes
`3 − 1 = 2` dummies, times `1` for the continuous predictor = `2 × 1 =` **2 interaction terms**.
