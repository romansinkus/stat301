# Practice 01 (Topic 4) — Logistic Prediction by Hand & Scale Conversions

*Gap-filler for Topic 4. Solutions: [`solutions/01-prediction-by-hand-solutions.md`](solutions/01-prediction-by-hand-solutions.md).
Companion to `../../practice/topic-4-logistic/` (3 scales, odds ratios, overdispersion — concepts).
`master_notes.md` flags "compute L, then p = e^L/(1+e^L)" as a **likely exam task** — this set drills it.*

> **Exam-style.** Show key steps (70% procedure, 30% answer). Circle final numbers. Calculator allowed.
> Useful values: `e^0.5 ≈ 1.649`, `e^−2 ≈ 0.135`, `ln 4 ≈ 1.386`, `ln 0.25 ≈ −1.386`.

---

## Problem 1 (17 pts) — From coefficients to a probability, then a classification

`glm(survived ~ fare + sex, family = binomial)` (female = reference) gives:

```
term          estimate
(Intercept)     -1.00
fare             0.015
sexmale         -2.50
```

**(a) (5 pts)** For a **female** who paid **fare = 100**, compute the **linear predictor** `L = b̂0 +
b̂1·fare + b̂2·sexmale`. Show the substitution. What scale is `L` on?

**(b) (5 pts)** Convert `L` to a **probability** using `p = e^L / (1 + e^L)`. Show the arithmetic and
circle `p`. As a **classifier** thresholding at 0.5, does the model predict she survived?

**(c) (5 pts)** Now a **male** who also paid **fare = 100**. Recompute `L` and `p`, and classify at 0.5.
Report the male–female difference **on the log-odds scale** and confirm it equals the `sexmale`
coefficient — then explain why the difference is **not** −2.50 on the probability scale.

**(d) (2 pts)** In one sentence, why do we go *through* the log-odds/`L` scale to make a probability
prediction, instead of writing a linear model for `p` directly?

---

## Problem 2 (14 pts) — Moving between the three scales numerically

**(a) (4 pts)** A passenger has **log-odds of survival = 0.5**. Compute their (i) **odds** and (ii)
**probability**. Show both conversions.

**(b) (4 pts)** A different passenger has **probability 0.80**. Compute their (i) **odds** and (ii)
**log-odds** (use `odds = p/(1−p)`, then take `ln`).

**(c) (4 pts)** The `sex` coefficient is `−2.50` on the log-odds scale. (i) Convert it to an **odds ratio**
(`e^−2.5 ≈ 0.082`). (ii) Give the correct **percent-change** statement for males vs. females (remember:
`OR < 1` → decrease `= (1 − OR)×100`). (iii) Is this the same on the log-odds scale as "significant if the
CI excludes ___"?

**(d) (2 pts)** Fill the blanks: raw `glm` coefficients live on the **____** scale; `exponentiate = TRUE`
puts them on the **____** scale; `predict(type = "response")` returns the **____** scale.
