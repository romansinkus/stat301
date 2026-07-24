# Solutions 07 — Multicollinearity

*Questions: [`../02-multicollinearity.md`](../02-multicollinearity.md).*

---

**Q1.** **Multicollinearity** = two or more predictors are **strongly associated with each other**,
so they carry **overlapping information**. The model can't isolate individual effects because it can't
tell how much of `Y`'s variation to credit to one collinear predictor vs. the other — they move
together, so their separate contributions are ambiguous.

---

**Q2.** `incomeUSD` is just `income` rescaled — the **same variable**. So **infinitely many
combinations** of the two coefficients produce the **exact same fitted values and the exact same
SSR** (you can shift "weight" from one to the other freely). With no unique minimizer, R can't
choose, so it drops one and returns `NA`.

---

**Q3.** Two employees who always work identical shifts and do identical work: payroll can see the
**team's** total output but can't attribute it to either person individually. Likewise, perfectly
collinear predictors have **unidentifiable individual contributions** — only their combined effect is
estimable.

---

**Q4.** Strong collinearity **inflates the standard errors** of the involved coefficients, which
**widens their CIs** and makes it **harder to reject `H0: bj = 0`** (their p-values inflate too). It
does **not** bias the point estimates, and the **overall `R^2`/fit can remain good** — it's
specifically the **precision of the individual coefficients** that suffers, because the model can't
separate their overlapping information.

---

**Q5.** **False.** Collinearity need **not** be pairwise — one predictor can be collinear with a
**linear combination of several others** (i.e. you could predict it well by regressing it on all the
rest). That's why pairwise checks can miss it.

---

**Q6.** Pairwise correlations only catch **two-variable** relationships; they **miss multi-variable
collinearity** where a predictor is redundant given a *combination* of others. **VIF/GVIF** catches
that, because it measures how inflated a coefficient's SE is when fit **with all the other
predictors**, not just against one at a time.

---

**Q7.** **VIF** captures how much a coefficient's **variance (SE²) is inflated** when the predictor is
fit *alongside* the others vs. *alone*. Guideline: **VIF > 5 (or 10)** is concerning. With categorical
predictors use **GVIF (Generalized VIF)** and compare **`GVIF^(1/(2*Df))`** against `sqrt(5) ≈ 2.23`
or `sqrt(10) ≈ 3.16` (equivalently square that column and compare to 5 / 10).

---

**Q8.** Compare `GVIF^(1/(2*Df)) = 1.87` against `sqrt(5) ≈ 2.23`. Since `1.87 < 2.23`, it's **below**
the threshold ⇒ **not concerning** by the rule-of-5. (Note you must use the `GVIF^(1/(2Df))` column,
**not** the raw `GVIF = 12.4`, which is distorted by the number of categories.)

---

**Q9.** Fixes:
1. **Drop** one of the collinear predictors — simplest, but you lose that variable's unique info (if
   any).
2. **Combine** them into a single predictor (e.g. an index/sum) — retains information but **changes
   the interpretation** depending on how you aggregate.
In the penguins model, **`species`** had the highest VIF; **removing it fixed the other inflated
VIFs**.
