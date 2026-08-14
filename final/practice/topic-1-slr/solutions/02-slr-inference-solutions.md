# Solutions 02 (Topic 1) — Inference in Simple Linear Regression

*Questions: [`../02-slr-inference.md`](../02-slr-inference.md).*

> Marking scheme: **70% for correct procedures, 30% for correct answers.**

---

## Problem 1 — Reading an `lm` inference table

**(a)** (i) The **SE of `b̂1`** is the standard deviation of the *sampling distribution* of the slope
estimate — it measures how much `b̂1` would **wobble from sample to sample**. It exists because `b̂1` is
computed from a **random sample**, so a different sample would give a different estimate. It would be
zero only with **no sampling variability** — e.g. you observed the entire population, or the data were
perfectly deterministic.
(ii) **False.** The scatter of points around the line is governed by the **error variance `σ²`** (how
far individual `Y`s fall from the line). The SE of `b̂1` is the wobble of the *estimated coefficient*
across repeated samples — a different quantity.

**(b)** `statistic = estimate / std_error = 0.750 / 0.079 ≈` **`9.53`** — how many SEs the estimate sits
from 0. Hypotheses: `H0: b1 = 0` (no linear association between education and wage) vs. `H1: b1 ≠ 0`
(there is an association).

**(c)** (i) **Correct:** "We are **95% confident** that a one-year increase in education is associated
with an increase in wage between **\$0.596 and \$0.905/hour**" — meaning that across many samples, 95%
of intervals built this way contain the true slope. The "95% probability the true slope is in *this*
interval" phrasing is wrong because once computed, the interval is **fixed** — the true slope either is
or is not in it (probability 0 or 1); the 95% refers to the **procedure** over repeated samples.
(ii) All three agree because they come from the same estimate and SE. The CI `(0.596, 0.905)`
**excludes 0** ⇒ reject `H0`; equivalently the statistic `9.53` exceeds the critical value `≈ 1.96`
⇒ reject; equivalently `p ≈ 0 < 0.05` ⇒ reject. The boundary is at **statistic ≈ 1.96** (`p = 0.05`):
there the CI endpoint would land exactly on 0.

**(d)** (i) **Yes** — a tiny p-value is strong evidence against `H0: b1 = 0`. (ii) **No** — it says
nothing about the *size* of the slope; with a large sample even a tiny slope can have a microscopic
p-value. (iii) **No** — report it as **"< 0.001"**; a printed `0` is rounded, the true value is a tiny
positive number, never exactly 0. (iv) Evidence strength lives in the **p-value**, effect size in the
**estimate**. The `p = 1e-9` study has overwhelming evidence of a *tiny* effect; the `p = 0.03` study,
weaker evidence of a *large* effect. "Important" needs both — read both columns.

---

## Problem 2 — Sampling distributions and the bootstrap

**(a)** (i) Because `b̂1` comes from a random sample it is a **random variable**; imagining many repeated
samples, the estimates form a **sampling distribution** whose SD is the SE. With only one sample, `lm()`
uses **theory**: assuming Normal errors (or, for large `n`, the **CLT**), the standardized estimate
follows a **t-distribution with `n − k` degrees of freedom** (`n` = sample size, `k` = number of
coefficients). *(In this course the t is approximated by the standard Normal, so `z = b̂1 / SE` is
compared to `±1.96`.)*
(ii) The distribution of **`b̂1`, the estimator of the slope.** Not the distribution of `Y` (that is the
response scatter), nor of the true `b1` (a fixed unknown constant, not random), nor of `X` (treated as
fixed).

**(b)** Treat your one sample as a stand-in for the population and **resample from it with replacement**,
each resample the **same size `n`** as the original. Refit the model on each resample to get many slope
estimates; their spread approximates the sampling distribution, and its SD estimates the SE. Sampling
**without** replacement at size `n` would just reproduce the original sample every time (identical rows,
zero variability), so it must be **with replacement**.

**(c)** Fresh samples from the population illustrate the sampling distribution *pedagogically*, but that
is not bootstrapping: **bootstrapping resamples (with replacement) from your one observed sample**, not
from the population. We resort to it because in practice you only ever have that **one** sample.

**(d)** (i) Sort the 1000 bootstrap slopes and read off the **2.5th and 97.5th percentiles** — those are
the lower/upper bounds of the 95% percentile CI (2.5% of resampled slopes in each tail). (ii) Sampling
**without replacement at size `n`** just returns the **original sample every time** (all `n` rows, no
repeats — same rows reordered), so all 1000 refits give the **identical** slope: the bootstrap
distribution collapses to a **single spike** with zero spread, and the "CI" would have zero width.
