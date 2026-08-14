# STAT 301 — Final Master Study Guide (Cumulative)

*The final is **cumulative**. This guide covers the whole course:*

- **Topic 1** — Simple Linear Regression (estimation, inference, categorical predictors)
- **Topic 2** — Multiple Linear Regression & Interactions
- **Topic 3** — Diagnostics (LINE), Multicollinearity & Causality
- **Topic 4** — Logistic Regression (binary response)
- **Topic 5** — Poisson Regression (count response)
- **Topic 6** — Model Evaluation: Goodness of Fit & Nested Models (linear)
- **Topic 7** — Goodness of Fit for GLMs (deviance)
- **Topic 8** — Model Selection: Regularization & the Post-Inference Problem
- **Topic 9** — Prediction Uncertainty (CIP vs PI)

> **The one unifying idea for Topics 4–9.** Topics 1–3 built the **linear model** for a
> *continuous* response. Topics 4–5 keep the **exact same linear machinery** (a linear
> combination of coefficients, interpreted the same way, tested the same way) but wrap it in a
> **link function** so it can model *binary* and *count* responses — these are **Generalized
> Linear Models (GLMs)**. Topics 6–7 ask *"is the model any good?"* (goodness of fit). Topic 8
> asks *"which variables should be in it?"* (selection) and warns about **re-using data**.
> Topic 9 asks *"how sure are we about a prediction?"*. Everything is still **association +
> uncertainty**, extended to new response types.

## Source files used to generate this guide

- `slides/topic1_simple_linear_regression_part1.pdf`
- `slides/topic1_simple_linear_regression_part2.pdf`
- `slides/topic2_MLR_part1.pdf`
- `slides/topic2_MLR_part2.pdf`
- `slides/topic3_d1_diagnostics.pdf`
- `slides/topic3_d2_designs.pdf`
- `slides/topic4-Logistic_Regression_part1-estimation.pdf` + `part2-residuals.pdf` (Titanic data)
- `slides/topic5-Poisson_Regression.pdf` (Bikeshare data)
- `slides/topic6_d1-Goodness_of_fit.pdf` + `topic6_d2-nested_models.pdf` (protein~mRNA data)
- `slides/topic7_GoodnessOfFitGLM.pdf` (deviance)
- `slides/topic8_part1_Regularization.pdf` + `topic8_part2_PostInference.pdf` (Ames Housing)
- `slides/topic9_PredictionUncertainty.pdf` (Strathcona property tax data)
- `in-class/activity5–12.ipynb` — wage-data walkthroughs for Topics 3–8 (VIF, logistic, Poisson/CD4, F-test, stepwise, LASSO)
- `notes/master.md` (the running personal notes for Topics 1–9, incl. open questions resolved below)
- `worksheets/worksheet_01.ipynb` (SLR estimation, inference & bootstrapping — cancer data)
- `worksheets/worksheet_02.ipynb` (categorical inputs, additive MLR & interactions — cancer data)
- `worksheets/worksheet_03.ipynb` — model assumptions & causality, explored by **simulation** (known true params)
- `worksheets/worksheet_04.ipynb` — **logistic** regression (binary responses)
- `worksheets/worksheet_05.ipynb` — **Poisson** regression (horseshoe `crabs`: `n_males` count)
- `worksheets/worksheet_06.ipynb` — goodness of fit & nested models (**protein~mRNA** Nature case study)
- `worksheets/worksheet_07.ipynb` — goodness of fit beyond MLR: **deviance** for a logistic model (Wisconsin breast-cancer data)
- `worksheets/worksheet_08.ipynb` — **regularization (LASSO/ridge) & post-inference** via two simulations
- `tutorials/tutorial_01.ipynb` — generative modelling, EDA, SLR estimation/inference/bootstrap (CASchools data)
- `tutorials/tutorial_02.ipynb` — MLR with categorical inputs & interactions (CASchools: `read ~ income * grades`)
- `tutorials/tutorial_04.ipynb` — **logistic** regression (`Default` credit-card data; odds ratios)
- `tutorials/tutorial_05.ipynb` — **Poisson** regression (`galapagos` plant-species counts)
- `tutorials/tutorial_06.ipynb` — goodness of fit & nested models (**protein~mRNA**, models 1–5)
- `tutorials/tutorial_07.ipynb` — **stepwise selection in MLR** (`regsubsets`/`stepAIC`, test RMSE — Ames housing + used cars)
- `in-class/activity1.ipynb` + `STAT301_activity1.pdf` — SLR estimation & correlation (wage data, Jul 7)
- `in-class/activity2.ipynb` + `STAT301_activity2.pdf` — SLR inference: significance, CI, z/p (wage data, Jul 9)
- `in-class/activity3.ipynb` + `STAT301_activity3.pdf` — additive MLR, `factor()` dummies & **ANOVA** (wage data, Jul 14)
- `in-class/activity4.ipynb` + `STAT301_activity4.pdf` — interactions & LINE diagnostics + `log()` fix (wage data, Jul 16)
- `midterm/review-slides.pdf` — the **Jul 21 review deck** (recaps the whole course as one MLR framework)
- `slides/final-review.pdf` — the **final review deck** (post-midterm recap + confirmed final logistics)
- `midterm/mt-info.md` — official midterm exam logistics

*(Tutorial 03's confounding simulation is referenced in the Causality section, as summarized from the Topic 3 designs deck. The four in-class activities all use the **`wage.txt`** dataset — `wage ~ education`, later adding `sex` and `occupation` — and are walked through in their own section below.)*

> **How to read this guide.** Math is written in plain text / code style (e.g. `Y = b0 + b1*X + e`)
> so it's readable anywhere. The big idea of this whole course: **regression models the *average*
> of a response, and we interpret what the coefficients *mean* — association, not causation.**

---

# EXAM LOGISTICS & WHAT'S TESTED

> **Confirmed from the final review deck (`slides/final-review.pdf`).** The final is **cumulative —
> it covers all term material (Topics 1–9)**, but with **more weight on the post-midterm material**
> (logistic, Poisson, diagnostics/evaluation, variable selection, post-inference, prediction
> uncertainty). The review deck itself **only covers the post-midterm topics** — you are expected to
> **review the pre-midterm material (Topics 1–3) on your own**. **What's new to interpret vs. the
> midterm:** **`glm` output** (logistic & Poisson), **deviance / AIC / BIC**, **`R²` / adjusted `R²` /
> RSE / MSE and `anova` F-tests**, the **χ² deviance test**, **LASSO paths & cross-validation**, and
> **prediction vs confidence intervals** — see Topics 4–9 below.

**When/where (FINAL — confirmed):** **Wednesday, August 19, 2026, 3:30–5:40pm (130 minutes)**, in
person, **Life Building 2302**. Hard copies are distributed; you then have up to **20 minutes
(5:40–6:00pm)** to upload your solutions as a **single PDF** to the Canvas **"Assignment"** section
("**Final Exam Solutions upload here**" link). You may either **write on the exam paper and scan it**,
or **write on your laptop and upload**. **Picture ID will be checked.** You may access Canvas/Internet
**only at the end**, for uploading.

**Format — read this carefully:**

- **Written answers only. There are NO multiple-choice questions.** You explain, interpret, and show
  reasoning in words.
- The exam tests **understanding of the basics + critical thinking**, *not* tedious computation or
  heavy math. Expect: **interpret an R output**, say **what a model component means**, and **explain a
  concept in the context of the given dataset.**
- **R code is NOT directly tested**, but you **must understand the R *outputs*** shown in class (e.g. a
  `get_regression_table()` / `lm` / `glm` summary, an ANOVA / deviance table, `glance()` metrics, VIF
  values, residual & Q-Q plots, a LASSO path / CV plot).
- **Some simple calculations** — **bring a simple calculator.**
- **Marking philosophy (standing course style):** show your **procedure / key steps** and **write
  word-answers clearly** — reasoning is where most marks live.
- **Closed book/notes**, but you may bring **TWO letter-size sheets (both sides, written or typed)** —
  *note this is **two** sheets for the final, vs. one for the midterm.*

**Framing tip from the review decks:** everything is **one Multiple Linear Regression framework** —
*SLR is the special case `p = 1`* — and, more broadly, linear/logistic/Poisson are all **one GLM**
`g(E[Y]) = b0 + b1*X1 + ... + bp*Xp` (the link `g` changes with the response type). Master the general
interpretation and the special cases fall out of it.

> **Two-sheet cheat-sheet candidates** (you get **two** pages for the final). *Post-midterm (weight
> them heavily):* the **GLM coefficient table** (log-odds/odds/rate-ratio, the 3 scales), the
> **overdispersion** check (`quasi*`, η vs. 1), **deviance / χ² test** vs. **F-test**,
> **R²/adjR²/RSE/MSE** definitions, **LASSO** (λ, CV, bias → post-LASSO), the **double-dipping** fix
> (split the data), and **CIP vs PI**. *Pre-midterm:* the coefficient-interpretation table, LINE
> assumptions + fixes + consequences, the interaction 4-coefficient table, VIF/GVIF thresholds, and
> the CI ⇔ test ⇔ p-value equivalence. See the [Master Cheat Sheet](#master-cheat-sheet) and
> [`blocks-ai.md`](blocks-ai.md).

---

# TABLE OF CONTENTS

0. [Exam Logistics &amp; What&#39;s Tested](#exam-logistics--whats-tested)
1. [The Big Picture](#the-big-picture)
2. [Topic 1 — Simple Linear Regression (SLR)](#topic-1--simple-linear-regression-slr)
3. [Topic 1 — Inference in SLR](#topic-1--inference-in-slr)
4. [Topic 1 — Categorical Predictors (the bridge to MLR)](#topic-1--categorical-predictors)
5. [Topic 2 — Multiple Linear Regression (MLR)](#topic-2--multiple-linear-regression-mlr)
6. [Topic 2 — Interactions](#topic-2--interactions)
7. [Topic 3 — Assumptions &amp; Diagnostics (LINE)](#topic-3--assumptions--diagnostics-line)
8. [Topic 3 — Multicollinearity](#topic-3--multicollinearity)
9. [Topic 3 — Causality &amp; Study Designs](#topic-3--causality--study-designs)
9b. [The GLM Bridge — Topics 4 &amp; 5 in one picture](#the-glm-bridge)
10. [Topic 4 — Logistic Regression (binary response)](#topic-4--logistic-regression)
11. [Topic 5 — Poisson Regression (count response)](#topic-5--poisson-regression)
12. [Topic 6 — Goodness of Fit &amp; Nested Models (linear)](#topic-6--goodness-of-fit)
13. [Topic 7 — Goodness of Fit for GLMs (deviance)](#topic-7--goodness-of-fit-for-glms)
14. [Topic 8 — Model Selection: Regularization &amp; Post-Inference](#topic-8--model-selection)
15. [Topic 9 — Prediction Uncertainty (CIP vs PI)](#topic-9--prediction-uncertainty)
16. [Worksheet Practice — R Code &amp; Extra Nuggets](#worksheet-practice--r-code--extra-nuggets)
17. [In-Class Activities — Wage Dataset Walkthrough](#in-class-activities--wage-dataset-walkthrough)
18. [Tutorials — CASchools Walkthrough](#tutorials--caschools-walkthrough)
19. [Master Cheat Sheet](#master-cheat-sheet)

---

# THE BIG PICTURE

STAT 201 was mostly about **one number** (the mean of a population, a single proportion).
STAT 301 is about **relationships between variables**: how does `Y` change as `X` changes?

Two kinds of relationships:

| Type                    | Meaning                                    | Example                                   | Uncertainty?                       |
| ----------------------- | ------------------------------------------ | ----------------------------------------- | ---------------------------------- |
| **Deterministic** | one variable*completely* fixes the other | `E = m*c^2`, circle area `A = pi*r^2` | **None**                     |
| **Stochastic**    | a*tendency*, with scatter around it      | taller people*tend* to weigh more       | **Yes** — this is our world |

**Analogy:** A deterministic relationship is a vending machine — press B4, always get the same chips.
A stochastic relationship is a coffee shop — order a "medium," and you get *roughly* the same amount
each time, but never to the exact milliliter. Statistics lives in the coffee-shop world.

Because there's uncertainty, every stochastic model carries a **random error term** `e` (epsilon):

```
Weight = b0 + b1*Height + e
```

Two people of the same height can have different weights — the `e` soaks up everything height doesn't explain.

**Terminology (memorize):**

- **Y** = response = *output* = dependent variable *(avoid saying "dependent")*
- **X** = predictor = *feature* = *input* = *covariate* = *regressor* = *explanatory variable*
  *(avoid saying "independent")*

Course's running datasets: **Palmer Penguins** (flipper length vs body mass), **CASchools**
(district `read` vs `income`), **US cancer data**, and a **house-prices** dataset.

**Generative modelling (the tutorials' framing).** The course frames regression as **generative
modelling**: we assume the data were *generated* by some underlying (stochastic) mechanism, and the
linear regression is our **approximation of that data-generating process.** The `b`'s are the unknown
true parameters of that mechanism; estimation recovers them, inference quantifies our uncertainty
about them, and **diagnostics check whether our assumed mechanism is plausible.** (Worksheet 03 leans
hard on this: it *simulates* data from a known mechanism so the true `b`'s are known, then shows what
breaks when an assumption is violated.)

---

# TOPIC 1 — SIMPLE LINEAR REGRESSION (SLR)

**"Simple"** = exactly **one** predictor.

## The model

```
Y_i = b0 + b1*X_i + e_i
```

for each observation `i` (e.g. each of the 344 penguins).

### The three components

```
Y_i =   b0    +   b1 * X_i   +   e_i
      intercept    slope         error
```

- **Intercept `b0`** — the value of `Y` when `X = 0` (where the line crosses the y-axis).
  Often not interesting on its own (e.g. a penguin with 0 mm flippers is nonsense).
- **Slope `b1`** — how much `Y` is expected to change for a **1-unit increase in `X`**.
  This is usually the star of the show.
- **Error `e`** — everything the model does NOT capture (other variables + pure noise).

**Slope analogy:** the slope is the "exchange rate." `b1 = 50` for `body_mass ~ flipper_length`
means "each extra 1 mm of flipper *buys* about 50 g of body mass, on average."

### The model IS a conditional average

The single most important conceptual line in Topic 1:

```
E[Y | X] = b0 + b1*X
```

The regression line gives the **mean of Y for a given value of X**. It does **not** predict any single
individual exactly — it predicts the *average* of everyone at that X.

- `E[Y|X] = b0 + b1*X` → the **line** (the average, smooth).
- `Y_i = b0 + b1*X_i + e_i` → a **specific point** (off the line by `e_i`).

**Analogy:** For all 1.63 m tall people, the line says the *average* weight is 62.2 kg. Individuals
scatter above and below — the line is the "center of the cloud" at each height, like the middle of a
swarm of bees moving up a hill.

## Fitting = Least Squares

We don't know the true `b0`, `b1`; we **estimate** them from a sample. R's `lm()` uses
**Least Squares (LS)**: pick the line that **minimizes the Sum of Squared Residuals (SSR)**:

```
minimize  SUM (observed_Y - predicted_Y)^2
```

**Why squared?** Squaring (1) makes all errors positive so they don't cancel, and (2) punishes big
misses much more than small ones. **Analogy:** it's like choosing the fairest meeting spot for a group —
you pick the point that keeps everyone's *squared* walking distance as small as possible, so no one
person is left absurdly far away.

```r
penguins_lm <- lm(body_mass_g ~ flipper_length_mm, data = penguins)
```

## Residuals vs. Errors — a classic exam trap

|                      | Symbol            | Lives in                       | Known?                         |
| -------------------- | ----------------- | ------------------------------ | ------------------------------ |
| **Error term** | `e_i` (epsilon) | the*population* / true model | Unknown, unknowable            |
| **Residual**   | `e_i` hat       | the*sample* / fitted model   | Computed:`observed - fitted` |

```
Population:  Y_i = b0 + b1*X + e_i          (true b's)
Sample:      Y_i = b0hat + b1hat*X + resid  (estimated b's)
```

The residual is our **observable stand-in** for the invisible error. They differ because our estimated
`b0hat, b1hat` are not exactly the true `b0, b1`. **Analogy:** the error is the real bullseye you can't
see; the residual is how far your dart landed from where *you aimed* — close, but not the same thing.

## Interpreting the coefficients

- **Slope:** "A 1-unit increase in `X` is **associated with** an expected change of `b1` units in `Y`."
- **Intercept:** "The average `Y` when `X = 0` is `b0`." (Often not meaningful.)

### ASSOCIATION IS NOT CAUSATION

This is drilled repeatedly. A good model shows `X` and `Y` **move together** — it does **not** prove
`X` *causes* `Y`. Causation needs more than a good fit (see [Topic 3 designs](#topic-3--causality--study-designs)).

**Analogy:** ice-cream sales and drowning deaths rise together (both caused by summer heat). Great
correlation, zero causation.

## Regression vs. Correlation analysis

|           | Correlation analysis               | Linear Regression                   |
| --------- | ---------------------------------- | ----------------------------------- |
| Goal      | strength of linear association     | model the conditional average `E[Y  |
| Roles     | symmetric — no response/predictor | asymmetric — one Y, one X          |
| Variables | both random/stochastic             | X treated as fixed (non-stochastic) |

> **What's fixed vs. random (from the review deck).** In a linear regression model the **predictors
> `X_j` AND the parameters `b_j` are treated as fixed** (not random); only the **response `Y` and the
> error `e` are random**. That's the frequentist view we use here — the parameters have one true
> (unknown) value we estimate. *(The review notes this would differ in a Bayesian framework, where the
> parameters themselves are treated as random — out of scope, but a nice critical-thinking contrast.)*

## The range problem & "all models are wrong"

- A line may fit well **only within the range of the observed data.** Extrapolating beyond it is risky —
  the relationship could bend. Don't predict a penguin's mass from a 500 mm flipper you never observed.
- **George Box:** *"Essentially, all models are wrong, but some are useful."* Every model here is an
  **approximation** of reality, chosen because it's helpful, not because it's true.

---

# TOPIC 1 — INFERENCE IN SLR

Point estimates (`b0hat`, `b1hat`) are one guess from one sample. **Inference** asks: what can we say
about the **true population** coefficients, given that a different sample would give different estimates?

## The key mental model: sampling distribution

Because `b0hat`, `b1hat` are computed from a **random sample**, they are **random variables**. Take a new
sample → get slightly different estimates. Repeat many times → the estimates form a **sampling
distribution**.

The house-price demo made this concrete: sampling 1000 houses repeatedly gave slopes of 2.618, 3.017,
2.448, … — all different, all estimating the same true slope.

- **Standard Error (SE)** = the standard deviation of that sampling distribution. It measures
  **sample-to-sample wobble** of the estimate.
- **SE is NOT the scatter of points around the line.** It's the wobble of the *estimated coefficient*.
  (So the shaded band from `geom_smooth(se=TRUE)` shows uncertainty of the *fitted line*, not the SE of
  the coefficients.)

**But we only have ONE sample.** How do we get the SE? Two routes:

### Route 1 — Theoretical (what `lm()` does)

**#--here--------------------------------------**

Assuming the errors are Normal (or, thanks to the **CLT**, when the sample is large and errors are
"nice enough"), the standardized estimate follows a **t-distribution with `n - k` degrees of freedom**
(`n` = sample size, `k` = number of coefficients). `lm()` uses this to produce SEs, p-values, and CIs.

> **Course/exam simplification — use the standard Normal (z).** The **review deck** states that a
> *t-distribution can be approximated by a Normal distribution*, so **for simplicity this course just
> uses the standard Normal** for regression inference. That's why the in-class activities call the
> ratio a **z-statistic**: `z = b_hat / SE(b_hat)`, compared to a **standard Normal**. Rule of thumb
> you can quote: **|z| > 1.96 ⇒ significant at 5%** (equivalently the 95% CI excludes 0, equivalently
> p < 0.05). The `t` vs. `z` distinction won't be the point — the *interpretation* is.

### Route 2 — Bootstrapping (like STAT 201)

Treat your one sample as a stand-in for the population, then **resample from it *with replacement*** many
times (e.g. 10 000). Each resample gives an estimate; the spread of those 10 000 estimates
**approximates the sampling distribution empirically.**

- **Analogy:** *"pull yourself up by your own bootstraps."* You have no external population, so you
  manufacture many pseudo-samples from the sample you already have.
- **"Population is to the sample as the sample is to the bootstrap sample."**
- Must sample **with replacement** and at the **same size `n`** — otherwise every resample is identical.
- NOT the same as taking fresh samples from the population (you almost never can in practice).
- **When/why use it (per the review deck):** bootstrap is especially useful for **non-Normal data or
  small sample sizes**, and is often used to compute **more reliable standard errors** without leaning
  on the Normal-errors assumption.

## The `tidy()` table — read every column

```r
broom::tidy(penguins_lm, conf.int = TRUE, conf.level = 0.95)
```

| Column                   | Meaning                                                            |
| ------------------------ | ------------------------------------------------------------------ |
| `term`                 | the coefficient's name (e.g.`flipper_length_mm`)                 |
| `estimate`             | `b hat` — the point estimate (**effect size lives here**) |
| `std.error`            | SE of that estimate (sample-to-sample wobble)                      |
| `statistic`            | `T = (b hat - 0) / SE` — how many SEs the estimate sits from 0  |
| `p.value`              | probability,**if true coef = 0**, of seeing a `              |
| `conf.low / conf.high` | the confidence interval                                            |

> **In-class equivalent — `moderndive::get_regression_table()`.** Every in-class activity reads the
> coefficient table with `get_regression_table(model)` instead of `broom::tidy()`. It returns the **same
> information** with friendlier column names — `term`, `estimate`, `std_error`, `statistic`, `p_value`,
> `lower_ci`, `upper_ci` — and includes a 95% CI **by default** (no `conf.int = TRUE` needed). Read it the
> exact same way. (**Activity 1** used it to read the SLR slope; **Activity 2** to read the CI and p-value.)

## Hypothesis test for a coefficient

We test whether `X` is linearly associated with `Y`:

```
H0: b1 = 0     (no linear association — flat)
H1: b1 != 0    (there is an association)
```

Test statistic:  `T = (b1hat - 0) / SE(b1hat)`, compared to a `t` with `n - k` df.
Reject `H0` if **p-value < alpha**.

### What the p-value does and does NOT tell you

- **Small p-value = strong evidence against `H0`.** p = 0.049 is weak; p = 1e-9 is overwhelming — the
  *magnitude* measures **strength of evidence**.
- It does **NOT** tell you the **size** of the effect. A tiny slope can have a microscopic p-value with
  enough data. **Effect size = `estimate`; evidence strength = `p.value`. Read both together.**
- p-value is **not** the probability the coefficient is 0.
- "p.value = 0" in output is really *rounded* — report as "< 0.001."
- Note the **"crisis of p-values"** (ASA statement): don't worship the 0.05 cutoff.

### Statistical vs. practical significance (Tutorial 02 — likely exam material)

A distinction the tutorials draw explicitly, and exactly the "critical thinking" the exam wants:

- **Statistically significant** = we have enough evidence (small p-value) that the association is
  **not zero / not just chance** — the coefficient is reliably different from 0 across samples. It says
  nothing about *how big* the effect is.
- **Practically significant** = the **magnitude** of the effect is large enough to **matter in the real
  world.**

With a big sample, a **tiny, practically meaningless** effect can be **highly statistically
significant.** So always pair the two: *is it real?* (p-value / CI excludes 0) **and** *is it big
enough to care about?* (the `estimate`). Reporting significance without magnitude — or vice versa —
is the classic mistake.

## Confidence Intervals

Classical CI: `b hat ± t*(alpha/2, n-k) * SE(b hat)` — or get it via bootstrap percentiles.

**Correct interpretation** (heavily emphasized):

> A 95% CI is **NOT** "the true value is in this range with 95% probability." Once computed, the interval
> is fixed — it either contains the true value or it doesn't. Rather: **across many samples, 95% of the
> intervals so constructed would contain the true coefficient.** We are "95% *confident*."

Example (penguins): "With 95% confidence, body mass increases between **47.12 and 53.18 g** for every 1 mm
increase in flipper length."

---

# TOPIC 1 — CATEGORICAL PREDICTORS

*(the pivot from SLR into MLR — this is where the whole "dummy variable" machinery starts)*

**Problem:** How do you put a category (`sex` = male/female) into an equation? Categories aren't numbers,
and you can't have `sex = 0.5`.

**Solution — the dummy variable trick.** `lm()` invents a 0/1 numeric variable for you (if the column is
a **factor**):

```
sex_i = 1  if penguin i is male
sex_i = 0  if penguin i is female
```

For a variable with **2 levels, you need only 1 dummy variable.** General rule:

> **# of dummy variables = (# of levels) − 1**

The **left-out** level (coded 0) is the **reference / baseline level.** By default R picks the level that
comes **first alphabetically** (so `female` before `male`). You can change it with `relevel()`.

### Why this is really just "comparing two means"

```
body_mass = b0 + b1*sexmale + e
```

Split by group:

```
Female (sexmale = 0):  body_mass = b0 + e         → mean = b0
Male   (sexmale = 1):  body_mass = b0 + b1 + e    → mean = b0 + b1
```

So:

- **`b0`** = mean body mass of the **reference** group (female).
- **`b1`** = the **difference** in means (male minus female).
- **`b0 + b1`** = mean of the other group (male).

Testing `H0: b1 = 0` is **exactly a two-sample t-test** of equal means! The penguin example confirmed it:
`lm` gave `sexmale = 683.41` and the `t.test()` gave the identical estimate and statistic (8.54).

Here `b0`, `b1` are **not** an intercept and slope in the geometric sense (there's no line) — R just
labels them that way. They're a **baseline mean** and a **difference of means**.

---

# TOPIC 2 — MULTIPLE LINEAR REGRESSION (MLR)

**MLR = a linear regression with MANY predictors**, of any type (continuous and/or categorical),
and possibly interactions.

```
Y = b0 + b1*X1 + b2*X2 + ... + e
```

> **Multiple** Linear Regression ≠ **Multivariate** Linear Regression. Multivariate = *many response*
> variables (out of scope). We always have **one** continuous response `Y`.

Response `Y` is **always continuous**; predictors can be **discrete or continuous**.

## 1. Categorical variable with MORE than 2 levels

Need **(levels − 1)** dummies. For `state` with 3 levels (Indiana, Kansas, Washington), Indiana = reference:

```
Y = b0 + b1*stateWashington + b2*stateKansas + e
```

- `b0` = mean response for the **reference** (Indiana).
- `b1` = difference (Washington − Indiana).
- `b2` = difference (Kansas − Indiana).

Each non-reference coefficient is a **comparison against the baseline**, never a group's absolute mean.

> **`factor()` on the fly.** If a categorical column is stored as numbers (like `occupation` = 1..6 in the
> wage data), wrap it so R treats it as categories, not a continuous number: `lm(wage ~ factor(occupation))`.
> Without `factor()`, R would fit a single slope on the *codes*, which is meaningless. (**Activity 3C**.)

### ANOVA — one overall test for a categorical predictor

A k-level categorical predictor produces **k − 1 coefficients**, each with its own t-test against the
baseline. But those individual tests don't answer the natural question: **"does this categorical variable
matter *at all*?"** (i.e. are the group means all equal, or is at least one different?)

**ANOVA (`anova(model)`) gives a single joint F-test** for that:

```
H0: all group means are equal   (every non-reference coefficient = 0 simultaneously)
H1: at least one group mean differs
```

```r
wage_model <- lm(wage ~ factor(occupation), data = wage_data)
anova(wage_model)     # one F-test for the WHOLE occupation variable
```

- A **small p-value** ⇒ reject `H0` ⇒ **at least one occupation's mean wage differs** from the others.
  (**Activity 3C**: `p ≈ 4.12e-21`, so wages differ significantly across occupations — though ANOVA alone
  doesn't say *which* pairs differ; the coefficient table does that.)
- **Why not just read the k − 1 t-tests?** Doing many separate tests inflates the false-positive rate;
  the single F-test bundles them into **one** honest test of "does this variable belong in the model?"
- ANOVA also tests a whole **interaction** at once — `anova()` on `wage ~ education*factor(occupation)`
  gives one p-value for all the `education:occupation` slope-difference terms together (**Activity 4B**).

## 2. Additive models (mixing variable types)

"Additive" = predictors are just **added**; each predictor's effect is assumed to **not depend on the
others.** Example — one categorical (`state`) + one continuous (`povertyPercent`):

```
Y = b0 + b1*stateWashington + b2*povertyPercent + e
```

This is secretly **two parallel lines** (one per state):

```
Indiana    (dummy=0):  Y = b0        + b2*poverty      → intercept b0,      slope b2
Washington (dummy=1):  Y = (b0+b1)   + b2*poverty      → intercept b0+b1,   slope b2
```

**Interpretation:**

- `b0` = intercept of the **reference** line.
- `b1` = **difference between the intercepts** of the two lines (a vertical shift).
- `b2` = the **COMMON slope** shared by both lines.

> **Key feature of additive models: PARALLEL lines (same slope).** 3 coefficients describe 2 lines,
> *because we forced them to share a slope.*

**Additive assumption in words:** "the expected change in `Y` per unit change in one predictor is the
same regardless of the values of the other predictors." Examples:

- calories burned per extra hour of exercise is the same for athletes of any age;
- price increase per extra square foot is the same regardless of location.

**Interpreting additive coefficients:** interpret each one "**holding all other variables constant**" —
and because the model is additive, **it doesn't matter at which value you hold them.** That's what makes
additive models easy, which is why they're popular in practice even when the assumption is unrealistic.

---

# TOPIC 2 — INTERACTIONS

**Motivation:** What if the slope itself **changes across groups**? (e.g. poverty affects mortality
*more steeply* in one state than another.) Parallel lines can't capture that. We add an **interaction
term.**

```
Y = b0 + b1*stateWashington + b2*povertyPercent + b3*(stateWashington * povertyPercent) + e
```

### Two lines, now with DIFFERENT slopes

```
Indiana (reference, dummy=0):
   Y = b0 + b2*poverty                          → intercept b0,      slope b2

Washington (dummy=1):
   Y = (b0+b1) + (b2+b3)*poverty                → intercept b0+b1,   slope b2+b3
```

### Interpreting all four coefficients (memorize this table)

| Coef   | Meaning                                                                                  |
| ------ | ---------------------------------------------------------------------------------------- |
| `b0` | intercept of the**reference** line                                                 |
| `b1` | **difference in intercepts** (other group − reference)                            |
| `b2` | **slope of the reference line**                                                    |
| `b3` | **difference in slopes** (other group − reference) — *this is the interaction* |

So the other group's **actual slope = `b2 + b3`** (you must add them). `b3` alone is a *slope gap*, not a slope.

### Counting coefficients

- 2-level categorical × continuous interaction → adds **1** coefficient (1 × 1).
- The full interaction model above has **4 coefficients for 2 lines** (vs. 3 for the additive/parallel version).
- General rule: interaction coefficients = (coefs from A) × (coefs from B). A 3-level categorical ×
  continuous → 2 interaction coefficients.

### How to read slopes off the `tidy()` table

For `Y ~ income * sex` (female = reference):

| Group             | Intercept to plot | Slope to plot                                            |
| ----------------- | ----------------- | -------------------------------------------------------- |
| Female (baseline) | `b0`            | `b2` = the `income` row **directly**           |
| Male              | `b0 + b1`       | `b2 + b3` = `income` row **+** interaction row |

The main-effect continuous coefficient (`b2`, the `income` row) is **only the reference group's
slope** — a very common mistake is to read it as "the" slope for everyone.

### Testing the interaction

The interaction row tests `H0: b3 = 0` — i.e. "the two groups have the **same slope**" (the association
is the same across groups). In the cancer example `b3` had p = 0.306 > 0.05, so there was **not enough
evidence** that the slopes differ; the parallel (additive) model would suffice.

### Interpretation caveat for interaction models

In additive models you interpret each coefficient "holding others constant, at any value." In
**interaction models you CANNOT** — the effect of one variable **depends on the value of the other.**
Saying "holding all else constant" is the common mistake flagged in lecture.

### Visual summary

- **Additive, 1 continuous + 1 categorical → parallel lines.**
- **Interaction, 1 continuous + 1 categorical → non-parallel lines.**
- **Additive with multiple continuous → a hyperplane.**

### Interaction model = "two SLRs in one"

Fitting the interaction model on the full data gives the *same* two lines you'd get by fitting a separate
SLR to each group. That's why the reference group's slope (`b2`) matches the reference-only SLR exactly,
and why the other group's slope is `b2 + b3`.

---

# TOPIC 3 — ASSUMPTIONS & DIAGNOSTICS (LINE)

Every inference (SE, CI, p-value) rests on **assumptions**. They may not hold — we must **check** them.
Remember them with **L-I-N-E**:

| Letter      | Assumption               | Meaning                                                          |
| ----------- | ------------------------ | ---------------------------------------------------------------- |
| **L** | **Linear**         | `E[Y                                                             |
| **I** | **Independent**    | the errors are independent of each other                         |
| **N** | **Normal**         | the conditional distribution of the errors is Normal             |
| **E** | **Equal variance** | all errors share the same variance`sigma^2` (homoscedasticity) |

The workhorse diagnostic is the **residuals-vs-fitted plot.** Residuals hold everything the model missed,
so patterns in them reveal problems.

> **Whose job is it? Yours. (Worksheet 03.)** `lm()` *assumes* either Normal errors or that the CLT
> applies, and then reports SEs/p-values as if the sampling distribution is `t`-Student (≈ Normal). It
> **does not check** the assumptions for you — **it is your job to check them** with diagnostic plots.
> As ISL puts it, *"identifying and overcoming these problems is as much an art as a science"* — and
> the review deck adds that judging some assumptions (especially independence) often needs **domain
> knowledge / a domain expert**, not just a plot.

## L — Linearity

- **Diagnose:** plot **residuals vs fitted values.** If the model is right, residuals should look like a
  **structureless cloud around 0.** A curve/wave = non-linearity (a straight line through an S-shaped
  cloud is a "very dubious model").
- **Fix:** add **transformations** of predictors (`X^2`, `log(X)`, `sqrt(X)`) or interaction terms. Adding
  a quadratic term flattened the CASchools residual pattern.
- **"Linear" is about being linear in the *parameters*, not a straight line.** `read = b0 + b1*income + b2*income^2` is still a *linear regression* — `X^2` is just another covariate. LS works identically;
  only the **interpretation** changes.

## I — Independence

- **When violated:** **temporal data** (measurements over time) and **repeated measurements of the same
  subject** — adjacent errors get correlated.
- **Diagnose:** a residual plot may show runs/trends; formal tests exist (Durbin-Watson) but are out of
  scope. Often you assess it from the **study design** (e.g. different districts' scores are safely
  independent).
- **Consequence:** the **SEs of the estimates become biased**, so **CIs and hypothesis tests are invalid.**
- **Fix:** methods for correlated data (time series, longitudinal analysis) — beyond this course.

## E — Equal variance (homoscedasticity)

- **Assumption:** `Var(e_i) = sigma^2` for all `i` (no subscript `i`). Violation = **heteroscedasticity.**
- **Diagnose:** residuals-vs-fitted plot — a **funnel/fan shape** (spread grows or shrinks with fitted
  value) signals trouble. You want **constant vertical spread** across the plot.
- **Consequence:** SEs are wrong → **CIs and p-values invalid.**
- **Fix:** **variance-stabilizing transformation** of the response (`sqrt(Y)`, `log(Y)`), or
  **Weighted Least Squares** (out of scope).

## N — Normality

- **Least severe** violation of the four.
- **Why it's forgiving:** with a **large sample the CLT** gives approximately-valid inference even if
  errors aren't Normal; **bootstrapping** also rescues you.
- **Why we'd want it:** if errors *are* Normal, it can be proven the conditional mean is linear (nice
  theory), and it justifies exact `t`-based inference in small samples.
- **Diagnose:** **Q-Q plot** of residuals (points on the diagonal = Normal) and **histograms.**
  `plot(model, 2)` gives the Q-Q plot.
- **Fix:** variable transformations; or rely on CLT / bootstrap.

**Summary of consequences:** violating **I** or **E** breaks your **SEs → invalid CIs and p-values**;
violating **L** makes the whole model dubious; violating **N** is usually survivable via CLT/bootstrap.

---

# TOPIC 3 — MULTICOLLINEARITY

**Definition:** two or more **predictors are strongly associated** with each other, so they carry
overlapping information and the model **can't isolate their individual effects.**

**Drastic example:** put both `income` (in \$1000s) and `incomeUSD = income*1000` in a model — they're the
*same variable* rescaled. R returns `NA` for one coefficient because **infinitely many coefficient
combinations give the exact same SSR** (you can shuffle "weight" from one to the other freely). R literally
can't choose.

**Analogy:** two employees who always work identical shifts and always do identical work. Payroll can see
the *team* produced the output, but can't tell **who** did what. Their individual "contributions" are
unidentifiable.

## Consequences

- **Inflates the standard errors** of estimates → **CIs too wide**, harder to reject `H0` for coefficients.
- In practice you rarely get *perfect* collinearity, just strong collinearity.
- It need **not** be between just two variables — one predictor can be collinear with a *combination* of
  several others. (Think of it as regressing one covariate on all the others and getting a great fit.)

## Diagnosis

- **Pairwise correlations** between predictors — helpful, but **not enough** (misses multi-variable
  collinearity).
- **VIF (Variance Inflation Factor)** — measures how much a coefficient's SE inflates when fit *with* the
  other variables vs. *alone.* Guideline: **VIF > 5 (or 10) is concerning** (just a guideline).
- **GVIF (Generalized VIF)** — preferred when categorical predictors are present (raw VIF is distorted by
  number of categories). Compare **`GVIF^(1/(2*Df))`** against `sqrt(5)` ≈ 2.23 or `sqrt(10)` ≈ 3.16
  (equivalently, square that column and compare to 5/10).

## Fixes

- **Drop** one of the collinear variables (simplest). In the penguins model, `species` had the highest
  VIF; removing it fixed the other inflated VIFs.
- **Combine** the collinear variables into one (may change interpretation depending on how you aggregate).

## The full workflow in practice (Tutorial 03 — CASchools)

The tutorial runs the whole detect-and-fix loop; it's a great exam template:

1. **Visualize** predictor correlations — `GGally::ggpairs()` and/or a **correlation heatmap**
   (`geom_tile()` over a melted `cor()` matrix). Flag pairs with `|r| > 0.6`.
2. **Fit the full model** (`lm(score ~ ., data = ...)` — the `.` means "all other columns") and compute
   **`car::vif()`**.
3. **Identify** the pair with the largest `|correlation|`, and of that pair **drop the variable with the
   larger VIF.**
4. **Refit** without it and **recompute VIF** to confirm the problem is gone.

Concrete result: only **`lunch`** had VIF > 5 (≈ 5.7); it sat in the highest-correlation pair
(`calworks`–`lunch`, r = 0.74) and had the larger VIF, so it was dropped. **After removing `lunch`,
every VIF fell below ~2** → multicollinearity resolved.

> **What dropping a collinear variable does to the *other* coefficients (Tutorial 03 Q1.9 — likely exam
> fodder).** Removing `lunch` **most changed the coefficients of the variables it was correlated with**
> (`income`, `calworks`, `english` all shifted noticeably; the uncorrelated `stratio` barely moved). Their
> **p-values dropped** (they became more significant) because removing the collinear partner
> **de-inflates their SEs.** Watch the subtlety: this SE relief only applies to the variables that
> *were* collinear with the dropped one — an *unrelated* predictor's SE can actually **rise** (dropping a
> strong predictor raises the residual variance), so don't claim "all SEs decreased."

---

# TOPIC 3 — CAUSALITY & STUDY DESIGNS

The recurring warning "**association is not causation**" finally gets its proper treatment. Whether you can
claim causation depends on **(1) how the data were collected** and **(2) the methods used.**

## Why naive causal claims fail

- **Reverse causality** — the arrow points the other way. *"Parental homework help hurts grades"* — more
  likely **struggling kids receive more help**, not that help causes struggle.
- **Confounding** — a **confounder `C`** causes changes in **both** the response `Y` **and** a predictor
  `X`, creating a misleading association. *Baseball:* home runs confound the Bases-on-Balls → Runs relationship.
- **Simpson's Paradox** — the direction of an association **flips** when you split by a subgroup.
  *UC Berkeley 1973:* looked like admissions favored men overall, but **within departments** it didn't —
  women applied to more competitive departments. Aggregated vs. stratified data disagree.

**Confounder diagram:**  `C → X` and `C → Y` (with `X → Y`). The `C→X→Y` and `C→Y` paths get tangled.

## Experimental vs. Observational

|               | **Experiment (randomized)**                        | **Observational study**                                  |
| ------------- | -------------------------------------------------------- | -------------------------------------------------------------- |
| Treatment     | **assigned by the researcher, randomly**           | just*measured* as it naturally occurs                        |
| Confounders   | **balanced on average** (even *unobserved* ones) | observed ones can be adjusted;**unobserved ones remain** |
| Causal claims | **Yes** — gold standard                           | **Cannot** naively establish causation                   |

**Why randomization is magic:** randomly assigning the treatment makes the groups **similar on average in
every way** — including variables you never measured — so any difference in `Y` can be pinned on the
treatment. **Analogy:** shuffle a deck thoroughly and deal two hands; on average they're balanced in suits,
faces, everything — even properties you didn't think to check.

### Two experimental designs

- **Completely Randomized Design (CRD):** units randomized freely across treatments; no correlation between
  observations. **Balances observed AND unobserved confounders → gold standard for causal inference.**
- **Randomized Block Design (RBD):** first split units into **homogeneous blocks** (to remove a known
  nuisance factor), then randomize treatments **within each block.** Balances **only observed** confounders,
  so only **average** treatment effects can be estimated (with appropriate methods).

### The confounding simulation (Tutorial 03) — with the actual numbers

New-vs-current TikTok ad, measuring **dwell time**, where **`athlete` is a confounder** (athletes both
have longer dwell times *and* prefer the new ad). Population means (true effect **= +8** in both rows):

|             | current ad | new ad |
| ----------- | ---------- | ------ |
| non-athlete | 15         | 23     |
| athlete     | 20         | 28     |

The tutorial simulates 1,000,000 customers (so the **true slope of +8 is known by design**), draws a
sample, and fits three models. The results are the whole lesson in three numbers:

| Analysis                         | Model                                                         | Estimated ad effect                                            |
| -------------------------------- | ------------------------------------------------------------- | -------------------------------------------------------------- |
| **Naive observational**    | `lm(y_obs ~ x_self_choice)` — omit the confounder          | **9.83** (inflated — biased **above** the true 8) |
| **Adjusted observational** | `lm(y_obs ~ x_self_choice + athlete)` — include confounder | **7.92** (≈ true 8)                                     |
| **Randomized experiment**  | `lm(y_exp ~ x_randomized)` — randomly assign the ad        | **8.03** (≈ true 8)                                     |

In the **observational** study customers **self-select** (athletes lean toward the new ad), so the new-ad
group is packed with high-dwell athletes → the athlete effect **inflates** the estimate to 9.83.
The athlete coefficient in the adjusted model is **≈ +5** (matching the design), confirming it's the
confounder.

### Two ways to deal with a confounder (Tutorial 03's punchline)

1. **Adjust for it** — put the confounder in the model (the 7.92 result). Works **only if you know
   about *and* measured** the confounder; in the real world confounders are **often unknown/unmeasured.**
2. **Randomize** — randomly assign the treatment (the 8.03 result). Balances the confounder across
   groups **by design, even confounders you never measured** — which is why it recovered +8 **without
   `athlete` in the model at all.** This is why randomized experiments are the **gold standard.**

*(Observational alternative when you can't randomize: **stratification** — compare `X`→`Y` within
subgroups that share the confounder's value.)* One-line takeaway: **adjustment fixes the confounders you
know; randomization fixes them all, known or not.**

---

# THE GLM BRIDGE

*(Read this once before Topics 4 and 5 — it's the single most important idea that ties the second half
of the course to the first.)*

So far the response `Y` has been **continuous** and we modelled its **average** directly:

```
E[Y | X] = b0 + b1*X1 + ... + bp*Xp
```

But many real responses aren't continuous: **survived/died** (binary), **number of bike rentals**
(count). For these, modelling the average *directly* with a straight line has a **range problem** — a
line runs off to ±∞, but a probability must live in `(0, 1)` and a count can't be negative.

**The fix (the whole trick):** don't model `E[Y|X]` directly. Model a **function `h(·)` of it** — the
**link function** — and set *that* equal to the linear part:

```
h( E[Y | X] )  =  b0 + b1*X1 + ... + bp*Xp
```

- `h` is chosen so the **left side can roam over all of (−∞, ∞)** to match the linear right side, while
  the **untransformed `E[Y|X]` stays in its legal range** (0–1 for a probability, positive for a count).
- **Ordinary linear regression is the special case `h(x) = x`** (the "identity link") — nothing is
  transformed. So MLR is itself a GLM.
- A model of this form is a **Generalized Linear Model (GLM)**, fit in R with **`glm(..., family = ...)`**.

| Response type | Distribution | Link `h` | Models... | R family |
| --- | --- | --- | --- | --- |
| **Continuous** | Normal/Gaussian | identity `h(x)=x` | the mean `E[Y]` | `gaussian` (default) |
| **Binary (0/1)** | Bernoulli/Binomial | **logit** `log(p/(1−p))` | the **log-odds** | `binomial` |
| **Count (0,1,2,…)** | Poisson | **log** `log(λ)` | the **log-mean** | `poisson` |

> **Why this is great news for the exam.** Once the link is applied, the right side is *just a linear
> model*. **Every skill from Topics 1–2 transfers**: adding predictors, dummy variables for categories,
> additive vs. interaction models, "difference of intercepts / difference of slopes", counting
> coefficients (`k−1` dummies per `k`-level factor). The **only** thing that changes is that
> coefficients are now interpreted **on the transformed (log-odds or log-mean) scale**, and — after
> exponentiating — on a **multiplicative** scale.

**Two structural facts that surprise people (memorize):**

- **There is NO error term `e` in a GLM.** We model a *function of the conditional expectation*
  directly, not `Y = ... + e`. (Randomness still exists — it's baked into the Bernoulli/Poisson
  distribution of `Y` — but there's no additive `e` written in the equation.)
- **Estimation is by Maximum Likelihood (MLE), not Least Squares**, and there is **no closed-form
  formula** — R runs an **iterative algorithm** ("Fisher Scoring iterations" in the summary), which
  **may occasionally fail to converge**. *(For
  Normal errors, MLE and LS give the identical answer — that's why `lm` and `glm(family=gaussian)`
  agree.)*

> **Analogy — the link function is a "power adapter."** Your wall socket delivers voltage over a huge
> range (the linear predictor, `−∞` to `+∞`), but your device only accepts a specific range (a
> probability in 0–1, or a positive count). The **link `g` is the adapter** that safely converts between
> the two: the linear predictor can swing anywhere, and the adapter squeezes it back into the legal range
> for the response. Different devices need different adapters — **logit** for probabilities, **log** for
> counts, and the **identity** ("no adapter needed") for an ordinary continuous response.

> **Cleared-up confusions (from the personal notes).**
> - **"What does GLM even mean?"** *Generalized* Linear Model — it **generalizes** ordinary linear
>   regression in two ways: (1) the response can follow a **non-Normal** distribution (Bernoulli, Poisson,
>   …), and (2) we model a **link `g` of the mean** rather than the mean directly. Plain linear
>   regression is the special case (Normal response, identity link). "Linear" survives because the
>   right-hand side `b0 + b1x1 + …` is still linear.
> - **"Why do we 'drop the `e`' when predicting?"** In a *linear* model `Y = b0 + b1x + e`, the best
>   prediction aims at the **average** `E[Y|X]`, and the error `e` has mean 0 — so its best guess is 0 and
>   it drops out, leaving `ŷ = b̂0 + b̂1x`. In a **GLM there's no `e` to drop in the first place**: we model
>   a function of the average directly, so the equation never had an additive error term.
> - **"MLE?"** **Maximum Likelihood Estimation** — pick the coefficients that make the **observed data
>   most probable** under the assumed distribution. (For Normal errors this coincides with least squares.)

---

# TOPIC 4 — LOGISTIC REGRESSION

**Use it when the response is BINARY** (two outcomes): survived/died, default/no-default,
accepted/rejected, disease present/absent. The **response** is what decides the model — *not* the
predictors. (Course dataset: **Titanic**, `survived` ~ `fare`, `sex`, ….)

**In R the response** must be numeric `0/1` or a **2-level factor**. Convert a string with
`y <- if_else(y == "success", 1, 0)`.

## Why not just use ordinary linear regression?

For a binary `Y`, the conditional expectation **IS a probability**: `E[Y|X] = P(Y = 1 | X)`. A straight
line for that probability produces **fitted values below 0 and above 1** (nonsense) — the **range
problem**. So we model a *function* of the probability whose range is all of `(−∞, ∞)`.

## The model — the logit link

Let `p = P(Y = 1 | X)`. The three equivalent forms (know all three — they're the three "scales" you can
interpret on):

```
probability:   p = e^(b0 + b1*X) / (1 + e^(b0 + b1*X))     ← always between 0 and 1 (the S-curve)
log-odds:      log( p / (1 - p) )  =  b0 + b1*X            ← this is the "logit"; the LINEAR one
odds:          p / (1 - p)         =  e^(b0 + b1*X)        ← exponentiate to get here
```

- **odds** = `p / (1 − p)` = "how many successes per failure." Odds of 3 means success is 3× as likely
  as failure (`p = 0.75`).
- **logit** = `log(odds)`. This is the quantity we set equal to the linear component. Its range is all
  real numbers, which cures the range problem.
- Fit with `glm(survived ~ fare, data = titan, family = binomial)`; the default link **is** the logit
  (the "**canonical link**").

## Interpreting coefficients — THREE scales (this is the whole exam)

Take the Titanic slope on `fare`, `b1 ≈ 0.0152` (raw) so `e^0.0152 ≈ 1.015`.

| Scale | What you report | Titanic example |
| --- | --- | --- |
| **Raw `b1` (log-odds)** | "a 1-unit rise in `X` is associated with a **change of `b1` in the log-odds** of success" | +\$1 fare → **+0.0152 in the log-odds** of surviving |
| **`e^b1` (odds ratio)** | "a 1-unit rise in `X` **multiplies the odds** by `e^b1`" | odds of surviving **× 1.015** per \$1 |
| **`(e^b1 − 1)×100%`** | "a 1-unit rise in `X` changes the odds by **that percent**" | odds of surviving **+1.5%** per \$1 |

- The **raw coefficients are on the log-odds scale**; **exponentiated coefficients are on the odds
  scale** (`tidy(model, exponentiate = TRUE)`). *You choose which to report* — both are correct, they
  just describe the same thing on different scales. Log-odds is "same wording as MLR"; odds is the
  **more natural** interpretation.
- **Intercept:** raw `b0` = log-odds of success when all `X = 0`; `e^b0` = the **baseline odds**.
- **`e^b1` is literally an ODDS RATIO** (`odds_group1 / odds_group0` for a categorical predictor).

### Categorical predictor = odds ratio between groups (Titanic `sex`)

`glm(survived ~ sex)` with **female = reference** gives `sexmale = −2.514` (raw). Then:

- `e^(-2.514) = 0.081`: a male's **odds of surviving are 0.081× a female's** — i.e. only **8.1%** of a
  female's odds, a **91.9% decrease** (`(0.081−1)×100`).
- Flip it for a cleaner sentence: males' **odds of *dying*** were `e^2.514 = 12.35×` those of females.
  *(Same story from either direction — good exam phrasing.)*

### Additive vs. interaction (identical logic to MLR — just on the log-odds scale)

- **Additive** `glm(survived ~ sex + fare)`: **same slope on `fare` for both sexes, different
  intercepts** → "**two logistic curves, same shape, shifted**." You **CAN** say "holding `sex`
  constant / for either sex" and "keeping `fare` constant at *any* value." The `fare` odds-ratio
  (`e^b2 ≈ 1.011`) applies to **both** groups.
  - **The probability curves will NOT look parallel** even though the linear (log-odds) components are
    parallel — the S-shape squashes them. Parallel-ness lives on the *log-odds* scale, not the
    probability scale. **Classic exam trap.**
- **Interaction** `glm(survived ~ sex * fare)`: **different slopes AND intercepts**. Now you **CANNOT**
  say "holding constant" — the effect of `fare` **depends on `sex`**. Read the four coefficients exactly
  like the MLR interaction table (`b2` = reference-group slope on log-odds, `b2 + b3` = other group's).
  To interpret the odds, you **multiply** exponentiated coefficients (e.g. male's `fare` odds-ratio
  `= e^(b2+b3) = e^b2 · e^b3`) — because exponentiation turns the additive log-odds into multiplicative
  odds.

## Inference — the Wald statistic

Inference for GLMs rests on the **CLT** (large-sample theory), so with a large `n`:

```
z = b_hat / SE(b_hat)  ~  N(0, 1)      ← this is the "Wald statistic"
CI:  b_hat ± z_(a/2) * SE(b_hat)       (95% ⇒ z ≈ 1.96)
```

Same machinery, same reading as SLR/MLR: **|z| > 1.96 ⇔ 95% CI excludes 0 ⇔ p < 0.05**. R does it all;
`tidy(model, conf.int = TRUE, exponentiate = TRUE)` gives odds-ratio CIs directly. A CI for `fare` of
`(1.008, 1.015)` reads "90% confident a \$1 fare rise is associated with a **0.8%–1.5% rise in the
odds** of surviving."

## Prediction & fitted values (WHICH SCALE?! — a favorite trap)

An estimated logistic model predicts on **whichever scale you ask for**:

- `predict(model, newdata, type = "link")` → **log-odds** (the default, since the linear part is on the
  log-odds scale).
- `predict(model, newdata, type = "response")` → **probability**.
- **By hand:** compute the log-odds `L = b0 + b1*X1 + ...`, then `p = e^L / (1 + e^L)`. *(The final may
  ask you to do exactly this for one observation — e.g. a male paying \$7.25 → log-odds `−1.694` →
  `p = 0.155`.)*
- **Fitted values gotcha:** `augment(model)`'s `.fitted` column is the **log-odds**, but the model
  object's `$fitted` / `fitted(model)` gives **probabilities**. Know which one you're holding.

## Residuals & diagnostics — why the residual plot is useless here

- **Raw residual** `r = y − p_hat`. Two problems: (1) the **variance is not constant** — for a Bernoulli
  response `Var(Y) = p(1−p)`, which changes with `p`, so residuals of different observations **aren't
  comparable**; (2) because `y` is only `0` or `1`, the raw residuals collapse onto **two parallel lines**
  (values `−p_hat` and `1 − p_hat`) in any residual plot. So a plain residuals-vs-fitted plot is **not
  informative**.
- **Fixes / scaled residuals:** **Pearson residual** divides by the SD:
  `r_pearson = (y − p_hat) / sqrt(p_hat(1 − p_hat))`. Also **deviance residuals** and
  **standardized** versions. You won't compute these by hand, but **know which one you're using**. Even
  with Pearson, the two-lines problem persists → use a **binned residual plot** (`binnedplot()` groups
  points and plots each bin's average).
- **Bottom line:** for logistic regression, don't lean on residual plots. **Overdispersion is the more
  important diagnostic.**

## Overdispersion (the key logistic/Poisson diagnostic)

The model **assumes** the variance equals the Bernoulli value `p(1−p)` (i.e. `Var(Y) = E(Y)(1−E(Y))`).
**Overdispersion** = the data's actual variability is **larger than the model assumes**
(`Var(Y) > E(Y)(1−E(Y))`). This **misspecifies the SEs (not the point estimates)** → CIs and p-values
become unreliable.

- **The dispersion parameter η (final-review framing).** Introduce a factor **η** and model
  `Var(Y) = η·E(Y)(1−E(Y))`. If the assumed Bernoulli/Binomial distribution **holds, η = 1**; **η > 1 =
  over-dispersion, η < 1 = under-dispersion**. (When η ≠ 1, `Y` is no longer strictly Bernoulli/Binomial.)
- **Detect:** refit with `family = quasibinomial` to **estimate η** and read the **dispersion
  parameter**. If it's **far from 1, use the `quasibinomial` results** instead of the plain `binomial`
  ones. (Titanic: dispersion ≈ **0.98** ⇒ no sign of overdispersion.)
- **Fix:** the **quasi-likelihood** approach (`quasibinomial`) estimates the dispersion and **corrects
  the standard errors**; the coefficient estimates are unchanged.

> **Cleared-up confusions (from the personal notes).**
> - **"Why don't we just model the probability directly — isn't that the most useful thing?"** Two
>   reasons. (1) **Range:** a probability is trapped in (0,1), but a straight line isn't — it would predict
>   nonsense like −0.3 or 1.4. (2) **Constant effect:** on the probability scale the effect of `X` isn't
>   constant (the S-curve is flat near 0 and 1, steep in the middle), so a single slope can't describe it.
>   The **log-odds** scale is unbounded *and* makes the effect a constant slope — the scale where a
>   *linear* model actually fits. We still **report probabilities for prediction** (just convert back with
>   `p = e^L/(1+e^L)`); we simply don't *model* on that scale. **Analogy:** the logit "unrolls" the
>   bounded probability into a straight, evenly-spaced ruler where one extra unit of `X` always means the
>   same step.
> - **"Additive or interaction? Some slides *add*, others *multiply* — which is it?"** Both, on different
>   scales. On the **log-odds** scale the model is **additive** (exactly like MLR: `b0 + b1x1 + b2x2 +
>   …`). When you **exponentiate** to the **odds** scale, addition becomes **multiplication**, because
>   `e^(a+b) = e^a·e^b`. So the *same* model looks additive in log-odds and multiplicative in odds — that's
>   why you see both. ("Interaction" is a separate idea: a product *term* `x1·x2` in the linear part.)
> - **"Why can't I use a Q-Q / residual plot for logistic like I did for linear regression?"** Those
>   plots assume **Normal errors with constant variance**. A logistic response is **0 or 1**, so (a) its
>   variance `p(1−p)` **changes** with the fitted probability (not constant), and (b) the raw residuals
>   collapse onto **two lines** (`−p̂` and `1−p̂`). There simply isn't a Normal, constant-variance error to
>   check — so the plots are uninformative, and we lean on **overdispersion** instead.

---

# TOPIC 5 — POISSON REGRESSION

**Use it when the response is a COUNT** (non-negative integers `0, 1, 2, …`): number of customer
arrivals, disease occurrences, traffic accidents, bike rentals. (Course dataset: **Bikeshare**,
`bikers` ~ `temp`, `season`, `workingday`, `windspeed`.) **Everything mirrors logistic regression** —
the only change is the link and the interpretation scale.

## Two problems that rule out ordinary linear regression

1. **Range problem:** counts are `≥ 0`, but a line predicts **negative** counts.
2. **Non-constant variance:** the Poisson distribution has the special property that its **mean equals
   its variance**: `λ = E[Y|X] = Var(Y|X)`. So anything that shifts the mean **also shifts the
   variance** — the constant-variance (E) assumption of linear regression is automatically violated.

## The model — the log link

Let `λ = E[Y|X]` be the **mean count**. Model:

```
mean:      E[Y|X] = λ = e^(b0 + b1*X1 + ...)     ← always positive (cures the range problem)
log-mean:  log(λ) = b0 + b1*X1 + ...             ← the LINEAR one (the "canonical link" is log)
```

Fit with `glm(bikers ~ ., data = bikeshare, family = poisson)`. Again: **no error term** (we model a
function of the conditional mean), estimated by **MLE / iterative algorithm**.

> **`factor()` gotcha (bites people constantly).** R only makes dummy variables out of **factors**. If a
> categorical variable is stored as a **number** (e.g. `season` = 1,2,3,4 or `workingday` = 0/1), `glm`
> silently treats it as **continuous** and fits **one meaningless slope on the codes**. Wrap it:
> `mutate(season = as.factor(season))` *before* fitting, so you get `season2, season3, season4` dummies.

## Interpreting coefficients — TWO scales

Take the Bikeshare `temp` coefficient `b5 ≈ 2.688` (raw), so `e^2.688 ≈ 14.7`.

| Scale | What you report | Bikeshare example |
| --- | --- | --- |
| **Raw `b` (log-mean)** | "a 1-unit rise in `X` is associated with a **change of `b` in the log-mean** count, holding others constant" | +1 in `temp` → **+2.688 in log-mean** bikers |
| **`e^b` (rate ratio)** | "a 1-unit rise in `X` **multiplies the mean count** by `e^b`" | mean bikers **× 14.7** per unit `temp` |
| **`(e^b − 1)×100%`** | percent change in the mean count | e.g. `season2` `e^b = 1.065` → **+6.5%** vs. season 1 |

- **Raw = log-mean scale; exponentiated = mean-count scale** (multiplicative). A **dummy coefficient**
  `e^b` = the **ratio of mean counts** between that level and the reference (e.g. `season3`
  `e^(-0.141) = 0.868` → season 3 has **86.8%** of season 1's mean usage = a **13.2% decrease**).
- **Why "multiplicative"** (derivation you may be asked to reproduce): compare `log λ` at `temp` and
  `temp+1`; everything else is held constant and cancels, leaving `log λ_(t+1) − log λ_t = b`. By the
  log-of-a-ratio rule, `log(λ_(t+1)/λ_t) = b`, so `λ_(t+1)/λ_t = e^b` ⇒ `λ_(t+1) = e^b · λ_t`.
- **Additive vs. interaction:** identical logic to logistic/MLR, on the log-mean scale. Additive ⇒ "keep
  others constant at any value"; interaction ⇒ effect of one variable **depends on** the other, so you
  **multiply** exponentiated coefficients to get a group's rate ratio (e.g. working-day `temp` effect
  `= e^(b_temp) · e^(b_interaction) = 14.7 × 0.483 = 7.11`).

## Inference — same as logistic

**Wald statistic** `z = b_hat / SE ~ N(0,1)` (CLT, large sample), CIs and tests exactly as before. R
does it; CIs can be reported on the log-mean or (exponentiated) mean scale.

## Residuals & overdispersion — Poisson USUALLY over-disperses

Same residual issues as logistic (discrete response, non-constant variance): raw and **Pearson**
residuals (`r_pearson = (y − λ_hat)/sqrt(λ_hat)`), residual plots not very useful → lean on
**overdispersion**.

- **Poisson regression *usually exhibits overdispersion*** because the "mean = variance" straitjacket is
  rarely true in real data. **This is a much bigger deal for Poisson than for logistic.**
- **The η framing (final review).** Under Poisson, `Var(Y) = E(Y) = e^(b0+b1x1+…)`. If the observed
  variance exceeds this, model `Var(Y) = η·E(Y)` with **η > 1** ⇒ over-dispersion; use `quasipoisson`
  for inference.
- **Detect:** refit with `family = quasipoisson` and check the **dispersion parameter** (want ≈ 1).
  Bikeshare: **dispersion ≈ 90.6** — *wildly* above 1 ⇒ **severe overdispersion**, the Poisson
  assumption clearly fails. *(Contrast the Titanic logistic dispersion of ≈ 0.98 — that's what "fine"
  looks like.)*
- **Fix:** **quasi-likelihood** (`quasipoisson`) re-estimates the dispersion and **corrects the SEs**;
  point estimates are unchanged. **If the dispersion is far from 1, the plain Poisson SEs/p-values can't
  be trusted.**

> **One-line contrast to lock in.** Logistic → **log-odds / odds** (odds ratios), variance `p(1−p)`,
> overdispersion *sometimes*. Poisson → **log-mean / mean** (rate ratios), variance `= λ`,
> overdispersion *usually*. Both: no error term, MLE, Wald inference, `factor()` your categoricals,
> exponentiate for a multiplicative interpretation.

> **Cleared-up confusions (from the personal notes).**
> - **"Why is a dispersion parameter of *1* the magic number?"** Because the Poisson distribution
>   *assumes* **mean = variance** exactly, so its **built-in (theoretical) dispersion is 1** — that's the
>   baseline the model promises. The dispersion parameter η is really the **ratio `actual variance ÷
>   assumed variance`**: **η = 1 means reality matches the assumption**, η > 1 means the data are more
>   spread out than Poisson allows (over-dispersion), η < 1 less. It's a **reality-check ratio**, and 1 is
>   "reality agrees with the model." (Same logic for logistic, where the assumed variance is `p(1−p)`.)
> - **"Why did the slides fit *separate models for leisure vs. working days*?"** That's an
>   **interaction** between `temp` and `workingday`: it lets the temperature effect **differ** by day type
>   (warm weather boosts leisure riding more than commuting). Fitting "two models" is just a vivid way to
>   picture one interaction model with **different slopes** per group — exactly the cat×continuous
>   interaction idea from Topic 2, now on the log-mean scale.
> - **"Why drop the `e` again?"** Same answer as the GLM bridge: a Poisson model has **no additive error
>   term** — we model `log(E[Y|X])` directly, so there's no `e` to write or drop.

---

# TOPIC 6 — GOODNESS OF FIT

*(Model evaluation for **linear** models estimated by LS. Splits into two classes: **Part 1** =
one-model metrics like `R²`; **Part 2** = comparing **nested** models with the `F`-test. Course case
study: predicting **protein from mRNA levels** — biology's "Central Dogma" says they should track, but
real data shows only a **weak** association, so it's a natural "is this model any good?" story.)*

## Part 1 — Is our model better than "nothing"?

"**Nothing**" = the **null model** = **intercept-only**, `Y = b0 + e`, whose best guess for every
observation is just the **sample mean `ȳ`** (no predictors used). So the question is: **does using `X`
beat just predicting the average?** Statistically, we compare our fitted `ŷ` (an estimate of `E[Y|X]`)
against `ȳ` (an estimate of `E[Y]`).

### The three sums of squares (know all three cold)

```
TSS = SUM (y_i − ȳ)^2     Total Sum of Squares    — total variation; residuals from the NULL model
ESS = SUM (ŷ_i − ȳ)^2     Explained Sum of Squares — variation the model EXPLAINS (fit vs. mean)
RSS = SUM (y_i − ŷ_i)^2   Residual Sum of Squares  — variation the model MISSES (leftover; LS minimizes this)
```

**The decomposition** (holds when the model has an **intercept** and is fit by **LS**):

```
TSS = ESS + RSS       "total variation = explained + unexplained"
```

**A good model makes ESS large and RSS small** relative to TSS.

### R² — the coefficient of determination

```
R² = 1 − RSS/TSS = ESS/TSS      (the two forms are equal only with an intercept + LS)
```

- **Meaning:** the **proportion of the total variation in `Y` that the model explains** — equivalently,
  the *gain* from using the model instead of the mean, relative to total variation.
- **Range 0 to 1** (larger = better fit), *because* we expect `RSS < TSS`. In SLR it literally equals the
  **square of the correlation**: `R² = r²`. (protein~mRNA on 3 genes: `R² ≈ 0.09` — only **9%** of
  protein variation explained by mRNA. In observational data even 20–50% can be "useful"; high `R²` is
  rare and noisy data is normal.)
- **CRITICAL caveats (all exam-worthy):**
  - `R²` is **computed in-sample (training data)** — it says nothing about **out-of-sample** (test)
    prediction.
  - `R²` **is NOT a test** — it has **no known distribution**, so you can't use it to test a hypothesis
    or declare one model "significantly" better.
  - `R²` **always increases when you add a predictor**, relevant or not. So it **cannot compare models of
    different sizes** and it tempts overfitting.

### Fixing the "always increases" flaw — Adjusted R²

```
adj R² = 1 − [ RSS/(n − p − 1) ] / [ TSS/(n − 1) ]      (p = #covariates excluding intercept)
```

Dividing `RSS` by `n − p − 1` **penalizes extra variables**: adding a useless predictor lowers `RSS` only
a little but costs a degree of freedom, so `adj R²` can **go down**. Use `adj R²` (not `R²`) to compare
models of **different sizes**. *(Linear models only — there's no `adj R²` for logistic/Poisson; that's
Topic 7's job.)*

### Other absolute metrics (smaller = better)

- **RSE (Residual Standard Error)** `= sqrt( RSS/(n − p − 1) )` — called **`sigma`** in `glance()`. It
  **estimates `σ = sqrt(Var(e))`**, the size of the *irreducible* error, and is what classical theory
  needs to compute the coefficient SEs.
- **MSE (Mean Squared Error)** `= (1/n) SUM (y_i − ŷ_i)²`. **Training MSE** uses the fitting data;
  **testing MSE** uses new/held-out data to judge **out-of-sample** prediction (the honest measure).
- **`glance(model)`** prints `r.squared`, `adj.r.squared`, `sigma`, the **F-statistic + its p-value**,
  `AIC`, `BIC`, `deviance`, etc., in one row.

> **AIC / BIC (one line).** `AIC = (goodness of fit) + (penalty for model size)`; **smaller AIC = better**.
> BIC is similar with a heavier size penalty. Like `adj R²`, they let you trade off fit against
> complexity, and they're what **stepwise selection** optimizes.

## Part 2 — Comparing NESTED models: the F-test

`R²` is a *descriptive* number, not a *test*. To ask a **yes/no significance question** — "do these
extra variables actually help?" — use an **`F`-test**, which **requires the two models to be nested**
(the smaller "reduced" model's predictors are a **subset** of the larger "full" model's).

### Case A — full vs. the intercept-only model ("is the model better than nothing?")

```
reduced (null):  Y = b0 + e
full:            Y = b0 + b1*X1 + ... + bp*Xp + e

H0: b1 = b2 = ... = bp = 0     (NONE of the predictors help — simultaneously)
H1: at least one bj ≠ 0        (at least one helps)
```

The **F-statistic** (you will **NOT** compute it by hand; just read R):

```
F = [ (RSS_reduced − RSS_full) / p ] / [ RSS_full / (n − p − 1) ]   ~  F(p, n−p−1) under H0
```

Big drop in RSS ⇒ big `F` ⇒ small p-value ⇒ reject `H0` ⇒ **the model beats the null**. In R:
**`glance(model)`** reports this F-test (its reduced model is *always* the intercept-only model).

### Case B — any nested pair (does an EXTRA block of variables help?)

```
reduced:  Y = b0 + b1*X1 + ... + bq*Xq + e            (q covariates)
full:     Y = b0 + b1*X1 + ... + bq*Xq + ... + bp*Xp + e   (p covariates, k = p − q extra)

H0: b_(q+1) = ... = bp = 0    (the k EXTRA coefficients are all 0 — the extra block adds nothing)
H1: at least one of them ≠ 0
```

`F = [ (RSS_reduced − RSS_full) / k ] / [ RSS_full / (n − p − 1) ] ~ F(k, n−p−1)`. In R: **`anova(model_reduced,
model_full)`** compares **any** nested pair (protein example: adding `gene` to `prot ~ mrna` gave
`F = 9.9`, `p = 0.001` ⇒ the bigger model is significantly better).

### t-test vs. F-test (a clean exam contrast)

- **`lm`'s t-test** on a coefficient tests **one** `bj = 0` at a time, **with the other variables still
  in the model** — "does *this* variable add anything, given the rest?"
- **The `F`-test** tests **many** coefficients **simultaneously** — "does this *whole block* (or the whole
  model) add anything?"
- **Special case `p = 1`:** with a single predictor the two hypotheses are identical, and indeed
  **`F = t²`** with the same p-value. Both rest on Normality / large-sample approximations.

> **The must-remember caveat (protein~mRNA punchline).** A significant `F`-test means the bigger model
> **fits significantly better** — it does **NOT** mean "we can predict `Y` from `X`." In the example,
> adding `gene` made the model significant, but that's because **`gene`** (not `mRNA`) carries the
> signal. **Significance of a model ≠ good prediction, and ≠ a specific predictor being useful.**

> ⚠️ **Model-selection warning (leads into Topic 8).** People use `F`-tests / `t`-tests to *pick*
> significant variables and then refit — but if you **select and test on the same data**, you've used
> the data twice and the inference is **no longer valid** (the **post-inference / "double-dipping"
> problem**).

> **Analogy — `R²` vs. adjusted `R²`.** Think of `R²` as a **student who gets extra credit for every
> assignment they *attempt*, whether or not they do it well** — so their score only ever goes up as they
> pile on more work (more predictors). **Adjusted `R²`** is a stricter grader who **deducts points for
> busywork**: a predictor has to actually improve the fit *enough to justify the degree of freedom it
> costs*, or the adjusted score drops. That's why you compare models of different sizes with **adjusted
> `R²`, never raw `R²`.**

> **R helpers for variable selection (from the personal notes — `step`, `drop1`, `add1`).** These
> automate the "which variables?" search using **AIC**:
> - **`drop1(model)`** — a **one-move what-if table**: from the *current* model, it shows the AIC (and a
>   test) for **removing each single variable**, one at a time. `add1(model, scope)` is the mirror image —
>   the effect of **adding** each candidate. Think "what happens if I take out (or put in) *one* player?"
> - **`step(model)`** — runs the **whole automated search to the end**: it repeatedly applies the `drop1`
>   / `add1` logic (forward, backward, or both), each time making the single best AIC move, until no move
>   improves AIC. Think "run the entire tryout process, not just one swap." So `drop1`/`add1` are the
>   **single steps**; `step` is the **full loop**. **Both work on `lm` *and* `glm`.** (Caveat: like all
>   selection, `step` optimizes AIC — it doesn't *know* which variables are truly important, and its
>   p-values afterward suffer the double-dipping problem.)

---

# TOPIC 7 — GOODNESS OF FIT FOR GLMs

**The single most important fact of this topic:** `R²`, `adj R²`, `RSE`, and `MSE` are **for LINEAR
regression only** — and the `F`-test is a linear-model tool too. **They do NOT apply to logistic or
Poisson regression.** For GLMs, the analogous quantity is the **DEVIANCE**.

## Deviance = the GLM's generalization of RSS

The **deviance** measures the gap between the **log-likelihood of your fitted model** and that of a
**"perfect" model** — the **saturated model**, which has one parameter per observation and fits the data
*exactly* (interpolates every point).

- **Think of deviance as "RSS for GLMs."** In fact, if a linear model has Normal errors, the deviance is
  **proportional to the RSS**.
- **Lower deviance = better fit.** (`glm` output shows **null deviance** = fit of the intercept-only
  model, and **residual deviance** = fit of your model — smaller residual deviance means your predictors
  helped.)
- **Perfect fit is BAD.** A model that passes through every point (the saturated model, `R² = 1` in the
  linear analogy) has **overfit**: it memorized noise and will make big errors on a *new* sample from
  the same population. We deliberately prefer **good-but-not-perfect** models. *"Anything taken to the
  extreme becomes bad."*

## Deviance test — comparing nested GLMs (the χ² test)

Just as the `F`-test compares nested linear models, the **deviance test** compares nested **GLMs**:

```
H0: the two (nested) models are equally good   (the extra coefficients add nothing)
H1: the larger model is better

test statistic = difference in deviance  ~  χ²(d)     under H0
   where d = difference in the number of predictors between the two models
```

- A **large deviance drop** ⇒ large χ² ⇒ small p-value ⇒ the extra terms significantly improve the fit.
- **This is a large-sample result** — it's only reliable when `n` is big.
- In R: **`anova(reduced, full, test = "Chisq")`** (or just `anova()` on GLMs) — same workflow as the
  `F`-test, different reference distribution.

> **Cheat-sheet mapping.** Linear model: **RSS → R²/adjR², F-test**. GLM (logistic/Poisson): **deviance
> → deviance χ²-test** (and **AIC**, which works for *both* since it's likelihood-based). If a question
> gives you a `glm` and asks about `R²`, the answer is "**you can't — use deviance.**"

> **Analogy — deviance is a "golf score."** It measures **how far your model is from a perfect (saturated)
> round** — so **lower is better**, and 0 would be a hole-in-one on every hole (the saturated model that
> hits every data point). Adding useful predictors *lowers your score* (residual deviance drops from the
> null deviance). But a **literal zero is bad news**, not bragging rights: it means you memorized the
> course (overfit) and will play terribly on a new one. The **deviance test** just asks whether a bigger
> model's lower score is a **real** improvement or within normal round-to-round noise (χ²). Don't confuse
> **deviance** (fit, lower = better) with **dispersion** (the variance reality-check from Topics 4–5).

---

# TOPIC 8 — MODEL SELECTION

Two big questions this topic answers: **(1)** how do we pick which variables belong in the model in a
*smooth* way (**regularization**), and **(2)** why is it dangerous to **select and infer on the same
data** (the **post-inference problem**)? (Course dataset: **Ames Housing**, predicting `SalePrice`.)

## Part 1 — Regularization (shrinkage) methods

**Recap — stepwise selection** (`step()`, `regsubsets(..., method="forward")`) adds/removes variables
one at a time. It's a **greedy** algorithm: results **depend on the order** variables enter, and a
variable is either **fully in or fully out** — its coefficient **jumps** from `0` to some value in a
single discrete step. *Can we do the selection more smoothly — somewhere between 0 and its full value?*

**Regularization** = add a **penalty** on the size of the coefficients to the objective, so coefficients
are **shrunk toward 0 continuously** as we dial up the penalty. Instead of minimizing just the RSS:

```
minimize:  SUM (Y_i − b0 − X_i·b)²  +  λ · penalty(b)
                └─ usual fit ─┘          └─ shrinks coefficients ─┘
```

| Method | Penalty | Norm | Shrinks to exactly 0? | Selects variables? |
| --- | --- | --- | --- | --- |
| **Ridge** | `λ · SUM b_j²` | **L2** (squared) | **No** (never quite 0) | **No** |
| **LASSO** | `λ · SUM |b_j|` | **L1** (absolute) | **Yes** | **Yes** — selects *and* trains at once |

*(The course focuses on **LASSO**. "LASSO" = **L**east **A**bsolute **S**hrinkage **a**nd **S**election
**O**perator, Tibshirani 1996. Ridge, Hoerl & Kennard 1970, is a multicollinearity remedy.)*

### The penalty parameter λ ("how much to shrink")

- **`λ = 0`** ⇒ no penalty ⇒ the objective is just the RSS ⇒ **you get back the ordinary LS estimates.**
- **As `λ` grows**, coefficients shrink. **LASSO drives them to *exactly 0* one by one** (that's how it
  *selects* variables — 0 means "dropped"); **Ridge shrinks them toward 0 but never reaches it** (so
  Ridge can't select). *(A LASSO coefficient path plot shows lines peeling off to 0 as `log λ` rises;
  the top axis counts how many coefficients are still non-zero.)*
- **Choosing `λ` ("tuning"):** pick the `λ` that **minimizes the test MSE**, estimated by
  **cross-validation** (CV splits the training data into internal train/test folds so no real test data
  is touched). **`cv.glmnet()`** does this and reports two choices:
  - **`lambda.min`** — the `λ` with the **smallest CV MSE**.
  - **`lambda.1se`** — the **largest** `λ` whose CV MSE is still within **1 standard error** of the
    minimum ⇒ **more shrinkage / a simpler model at almost no cost in error.**

### Bias–variance tradeoff (why we'd accept a *biased* estimator)

Shrinkage **biases** the coefficients (pulls them toward 0), so `E[b_hat] ≠ b`. Why do it? Because
`MSE = Variance + Bias²`, and **paying a little bias buys a big drop in variance**, which **improves
prediction**. LASSO was designed for **prediction**, especially the **high-dimensional** case where
`p` (predictors) `>> n` (sample size). **Because the penalty depends on coefficient *size*, you must
STANDARDIZE the inputs first** (`glmnet` does this by default).

### In R (`glmnet`)

- Needs a **matrix** `x` of predictors + a response **vector** `y` (not a formula/data-frame).
- `alpha = 1` ⇒ **LASSO**; `alpha = 0` ⇒ **Ridge**; in between = **Elastic Net**.
- `cv.glmnet()` for CV; `coef(cv_fit, s = "lambda.min")` pulls the coefficients (dropped ones show as
  `.`); `predict(cv_fit, newx = X_test, s = "lambda.min")` for prediction on the test set.

## Part 2 — The post-inference problem ("double-dipping")

**The core sin:** using the **same data** to (a) **select** which variables go in the model *and* (b)
**test/estimate** those variables. Selection cherry-picks variables that happen to look good **in this
sample**, so the follow-up inference is **over-optimistic** — you **reject `H0` far too often**.

**The simulation proof (know this design):** generate data where **ALL true coefficients are 0** (so the
**intercept-only model is genuinely correct** — no variable should look significant). Then, on each of
1000 datasets: **forward-select** up to 3 variables using `adj R²`, and `F`-test the selected model on
the **same** data. Result: in a **large fraction** of datasets the `F`-test **wrongly rejects `H0`** —
the **Type I error rate is badly inflated** (should be ~5%, comes out much higher). *Selecting on the
data inflated `adj R²`, which then fooled the test.*

**The fix — split the data:** use **one part to select** the model and a **separate part to fit and test**
it. Because the inference part never saw the selection, its Type I error is **controlled** (back to ~5%).
The course verifies this with the same simulation on split data. *(The final-review deck frames this as
**the same idea behind cross-validation** — hold out data the model-building step never touched.)*

- **postLASSO (bridges to Topic 9):** LASSO's coefficients are *biased*. But if you take the variables
  **LASSO selected** and refit **ordinary LS on just those variables**, that **postLASSO** estimator is
  **unbiased**. *However* — to make **valid inference** with postLASSO you **still must split the data**
  (selecting and inferring on the same data is the same double-dipping sin).
- **Takeaway:** you **cannot select variables and do valid inference on the same data**. Split it, or use
  more advanced methods (beyond this course). *(R tooling for the worksheets: `map`/`map_dbl`/`map2`
  apply a function across a list of datasets; `update()` refits a model with a tweaked formula.)*

> **`k`-fold cross-validation (how `cv.glmnet` really picks λ).** Instead of one train/test split, CV
> **rotates**: chop the training data into `k` equal parts ("folds"), then `k` times train on `k−1` folds
> and measure error on the held-out fold, so **every observation gets used for testing exactly once**.
> Average the `k` error estimates for each candidate λ and pick the λ with the smallest average (or the
> `lambda.1se` simpler choice). **Analogy:** rather than judging a chef on one dish, you have them cook for
> `k` different tasting panels and average the reviews — a more stable verdict. `k = 10` (10-fold) is the
> usual default.

> **Cleared-up confusions (from the personal notes).**
> - **"If LASSO isn't mainly for shrinking model size, what *is* it for now?"** Its headline use today is
>   building **strong *predictive* models** — the shrinkage trades a little bias for a big variance
>   reduction (`MSE = Var + Bias²`), which improves out-of-sample prediction. It's *also* still great for
>   **high-dimensional** problems (`p >> n`, more predictors than observations) where ordinary least
>   squares breaks down, and it conveniently **selects variables** as a side effect (coefficients hit
>   exactly 0). What it's *not* good for is **unbiased inference** — for that you need postLASSO + a data
>   split.
> - **"Why was getting *small p-values* a *bad* thing in the double-dipping simulation?"** Because in that
>   simulation the truth was rigged so that **no variable matters** (every true coefficient is 0), i.e.
>   **`H0` is actually true.** A correctly behaving test should then reject only about **5%** of the time.
>   Getting small p-values (rejecting) far more often means the test is **crying "significant!" on pure
>   noise** — **false positives / inflated Type I error** — which is exactly the bug the simulation was
>   built to expose. Small p-values are only "good" when there's a real effect; here there isn't.

---

# TOPIC 9 — PREDICTION UNCERTAINTY

**The setup:** an estimated model gives a prediction `ŷ = b0_hat + b1_hat·X + …`. But `b_hat` came from a
**random sample**, so a **different sample would give different coefficients and thus a different
prediction** — **predictions are random variables**. This topic quantifies that uncertainty with **two
different intervals**, and the whole exam point is **knowing which one to use.** (Focus is **MLR**;
extending intervals to GLMs is hard and out of scope. Course dataset: **Strathcona property tax**,
`assess_val ~ BLDG_METRE`.)

## The key question: WHAT are you predicting? (average vs. actual)

For a house of a given size `X`, you might want to predict either:

- the **AVERAGE** assessed value of *all* houses of that size: **`E[Y | X]`** (a point on the population
  line), **or**
- the **ACTUAL** assessed value of *one specific new* house of that size: **`Y`** (which = the average
  **plus** its own random error `e`).

These are different targets with **different amounts of uncertainty**, so they get **different
intervals**. Recall `Y = E[Y|X] + e = b0 + b1·X + e`; the prediction `ŷ = b0_hat + b1_hat·X` is used to
approximate **both**, but the error budget differs.

| | **Confidence Interval for Prediction (CIP)** | **Prediction Interval (PI)** |
| --- | --- | --- |
| **Predicting** | the **average**, `E[Y|X]` | an **actual new** value, `Y` |
| **Sources of uncertainty** | **ONE** — sample-to-sample variation in `b_hat` | **TWO** — sample-to-sample variation in `b_hat` **+** the random error `e` |
| **Width** | narrower | **wider** (extra `e` term) |
| **Centred at** | the fitted value `ŷ` | the same fitted value `ŷ` |
| **Interpret with** | "**confidence**" (target is a fixed number) | "**probability**" (target is a random variable) |
| **R** | `predict(model, interval = "confidence")` | `predict(model, interval = "prediction")` |

### Why PI is WIDER (the exam's favorite question)

The CIP only has to account for **uncertainty 1**: our estimated line `b0_hat + b1_hat·X` **approximates**
the true average line `b0 + b1·X` (sample-to-sample wobble). The PI must **also** account for
**uncertainty 2**: even if we knew the true average line perfectly, an **individual** house still scatters
around it by its own error `e`. **Two sources of uncertainty > one**, so **PI ⊃ CIP** — the PI is always
wider. Predicting **one actual value is harder** (more uncertain) than predicting the **average**.

### Interpretation templates (Strathcona, house of size 220 m)

- **CIP:** "With **95% confidence**, the **average** assessed value of houses of size **220 m** is between
  **\$671,944 and \$748,198**." *(Confidence, because the average is a fixed unknown number — once the
  interval is computed it either contains it or not.)*
- **PI:** "With **95% probability**, the value of **a (single) house** of size **220 m** is between
  **\$454,519 and \$965,622**." *(Probability, because an individual house's value is itself random.
  Note how much wider — that's the `e` term.)*

> **The one diagram to carry.** Three stacked equations: `Y = E[Y|X] + e` (truth) → `Y = b0 + b1·X + e`
> (linearity assumption) → `ŷ = b0_hat + b1_hat·X` (our prediction). **CIP** aims the prediction at the
> **middle red part** `b0 + b1·X` (the average). **PI** aims it at the **whole top** `Y` (average + `e`).
> Same `ŷ`, different target, different interval width.

> **Connection to `geom_smooth(se = TRUE)`.** The shaded band `ggplot` draws around a regression line is
> the **CIP band** (uncertainty of the *fitted line/average*) — **not** a PI, and **not** the scatter of
> the points. This is the same "SE of the line ≠ scatter of the points" idea from Topic 1 inference.

> **Analogy — bus arrival times.** The **CIP** is like predicting the **average** arrival time of the
> 8:05 bus over all weekdays — with lots of data you can pin the *average* down quite tightly (a **narrow**
> interval). The **PI** is like predicting when **tomorrow's specific bus** will arrive — even if you knew
> the true average perfectly, *this one bus* still varies with traffic and weather (its own error `e`), so
> your interval must be **wider**. Same best guess (`ŷ`), but "the average bus" is far easier to predict
> than "tomorrow's bus." That extra `e` is exactly why **PI ⊃ CIP, always.**

---

# WORKSHEET PRACTICE — R CODE & EXTRA NUGGETS

The **Topic 1–3 worksheets** use the **`US_cancer_data`** dataset (`TARGET_deathRate` = cancer deaths per
100 000; `povertyPercent`; `PctPrivateCoverage`; `state`); the **post-midterm worksheets** move to new
data — **Worksheet 07** (breast-cancer logistic, deviance) and **Worksheet 08** (two model-selection
simulations). They are where the theory above becomes runnable R code. Below is everything the worksheets
add or reinforce — **great exam-prep material because it's exactly the style of question you'll be
asked.**

## Worksheet 01 — SLR: estimation, inference, bootstrapping

### The three goals of regression (framing)

- **Estimation** — estimate the true unknown relationship.
- **Inference** — use the model to infer things about that unknown relationship (CIs, tests).
- **Prediction** — predict `Y` for a *new* observation.

  *Worksheet example:* "How can we determine the association across all counties?" = **inference/estimation**.
  "A new county has 14% poverty — what mortality do we expect?" = **prediction**.

### `lm()` essentials

```r
lm(response ~ input, data = df)      # standard SLR
lm(response ~ ., data = df)          # use ALL other columns as predictors
lm(response ~ input - 1, data = df)  # forces intercept = 0 — DON'T unless you truly know why
```

### The "best line" = Least Squares, measured *vertically*

When asked what distance to minimize, the answer is the **vertical** distance (in the `Y` / response
direction) — because we're explaining `Y`. LS minimizes the **sum of squared residuals**, where a residual
is that vertical gap between a point and the line. (The worksheet links the classic
[setosa.io OLS applet](http://setosa.io/ev/ordinary-least-squares-regression/).)

### Slope interpretation — pick the wording carefully

For slope ≈ 1.52 in `TARGET_deathRate ~ povertyPercent`, the **correct** phrasing is:

> "A one-percent increase in the county's populace in poverty is **associated with** a 1.52 increase in
> cancer mortality per capita."

**Wrong** options to recognize on an exam: anything saying "**causes**" (this is observational data), or "the
**effect** of" (also implies causation).

### Sampling variation demo (NOT bootstrapping)

Taking fresh samples with `rep_sample_n()` / `slice_sample()` and refitting gives different estimates each
time — illustrating that `b0hat, b1hat` are random variables with a sampling distribution.
This is a *pedagogical* exercise: **in practice you take only ONE sample**, and taking fresh samples from
the population is **not** bootstrapping (bootstrapping resamples *from your one sample*).

### Hypothesis testing details

- Null is always about the **population parameter**, written `H0: b1 = 0` (**not** `b1hat`, which is a
  computed number, never hypothesized).
- Alternative can be **one-sided** when you have a directional belief: `H1: b1 > 0` (positive association).
  Default in `lm()` is two-sided `H1: b1 != 0`.
- **Which p-value statement is TRUE?** → *"The p-value is not the probability that the null hypothesis is
  true."* All the tempting alternatives are classic misconceptions (it is **not** the effect size, **not**
  "probability results were due to chance," **not** "probability the alternative is false").
- **Reject vs. fail to reject:** we never "accept" or "prove." With p < 0.05 we **"reject H0; poverty is
  statistically associated with mortality."**

### Bootstrapping in R — two ways

**Manual (`replicate` + `sample_n` with replacement):**

```r
lm_boot250 <- replicate(1000, {
  sample_n(US_cancer_sample250, size = 250, replace = TRUE) %>%   # size = n, WITH replacement
    lm(TARGET_deathRate ~ povertyPercent, data = .) %>%
    .$coef
})
lm_boot250 <- data.frame(boot_intercept = lm_boot250[1, ], boot_slope = lm_boot250[2, ])
```

**Tidy (`infer` package — specify → generate → calculate):**

```r
US_cancer_sample250 %>%
  specify(formula = TARGET_deathRate ~ povertyPercent) %>%
  generate(reps = 1000, type = "bootstrap") %>%
  calculate(stat = "slope")
```

(In regression this is called **case bootstrapping** — resampling whole `(X, Y)` rows.)

### Bootstrap percentile CI

```r
lm_boot250 %>%
  pivot_longer(contains("boot"), names_prefix = "boot_", names_to = "statistic") %>%
  group_by(statistic) %>%
  summarise(avg = mean(value),
            lower_ci = quantile(value, 0.025),   # 2.5th percentile
            upper_ci = quantile(value, 0.975))   # 97.5th percentile
```

The `infer` equivalent is `get_confidence_interval(type = "percentile", level = 0.95)`.

### Does sample size matter? (key takeaway)

Bootstrapping from samples of `n = 250, 500, 1500` and comparing the sampling distributions:

> **As `n` grows, the sampling distribution gets TIGHTER (smaller SE); its center stays put.**
> More data → more precise estimates, same target. This is the practical payoff of a bigger sample.

## Worksheet 02 — categorical inputs, additive MLR & interactions

### Building a categorical column & pairwise plots

```r
mutate(state = as_factor(str_trim(str_extract(Geography, "[^,]+$"))))  # make a factor
US_cancer_data %>% GGally::ggpairs()                                    # all pairwise scatter/corr at once
```

`ggpairs()` is the go-to first look at many variables (scatterplots + correlations in one grid) — also handy
for **spotting multicollinearity** early (Topic 3).

### 2-level categorical = a two-sample t-test (confirmed in code)

`lm(TARGET_deathRate ~ state)` with Alabama as reference gives `stateCalifornia` = the **difference of
means**. Running `t.test(TARGET_deathRate ~ state, var.equal = TRUE)` returns the **identical** estimate —
*"`lm()` is running the same t-test."* Interpretation of `stateCalifornia = -34.63`: "mean mortality in
California is 34.63 **below** Alabama."

### Overriding the reference level → get raw group means

```r
lm(TARGET_deathRate ~ 0 + state, data = ACK_cancer_data)   # the 0 removes the intercept
```

With `0 +`, **each coefficient becomes that group's actual mean** instead of a difference from the reference.
Handy, but **not the default** — know when you're using it. (Otherwise: Alabama = 192.73;
California = 192.73 − 34.63 = 158.10; Kansas = 192.73 − 24.89 = 167.84.)

### The SAME variable's coefficient changes between SLR and MLR — why?

`PctPrivateCoverage`'s slope differs in `lm(y ~ PctPrivateCoverage)` vs.
`lm(y ~ povertyPercent + PctPrivateCoverage)`. Because:

- In the **MLR**, the coefficient is the association **holding poverty fixed (at any value).**
- In the **SLR**, poverty isn't in the model, so its influence is dumped into the **error term** — an
  *omitted variable* that contaminates the lone coefficient.

**This is the whole reason to interpret MLR coefficients as "holding all other variables *in the model*
constant."**

### Additive vs. interaction — the punchline the worksheet hammers

- **Additive** `lm(y ~ poverty + state)` → **3 coefficients for 2 lines** because it assumes a
  **common slope, different intercepts** (parallel lines). *"3 coefficients for 2 lines because the additive
  model assumes a common slope."*
- **Interaction** `lm(y ~ poverty * state)` → **4 coefficients for 2 lines** because it allows
  **different slopes AND different intercepts** (non-parallel). *"4 coefficients for 2 lines because we do
  NOT assume a common slope."*

Fit them the same way with `+` vs `*`:

```r
lm(TARGET_deathRate ~ povertyPercent + state, data = AC_cancer_data)   # additive  (parallel)
lm(TARGET_deathRate ~ povertyPercent * state, data = AC_cancer_data)   # interaction (non-parallel)
```

### Plotting fitted lines per group (the `add_predictions` pattern)

```r
AC_cancer_data <- AC_cancer_data %>%
  add_predictions(MLR_state_poverty_int, var = "pred")     # modelr::add_predictions
ggplot(AC_cancer_data, aes(povertyPercent, TARGET_deathRate, color = state)) +
  geom_point() +
  geom_line(aes(y = pred, color = state))                  # one line per state, from the MLR
```

### Reading interaction results (worksheet's own answer key)

In `MLR_state_poverty_int_results`, the row that tests whether the **slopes differ** is the interaction term
(`povertyPercent:stateCalifornia`). If only the `povertyPercent` row is significant (and the interaction is
not), the correct reading is: **"In the reference state (Alabama), mortality is significantly associated with
poverty"** — *not* that the slopes differ between states. This is the same "main effect = reference-group
slope" idea from the Interactions section.

## Worksheet 03 — model assumptions & causality, via *simulation*

Worksheet 03 is the **Topic 3 lab**, and its method is the thing to remember: it **simulates** data
from a data-generating process where **the true `b`'s are known**, deliberately breaks one assumption
at a time, and watches what goes wrong. Because the truth is known, you can *see* the damage — which is
impossible with real data. This is the cleanest way to learn *which assumption hurts what.*

### Warm-up true/false (exact exam style — know these cold)

| Claim                                                                                                            | Verdict         | Why                                                                                                                               |
| ---------------------------------------------------------------------------------------------------------------- | --------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| `lm()`'s hypothesis tests are valid **only if errors are *exactly* Normal**.                           | **False** | Large`n` + **CLT** gives approximately valid inference without exact Normality.                                           |
| Multicollinearity = correlation between an**input and the response**.                                      | **False** | It's correlation**among the inputs** (predictors), not input↔response.                                                     |
| Under multicollinearity it's hard to tell how collinear variables are**separately** associated with `Y`. | **True**  | Overlapping info ⇒ can't isolate individual effects.                                                                             |
| Multicollinearity**inflates the SEs** of the LS estimators.                                                | **True**  | Wider CIs, harder to reject`H0` for those coefficients.                                                                         |
| Equal-variance assumption**does not affect** the SE estimator of the LS coefficients.                      | **False** | The usual SE formula**assumes** constant `sigma^2`; heteroscedasticity ⇒ wrong SEs (the point estimates are still fine). |

### The controlled experiment (benchmark → break one thing)

- **Benchmark (all assumptions hold):** simulate `Y = b0 + b1*X1 + b2*X2 + e`, `e ~ N(0, 4)`, with
  true `(b0,b1,b2) = (10,8,5)`. `lm` recovers estimates **within ~2 SE of the truth**, and the 95% CIs
  **contain the true values.** (Reminder: even correct CIs miss the truth ~5% of the time.)
- **Heteroscedasticity** (simulate `Var(e_i) = X_i1^4`): the **point estimates stay ~unbiased**, but
  the **SEs are wrong** ⇒ CIs/p-values invalid. **Detect:** residuals-vs-fitted shows a **funnel.**
- **Non-Normal errors** (simulate `e ~ Uniform(−10,10)`): the **mildest** violation — estimates barely
  affected; with large `n` the **CLT** keeps inference ≈ valid. **Detect:** **Q-Q plot** + histogram of
  residuals. *(`lm` reports a `t`-Student sampling distribution because `sigma` is estimated; `t` ≈
  Normal.)*
- **Multicollinearity** (simulate `X1, X2` with correlation `rho = 0.95` vs. `0.001`, refit **1000×**):
  the histogram of `b1_hat` is **much wider** under high correlation ⇒ **inflated SE.** Note: this is a
  **repeated-sampling** demo from a known population — **not** bootstrapping.

### Part III — causality

Worksheet 03 closes on causality using the **`tutorial_03` confounding simulation** already covered in
the [Causality section](#topic-3--causality--study-designs) (the ad / `athlete` confounder). Takeaway
it states outright: **the goal of generative modelling is usually a causal claim, but with
observational data we usually can't make one** — confounders block it.

## Worksheet 04 — binary responses (logistic regression) → *Topic 4*

Worksheet 04 is the **logistic-regression lab**. It opens by motivating *why* MLR fails for a
**dichotomous** response (yes/no, success/failure, sick/not-sick) and frames logistic regression as
doing the same two jobs as linear regression — **inference** (test the true relationship) and
**prediction** (a probability, i.e. a **classifier**). Concrete examples it lists: drug vs. placebo
(bacteria present/not), **loan default**, and admission from GPA/ACT.

- **The whole point in one line:** for a 0/1 response, `E[Y|X] = P(Y=1|X)` is a **probability**, so a
  straight line would predict impossible values outside (0,1) — the **range problem**. We instead model
  a *function* of that probability, the **logit** `log(p/(1−p))`, with the linear predictor.
- **Reading the R output:** `glm(y ~ x, family = binomial)`; the raw coefficient is on the **log-odds**
  scale, `exp(coef)` is the **odds ratio**. The worksheet has you interpret both, and warns against the
  classic mistake of reading a log-odds coefficient as if it were a probability.
- **Prediction by hand** (a likely exam task): compute the linear predictor `L = b̂0 + b̂1x`, then
  `p = e^L/(1+e^L)`. As a **classifier** you'd threshold at 0.5.
- Everything ties back to the concept section: [Topic 4 — Logistic](#topic-4--logistic-regression).

## Worksheet 05 — discrete count responses (Poisson) → *Topic 5* (horseshoe `crabs`)

Worksheet 05 is the **Poisson lab**, on the **`crabs`** dataset (`faraway`): **173 horseshoe crabs**,
response **`n_males`** = the count of satellite males around a female's nest, with inputs `color`
(4-level factor), `spine` (3-level factor), carapace `width` (cm), and `weight` (g).

- **Why Poisson, not MLR:** `n_males` is a **count** (non-negative integer) — a line would predict
  negative counts (range problem), and the Poisson **mean = variance** property breaks constant variance.
- **Workflow:** start with an EDA scatter of `n_males` vs. `width` (even though a straight line isn't the
  model), fit `glm(n_males ~ ., family = poisson)`, and interpret `exp(coef)` as a **rate ratio** (the
  multiplicative change in the *mean count*). Remember to **`as.factor()`** `color`/`spine` so R makes
  dummies instead of treating the level codes as numbers.
- Diagnostics: Pearson residuals + the **overdispersion** check (`quasipoisson`), since count data
  usually over-disperses. Concept section: [Topic 5 — Poisson](#topic-5--poisson-regression).

## Worksheet 06 — goodness of fit & nested models (protein vs mRNA) → *Topic 6*

Worksheet 06 is the **goodness-of-fit lab** and the **origin of the protein~mRNA case study** used
throughout Topic 6. It's a real published controversy: a 2014 *Nature* paper (Wilhelm et al.) claimed
mRNA predicts protein well; a 2017 reanalysis (Fortelny et al.) showed the data **don't** support that
(protein and mRNA are only weakly correlated). You re-analyze their data with course tools.

- **What it drills:** `R²` as "proportion of variation explained," **why `R²` alone is misleading**
  (always rises with more predictors; not a test), **adjusted `R²`** to compare sizes, and the
  **F-test** (`anova`) to ask whether adding a predictor is *significant*.
- **The punchline** (carried into the lectures): the model can look "significant" because of **`gene`**,
  not `mRNA` — **a significant model ≠ mRNA predicts protein**. It's the cautionary tale for confusing
  significance, prediction, and a specific predictor mattering. Concept section:
  [Topic 6 — Goodness of Fit](#topic-6--goodness-of-fit).

## Worksheet 07 — goodness of fit beyond MLR (deviance for a logistic model) → *Topic 7*

Worksheet 07 evaluates a **logistic** model on the **Wisconsin Diagnostic Breast Cancer** data
(`breast_cancer`; binary `target` = **malignant = 1 / benign = 0**, 16 continuous inputs, train/test
split). It's the **deviance-in-R workflow** made concrete:

- **Recode the response** to 0/1 (`if_else(target == "malignant", 1, 0)`), then fit
  `glm(target ~ ., family = binomial)` (exclude the `ID` column).
- **Residual types:** `augment()` returns **deviance** residuals by default; `residuals(model, type = ...)`
  gives **`"response"`, `"pearson"`, `"deviance"`** — the worksheet builds all three side by side (recall
  raw residual plots are near-useless here; Pearson/deviance are the right ones).
- **Residual deviance = "RSS for GLMs".** You compute it from the deviance residuals
  (`sum(deviance_resid²)`) and verify it equals **`model$deviance`**. `glance()` reports both the
  **`null.deviance`** (intercept-only) and the **`deviance`** (residual, your model); `model$null.deviance`
  matches `glance`'s null.
- **Why the null model's null deviance = its residual deviance (Q1.5):** for the intercept-only model
  *there are no predictors to add*, so the "model being fit" **is** the null model — the two deviances
  refer to the same fit, hence they're equal.
- **Deviance χ² test:** `anova(model_null, breast_cancer_model, test = "Chisq")` tests the full additive
  model vs. intercept-only → **reject H0**, the full model is significantly better (answer **B**: "reject;
  the full model is significantly better"). The `Resid. Dev` column holds the **residual deviances of the
  two models** (Q1.7 **true**).
- **Any nested pair:** compare the full model to a **reduced** 4-variable model
  (`mean_fractal_dimension + mean_smoothness + mean_compactness + mean_concavity`) with `anova(..., test =
  "Chisq")`. At α = 0.01 you **reject** → the extra variables *are* jointly relevant (answer **A**). Note
  a reduced model can fit well **even though some of its variables weren't individually significant** in
  the full model.
- **Same workflow for Poisson** — just swap `family = poisson`.

## Worksheet 08 — regularization & post-inference (two simulations) → *Topic 8*

Worksheet 08 is the **model-selection lab**, built on **two simulation studies** so the true model is
known. Uses `glmnet` (LASSO/ridge), `leaps`/`regsubsets` (forward selection), and the
`map`/`nest`/`map_dbl`/`map2` toolkit to run **1000 datasets at once**.

- **Part I — LASSO is biased.** True model `E[Y|X] = 75·X1 − 5·X2 + 0·X3` (so **β₃ = 0**; X3 irrelevant),
  `n = 1000`, `rep = 1000`, LASSO at a **fixed λ = 30** via `glmnet(x, y, alpha = 1, lambda = 30)`
  (**`alpha = 1` = LASSO**, `alpha = 0` = ridge). Pull each β̂₁ with `coef(.x)[2, ]` and plot its
  **sampling distribution** against the true 75 → it's **NOT centred at 75** (shrunk toward 0), so the
  LASSO estimator is **biased** (Q1.3 = **false**). The `.` in `coef()` output = a coefficient shrunk to
  **exactly 0** (variable dropped).
- **Post-LASSO fix:** use LASSO only to **select** variables, then **re-fit with `lm`** on the selected
  covariates. That `ls_beta1` sampling distribution **is** centred at 75 — bias removed. (Bias is `E[β̂] ≠
  β`; an estimator whose sampling distribution isn't centred on the truth.)
- **Part II — double-dipping.** New sim: `Y` + `p = 10` predictors, **none related to Y** (intercept-only
  is truly correct), `n = 100`, `rep = 1000`. On each dataset **forward-select ≤ 3 variables by adjusted
  R²** (`regsubsets(..., nvmax = 3, method = "forward")`), then **F-test** the selected model vs.
  intercept-only. `H0`: **all selected coefficients = 0** (Q2.2 = **B**). Nominal Type I error = **0.05**
  (Q2.4), but the **observed** proportion of `p < 0.05` comes out **much higher** (Q2.5) — selecting the
  best-looking variables *in that sample* then testing on it inflates Type I error.
- **Part III — data-splitting fix.** Split each dataset **50/50**: select on the first half, do inference
  (via `update(model, data = tail(50))`) on the second. The p-values from the **selection** half stay
  **inflated** (Q3.1); the p-values from the **held-out** half return to **≈ 0.05** (Q3.2) — so splitting
  fixes it (Q3.3 = **true**). The **same problem afflicts LASSO**, fixed the same way (split, or postLASSO
  **with** a split). Full theory in [Topic 8 Part 2](#part-2--the-post-inference-problem-double-dipping).

---

# IN-CLASS ACTIVITIES — WAGE DATASET WALKTHROUGH

The in-class activities run mostly on **`in-class/data/wage.txt`** (`read.table(..., header = TRUE)`;
columns include `wage`, `education`, `sex`, `experience`, `age`, `union`, `race`, `occupation`, `sector`,
`marr`, `south`). They march through the **whole course arc on one dataset** — SLR → inference → additive
MLR/ANOVA → interactions/diagnostics (Activities 1–4), then **multicollinearity → logistic → Poisson →
goodness-of-fit → stepwise → LASSO** (Activities 5–12) — so they're the most faithful preview of
exam-style questions. (Activity 9 detours to a Poisson **CD4-count** medical dataset.) Coefficient tables
are read with `moderndive::get_regression_table()` (linear) or `summary()`/`tidy()` (GLMs).

## Activity 1 (Jul 7) — SLR estimation & correlation → *Topic 1 SLR*

Model: `lm(wage ~ education)`.

- **(A) Plot `wage ~ education` — linear?** Yes, but a **weak** positive linear relationship (lots of
  scatter). Reinforces: *look at the scatterplot before trusting any number.*
- **(B) Correlation coefficient.** `get_correlation(wage ~ education)` and base `cor()` both give
  **r ≈ 0.382** — a **weak, positive** correlation, consistent with (A). Correlation ⇒ association, **not
  causation.**
- **(C) Fit the SLR.** Slope `estimate ≈ 0.750` (positive) — consistent with the positive `r` in (B) and the
  upward cloud in (A). Overlay the fit with `geom_smooth(method = "lm", se = FALSE)`.
- **Takeaway:** the scatterplot, the correlation coefficient, and the SLR slope are **three views of the same
  association** and should agree in sign and rough strength.

## Activity 2 (Jul 9) — SLR inference → *Topic 1 Inference*

Same `lm(wage ~ education)`, now interrogating uncertainty.

- **(A) Is the relationship significant?** The `education` p-value is **≈ 0 < 0.05** ⇒ statistically
  significant association.
- **(B) 95% CI for β₁.** `(0.596, 0.905)`. It **excludes 0**, so reject `H0: β₁ = 0` at 5% — consistent
  with (A).
- **(C) Link CI ↔ statistic ↔ p-value.** All three tell the **same story**. The `statistic ≈ 9.53` is far
  beyond the `≈ 1.96` threshold, `p ≈ 0`, and the CI misses 0 — these are three equivalent expressions of
  "significant at 5%." At exactly `statistic = 1.96` / `p = 0.05`, the CI's endpoint would sit on 0.
  *(The course calls it a z-statistic here; it's the same `estimate / std_error` ratio.)*

## Activity 3 (Jul 14) — additive MLR, dummies & ANOVA → *Topic 1 Categorical / Topic 2 Additive*

- **(A) "Adjust for sex" = additive model** `lm(wage ~ education + sex)`, i.e.
  `wage = b0 + b1*education + b2*sex + e`. The education CI barely moves — from `(0.596, 0.905)` to
  `(0.600, 0.902)`, p still ≈ 0. **Small change ⇒ education and sex are only weakly related**; if they were
  strongly related, adding `sex` would have shifted the education coefficient a lot. *(This is the
  omitted-variable idea from Worksheet 02 in action.)*
- **(B) Interpreting β₁ now.** With `sex` in the model, `b1 ≈ 0.751` is the education slope **holding sex
  constant** — the same slope for males and females (additive ⇒ parallel lines), but the two sexes sit on
  **different intercepts**, so equal education does **not** imply equal predicted wage.
- **(C) Categorical `occupation` + ANOVA.** `lm(wage ~ factor(occupation))` (occupation 1 = reference)
  shows levels 2, 3, 4, 6 differing notably from baseline. `anova()` gives one F-test, `p ≈ 4.12e-21` ⇒
  **at least one occupation's mean wage differs.** (See the [ANOVA subsection](#anova--one-overall-test-for-a-categorical-predictor).)

## Activity 4 (Jul 16) — interactions & LINE diagnostics → *Topic 2 Interactions / Topic 3 Diagnostics*

- **(A) Does the education–wage slope depend on sex?** `lm(wage ~ education * sex)`. The `education:sex`
  interaction has **p ≈ 0.273 > 0.05** ⇒ **fail to reject `H0: β₃ = 0`** ⇒ **no** evidence the slopes differ;
  the additive (parallel) model suffices. Note: once an interaction is in the model, `b1` is only the
  **reference group's** slope.
- **(B) Does it depend on occupation?** `lm(wage ~ education * factor(occupation))`; use `anova()` on the
  interaction block. Some `education:occupation` terms are significant ⇒ the education–wage slope **may
  depend on occupation.**
- **(C) LINE diagnostics + fix.** For `lm(wage ~ education + factor(occupation) + sex)`:
  - `plot(fitted(model), resid(model))` → residual spread **grows** as fitted values grow — a **funnel** ⇒
    **heteroscedasticity** (violates **E**).
  - `plot(model, 2)` → Q-Q points **drift off the diagonal** ⇒ errors **not Normal** (violates **N**).
  - **Fix:** refit with a **log-transformed response** `lm(log(wage) ~ education + factor(occupation) + sex)`.
    The residual plot now has **constant spread** and the Q-Q plot **hugs the diagonal** — the classic
    `log(Y)` variance-stabilizing fix from Topic 3.

> **Activities 5–12 continue on the same `wage` data** (with one Poisson detour) and march through the
> **post-midterm** topics. They're your own worked answers — great "here's the exact style of the exam
> question" review.

## Activity 5 (Jul 21) — multicollinearity & VIF → *Topic 3* (wage)

Diagnosing collinearity among the wage predictors before trusting any coefficients.

- **(A) Detect:** pairwise correlations show **`age` & `experience` almost perfectly correlated
  (r ≈ 0.978)** (and a weak `experience`–`education` link, −0.35). Then **VIF/GVIF** on the model flags
  **`experience`** with a huge (G)VIF — well above the `√5` and `5` thresholds — while `education` and
  `age` sit below them.
- **(B) Fix:** **drop `experience`** (the collinear continuous variable). After removing it, **all GVIFs
  fall below `√5`** ≈ 2.23.
- **(C) Causation:** this is **observational** data (the traits already exist; nothing was randomly
  assigned — and randomizing someone's education/sex would be impossible/unethical), so **no causal
  claim** — association only. Concept: [Multicollinearity](#topic-3--multicollinearity).

## Activity 6 (Jul 23) — logistic regression, one predictor → *Topic 4* (wage)

Here the response is turned **binary**: is a person's wage **above/below average**?
`glm(above_avg ~ education, family = binomial)`.

- `education` is highly significant (**p ≈ 1.86e-13**). The estimate **0.3017** is on the **log-odds**
  scale; exponentiating, `e^0.3017 ≈ 1.35`, so **each extra year of education multiplies the odds of
  an above-average wage by ~1.35 → a ~35% increase in the odds.** A clean demonstration of the odds-ratio
  interpretation. Concept: [Topic 4 — coefficients](#interpreting-coefficients--three-scales-this-is-the-whole-exam).

## Activity 7 — logistic with two predictors + prediction → *Topic 4* (wage)

`glm(above_avg ~ education + sex, family = binomial)` (**coding: 0 = male, 1 = female**).

- **(A)** Both significant: `education` p ≈ 1.41e-13, `sex` p ≈ 2.89e-05. More education → higher odds of
  above-average wage (`+0.309`); **being female is associated with lower odds** (`sexfemale = −0.815`),
  equivalently males have higher odds.
- **(B) Prediction:** for a **female with 16 years of education**, plug into `p = e^L/(1+e^L)` →
  **≈ 49.6%** probability of an above-average wage. (This is the by-hand log-odds→probability calc the
  exam may ask for.) Concept: [prediction scale](#prediction--fitted-values-which-scale--a-favorite-trap).

## Activity 9 (Jul 30) — Poisson regression + overdispersion → *Topic 5* (CD4 counts)

A **Poisson** detour on a medical dataset: modelling **CD4 cell counts** by treatment arm (`trarm`).

- **(A)** `trarm` is highly significant (**p ≈ 2e-16 < 0.05**) → the treatment arm is associated with CD4
  counts.
- **(B) Overdispersion:** refit with **`quasipoisson`** → **dispersion ≈ 70.09**, wildly above 1 ⇒
  **severe overdispersion**, so the plain Poisson SEs/p-values can't be trusted (use the quasi-Poisson
  fit). A textbook "Poisson usually over-disperses" case. Concept:
  [Overdispersion](#residuals--overdispersion--poisson-usually-over-disperses).

## Activity 10 (Aug 4) — goodness of fit & the F-test → *Topic 6* (wage)

Comparing two nested linear models of `wage`.

- **(A) Adjusted `R²`:** model 2 (**adds `sex`**) has **adj `R²` = 0.185** vs. model 1's **0.144** —
  and because it's *adjusted*, the rise isn't just from adding a variable, so model 2 genuinely fits
  better. (Note: adj `R²` alone doesn't tell you the addition is *significant*.)
- **(B) F-test (`anova`):** adding `sex` cuts the Sum of Squares by **598.2** with **p ≈ 1.95e-07 < 0.05**
  ⇒ **reject H0** that `sex` has no effect → model 2 is **significantly** better. The clean pairing of
  *descriptive* (adj `R²`) with a *test* (F). Concept: [F-test](#part-2--comparing-nested-models-the-f-test).

## Activity 11 (Aug 6) — stepwise selection + deviance test → *Topic 8 / Topic 7* (wage)

- **(A) Backward stepwise** (`step()`, start full → drop one at a time by AIC) keeps **every predictor
  except `south`**. But **AIC-selected ≠ all significant**: by p-value only `sex, union, race,
  occupation, sector` are significant; `education, experience, age` were *kept* yet aren't individually
  significant — and their **identically inflated SEs** hint at leftover **multicollinearity**.
- **(B) Deviance test** for whether `south` belongs: adding `south` drops the deviance by only **1.84**,
  **p = 0.174 > 0.05** ⇒ **fail to reject** the smaller model → **not enough evidence to add `south`**.
  (`H0`: the reduced model suffices.) Concept: [deviance test](#deviance-test--comparing-nested-glms-the-χ²-test).

## Activity 12 (Aug 11) — LASSO vs. stepwise selection → *Topic 8* (wage)

Selecting wage predictors two ways and contrasting them.

- **(A) LASSO** (λ chosen by **cross-validation**) selects **education, south, sex, union, age, race,
  occupation, sector, marr**.
- **(B) Backward stepwise** (AIC) selects **education, south, sex, experience, union, occupation** —
  a **different set** (stepwise drops `age, race, sector, marr` but keeps `experience`, which LASSO
  dropped).
- **Why they differ:** **LASSO is smooth** — it shrinks coefficients continuously toward 0 by the λ
  penalty; **stepwise is binary** — a variable is fully in or fully out, decided greedily by AIC. Two
  different mechanisms → two different models, and that's expected (there's "no single perfect model").
  Concept: [Topic 8 — Model Selection](#topic-8--model-selection).

---

# TUTORIALS — CASCHOOLS WALKTHROUGH

The two tutorials build one worked example on the **CASchools** dataset (420 California districts):
`read` (avg reading score) vs `income` (district avg income, in \$1000s), later adding `grades`
(2 levels: **KK-06**, **KK-08**). They mirror the topic arc (SLR → inference → additive → interaction)
and introduce **generative modelling**, **EDA**, and **statistical vs. practical significance**.

## Tutorial 01 — generative modelling, EDA, SLR + inference + bootstrap

- **Framing:** regression **approximates the mechanism that generated the data**; the `b`'s are unknown
  true parameters we estimate. Warm-ups reinforce: SLR is **not** an *exact* linear function (it has an
  error term `e`); `e` carries **omitted explanatory variables + noise**; the true `b1` is **unknown**
  and must be estimated.
- **EDA first (from *The Art of Data Science*):** the analysis cycle is **iterative ("epicycles"),** not
  linear. Use an **EDA checklist** (formulate the question, read the data, check packaging, look at
  top/bottom, check your "n"s) and **`GGally::ggpairs()`** for an at-a-glance matrix of distributions +
  pairwise relationships. `ggpairs()` beats base `pairs()` because it **picks the right plot per variable
  type**, shows **distributions on the diagonal**, and reports **correlations** instead of duplicating
  scatterplots. `income` here is **right-skewed.**
- **SLR:** `read ~ income` is **positive and (roughly) linear**; fit with `lm()`, read with `tidy()`.
  Slope ≈ **1.94** ⇒ *"each extra \$1000 of district income is associated with ≈ 1.94 more reading-score
  points, on average."*
- **Inference:** `income` is significant (p < 0.05); the 95% CI for its slope is ≈ **(1.75, 2.13)** —
  excludes 0, consistent with the test. The `lm` p-values come from **classical theory**, *not*
  bootstrap.
- **Sampling distribution = the distribution of `b1_hat`** (the *estimator* of the slope) — **not** the
  distribution of `Y`, of the true `b1`, or of `X`. Common exam trap.
- **Bootstrap:** resample the data **B = 10 000** times, refit each time, collect `boot_intercept` /
  `boot_slope` in `lm_boot`; the spread approximates the sampling distribution and its **percentiles**
  give CIs (e.g. 2.5% / 97.5% for 95%, or 5% / 95% for a 90% CI). Useful when you don't want to assume
  Normal errors.

## Tutorial 02 — MLR with a categorical input & interactions

- **Setup:** `grades` is a 2-level factor; `lm()` picks **KK-06 as the baseline** (first level) and makes
  **1 dummy** (`gradesKK-08`). *(Make sure a categorical is a `factor`, or `lm` won't dummy-code it.)*
- **Additive** `lm(read ~ income + grades)` → **two parallel lines** (same slope, different intercepts).
  The `income` coefficient ≈ **1.93** = expected change in `read` per +\$1000 income, **holding grades
  constant** (same for both school types).
- **Interaction** `lm(read ~ income * grades)` → **4 coefficients**, two lines with **different slopes
  and intercepts**:
  - `income` ≈ **2.02** = slope for the **reference** group (KK-06).
  - `income:gradesKK-08` ≈ **−0.11** = **difference in slopes**; so KK-08's slope = `2.02 + (−0.11) =`
    **1.91**. The interaction is **not significant** (p ≈ 0.68 > 0.10) ⇒ **no evidence the slopes
    differ**; prefer the additive model. Since it's non-significant, interpret `−0.11` only *with the
    caveat* that it's indistinguishable from 0.
- **Interaction = two SLRs in one (the Q2.7 punchline):** fitting a separate SLR on **only KK-06** rows
  gives the **same `income` slope (2.02)** as the interaction model's `income` row (KK-06 is the
  reference, so its dummy is 0). A separate SLR on **only KK-08** rows gives **1.91**, which the
  interaction model reproduces as `income + income:gradesKK-08`. The interaction coefficient (−0.11) by
  itself is a **slope *gap*, not a slope.**
- **Statistical vs. practical significance:** see the
  [Inference section](#statistical-vs-practical-significance-tutorial-02--likely-exam-material) — a
  result can be statistically significant yet too small to matter, and vice versa.

## Tutorial 03 — multicollinearity in practice + causality

Tutorial 03 is the **Topic 3 lab**, in two halves (both on CASchools / a simulation):

- **Part 1 — multicollinearity workflow (CASchools, response `score` = avg of math & read):** visualize
  predictor correlations (`ggpairs` + a `geom_tile` **heatmap**), fit `lm(score ~ .)`, get **`car::vif()`**,
  then **drop the higher-VIF member of the most-correlated pair** and recheck. Here only **`lunch`** had
  VIF > 5 (≈ 5.7), sat in the top-correlation pair (`calworks`–`lunch`, r = 0.74), and was dropped — after
  which **all VIFs dropped below ~2.** Removing it **shifted the coefficients of the variables correlated
  with it** and **lowered their p-values** (SE de-inflation). Full detail in the
  [Multicollinearity section](#the-full-workflow-in-practice-tutorial-03--caschools).
- **Part 2 — causality (the TikTok confounding sim):** the ad/`athlete` simulation with the three key
  estimates — **naive 9.83**, **adjusted 7.92**, **randomized 8.03** (true = 8). See
  [The confounding simulation](#the-confounding-simulation-tutorial-03--with-the-actual-numbers) and the
  **two fixes** (adjust vs. randomize) beside it.

## Tutorial 04 — binary responses (logistic) → *Topic 4* (`Default` credit-card data)

Tutorial 04 is the **logistic lab**, on the **`Default`** dataset from *Introduction to Statistical
Learning* — **n = 10,000** customers with `default` (Yes/No — the binary response), `student` (Yes/No),
`balance` (credit-card balance), and `income`.

- **Odds & odds ratios worked cleanly here:** for a binary predictor, `odds_female = e^b0`,
  `odds_male = e^(b0+b1) = e^b0·e^b1`, so the **odds ratio between groups is `e^b1`** — this tutorial is
  where the "exponentiated coefficient = odds ratio" identity is made concrete.
- **Workflow:** `glm(default ~ balance + student + income, family = binomial)`, read log-odds vs. odds,
  test coefficients with the **Wald z**, and do **model diagnostics** (Pearson/deviance residuals, and
  the reminder that residual plots are weak → lean on overdispersion).
- A natural exam-style task from this data: predict the **probability** of default for a customer with a
  given balance (compute `L`, then `p = e^L/(1+e^L)`). Concept:
  [Topic 4 — Logistic](#topic-4--logistic-regression).

## Tutorial 05 — count responses (Poisson) → *Topic 5* (`galapagos` species)

Tutorial 05 is the **Poisson lab**, on the **`galapagos`** dataset (`faraway`): **30 Galápagos islands**,
response = the **number of plant species** on each island, predicted from island characteristics (area,
elevation, distance to nearest island, etc.).

- Reinforces the **log link** `log(E[Y|X]) = b0 + b1x1 + …` ⇔ `E[Y|X] = e^(…)` (always positive → no
  range problem), coefficients interpreted as **rate ratios** after exponentiating, Wald inference, and
  the **overdispersion** check (`quasipoisson`) — counts of species across very different island sizes
  are a natural over-dispersion setting. Concept: [Topic 5 — Poisson](#topic-5--poisson-regression).

## Tutorial 06 — goodness of fit & nested models → *Topic 6* (protein~mRNA, models 1–5)

Tutorial 06 is the **nested-models lab**, continuing the **protein~mRNA** case study from Worksheet 06 on
a 3-gene dataset (`dat_3genes`). It lays out **five nested models** and compares them — a perfect map of
Topic 6's tools:

| Model | Form | What it adds |
| --- | --- | --- |
| model.1 | `prot = b0 + e` | null (intercept only) |
| model.2 | `prot = b0 + b1·mrna + e` | mRNA alone |
| model.3 | `prot = b0 + b2·gene2 + b3·gene3 + e` | gene dummies only |
| model.4 | `prot = b0 + b1·mrna + b2·gene2 + b3·gene3 + e` | **additive** |
| model.5 | model.4 `+ b4·gene2·mrna + b5·gene3·mrna` | **interaction** |

- **`glance()`** gets `R²` and **adjusted `R²`** for each; comparing model.4 vs model.5 shows the key
  lesson: **model.5 has the larger `R²`** (adding predictors always raises `R²`) but model.4's
  **adjusted `R²` is essentially as high or higher** — so the extra interaction terms don't earn their
  keep. Use **adjusted `R²` (not `R²`) to compare different sizes**.
- **`anova(reduced, full)`** runs the **F-test** for whether a block of terms significantly helps. Concept:
  [Topic 6 — Goodness of Fit](#topic-6--goodness-of-fit).

## Tutorial 07 — stepwise selection in MLR → *Topic 6 / Topic 8* (Ames housing + used cars)

Tutorial 07 is the **stepwise-selection lab**. It opens by splitting the goal in two — **inference
(generative)** vs. **prediction** — because *that choice decides which metric you use.*

- **Generative-model metrics (in-sample):** `R²`, **adjusted `R²`** (compare different sizes), in-sample
  **MSE**, and **nested-model `F`-tests** to select variables.
- **Predictive-model metrics (out-of-sample — the tutorial's emphasis):** **test MSE** and **test
  RMSE**, computed on a **held-out test set** — `MSE_test = (1/n_new) Σ(y_new − ŷ_new)²`,
  `RMSE_test = √MSE_test`. **You must not evaluate on the training data.** You can compute RMSE by hand
  (`sqrt(mean((y − pred)²))`) or with `yardstick::metrics()` / `rmse()`; the tutorial has you do it
  **manually** for both the full and a reduced model and compare (interestingly the **full** model won on
  *this* split — a reminder that a single train/test split is itself noisy).
- **`regsubsets()` (package `leaps`)** — best-subset / **forward & backward** selection.
  `regsubsets(y ~ ., data = train, nvmax = p, method = "forward")`; **`nvmax` = the largest model size to
  search** (set it to the number of predictors so every size 1…p is evaluated — the default is only 8!).
  `summary(fit)` returns one "best" model per size plus vectors **`$rsq`, `$rss`, `$adjr2`, `$cp` (Mallows'
  Cp), `$bic`** and the `$which` selection matrix — you pick the best size by **max adjusted `R²`** or **min
  `Cp` / `BIC`**.
- **`stepAIC()` (package `MASS`)** — stepwise by information criterion: `direction = "forward" /
  "backward" / "both"`, with **`k = log(n)` ⇒ BIC** and **`k = 2` ⇒ AIC** (smaller = better).
- **`regsubsets` vs. `stepAIC` on categoricals (the tutorial's key subtlety):** `regsubsets` evaluates
  each **dummy column separately**, so it can keep some levels of a factor and drop others (and *which*
  depends on the arbitrary reference level) — awkward for inference. **`stepAIC` adds/removes a whole
  categorical variable at once**, which is usually what you want.
- **Post-selection caveat (stated in the tutorial, bridges to Topic 8):** `summary()` on the selected
  model gives inference computed on the **same data used to select it** — those p-values/CIs are **not
  valid** (double-dipping). See [Topic 8 Part 2](#part-2--the-post-inference-problem-double-dipping).

---

# MASTER CHEAT SHEET

### Coefficient interpretation by model type

| Model                               | Form                             | What the coefficients mean                                                               |
| ----------------------------------- | -------------------------------- | ---------------------------------------------------------------------------------------- |
| **SLR (continuous X)**        | `Y = b0 + b1*X`                | `b1` = expected change in Y per +1 X; `b0` = mean Y at X=0                           |
| **2-level categorical**       | `Y = b0 + b1*D`                | `b0` = reference mean; `b1` = difference of means; test = 2-sample t-test            |
| **k-level categorical**       | `Y = b0 + b1*D1 + ...`         | `b0` = reference mean; each `b` = that level minus reference                         |
| **Additive (cat + cont)**     | `Y = b0 + b1*D + b2*X`         | parallel lines:`b0`=ref intercept, `b1`=intercept gap, `b2`=**common slope** |
| **Interaction (cat × cont)** | `Y = b0 + b1*D + b2*X + b3*DX` | `b2`=ref slope, `b3`=slope gap, other slope = `b2+b3`; **non-parallel**      |

### Counting coefficients

- categorical with `k` levels → `k − 1` coefficients
- interaction of A and B → (coefs of A) × (coefs of B)
- 2-level cat × continuous → 1 extra coefficient

### `tidy()` columns

`estimate` = effect size · `std.error` = wobble · `statistic` = est/SE · `p.value` = evidence strength ·
`conf.low/high` = CI. **In-class equivalent:** `moderndive::get_regression_table()` — same columns
(`std_error`, `p_value`, `lower_ci`, `upper_ci`), 95% CI shown by default.

### ANOVA vs. coefficient t-tests

Coefficient table = k − 1 **separate** t-tests (each level vs. baseline). `anova(model)` = **one joint
F-test** — "does this categorical variable (or interaction block) matter *at all*?" Small p ⇒ at least one
group differs; use the coefficient table to see which.

### p-value literacy

Small p = **strong evidence** against H0, **NOT** a big effect. Effect size = `estimate`; strength = `p.value`. Read both.

### Statistical vs. practical significance

**Statistical** = evidence the effect isn't 0 (p-value / CI). **Practical** = the effect is **big enough
to matter** (magnitude of `estimate`). Big `n` ⇒ tiny effects can be statistically significant yet
practically trivial. Report **both**.

### CI literacy

"95% of such intervals (over repeated samples) contain the truth" — **not** "95% probability the truth is here."

### The one equivalence to memorize

For any coefficient `bj`, these three say the **same thing** at the 5% level:
**95% CI excludes 0** ⇔ **|z| = |b_hat / SE| > 1.96** ⇔ **p < 0.05** ⇒ reject `H0: bj = 0`.
(Confidence interval and hypothesis test are equivalent — the review deck states this explicitly.)

### Two ways to do inference

1. **Theory** (`lm`) — exact version uses a t-distribution with `n−k` df; **this course simplifies to
   the standard Normal (z)** since t ≈ Normal. Justified by Normal errors or the CLT.
2. **Bootstrap** — resample **with replacement**, same size `n`, many times; empirical sampling
   distribution. Best for **non-Normal data / small `n`**, gives **more reliable SEs**.

### LINE assumptions & fixes

- **L**inear → residuals-vs-fitted (want no pattern) → add `X^2`/`log`
- **I**ndependent → design / residual runs → time-series methods (violation ⇒ invalid SE/CI/p)
- **N**ormal → Q-Q plot (least severe; CLT/bootstrap saves you)
- **E**qual variance → residuals-vs-fitted funnel shape → transform Y (violation ⇒ invalid SE/CI/p)

### Multicollinearity

Predictors carrying the same info → inflated SEs, `NA`s in extreme cases. Diagnose with **VIF/GVIF > 5–10**;
fix by **dropping or combining** variables.

### Causation

Need **randomized experiment** (CRD balances even unobserved confounders = gold standard). Observational
data → beware **confounding, reverse causality, Simpson's paradox** → association only.

### GLMs — pick the model by the RESPONSE type

| Response | Model | Link (canonical) | Models | `glm(family=)` | Variance |
| --- | --- | --- | --- | --- | --- |
| continuous | linear (MLR) | identity | mean `E[Y]` | `gaussian` | `σ²` (constant) |
| binary 0/1 | **logistic** | **logit** `log(p/(1−p))` | **log-odds** | `binomial` | `p(1−p)` |
| count 0,1,2… | **Poisson** | **log** `log(λ)` | **log-mean** | `poisson` | `λ` (= mean) |

- **No error term** in a GLM; estimated by **MLE / iterative algorithm** (not LS).
- **`factor()` your numeric categoricals** or `glm` fits a meaningless slope on the codes.

### GLM coefficient interpretation

- **Logistic** — raw `b` = change in **log-odds**; `e^b` = **odds ratio** (multiply the odds); `(e^b−1)·100%`
  = % change in odds. `e^(intercept)` = baseline odds.
- **Poisson** — raw `b` = change in **log-mean**; `e^b` = **rate ratio** (multiply the mean count);
  `(e^b−1)·100%` = % change in the mean count.
- **Additive** ⇒ "holding others constant at any value" OK. **Interaction** ⇒ effect **depends on** the
  other variable; to combine, **multiply** exponentiated coefficients (`e^(b2+b3)=e^b2·e^b3`).
- **Predict:** logistic `type="link"` = log-odds (default), `type="response"` = probability. Fitted:
  `augment`'s `.fitted` = log-odds, but `$fitted` = probabilities.

### GLM inference & diagnostics

- **Wald statistic** `z = b_hat/SE ~ N(0,1)` (CLT). Same **|z|>1.96 ⇔ CI excludes 0 ⇔ p<0.05**.
- **Residual plots ~useless** (discrete response, 2-line pattern, non-constant variance) → use **Pearson**
  residuals + **binned** plot. **Overdispersion** is the key diagnostic.
- **Overdispersion:** refit `quasibinomial`/`quasipoisson`, check **dispersion ≈ 1** (fixes SEs, not
  estimates). **Logistic: usually fine** (Titanic ≈ 0.98). **Poisson: usually over-dispersed** (Bikeshare
  ≈ 90.6!).

### Goodness of fit — LINEAR models (Topic 6)

- **TSS = ESS + RSS** (intercept + LS). `R² = 1 − RSS/TSS = ESS/TSS` = **proportion of variance explained**;
  `R² = r²` in SLR.
- `R²` is **in-sample**, **not a test** (no distribution), and **always ↑ with more predictors** ⇒ can't
  compare different sizes. Use **`adj R²`** (penalizes `p`) to compare sizes; **AIC/BIC** smaller = better.
- **F-test** (nested only): **`glance()`** = full vs. intercept-only (`H0: all b=0`); **`anova(reduced,
  full)`** = any nested pair (`H0`: extra block = 0). `F = t²` when `p=1`.
- **Significant model ≠ good prediction ≠ a given predictor matters** (protein~mRNA: `gene`, not mRNA,
  carried it).

### Goodness of fit — GLMs (Topic 7)

`R²`/`adjR²`/`RSE`/`MSE`/`F`-test are **LINEAR-only**. For logistic/Poisson use **DEVIANCE** (generalized
RSS; **lower = better**; perfect/saturated fit = overfit = bad). Compare nested GLMs with the **deviance
test**, `χ²(d)` distribution, via **`anova(..., test="Chisq")`**.

### Model selection (Topic 8)

- **Stepwise** = greedy, order-dependent, coefficients jump 0↔value. **Regularization** = smooth shrinkage
  via a penalty `λ·penalty(b)`.
- **LASSO (L1)** shrinks coefficients **to exactly 0** ⇒ selects + trains at once. **Ridge (L2)** shrinks
  but **never to 0** ⇒ no selection. `λ=0` ⇒ ordinary LS. Tune `λ` by **CV** minimizing test MSE
  (`cv.glmnet`; `lambda.min` vs `lambda.1se`). **Standardize inputs.** Biased on purpose:
  `MSE=Var+Bias²`, trade bias for variance to predict better.
- **Post-inference / double-dipping:** can't **select AND infer on the same data** (Type I error inflates).
  **Fix: split the data.** **postLASSO** (LS on LASSO-selected vars) is **unbiased** but still needs a split
  for valid inference.

### Prediction uncertainty (Topic 9)

- Predictions are **random** (depend on the sample). Two intervals, **both centred at `ŷ`**:
- **CIP** (`interval="confidence"`) → predicts the **average `E[Y|X]`**; **one** source (sample-to-sample);
  say "**confidence**"; **narrower**.
- **PI** (`interval="prediction"`) → predicts an **actual new `Y`**; **two** sources (estimation **+** error
  `e`); say "**probability**"; **wider**.
- **PI is always wider than CIP** — predicting one actual value is harder than predicting the average.
  `geom_smooth` band = the CIP band.

### The one-liner that ties it together

> Regression estimates the **average of Y given X** (or a **link** of it — log-odds for binary, log-mean
> for counts, giving **GLMs**), fit by **least squares** (`lm`) or **maximum likelihood** (`glm`). We
> quantify coefficient uncertainty with **SEs → CIs/tests**, **check assumptions** (LINE +
> multicollinearity for `lm`; overdispersion for GLMs), judge fit with **`R²`/`adjR²`/F-test** (linear) or
> **deviance** (GLMs), **select** variables carefully (**LASSO**, and never select-and-infer on the same
> data), report prediction uncertainty with **CIP vs PI**, and only claim **causation when the design
> (randomization) earns it.**
