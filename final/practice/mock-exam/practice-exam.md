# Comprehensive Final Practice Exam (cumulative, Topics 1–9)

*All topics. Solutions: [`solutions/practice-exam-solutions.md`](solutions/practice-exam-solutions.md).*

> **Exam-style, cumulative.** Written short answer only — **no multiple choice**. Time yourself
> (~130 min, like the real final). **Show the key steps** — marking is **70% for correct procedure, 30%
> for the correct answer.** Circle final numeric answers, respect word limits, and use `alpha = 0.05`
> unless told otherwise. A simple calculator is allowed. **5 problems, 77 points.**

Three running datasets in this paper:
- **`homes`** — `price` (\$), `area` (m²), `waterfront` (0/1), `neighbourhood` (4-level factor). Linear.
- **`loans`** — `default` (0/1), `income` (\$1000s), `homeowner` (yes/no). Logistic.
- **`clinic`** — `visits` (a count), `age`, `chronic` (0/1). Poisson.

---

## Problem 1 (16 pts) — Linear regression on `homes`

`lm(price ~ area + waterfront + neighbourhood)` gives `area = 2450` (95% CI `(2100, 2800)`, `p ≈ 0`). The
model has `TSS = 8.0e12` and `RSS = 2.4e12`.

**(a) (4 pts)** (i) Interpret the `area` slope in one careful sentence (include the right caveat). (ii) Is
it significant, and how do the CI and p-value each show it? (iii) Give one *incorrect* causal phrasing and
say what is wrong with it.

**(b) (4 pts)** (i) Compute `ESS` and `R²`. (ii) Interpret `R²` in one sentence. (iii) Name two reasons you
would **not** use this `R²` to decide whether to add a fifth predictor.

**(c) (5 pts)** You compare `lm(price ~ area)` (reduced) to the full model with `anova(reduced, full)`,
getting `F = 12.4`, `p = 3e-06`. (i) What are `H0` and `H1` in words? (ii) What must be true of the two
models for this test to be valid? (iii) State the conclusion — and one thing this significant result does
**not** prove.

**(d) (3 pts)** In one or two sentences, explain why "**significance**," "**good prediction**," and
"**causation**" are three different things.

---

## Problem 2 (18 pts) — Logistic regression on `loans`

`glm(default ~ income, family = binomial)` gives an `income` coefficient of `−0.08`.

**(a) (4 pts)** (i) In a GLM, is there an additive error term `e` as in `Y = b0 + b1X + e`? What method
estimates a GLM's coefficients, and why is there "no closed-form formula"? (ii) On which scale is the raw
`income` coefficient?

**(b) (5 pts)** (i) A logistic model *could* report a probability directly, yet we **model the log-odds**.
Give the two reasons (think "range" and "constant effect"), and say whether we ever go back to the
probability scale. (ii) For `income = −0.08`, give the odds ratio and the percent change in the odds of
default per \$1000. (iii) Describe the two-step calculation to get a fitted **probability** for one
borrower from the raw coefficients.

**(c) (5 pts)** You also fit `glm(default ~ income + homeowner)` (additive) and
`glm(default ~ income * homeowner)` (interaction). (i) In the additive model, can you say "holding
homeownership constant, the income effect is…"? Why? (ii) In the interaction model, how do you get the
income odds ratio for **homeowners**, and why is it a *product* of exponentials? (iii) A plot of fitted
**probability** curves for owners vs. renters in the **additive** model looks non-parallel — does that
prove an interaction? Explain.

**(d) (4 pts)** (i) Can you report an `R²` for this logistic model? If not, what do you use instead — and
for two nested logistic models, which test replaces the F-test (give the statistic, its reference
distribution, and the R command)? (ii) Why is a plain residual / Q-Q plot **uninformative** for logistic
regression (name the two things that break)?

---

## Problem 3 (15 pts) — Poisson regression on `clinic`

`glm(visits ~ age + chronic, family = poisson)` gives `chronic = 0.55`. Refitting with `quasipoisson`
reports a dispersion parameter of `6.4`.

**(a) (5 pts)** For `chronic = 0.55`: (i) interpret on the log-mean scale; (ii) convert to a rate ratio
and a percent change; (iii) if a 50-year-old without a chronic condition has a predicted mean of 3 visits,
what is the predicted mean for an otherwise identical person **with** a chronic condition?

**(b) (4 pts)** (i) What does the dispersion parameter of `6.4` indicate, and does it damage the estimates
or the SEs? (ii) Why is a dispersion of **exactly 1** the reference value — what ratio does it compare?

**(c) (3 pts)** Why must you `factor()` a categorical variable stored as numbers (e.g. `neighbourhood`
coded 1–4) before fitting? What does R do if you forget?

**(d) (3 pts)** The log-mean equation is **additive**, but the rate interpretation is **multiplicative**.
Explain why the *same* model is both — what algebra turns the "+" into a "×"?

---

## Problem 4 (16 pts) — Model selection & prediction uncertainty (`homes`)

**(a) (5 pts)** You run LASSO on `homes` with many candidate predictors. (i) What does LASSO do that
stepwise selection does not (name the key mechanism)? (ii) What happens at `λ = 0`? (iii) Cross-validation
reports both `lambda.min` and `lambda.1se` — what is the difference, and why might you prefer
`lambda.1se`?

**(b) (3 pts)** What is **`k`-fold cross-validation**, and what is it used to choose in a LASSO fit?

**(c) (4 pts)** A data scientist uses forward selection on the full `homes` dataset to pick the
"significant" predictors, then reports p-values and CIs for those predictors **from the same dataset**.
(i) Name the problem and say what happens to the Type I error rate. (ii) In the course's simulation of
this, **all true coefficients were 0** — explain why obtaining small p-values *frequently* was the *bad*
outcome, and what rate you would want instead. (iii) What is the fix?

**(d) (4 pts)** For a house of size 200 m², `predict()` returns `interval = "confidence"` = `(590k, 650k)`
and `interval = "prediction"` = `(410k, 830k)`. (i) Label each interval. (ii) Write the correct
one-sentence interpretation of each (mind "confidence" vs. "probability"). (iii) A client asking about
**their own** 200 m² house should be quoted which one, and why?

---

## Problem 5 (12 pts) — The unifying picture

**(a) (5 pts)** (i) You have three responses: a house price, whether a loan defaults (0/1), and a count of
clinic visits. Name the appropriate regression model, the `glm` family (or `lm`), and the link function
for each. (ii) State the single unifying idea connecting MLR, logistic, and Poisson regression — what
changes and what stays the same?

**(b) (4 pts)** Explain the unifying idea behind the **F-test** (linear) and the **deviance test** (GLM):
what does each measure, and how is the workflow the same?

**(c) (3 pts)** (i) Give the one-line difference between a CIP and a PI, and say which is wider.
(ii) "Because a GLM has no error term `e`, it has no randomness." True or false? Explain where the
randomness lives, and how a GLM is estimated.
