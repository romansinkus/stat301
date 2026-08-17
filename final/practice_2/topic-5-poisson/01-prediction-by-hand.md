# Practice 01 (Topic 5) — Poisson Prediction by Hand

*Gap-filler for Topic 5. Solutions: [`solutions/01-prediction-by-hand-solutions.md`](solutions/01-prediction-by-hand-solutions.md).
Companion to `../../practice/topic-5-poisson/` (rate ratios, `factor()`, overdispersion — concepts).
This set drills the `λ = e^(b0+b1x)` computation.*

> **Exam-style.** Show key steps (70% procedure, 30% answer). Circle final numbers. Calculator allowed.
> Useful: `e^2.6 ≈ 13.46`, `e^2.9 ≈ 18.17`, `e^2.75 ≈ 15.64`, `e^0.3 ≈ 1.350`, `e^0.15 ≈ 1.162`.

---

## Problem 1 (17 pts) — From coefficients to a predicted count

`glm(bikers ~ temp + workingday, family = poisson)` (`workingday`: 0 = no, 1 = yes) gives:

```
term          estimate
(Intercept)     2.00
temp            0.03
workingday      0.15
```

**(a) (4 pts)** Write the model in **log-mean** form and in **mean** form. Which one is "the linear one,"
and what scale is `2.00 + 0.03·temp + 0.15·workingday` on?

**(b) (5 pts)** Predict the **mean number of bikers** on a **non-working day** at **temp = 20**. Compute the
log-mean first, then exponentiate. Circle `λ̂`.

**(c) (5 pts)** Predict the mean at **temp = 30** on a non-working day. Then show that the ratio of the two
predicted means (temp 30 vs. 20) equals `e^(0.03×10)`, and connect that to the **rate ratio**
interpretation of `temp`.

**(d) (3 pts)** Predict the mean on a **working day** at **temp = 20**. By what factor does it exceed the
non-working prediction from (b), and which coefficient controls that factor? Give the percent change.

---

## Problem 2 (13 pts) — Rate ratios and the "no negative counts" property

**(a) (4 pts)** The `temp` coefficient is `0.03`. (i) Interpret it on the **log-mean** scale (one
sentence). (ii) Convert to a **rate ratio** per 1-degree rise (`e^0.03 ≈ 1.030`) and give the percent
change — remember to use the word **mean/expected**.

**(b) (4 pts)** A shortcut: if the predicted mean at some temperature is **40 bikers**, what is the
predicted mean **one degree** warmer? (Use `40 × e^0.03`.) Why is this a *multiply*, not an *add*?

**(c) (3 pts)** Explain in ≤ 30 words why the **log link guarantees the predicted mean is never negative**,
no matter what values the predictors take — and why plain linear regression can't promise that for counts.

**(d) (2 pts)** True/false, justify: "Because `λ̂ = 13.46` isn't a whole number, the Poisson model is
wrong." (Think about what `λ` *is*.)
