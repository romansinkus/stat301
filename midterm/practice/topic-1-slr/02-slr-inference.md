# Practice 02 — Inference in Simple Linear Regression

*Topic 1 (Inference). Solutions: [`solutions/02-slr-inference-solutions.md`](solutions/02-slr-inference-solutions.md).*

---

**Q1 [SA].** Define the **standard error** of a slope estimate `b1hat`. Explain why it exists *at
all* — what would have to be true for it to be zero?


---

**Q2 [TF].** "The standard error of `b1hat` measures how much the individual data points scatter
around the fitted line." True or false? Justify. (What *does* the point scatter correspond to,
and what does the SE correspond to?)



---

---

**Q4 [SA].** Explain **bootstrapping** to estimate the SE of a slope. Your answer must mention:
(a) resampling *with replacement*, (b) the sample size of each resample, and (c) why sampling
*without* replacement would fail.

---

**Q5 [SA].** Taking many *fresh* samples from the full population and refitting each time illustrates
the sampling distribution — but explain why this is **not** the same as bootstrapping. What exactly
does bootstrapping resample from, and why do we resort to it in practice?

---

**Q6 [SA].** From `get_regression_table()` on the wage SLR you read: `education` estimate `0.750`,
`std_error 0.079`, `statistic 9.53`, `p_value 0`, `lower_ci 0.596`, `upper_ci 0.905`. Show how the
`statistic` column is computed from the other columns, and state the hypotheses being tested.

---

**Q7 [SA].** Using the same table, give the **correct** interpretation of the 95% CI
`(0.596, 0.905)`. Then explain why "there is a 95% probability the true slope is between 0.596 and
0.905" is the *wrong* interpretation.

---

**Q8 [SA].** Explain the equivalence the in-class Activity 2 asked about: how do the **95% CI**, the
**test statistic**, and the **p-value** all tell the same story about significance at the 5% level?
What value of the statistic sits exactly at the boundary?

---

**Q9 [SA].** A slope has `p_value = 1e-12`. State what this **does** and **does not** tell you.
Address specifically: (i) is it strong evidence against `H0: b1 = 0`? (ii) does it mean the slope is
large? (iii) is it "the probability the null is true"? (iv) where do you look to judge effect size?

---

**Q10 [TF].** "Because the output shows `p.value = 0`, we should report that the p-value is exactly
zero." True or false? Justify.

---

**Q11 [SA].** A study reports a slope with `p = 0.03` and a *huge* estimate, and another reports a
slope with `p = 1e-9` and a *tiny* estimate. A journalist says the second finding is "more
important." Untangle the confusion between **evidence strength** and **effect size**.

---

**Q12 [SA].** You have 1000 bootstrap slope estimates for `TARGET_deathRate ~ povertyPercent`.
(a) Describe how to turn them into a **95% percentile confidence interval** — which values do you
read off? (b) A classmate built their 1000 resamples by sampling *without* replacement at the full
size `n`. What went wrong, and what will their bootstrap distribution look like?

**Q3 [SA].** We only ever collect **one** sample, yet we talk about a "sampling distribution" of


`b1hat`. Explain the sampling-distribution idea and how `lm()` produces an SE from a single sample
(name the distribution and its degrees of freedom).
