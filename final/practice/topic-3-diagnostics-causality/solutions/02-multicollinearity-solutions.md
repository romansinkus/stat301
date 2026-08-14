# Solutions 02 (Topic 3) — Multicollinearity

*Questions: [`../02-multicollinearity.md`](../02-multicollinearity.md).*

> Marking scheme: **70% for correct procedures, 30% for correct answers.**

---

## Problem 1 — What multicollinearity is and does

**(a)** **Multicollinearity** = two or more predictors are **strongly associated with each other**, so
they carry **overlapping information**. The model cannot isolate individual effects because it cannot
tell how much of `Y`'s variation to credit to one collinear predictor vs. the other — they move
together, so their separate contributions are ambiguous.

**(b)** `incomeUSD` is just `income` rescaled — the **same variable**. So **infinitely many combinations**
of the two coefficients produce the **exact same fitted values and the exact same SSR** (you can shift
"weight" from one to the other freely). With no unique minimizer, R cannot choose, so it drops one and
returns `NA`.

**(c)** (i) Two employees who always work identical shifts and do identical work: payroll sees the
**team's** total output but cannot attribute it to either individually. Likewise, perfectly collinear
predictors have **unidentifiable individual contributions** — only their combined effect is estimable.
(ii) Strong collinearity **inflates the standard errors** of the involved coefficients, **widening their
CIs** and making it **harder to reject `H0: bj = 0`**. It does **not** bias the point estimates, and the
overall **`R²`/fit can remain good** — it is specifically the **precision of the individual
coefficients** that suffers.

**(d)** **False.** Collinearity need **not** be pairwise — one predictor can be collinear with a **linear
combination of several others** (you could predict it well by regressing it on all the rest). That is why
pairwise checks can miss it.

---

## Problem 2 — Detecting and fixing multicollinearity

**(a)** Pairwise correlations only catch **two-variable** relationships; they **miss multi-variable
collinearity** where a predictor is redundant given a *combination* of others. **VIF/GVIF** catches that,
because it measures how inflated a coefficient's SE is when fit **with all the other predictors**, not
just against one at a time.

**(b)** **VIF** captures how much a coefficient's **variance (SE²) is inflated** when the predictor is fit
*alongside* the others vs. *alone*. Guideline: **VIF > 5 (or 10)** is concerning. With categorical
predictors use **GVIF (Generalized VIF)** and compare **`GVIF^(1/(2*Df))`** against `sqrt(5) ≈ 2.23` or
`sqrt(10) ≈ 3.16` (equivalently, square that column and compare to 5 / 10).

**(c)** Compare **`GVIF^(1/(2*Df)) = 1.87`** against `sqrt(5) ≈ 2.23`. Since `1.87 < 2.23`, it is
**below** the threshold ⇒ **not concerning** by the rule-of-5. (You must use the `GVIF^(1/(2Df))` column,
**not** the raw `GVIF = 12.4`, which is distorted by the number of categories.)

**(d)** Fixes: **(1) Drop** one of the collinear predictors — simplest, but you lose that variable's
unique info (if any). **(2) Combine** them into a single predictor (e.g. an index/sum) — retains
information but **changes the interpretation**. In the penguins model, **`species`** had the highest VIF;
**removing it fixed the other inflated VIFs**.
