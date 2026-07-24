# Solutions 02 — Inference in Simple Linear Regression

*Questions: [`../02-slr-inference.md`](../02-slr-inference.md).*

---

**Q1.** The **SE of `b1hat`** is the standard deviation of the *sampling distribution* of the slope
estimate — it measures how much `b1hat` would **wobble from sample to sample**. It exists because
`b1hat` is computed from a **random sample**, so a different sample would give a different estimate.
It would be zero only if there were no sampling variability — e.g. you observed the entire population,
or the data were perfectly deterministic.

---

**Q2.** **False.** The scatter of points around the line is governed by the **error variance**
`sigma^2` (how far individual `Y`s fall from the line). The **SE of `b1hat`** is the wobble of the
*estimated coefficient* across repeated samples — a different quantity. (Confusingly, `geom_smooth(se
= TRUE)`'s band shows uncertainty of the fitted *line*, not the point scatter and not the coefficient
SE directly.)

---

**Q3.** Because `b1hat` comes from a random sample, it's a **random variable**; imagining many
repeated samples, the estimates form a **sampling distribution** whose SD is the SE. We only have one
sample, so `lm()` uses **theory**: assuming Normal errors (or, for large `n`, leaning on the **CLT**),
the standardized estimate follows a **t-distribution with `n − k` degrees of freedom** (`n` = sample
size, `k` = number of coefficients). That theory yields the SE, p-values, and CIs from one sample.
*(For this course/exam the t is approximated by the **standard Normal**, so the ratio is treated as a
**z-statistic**, `z = b1hat / SE`, compared to a standard Normal — hence the `|z| > 1.96` rule.)*

---

**Q4.** **Bootstrapping:** treat your one sample as a stand-in for the population and **resample from
it with replacement**, each resample the **same size `n`** as the original. Refit the model on each
resample to get many slope estimates; their spread approximates the sampling distribution, and its SD
estimates the SE. Sampling **without** replacement at size `n` would just reproduce the original
sample every time (identical rows, zero variability), so it must be **with replacement**.

---

**Q5.** Taking fresh samples from the population illustrates the sampling distribution
**pedagogically**, but it isn't bootstrapping: **bootstrapping resamples (with replacement) from your
one observed sample**, not from the population. We resort to it because in practice you only ever have
that **one** sample — you can't go back and draw new samples from the population.

---

**Q6.** `statistic = estimate / std_error = 0.750 / 0.079 ≈ 9.53` — how many SEs the estimate sits
from 0. Hypotheses: `H0: b1 = 0` (no linear association between education and wage) vs.
`H1: b1 ≠ 0` (there is an association).

---

**Q7.** **Correct:** "We are **95% confident** that a one-year increase in education is associated
with an increase in wage between **\$0.596 and \$0.905/hour**" — meaning that across many samples,
95% of intervals built this way would contain the true slope. The "95% probability the true slope is
in this specific interval" phrasing is wrong because once computed, the interval is **fixed** — the
true slope either is or isn't in it (probability 0 or 1); the 95% refers to the **procedure** over
repeated samples, not this one interval.

---

**Q8.** All three agree because they're computed from the same estimate and SE. The 95% CI
`(0.596, 0.905)` **excludes 0** ⇒ reject `H0` at 5%. Equivalently the statistic `9.53` exceeds the
critical value `≈ 1.96` ⇒ reject; equivalently `p ≈ 0 < 0.05` ⇒ reject. The boundary is at
**statistic ≈ 1.96** (and `p = 0.05`): there the CI endpoint would land exactly on 0.

---

**Q9.** (i) **Yes** — a tiny p-value is **strong evidence against `H0: b1 = 0`.** (ii) **No** — it
says nothing about the *size* of the slope; with a large sample even a *tiny* slope can have a
microscopic p-value. (iii) **No** — the p-value is **not** the probability the null is true. (iv) To
judge **effect size**, read the **`estimate`** (and its CI), not the p-value.

---

**Q10.** **False.** A printed `p.value = 0` is **rounded** — the true p-value is a tiny positive
number, never exactly 0. Report it as **"< 0.001."**

---

**Q11.** The journalist is conflating two different things. **Evidence strength** (how sure we are the
effect isn't 0) lives in the **p-value**; **effect size** (how big the effect is) lives in the
**estimate**. The `p = 1e-9` study has overwhelming evidence of a **tiny** effect; the `p = 0.03`
study has weaker evidence of a **large** effect. "Important" usually means large *and* well-supported
— you must read **both** columns; neither number alone settles it.

---

**Q12.**
(a) Sort the 1000 bootstrap slopes and read off the **2.5th and 97.5th percentiles** — those two
values are the lower and upper bounds of the **95% percentile CI** (they leave 2.5% of the resampled
slopes in each tail).
(b) Sampling **without replacement at the full size `n`** just returns the **original sample every
time** (you'd be drawing all `n` rows with no repeats — the same rows in a different order). So all
1000 refits give the **identical** slope: the bootstrap distribution collapses to a **single spike**
with zero spread, and the "CI" would have zero width. Bootstrapping *must* be **with replacement** so
that resamples differ.
