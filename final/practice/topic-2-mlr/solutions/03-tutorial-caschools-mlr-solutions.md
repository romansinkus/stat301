# Solutions 03 (Topic 2) — Tutorial 02: MLR with Categorical Input & Interactions

*Questions: [`../03-tutorial-caschools-mlr.md`](../03-tutorial-caschools-mlr.md).*

> Marking scheme: **70% for correct procedures, 30% for correct answers.**

---

## Problem 1 — The additive model `read ~ income + grades`

**(a)** `lm()` creates **1 dummy** for a 2-level factor (`L − 1 = 1`), here `gradesKK-08` (so `KK-06` is
the baseline). For `lm()` to dummy-code it at all, the `grades` column **must be a factor** — if it is
stored as plain text/number, `lm()` will not build the dummy correctly.

**(b)** (i) Each additional **\$1000** of income is **associated with** about a **1.93**-point increase
in average reading score, **holding grade span (`grades`) constant** — and because the model is
additive, this slope is the **same for both** KK-06 and KK-08. (ii) The fitted lines are **two parallel
lines** (one per school type): **same slope, different intercepts**. The additive model *forces* the
common slope by omitting an interaction term.

**(c)** **Statistical significance** = evidence (small p-value / CI excluding 0) that the effect is **not
zero / not just chance** — it says nothing about size. **Practical significance** = the effect is **large
enough to matter** in the real world (the magnitude of the estimate). Scenario: with a huge sample, an
`income` slope of, say, **0.002** reading points per \$1000 could have `p < 0.001` (statistically
significant) yet be far too small to care about (not practically significant). Always report both.

---

## Problem 2 — The interaction model `read ~ income * grades`

**(a)** (i) KK-06 slope = **2.02** (the reference group's `income` coefficient). (ii) KK-08 slope =
`2.02 + (−0.11) =` **1.91**. (iii) The `−0.11` is the **difference in slopes** (KK-08 minus KK-06) — a
slope *gap*, **not** a slope by itself.

**(b)** **4 coefficients**: intercept, `income`, `gradesKK-08`, and `income:gradesKK-08`. The two lines
have **different slopes AND different intercepts** (non-parallel) — that is what the interaction buys
over the additive (parallel) model.

**(c)** `p ≈ 0.68 > 0.10` ⇒ **fail to reject `H0: b3 = 0`** ⇒ **no evidence** that the income–reading
slope differs between KK-06 and KK-08 (lines effectively parallel). Report the simpler **additive model**
`read ~ income + grades`: not contradicted by the data and easier to interpret. (If you mention the
`−0.11`, caveat that it is statistically indistinguishable from 0.)

**(d)** The KK-06-only SLR matches the interaction model's `income` coefficient because **KK-06 is the
reference**: for those rows the `gradesKK-08` dummy is 0, so the interaction model reduces to exactly
`read = b0 + b_income * income` — the same line the reference-only SLR fits. For KK-08, the interaction
model's line is `(b0 + b_gradesKK08) + (b_income + b_interaction)*income`, so its **slope is
`income + income:gradesKK-08` = 1.91**. The interaction coefficient (−0.11) alone is only the *gap*
between the two slopes, which is why the KK-08 SLR slope equals the **sum**, not −0.11.
