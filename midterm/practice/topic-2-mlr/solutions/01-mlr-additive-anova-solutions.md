# Solutions 04 — Additive MLR, k-Level Categoricals & ANOVA

*Questions: [`../01-mlr-additive-anova.md`](../01-mlr-additive-anova.md).*

---

**Q1.** **False.** **Multiple** regression = one continuous response with **many predictors**.
**Multivariate** regression = **many response variables** (out of scope here). In this course `Y` is
**always a single continuous response**.

---

**Q2.**
```
Indiana    (dummy = 0):  Y = b0       + b2*poverty   → intercept b0,     slope b2
Washington (dummy = 1):  Y = (b0+b1)  + b2*poverty   → intercept b0+b1,  slope b2
```
- **`b0`** = intercept of the **reference** (Indiana) line.
- **`b1`** = **difference between the two intercepts** (a vertical shift up/down for Washington).
- **`b2`** = the **common slope** shared by both lines (poverty's effect, same for both states).
The two lines are **parallel**.

---

**Q3.** **Additive assumption:** the expected change in `Y` per one-unit change in a predictor is the
**same regardless of the values of the other predictors**. Because of this, you interpret each
coefficient "**holding the other variables constant**," and — crucially — **it doesn't matter at
which value** you hold them, since the effect is constant everywhere. In an interaction model that's
false: one variable's effect *depends* on the other's value, so "at any value" no longer applies.

---

**Q4.** The tiny CI change means `education` and `sex` are **only weakly related**: adding `sex`
barely changes what `education` explains, so `sex` wasn't distorting the education coefficient. A
**large** change would have implied the two predictors are strongly related (overlapping
information) — i.e. `sex` had been confounding/omitted from the simple model and materially altered
the education estimate once included.

---

**Q5.** A predictor's coefficient is "its association **holding the other predictors in the model
constant**." In the SLR, the omitted variable isn't held constant — its influence gets **dumped into
the error term** and, if it's correlated with the included predictor, **contaminates** that lone
coefficient (omitted-variable effect). Adding it to the MLR "cleans up" the estimate, so the value
changes. This is exactly why MLR coefficients must be read as "holding all other variables *in the
model* constant."

---

**Q6.** `anova(model)` gives a single **joint F-test** for the whole categorical predictor.
- `H0`: **all group means are equal** (every non-reference coefficient = 0 simultaneously).
- `H1`: **at least one group mean differs**.
The individual coefficient **t-tests** instead each test one level *vs. the reference* separately.

---

**Q7.** The tiny p-value ⇒ reject `H0` that all occupation means are equal, so **at least one
occupation's mean wage differs from the others** — i.e. wage **is associated with occupation.** It
does **not** say every pair of occupations differs, does **not** identify which occupation is highest
(the coefficient table does that), and is **not** a reason to drop the variable.

---

**Q8.** Running many separate t-tests inflates the **false-positive (Type I error) rate** — with
enough comparisons some will look "significant" by chance. The single ANOVA **F-test bundles them
into one honest test** of "does this variable belong in the model at all?", controlling that error
rate. (Then you use the coefficient table to see *which* groups differ.)

---

**Q9.**
(a) **3 lines** (one per level of the 3-level categorical).
(b) They share a **common slope** (`b3`) but have **different intercepts** — additive ⇒ parallel.
(c) **4 coefficients** total: intercept `b0`, two dummies `b1`, `b2`, and the slope `b3`.

---

**Q10.**
(a) With occupation 1 and female as references:
```
wage = b0 + b1*education
          + b2*occ2 + b3*occ3 + b4*occ4 + b5*occ5 + b6*occ6   (5 dummies for 6 levels)
          + b7*sexmale
          + e
```
(b) **8 coefficients**: intercept (1) + education (1) + occupation (6 − 1 = 5) + sex (2 − 1 = 1) = 8.
(c) An **ANOVA F-test** on the occupation term (`anova` of the fitted model). Its null hypothesis is
that **all occupation group means are equal** (all five occupation dummy coefficients = 0
simultaneously) — i.e. occupation is not associated with wage.
