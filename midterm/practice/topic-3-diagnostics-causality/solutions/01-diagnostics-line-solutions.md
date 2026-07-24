# Solutions 06 — Assumptions & Diagnostics (LINE)

*Questions: [`../01-diagnostics-line.md`](../01-diagnostics-line.md).*

---

**Q1.**
- **L — Linearity:** the conditional mean is linear, `E[Y|X] = b0 + b1*X`.
- **I — Independence:** the errors are independent of one another.
- **N — Normality:** the conditional distribution of the errors is Normal.
- **E — Equal variance (homoscedasticity):** all errors share the same variance `sigma^2`.

---

**Q2.** **False.** The equal-variance (homoscedasticity) assumption **directly affects the standard
error estimator** of the LS coefficients: the usual SE formula assumes a single constant `sigma^2`.
If that assumption is wrong (heteroscedasticity), those SEs are **biased/invalid**, and so are the
CIs and p-values built from them. (Note: the **point estimates** `b0hat`, `b1hat` are unaffected —
LS produces them regardless — but their **SEs** are not. The statement is about the SE estimator, so
it's false.)

---

**Q3.** Residuals hold **everything the model didn't capture**, so any structure the model missed
shows up as a **pattern** in them. Plotting residuals vs. fitted values, a good model gives a
**structureless cloud centered on 0** with roughly constant vertical spread and no curve or funnel.

---

**Q4.** It violates **E — Equal variance (homoscedasticity)**; the technical name for the problem is
**heteroscedasticity** (the error variance isn't constant — here it grows with the fitted value). When
the assumption *holds*, the plot is a **structureless horizontal band of roughly constant vertical
spread** around 0 — no funnel or fan.

---

**Q5.**
- **L violated:** the whole model is **dubious/misspecified** (fitted relationship is wrong shape).
- **I violated:** the **SEs are biased** → CIs and hypothesis tests are invalid.
- **E violated:** the **SEs are wrong** → CIs and p-values invalid.
The two that specifically **break the standard errors** are **I (Independence)** and **E (Equal
variance)**.

---

**Q6.** Normality is "least severe" because with a **large sample the CLT** makes inference
approximately valid even with non-Normal errors, and **bootstrapping** also gives valid inference
without the Normality assumption. So violating N usually doesn't sink your CIs/p-values the way I or E
do.

---

**Q7.**
(a) **Linearity (L)** is violated (a systematic curve, not a structureless cloud).
(b) Fix: add a **transformation of the predictor** — e.g. an `income^2` (quadratic) term, or `log`.
(c) It's still a **linear regression** because "linear" means **linear in the parameters** — `income^2`
is just another covariate multiplying a coefficient; LS works identically, only the interpretation
changes.

---

**Q8.** The **Q-Q plot** of residuals (`plot(model, 2)`) diagnoses Normality. **Good** = points lie
**on the diagonal** reference line. A violation shows up as **systematic bending off the diagonal**,
especially at the **tails**.

---

**Q9.** The funnel = **heteroscedasticity (E violated)**; the Q-Q drift = **non-Normal errors (N
violated)**. Refitting `log(wage)` compresses large values more than small ones, which **stabilizes
the variance** (shrinks the funnel) and **pulls in a right-skewed error distribution** toward
symmetry/Normal — so a single response transformation can fix both the E and N problems at once.

---

**Q10.** Independence most often fails with **temporal data** (measurements over time) and **repeated
measurements on the same subject**, where adjacent errors are correlated. You often judge it from the
**study design** because a residual plot can't always reveal correlation, whereas the design tells you
directly whether observations are linked (e.g. same person measured repeatedly) or safely separate
(e.g. different districts).

---

**Q11.**

| Assumption | Plot to inspect | 'Bad' pattern that signals a violation |
| --- | --- | --- |
| **L** (linearity) | residuals-vs-fitted | a **curve / wave** (e.g. U-shape) instead of a structureless cloud around 0 |
| **E** (equal variance) | residuals-vs-fitted | a **funnel / fan** — spread widens or shrinks with the fitted value |
| **N** (normality) | Q-Q plot of residuals | points **bending off the diagonal**, especially at the tails |

(Residuals-vs-fitted does double duty for L and E: look at *shape* for L, *spread* for E.)
