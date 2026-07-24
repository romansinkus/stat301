# Solutions 09 — Comprehensive Midterm Practice Exam

*Questions: [`../practice-exam.md`](../practice-exam.md).*

---

## Section A — Quick concepts

**A1.** `E[Y|X]` is the **average (mean) response over everyone at that value of `X`** — a conditional
mean, **not** a single individual's predicted value. Individuals scatter around it via the error term.

**A2.** Correct reading: **across many samples, 95% of intervals built this way would contain the true
slope** (we are "95% confident"). The slope **is significant at 5%** because the interval **excludes 0**
(both endpoints 2.1 and 4.8 are > 0), equivalently p < 0.05. *(The "95% chance the true slope is in
this fixed interval" phrasing is wrong — once computed, the interval either contains the truth or not.)*

**A3.** Reject `H0` that all state means are equal ⇒ **at least one state's mean death rate differs**
from the others; i.e. death rate **is associated with state.** It does **not** say every pair of
states differs, nor which state is highest/lowest.

**A4.** **Equal variance (E)** is violated; the problem is called **heteroscedasticity.**

**A5.** It **inflates the standard errors** of the involved coefficients (widening CIs and making
significance harder). It does **not** bias the slope estimates, and overall `R^2`/fit can stay high.

---

## Section B

**B1.**
(a) "A **one-percentage-point increase** in a county's poverty rate is **associated with** about
**1.52 more** cancer deaths per 100 000, on average."
(b) **Yes, significant.** The 95% CI `(1.40, 1.64)` **excludes 0**, and `p ≈ 0 < 0.05` — both say we
reject `H0: b1 = 0`.
(c) Wrong phrasing: "Poverty **causes** 1.52 extra deaths" or "the **effect** of poverty is 1.52." The
data are **observational**, so "causes"/"effect" overreach — use "associated with."

**B2.** The **error term** `e_i` lives in the true population model and is **unknown/unobservable**;
the **residual** `= observed − fitted` is computed from the **sample** and is **observable**. They
differ because residuals use the **estimated** coefficients (`b0hat`, `b1hat`), which aren't exactly
the true `b0`, `b1`. The residual is our observable stand-in for the invisible error.

**B3.** **Theory (`lm`)** assumes Normal errors (or relies on the **CLT** for large `n`) and uses a
**t-distribution with `n − k` df** to get the SE. **Bootstrap** assumes your sample is representative
of the population and **resamples from it with replacement**, each resample of **size `n`**, refits,
and uses the spread of the resampled slopes as the sampling distribution / SE. Theory needs a
distributional assumption; bootstrap trades that for computation and a representative sample.

**B4.**
(a) It describes **parallel lines** — one per state, all sharing a **common poverty slope** but with
**different intercepts**.
(b) The `povertyPercent` coefficient = expected change in death rate per +1 poverty point, **holding
state constant** (and it's the same at any state, because additive).
(c) The slope differs from the SLR because in the SLR **state was omitted** and its influence was
**dumped into the error term**, contaminating the poverty coefficient; the MLR holds state constant,
cleaning up the estimate.

**B5.**
(a) It tests `H0: b3 = 0` — whether California's **poverty slope differs** from Alabama's (the
reference).
(b) `p = 0.28 > 0.05` ⇒ **fail to reject**; no evidence the two states' poverty slopes differ (lines
are parallel as far as the data show).
(c) The **additive** model is justified — simpler, and the interaction isn't supported by the data.

**B6.**
- **L**inear: `E[Y|X]` is linear. Violation ⇒ the whole model is **misspecified/dubious**.
- **I**ndependent errors. Violation ⇒ **biased SEs** ⇒ invalid CIs/tests.
- **N**ormal errors. (Least severe; CLT/bootstrap rescue.)
- **E**qual variance. Violation ⇒ **wrong SEs** ⇒ invalid CIs/p-values.
(Consequences asked for L, I, E given above.)

---

## Section C

**C1.** The claim is **causal from observational data**, so it's unwarranted. At least two problems:
- **Confounding:** wealth/education could drive *both* higher private coverage *and* lower cancer
  mortality (better diet, screening, environment) — a confounder `C → X` and `C → Y`.
- **Reverse causality / selection:** healthier or higher-income populations both buy private coverage
  and have lower death rates; coverage may be a *marker*, not a cause.
A causal claim would need a **randomized experiment** (randomly assign coverage), because
randomization balances **observed and unobserved** confounders on average, letting you attribute the
mortality difference to coverage itself. (Such an experiment is likely infeasible/unethical here —
which is exactly why only association can be claimed.)

**C2.**
(a) **Multicollinearity** — poverty, private coverage, and median income are strongly interrelated
(they carry overlapping information), so the model can't cleanly separate their individual effects,
**inflating the SEs** even while overall fit stays good.
(b) Diagnose with **VIF** (rule of thumb **> 5 or 10** is concerning); with categorical predictors
use **GVIF** and compare **`GVIF^(1/(2Df))`** to `sqrt(5) ≈ 2.23` / `sqrt(10) ≈ 3.16`.
(c) Fixes: **drop** one collinear predictor (simple, but lose its unique info) or **combine** them
into one index (keep info, but interpretation changes).

**C3.**
(a) Funnel = **heteroscedasticity (E)**; Q-Q bending at the tails = **non-Normal errors (N)**.
(b) A **log transform of the response** (`log(TARGET_deathRate)`) — it compresses large values more
than small ones, **stabilizing the variance** and pulling in a right-skewed error distribution toward
Normal, addressing **both** at once.
(c) After the fix: the residuals-vs-fitted plot should show a **structureless band of roughly constant
spread** around 0, and the Q-Q plot should have points **lying on the diagonal**.
