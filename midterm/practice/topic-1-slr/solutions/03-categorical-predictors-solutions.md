# Solutions 03 — Categorical Predictors

*Questions: [`../03-categorical-predictors.md`](../03-categorical-predictors.md).*

---

**Q1.** The **dummy variable** trick replaces a category with a 0/1 numeric indicator that `lm()`
creates automatically when the column is a **factor** (e.g. `sexmale = 1` for males, `0` for
females). General rule: a categorical variable with `L` levels needs **`L − 1` dummy variables** (one
level is left out as the reference).

---

**Q2.** **`female` is the reference** (coded 0), chosen because it's **first alphabetically**. R
creates **one** dummy for this 2-level factor (`L − 1 = 1`) — the `sexmale` indicator — so the model
has that single coefficient plus the intercept (no separate `sexfemale`).

---

**Q3.**
```
Female (sexmale = 0):  body_mass = b0 + e         → mean = b0
Male   (sexmale = 1):  body_mass = b0 + b1 + e    → mean = b0 + b1
```
- **`b0`** = mean body mass of the **reference** group (female).
- **`b1`** = the **difference** in means (male − female).
- **`b0 + b1`** = mean body mass of males.

---

**Q4.** **False.** With a categorical predictor there's no line, so `b0` and `b1` aren't a geometric
intercept/slope — R just labels them that way. `b0` is a **baseline group mean** and `b1` is a
**difference between two group means**.

---

**Q5.** It's equivalent to a **two-sample t-test** of equal means. Splitting the model by group shows
`b0` = one group's mean and `b0 + b1` = the other's, so testing `H0: b1 = 0` tests equal means. In
class it was shown "equivalent" because `lm()` and `t.test()` returned the **identical estimate and
test statistic** (e.g. the penguin `sexmale = 683.41` with statistic `8.54`).

---

**Q6.**
(a) "The mean cancer death rate in California is **34.63 lower** than in Alabama (the reference)."
(b) California mean = `192.73 + (−34.63) = 158.10`.
(c) With `~ 0 + state`, removing the intercept makes each coefficient the group's **actual mean**, so
`stateCalifornia` would be `158.10` — because there's no baseline to difference against, each
coefficient stands alone as that state's mean.

---

**Q7.** You'd override the reference with `relevel()` to make a more **meaningful baseline** (e.g. a
control group, or the most common category) so the reported differences are the comparisons you care
about. Changing the reference changes which differences the coefficients express, but the **fitted
values, predictions, and overall fit (`R^2`, residuals) are identical** — it's the same model
re-parameterized.

---

**Q8.** A 4-level categorical needs `4 − 1 = 3` dummies; add the intercept ⇒ `3 + 1 =` **4
coefficients**.

---

**Q9.** If `occupation` is stored as numbers `1..6`, `lm(wage ~ occupation)` treats it as
**continuous** and fits a **single slope** on the codes — implying, nonsensically, that occupation 4
is "twice as much occupation" as occupation 2 and that the wage change from 1→2 equals 5→6. The slope
is a meaningless "wage per unit of occupation code." `factor(occupation)` tells R the numbers are
**labels**, so it builds `6 − 1 = 5` dummies and estimates a separate mean difference for each
occupation vs. the reference.
