# Practice 01 (Topic 3) — Interpreting Log-Transformed Models

*Gap-filler for Topic 3. Solutions: [`solutions/01-log-transformed-models-solutions.md`](solutions/01-log-transformed-models-solutions.md).
Companion to `../../practice/topic-3-diagnostics-causality/` (LINE, VIF, causality). The other set uses
`log(Y)` as a **fix** for funnel/curvature but never asks you to **interpret** the resulting coefficient —
that's this set's job.*

> **Exam-style.** Show key steps (70% procedure, 30% answer). Circle final numbers.

---

## Problem 1 (16 pts) — `log(Y)` models (the semi-log)

A wage model funnels and its Q-Q plot drifts, so you refit `lm(log(wage) ~ education)` and get:

```
term          estimate
(Intercept)      1.20
education        0.08
```

**(a) (4 pts)** First, the *why*: name the **two** LINE-related problems that logging `Y` often fixes at
once, and why `log(wage)` is still an ordinary **linear** regression (what is "linear" actually referring
to?).

**(b) (5 pts)** Interpret the `education` slope `0.08`. (i) Give the **exact** percentage interpretation
using `(e^β − 1)×100`. (ii) Give the **approximate** rule-of-thumb `≈ 100·β %` and say when the
approximation is good. (iii) Circle the plain-language sentence you'd write on the exam.

**(c) (4 pts)** A classmate writes: "each extra year of education adds **0.08 dollars** to wage." Explain
what's wrong (two things: the scale, and additive-vs-multiplicative), and give the corrected statement.

**(d) (3 pts)** On the `log(wage)` scale the effect is *additive/constant*; on the **dollar** scale it is
not. In ≤ 30 words, explain what "constant on the log scale" implies about the dollar effect at low vs.
high wages (whose gap is bigger in dollars?).

---

## Problem 2 (15 pts) — `log(X)` and log–log (elasticity)

**(a) (5 pts)** A demand study fits `lm(log(sales) ~ log(price))` (a **log–log** model) with a `log(price)`
coefficient of **−1.5**. State the special name for this coefficient, and give its interpretation: a **1%**
increase in price is associated with approximately what change in sales? Is demand elastic or inelastic
here?

**(b) (4 pts)** A different model is **linear–log**: `lm(mpg ~ log(weight))` with a `log(weight)`
coefficient of **−6**. Interpret it: a **1%** increase in weight is associated with what change in `mpg`?
What about a **doubling** of weight (show the `× ln 2` step)?

**(c) (4 pts)** Fill in the interpretation cheat-table (what a **1-unit** change in the RHS predictor does,
per model form):

| Model | Coefficient `β` interprets as… |
| --- | --- |
| `Y ~ X` (level–level) | ? |
| `log(Y) ~ X` (log–level) | ? |
| `Y ~ log(X)` (level–log) | ? |
| `log(Y) ~ log(X)` (log–log) | ? |

**(d) (2 pts)** In one sentence: why do economists like the **log–log** form so much (what makes the
coefficient unit-free and comparable across variables)?
