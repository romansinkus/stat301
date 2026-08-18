# Solutions 01 (Topic 9) — Prediction Uncertainty (CIP vs. PI) 

*Questions: [`../01-cip-vs-pi.md`](../01-cip-vs-pi.md).*

> Marking scheme: **70% for correct procedures, 30% for correct answers.**

---

## Problem 1 — The two targets: CIP vs. PI

**(a)** The coefficients `b̂0, b̂1` are estimated from a **random sample**, so a **different sample would
give different coefficients** and therefore a different `ŷ`. The prediction inherits that
sample-to-sample randomness — it is a **random variable**, not a fixed number.

**(b)** (1) The **average** value of *all* units at that `X`: **`E[Y|X]`** — a point on the population
regression line. (2) The **actual** value of *one specific new* unit at that `X`: **`Y`**, which equals
the average **plus its own random error**, `Y = E[Y|X] + e`. So `Y` carries the extra individual error `e`
that `E[Y|X]` does not.

**(c)**

| | CIP | PI |
| --- | --- | --- |
| Predicting | the **average** `E[Y|X]` | an **actual new** value `Y` |
| Sources of uncertainty | **one** — sample-to-sample wobble in `b̂` | **two** — wobble in `b̂` **+** the random error `e` |
| Width | narrower | **wider** |
| Interpret with the word... | **confidence** | **probability** |
| `predict(interval = ?)` | `"confidence"` | `"prediction"` |

Both are centred at the same fitted value `ŷ`.

**(d)** `Y = E[Y|X] + e` (truth) → `Y = b0 + b1X + e` (linearity assumption) → `ŷ = b̂0 + b̂1X` (our
prediction). The **CIP** aims `ŷ` at the **middle part `b0 + b1X`** — the **average line** `E[Y|X]` — so it
only needs to cover the gap between `b̂` and `b` (estimation wobble). The **PI** aims `ŷ` at the **whole
top line `Y = b0 + b1X + e`** — the average **plus** the individual error — so it must cover **both** the
estimation wobble **and** the `e` scatter. Same `ŷ`, different target, different width.

---

## Problem 2 — Reading and applying `predict()` output

**(a)** The **CIP** accounts for only **one** source of uncertainty: our estimated line `b̂0 + b̂1X`
approximates the true average line `b0 + b1X` (sample-to-sample wobble). The **PI** must **also** account
for a **second** source: even if we knew the true average line perfectly, an **individual** unit still
scatters around it by its own error `e`. **Two sources > one**, so the PI is **always wider** — predicting
**one actual value is harder** than predicting **the average**.

**(b)** The **CIP**'s target, the average `E[Y|X]`, is a **fixed unknown constant** — so we speak of
**confidence** (over repeated samples, 95% of such intervals capture that fixed number). The **PI**'s
target, an individual `Y`, is **itself a random variable**, so we speak of **probability** (there is
genuine randomness in the outcome we are bracketing). Fixed target → confidence; random target →
probability.

**(c)** (i) `(671944, 748198)` is the **CIP** (`interval = "confidence"`) and `(454519, 965622)` is the
**PI** (`interval = "prediction"`) — you can tell because the **PI is much wider** (it contains the extra
error term `e`). (ii) **CIP:** "With **95% confidence**, the **average** assessed value of houses of size
220 m is between **\$671,944 and \$748,198**." **PI:** "With **95% probability**, the value of **a single**
house of size 220 m is between **\$454,519 and \$965,622**." (iii) Both are centred at the same fitted
value `ŷ` — roughly the midpoint, about **\$710,000**.

**(d)** (i) **False.** The `geom_smooth(se = TRUE)` band is the **CIP band** — it shows the uncertainty of
the **fitted line / average `E[Y|X]`**, i.e. how much the *line itself* could wobble from sample to
sample. It is **not** a PI and does **not** show where individual points fall (that scatter is much wider,
governed by `e`). (ii) For the **single specific house**, give the **PI** — the client cares about **one
actual `Y`**, which carries the individual error `e`, so the wider interval is the honest range. For the
**city's average** over all 220 m houses, give the **CIP** — the target is the **average `E[Y|X]`**, a
fixed number with only estimation uncertainty. (Using a CIP for the single house would badly **understate**
the uncertainty.)
