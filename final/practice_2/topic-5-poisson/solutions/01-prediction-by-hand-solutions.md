# Solutions — Practice 01 (Topic 5): Poisson Prediction by Hand

## Problem 1

**(a)** Log-mean form: `log(λ) = 2.00 + 0.03·temp + 0.15·workingday`. Mean form:
`λ = e^(2.00 + 0.03·temp + 0.15·workingday)`. The **log-mean form is the linear one**; the expression
`2.00 + 0.03·temp + 0.15·workingday` is on the **log-mean (log-count)** scale.

**(b)** Non-working (`workingday = 0`), `temp = 20`: `log λ = 2.00 + 0.03×20 + 0 = 2.00 + 0.60 = 2.60`.
`λ̂ = e^2.60 = **13.46 bikers**`.

**(c)** `temp = 30`: `log λ = 2.00 + 0.90 = 2.90`, `λ̂ = e^2.90 = **18.17 bikers**`. Ratio =
`18.17/13.46 = **1.35** = e^(0.03×10) = e^0.30`. So each **1-degree** rise multiplies the mean by
`e^0.03 ≈ 1.030` (a 3.0% increase), and **10 degrees** multiplies it by `e^0.3 ≈ 1.35` — that multiplicative
factor is the **rate ratio**. *(The temp effect is multiplicative on the mean count.)*

**(d)** Working day (`workingday = 1`), `temp = 20`: `log λ = 2.00 + 0.60 + 0.15 = 2.75`, `λ̂ = e^2.75 =
**15.64**`. Factor over non-working = `e^0.15 = **1.162**`, controlled by the **`workingday` coefficient**
→ working days have about **16.2% more** expected bikers. *(Check: 15.64/13.46 = 1.16 ✓.)*

## Problem 2

**(a)** (i) A 1-degree rise in temp is associated with a **+0.03 increase in the log-mean** number of
bikers, holding workingday constant. (ii) `e^0.03 ≈ 1.030` → a 1-degree rise **multiplies the mean/expected
count by ~1.03**, i.e. about a **3.0% increase** in the mean count.

**(b)** `40 × e^0.03 = 40 × 1.030 = **41.2 bikers**`. It's a **multiply** because Poisson coefficients act
on the **log**-mean — additive on the log scale means multiplicative on the count scale (`e^(a+b) =
e^a·e^b`).

**(c)** The mean is `λ = e^(linear predictor)`, and `e^(anything)` is **always positive**, so the predicted
mean can never go negative regardless of the predictor values. Plain linear regression models the count
directly as `b0 + b1x`, a straight line that runs below 0 for some inputs → it can predict impossible
negative counts.

**(d)** **False.** `λ` is the **mean/expected** count, an average — averages need not be whole numbers
(a mean of 13.46 bikers is fine). Individual counts drawn from the Poisson are integers; their *mean* isn't
required to be.
