# Solutions 01 (Topic 2) — Additive MLR, k-Level Categoricals & ANOVA

*Questions: [`../01-mlr-additive-anova.md`](../01-mlr-additive-anova.md).*

> Marking scheme: **70% for correct procedures, 30% for correct answers.**

---

## Problem 1 — Additive MLR: two parallel lines

**(a)** **False.** **Multiple** regression = one continuous response with **many predictors**;
**multivariate** regression = **many response variables** (out of scope here). In this course `Y` is
**always a single continuous response**.

**(b)**
```
Indiana    (dummy = 0):  Y = b0       + b2*poverty   → intercept b0,     slope b2
Washington (dummy = 1):  Y = (b0+b1)  + b2*poverty   → intercept b0+b1,  slope b2
```
- **`b0`** = intercept of the **reference** (Indiana) line.
- **`b1`** = **difference between the two intercepts** (vertical shift for Washington).
- **`b2`** = the **common slope** shared by both lines (poverty's effect, same for both).
The two lines are **parallel**.

**(c)** **Additive assumption:** the expected change in `Y` per one-unit change in a predictor is the
**same regardless of the values of the other predictors**. Because of this you interpret each
coefficient "**holding the other variables constant**," and — crucially — **it does not matter at which
value** you hold them, since the effect is constant everywhere. In an interaction model this is false:
one variable's effect *depends* on the other's value, so "at any value" no longer applies.

**(d)** (i) The tiny CI change means `education` and `sex` are only **weakly related**: adding `sex`
barely changes what `education` explains, so `sex` was not distorting the education coefficient. A
**large** change would have implied the predictors are strongly related (overlapping information) — i.e.
`sex` had been confounding the simple model and materially altered the estimate once included.
(ii) In the SLR an omitted variable is not held constant — its influence gets **dumped into the error
term**, and if it is correlated with the included predictor it **contaminates** that coefficient; adding
it to the MLR "cleans up" the estimate, so the value changes.

---

## Problem 2 — ANOVA for a categorical predictor

**(a)** (i) `anova(model)` gives a single **joint F-test** for the whole categorical predictor:
`H0`: **all group means are equal** (every non-reference coefficient = 0 simultaneously); `H1`: **at
least one group mean differs**. The individual coefficient **t-tests** instead each test one level *vs.
the reference* separately. (ii) Running many separate t-tests inflates the **false-positive (Type I)
rate** — with enough comparisons some look "significant" by chance. The single F-test bundles them into
one honest test of "does this variable belong at all?", controlling that error rate.

**(b)** The tiny p-value ⇒ reject `H0` that all occupation means are equal, so **at least one
occupation's mean wage differs** — wage **is associated with occupation**. It does **not** say every
pair of occupations differs, does **not** identify which occupation is highest (the coefficient table
does that), and is **not** a reason to drop the variable.

**(c)** (i) **3 lines** (one per level of the 3-level categorical). (ii) They share a **common slope**
(`b3`) but have **different intercepts** — additive ⇒ parallel. (iii) **4 coefficients**: intercept
`b0`, two dummies `b1, b2`, and the slope `b3`.

**(d)** (i) With occupation 1 and female as references:
```
wage = b0 + b1*education
          + b2*occ2 + b3*occ3 + b4*occ4 + b5*occ5 + b6*occ6   (5 dummies for 6 levels)
          + b7*sexmale
          + e
```
(ii) **8 coefficients**: intercept (1) + education (1) + occupation (6 − 1 = 5) + sex (2 − 1 = 1) = 8.
(iii) An **ANOVA F-test** on the occupation term (`anova` of the fitted model). Null hypothesis: **all
occupation group means are equal** (all five occupation dummy coefficients = 0 simultaneously) — i.e.
occupation is not associated with wage.
