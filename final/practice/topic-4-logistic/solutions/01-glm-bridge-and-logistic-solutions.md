# Solutions 01 (Topic 4) — The GLM Bridge & Logistic Regression

*Questions: [`../01-glm-bridge-and-logistic.md`](../01-glm-bridge-and-logistic.md).*

> Marking scheme: **70% for correct procedures, 30% for correct answers.**

---

## Problem 1 — The GLM bridge and the three scales

**(a)** (i) For a **binary** response, `E[Y|X] = P(Y=1|X)` is a **probability** that must stay in
**(0,1)**, but a straight line runs off to **±∞**, producing fitted "probabilities" below 0 and above 1.
(ii) For a **count**, `E[Y|X]` must be **≥ 0**, but a line predicts **negative** counts. **The trick:**
do not model `E[Y|X]` directly — model a **link function `h(E[Y|X])`** and set *that* equal to the linear
part, choosing `h` so the left side can roam over (−∞, ∞) while `E[Y|X]` stays in its legal range.

**(b)**

| Response type | Distribution | Link | `glm(family=)` | Models... |
| --- | --- | --- | --- | --- |
| continuous | Normal/Gaussian | identity | `gaussian` | the mean `E[Y]` |
| binary 0/1 | Bernoulli/Binomial | **logit** `log(p/(1−p))` | `binomial` | the **log-odds** |
| count 0,1,2… | Poisson | log | `poisson` | the **log-mean** |

Ordinary linear regression is the special case `h(x) = x` (the **identity** link) — nothing is
transformed — so it is itself a GLM.

**(c)** (i) **False on two counts.** (1) A GLM has **no error term `e`** — we model a *function of the
conditional expectation* directly (the randomness lives in the Bernoulli distribution of `Y`). (2) GLMs
are estimated by **maximum likelihood (MLE)** via an iterative algorithm (Fisher scoring), **not least
squares** (they coincide only for Normal errors). (ii) With `p = P(Y=1|X)`:
- **probability:** `p = e^(b0+b1X) / (1 + e^(b0+b1X))` (the S-curve, always in (0,1)),
- **log-odds (logit):** `log(p/(1−p)) = b0 + b1X` ← **the linear one**,
- **odds:** `p/(1−p) = e^(b0+b1X)`.
The log-odds works because it ranges over **all real numbers** (as `p` goes 0→1 the logit goes −∞→+∞), so
it can match a linear predictor that also ranges over all reals — while `p` itself stays in (0,1).

**(d)** **Odds** `= p/(1−p)` = "successes per failure." For `p = 0.8`: odds `= 0.8/0.2 =` **4** (survival
4× as likely as death). For odds `= 0.25`: `p/(1−p) = 0.25` ⇒ `p = 0.25/1.25 =` **0.2**.

---

## Problem 2 — Interpreting a fitted logistic model (Titanic)

**(a)** (i) "A \$1 increase in fare is associated with a **+0.0152 change in the log-odds** of surviving."
(ii) `e^0.0152 ≈ 1.015`: "a \$1 increase in fare **multiplies the odds** of surviving by **1.015**." (iii)
`(1.015 − 1) × 100 =` **+1.5%**: "…about a **1.5% increase in the odds** of surviving per \$1."

**(b)** (i) `e^(−2.514) = 0.081`: a male's **odds of surviving are 0.081× a female's** — only **8.1%** of
a female's odds (a 91.9% decrease). (ii) Flipping to the odds of **dying**, `e^2.514 = 12.35`: a male's
**odds of dying were 12.35× a female's**. (iii) Same story — being far **less** likely to survive is
identical to being far **more** likely to die; the reciprocal odds ratios (`1/0.081 ≈ 12.35`) describe one
relationship from two directions.

**(c)** (i) `e^(−1.694) ≈ 0.1838`, so `p ≈ 0.1838 / 1.1838 ≈` **0.155**. (ii) `0.155 < 0.5`, so under a
0.5 cutoff this passenger is predicted **not to survive**. (iii) `type = "link"` returns the **log-odds**
`L` (default); `type = "response"` returns the **probability** `p`.

**(d)** (i) The **odds (exponentiated) scale** — these are odds ratios (`exponentiate = TRUE`). (ii) "Each
\$1 increase in fare is associated with a **1.1% increase in the odds** of surviving (odds ratio 1.011);
we are 95% confident the true odds ratio is between **1.008 and 1.015**." (iii) Yes, `fare` is
**significant**: on the odds scale the CI must exclude **1** (no effect), and `(1.008, 1.015)` does.

---

## Problem 3 — Additive vs. interaction, diagnostics, overdispersion

**(a)** They are wrong. An **additive** logistic model is **parallel on the log-odds scale** — same
`fare` slope for both sexes, different intercepts. But the **logit → probability** transformation (the
S-curve) **squashes** the log-odds nonlinearly, so equal log-odds gaps map to **unequal probability
gaps**; the fitted **probability** curves therefore look non-parallel even though nothing is interacting.
Parallelness lives on the **log-odds** scale, not the probability scale.

**(b)** On the **log-odds** scale the male fare-slope is `b2 + b3` (reference slope plus the interaction
gap) — additive. Exponentiating to get the **odds** ratio turns that sum into a **product**:
`e^(b2+b3) = e^b2 · e^b3` (because `e^(a+b) = e^a·e^b`). You **cannot** say "holding sex constant, the
fare effect is…" because in an interaction the **effect of fare depends on sex** — there is no single fare
effect; report one odds ratio for females and a different one for males.

**(c)** (1) The **variance is not constant** — for a Bernoulli response `Var(Y) = p(1−p)` changes with the
fitted probability, so residuals are not comparable; (2) because `y` is only **0 or 1**, the raw residuals
collapse onto **two parallel lines** (`−p̂` and `1−p̂`), showing structure that is not a model problem.
Rely instead on **overdispersion** (and, if you must plot, a **binned residual plot** of **Pearson**
residuals).

**(d)** **Overdispersion** = the data's actual variability is **larger than the model assumes**
(`Var(Y) > p(1−p)` for logistic). It misspecifies the **standard errors, not the point estimates**, so
CIs and p-values become unreliable. **Detect:** refit with `family = quasibinomial` and read the
**dispersion parameter** — **≈ 1 is fine**, **> 1 = overdispersion**. **Fix:** the **quasi-likelihood**
approach (`quasibinomial`) estimates the dispersion and **corrects the SEs** (coefficients unchanged).
Titanic dispersion ≈ **0.98** is essentially 1, so there is **no overdispersion problem**.
