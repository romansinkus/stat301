# Practice 01 (Topic 4) — The GLM Bridge & Logistic Regression

*Topic 4 (+ the GLM bridge). Solutions:
[`solutions/01-glm-bridge-and-logistic-solutions.md`](solutions/01-glm-bridge-and-logistic-solutions.md).
Course dataset: Titanic (`survived ~ fare, sex, …`).*

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Circle
> final numeric answers, and respect any word limits. A simple calculator is allowed.

---

## Problem 1 (16 pts) — The GLM bridge and the three scales

**(a) (4 pts)** Ordinary linear regression models `E[Y|X]` directly with a straight line. Explain the
**range problem** that makes this fail for (i) a binary response and (ii) a count response. Then state
the GLM "trick" in one sentence — what do we model instead of `E[Y|X]`?

**(b) (4 pts)** Fill in the table for the three GLM families taught in the course, then explain why
"ordinary linear regression is itself a GLM."

| Response type | Distribution | Link (canonical) | `glm(family = ?)` | Models... |
| --- | --- | --- | --- | --- |
| continuous | ? | identity | ? | ? |
| binary 0/1 | ? | ? | binomial | ? |
| count 0,1,2… | ? | log | ? | ? |

**(c) (4 pts)** (i) "Like the linear model `Y = b0 + b1X + e`, a logistic regression has an error term
`e` that is estimated by least squares." True or false? Correct every wrong part. (ii) Write the **three
equivalent forms** of the logistic model (probability, log-odds, odds), say which one is "the linear
one," and explain why putting the **log-odds** (not the probability) equal to `b0 + b1X` solves the range
problem.

**(d) (4 pts)** Define **odds** in terms of a probability `p`. If a passenger's probability of survival
is `p = 0.8`, what are the odds? If the odds are 0.25, what is `p`? (show the arithmetic).

---

## Problem 2 (16 pts) — Interpreting a fitted logistic model (Titanic)

`glm(survived ~ fare + sex, family = binomial)` (female = reference) gives, among others,
`b_fare = 0.0152` and `sexmale = −2.514`. Separately, `tidy(model, conf.int = TRUE,
exponentiate = TRUE)` reports for `fare` an estimate of `1.011` with CI `(1.008, 1.015)`.

**(a) (5 pts)** For `b_fare = 0.0152`: (i) interpret this raw coefficient on the **log-odds** scale;
(ii) compute `e^0.0152` and interpret it as an **odds ratio**; (iii) convert to a **percent change in the
odds** per \$1 of fare.

**(b) (4 pts)** (i) Compute and interpret `e^(−2.514) = 0.081` as an odds ratio for males vs. females
(surviving). (ii) Re-express the same fact in terms of the odds of **dying** using `e^2.514 = 12.35`.
(iii) Why are (i) and (ii) telling the same story?

**(c) (4 pts)** A fitted model gives log-odds `L = −1.694` for a male paying \$7.25. (i) Convert to a
probability using `p = e^L / (1 + e^L)`. (ii) Is this person predicted to survive under a 0.5 cutoff?
(iii) Which `predict()` `type=` argument returns `L` directly, and which returns `p`?

**(d) (3 pts)** For the `fare` row of the `tidy(exponentiate = TRUE)` output above: (i) what scale are
`1.011` and its CI on? (ii) Interpret the estimate and CI in a sentence. (iii) Is `fare` significant, and
how can you tell from this CI (what value must it exclude)?

---

## Problem 3 (15 pts) — Additive vs. interaction, diagnostics, overdispersion

**(a) (4 pts)** An **additive** model `glm(survived ~ sex + fare)` produces two logistic curves. A
classmate plots the fitted **probability** curves for males and females and says "these are not parallel,
so it must be an interaction model." Explain why they are wrong — on which scale *is* the model parallel,
and why does the probability plot look non-parallel?

**(b) (4 pts)** In an **interaction** model `glm(survived ~ sex * fare)`, the `fare` odds ratio is `e^b2`
for females (reference) and `e^(b2+b3)` for males. Explain why you **multiply** the exponentiated
coefficients (`e^(b2+b3) = e^b2 · e^b3`) to get the male odds ratio, and why you **cannot** say "holding
sex constant, the fare effect is…".

**(c) (3 pts)** Explain why a plain **residuals-vs-fitted plot is uninformative** for logistic regression
(give the two reasons), and name the diagnostic the course says to rely on **instead**.

**(d) (4 pts)** Define **overdispersion**. Does it damage the point estimates or the standard errors? How
do you **detect** it (what family, what number, what is the "fine" value), and how do you **fix** it?
Given the Titanic dispersion ≈ 0.98, is there an overdispersion problem?
