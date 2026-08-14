# Solutions 01 (Topic 3) — Assumptions & Diagnostics (LINE)

*Questions: [`../01-diagnostics-line.md`](../01-diagnostics-line.md).*

> Marking scheme: **70% for correct procedures, 30% for correct answers.**

---

## Problem 1 — The LINE assumptions and their consequences

**(a)**
- **L — Linearity:** the conditional mean is linear, `E[Y|X] = b0 + b1*X`.
- **I — Independence:** the errors are independent of one another.
- **N — Normality:** the conditional distribution of the errors is Normal.
- **E — Equal variance (homoscedasticity):** all errors share the same variance `σ²`.

**(b)** **False.** The equal-variance assumption **directly affects the SE estimator** of the LS
coefficients: the usual SE formula assumes a single constant `σ²`. If that fails (heteroscedasticity),
those SEs are **biased/invalid**, and so are the CIs and p-values. (The **point estimates** `b̂0, b̂1`
are unaffected — LS produces them regardless — but their **SEs** are not, so the statement is false.)

**(c)** **L violated:** the whole model is **misspecified** (wrong shape). **I violated:** the **SEs are
biased** → CIs and tests invalid. **E violated:** the **SEs are wrong** → CIs and p-values invalid. The
two that specifically **break the standard errors** are **I (Independence)** and **E (Equal variance)**.

**(d)** (i) Normality is "least severe" because with a **large sample the CLT** makes inference
approximately valid even with non-Normal errors, and **bootstrapping** also gives valid inference without
Normality. (ii) Independence most often fails with **temporal data** (measurements over time) and
**repeated measurements on the same subject**, where adjacent errors are correlated. You judge it from
the **study design** because a residual plot cannot always reveal correlation, whereas the design tells
you directly whether observations are linked (same person measured repeatedly) or safely separate.

---

## Problem 2 — Reading diagnostic plots

**(a)** Residuals hold **everything the model did not capture**, so any missed structure shows up as a
**pattern** in them. Plotting residuals vs. fitted values, a good model gives a **structureless cloud
centered on 0** with roughly constant vertical spread and no curve or funnel.

**(b)** (i) The funnel violates **E — Equal variance**; the technical name is **heteroscedasticity** (the
error variance is not constant — here it grows with the fitted value). When the assumption *holds*, the
plot is a **structureless horizontal band of roughly constant vertical spread** around 0. (ii) The
U-shape violates **Linearity (L)**. Fix: add a **transformation of the predictor** — e.g. an `income^2`
(quadratic) term. It is still a **linear** regression because "linear" means **linear in the
parameters** — `income^2` is just another covariate multiplying a coefficient; LS works identically.

**(c)** (i) The **Q-Q plot** of residuals (`plot(model, 2)`) diagnoses Normality. **Good** = points lie
**on the diagonal** reference line; a violation shows **systematic bending off the diagonal**, especially
at the **tails**. (ii) The funnel = **heteroscedasticity (E)**; the Q-Q drift = **non-Normal errors
(N)**. Refitting `log(wage)` compresses large values more than small ones, which **stabilizes the
variance** (shrinks the funnel) and **pulls in a right-skewed error distribution** toward symmetry — so a
single response transformation fixes both the E and N problems at once.

**(d)**

| Assumption | Plot to inspect | 'Bad' pattern that signals a violation |
| --- | --- | --- |
| **L** (linearity) | residuals-vs-fitted | a **curve / wave** (e.g. U-shape) instead of a structureless cloud around 0 |
| **E** (equal variance) | residuals-vs-fitted | a **funnel / fan** — spread widens or shrinks with the fitted value |
| **N** (normality) | Q-Q plot of residuals | points **bending off the diagonal**, especially at the tails |

*(Residuals-vs-fitted does double duty for L and E: look at *shape* for L, *spread* for E.)*
