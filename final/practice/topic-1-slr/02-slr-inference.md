# Practice 02 (Topic 1) — Inference in Simple Linear Regression

*Topic 1 (Inference). Solutions: [`solutions/02-slr-inference-solutions.md`](solutions/02-slr-inference-solutions.md).*

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Circle
> final numeric answers and respect the word limits. A simple calculator is allowed.

---

## Problem 1 (16 pts) — Reading an `lm` inference table

For the wage data, `get_regression_table()` for `lm(wage ~ education)` reports:

```
term          estimate   std_error   statistic   p_value   lower_ci   upper_ci
(Intercept)     -0.746      0.485       -1.54       0.124     -1.698     0.206
education        0.750      0.079        9.53       0.000      0.596     0.905
```

**(a) (4 pts)** (i) Define the **standard error** of the slope estimate `b̂1`, and explain why it exists
*at all* — what would have to be true for it to be zero? (ii) "The standard error of `b̂1` measures how
much the individual data points scatter around the fitted line." True or false? Justify.

**(b) (4 pts)** Show how the `statistic` value `9.53` for `education` is computed from the other columns,
and state the two hypotheses being tested.

**(c) (4 pts)** (i) Give the **correct** interpretation of the 95% CI `(0.596, 0.905)`, and explain why
"there is a 95% probability the true slope is between 0.596 and 0.905" is the *wrong* interpretation.
(ii) Explain how the **CI**, the **statistic**, and the **p-value** all tell the same story about
significance at the 5% level, and what value of the statistic sits exactly at the boundary.

**(d) (4 pts)** A different slope (in another study) has `p_value = 1e-12`, printed by R as `0`.
(i) Is this strong evidence against `H0: b1 = 0`? (ii) Does it mean the slope is *large*? (iii) Should
you report the p-value as exactly zero? (iv) A journalist calls a `p = 1e-9`, *tiny*-estimate finding
"more important" than a `p = 0.03`, *huge*-estimate finding. In ≤ 30 words, untangle the confusion
between **evidence strength** and **effect size**.

---

## Problem 2 (16 pts) — Sampling distributions and the bootstrap

**(a) (5 pts)** We only ever collect **one** sample, yet we speak of a "sampling distribution" of `b̂1`.
(i) Explain the sampling-distribution idea and how `lm()` produces an SE from a single sample (name the
distribution and its degrees of freedom). (ii) Fill in the blank correctly and justify: "One of the
sampling distributions in SLR is the distribution of ___" — and say why it is **not** the distribution
of `Y`, of the true slope `b1`, or of `X`.

**(b) (4 pts)** Explain how to use **bootstrapping** to estimate the SE of the slope. Your answer must
mention (i) resampling *with replacement*, (ii) the size of each resample, and (iii) why sampling
*without* replacement would fail.

**(c) (3 pts)** Taking many *fresh* samples from the full population and refitting each time also
illustrates the sampling distribution — but explain in ≤ 30 words why this is **not** the same as
bootstrapping. What exactly does bootstrapping resample from, and why do we resort to it in practice?

**(d) (4 pts)** You have 1000 bootstrap slope estimates for `TARGET_deathRate ~ povertyPercent`.
(i) Describe how to turn them into a **95% percentile confidence interval** — which values do you read
off? (ii) A classmate built their 1000 resamples by sampling *without* replacement at the full size `n`.
What went wrong, and what will their bootstrap distribution look like?
