# STAT 301 — Midterm Master Study Guide

*Covers Topic 1 (Simple Linear Regression), Topic 2 (Multiple Linear Regression),
and Topic 3 (Diagnostics, Multicollinearity & Causality).*

## Source files used to generate this guide

- `slides/topic1_simple_linear_regression_part1.pdf`
- `slides/topic1_simple_linear_regression_part2.pdf`
- `slides/topic2_MLR_part1.pdf`
- `slides/topic2_MLR_part2.pdf`
- `slides/topic3_d1_diagnostics.pdf`
- `slides/topic3_d2_designs.pdf`
- `worksheets/worksheet_01.ipynb` (SLR estimation, inference & bootstrapping — cancer data)
- `worksheets/worksheet_02.ipynb` (categorical inputs, additive MLR & interactions — cancer data)
- `worksheets/worksheet_03.ipynb` — model assumptions & causality, explored by **simulation** (known true params)
- `tutorials/tutorial_01.ipynb` — generative modelling, EDA, SLR estimation/inference/bootstrap (CASchools data)
- `tutorials/tutorial_02.ipynb` — MLR with categorical inputs & interactions (CASchools: `read ~ income * grades`)
- `in-class/activity1.ipynb` + `STAT301_activity1.pdf` — SLR estimation & correlation (wage data, Jul 7)
- `in-class/activity2.ipynb` + `STAT301_activity2.pdf` — SLR inference: significance, CI, z/p (wage data, Jul 9)
- `in-class/activity3.ipynb` + `STAT301_activity3.pdf` — additive MLR, `factor()` dummies & **ANOVA** (wage data, Jul 14)
- `in-class/activity4.ipynb` + `STAT301_activity4.pdf` — interactions & LINE diagnostics + `log()` fix (wage data, Jul 16)
- `midterm/review-slides.pdf` — the **Jul 21 review deck** (recaps the whole course as one MLR framework)
- `midterm/mt-info.md` — official exam logistics

*(Tutorial 03's confounding simulation is referenced in the Causality section, as summarized from the Topic 3 designs deck. The four in-class activities all use the **`wage.txt`** dataset — `wage ~ education`, later adding `sex` and `occupation` — and are walked through in their own section below.)*

> **How to read this guide.** Math is written in plain text / code style (e.g. `Y = b0 + b1*X + e`)
> so it's readable anywhere. The big idea of this whole course: **regression models the *average*
> of a response, and we interpret what the coefficients *mean* — association, not causation.**

---

# EXAM LOGISTICS & WHAT'S TESTED

**When/where:** Thursday **July 23, 2026, 3:45–4:45pm (60 minutes)**, in person, **ESB1012**. Hard
copies handed out; then 15 min (until 5:00pm) to upload a **single PDF** to Canvas
(filename `LastName-FirstName.pdf`). Also hand in the hard copy. Covers everything **up to and
including the Tuesday July 21 review class.**

**Format — read this carefully:**

- **Written answers only. There are NO multiple-choice questions.** You explain, interpret, and show
  reasoning in words.
- The exam tests **understanding of the basics + critical thinking**, *not* tedious computation or
  heavy math. Expect: **interpret an R output**, say **what a model component means**, and **explain a
  concept in the context of the given dataset.**
- **R code is not directly tested**, but you must understand the R *outputs* shown in class (e.g. a
  `get_regression_table()` / `lm` summary, an ANOVA table, VIF values, residual & Q-Q plots).
- **Some simple calculations** — **bring a simple calculator.**
- **Marking: 70% for correct procedure / key steps, 30% for the correct answer.** ⇒ *Always show your
  steps*, and **write word-answers clearly** or lose marks.
- **Closed book/notes**, but you may bring **one letter-size sheet (both sides, written or typed).**

**Framing tip from the review deck:** the review treats **everything as one Multiple Linear Regression
framework** — *SLR is just the special case with one predictor (p = 1)*. So master the general
`Y = b0 + b1*X1 + ... + bp*Xp + e` interpretation and the special cases fall out of it.

> **One-sheet cheat-sheet candidates** (what's worth putting on your allowed page): the coefficient-
> interpretation table, the LINE assumptions + their fixes + consequences, the interaction 4-coefficient
> table, VIF/GVIF thresholds, and the CI ⇔ hypothesis-test ⇔ p-value equivalence. See the
> [Master Cheat Sheet](#master-cheat-sheet).

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
10. [Worksheet Practice — R Code &amp; Extra Nuggets](#worksheet-practice--r-code--extra-nuggets) *(now includes Worksheet 03)*
11. [In-Class Activities — Wage Dataset Walkthrough](#in-class-activities--wage-dataset-walkthrough)
12. [Tutorials — CASchools Walkthrough](#tutorials--caschools-walkthrough)
13. [Master Cheat Sheet](#master-cheat-sheet)

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

# WORKSHEET PRACTICE — R CODE & EXTRA NUGGETS

The two worksheets use the **`US_cancer_data`** dataset (`TARGET_deathRate` = cancer deaths per 100 000;
`povertyPercent`; `PctPrivateCoverage`; `state`). They are where the theory above becomes runnable R code.
Below is everything the worksheets add or reinforce — **great exam-prep material because it's exactly the
style of question you'll be asked.**

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

---

# IN-CLASS ACTIVITIES — WAGE DATASET WALKTHROUGH

All four in-class activities run on **`in-class/data/wage.txt`** (`read.table(..., header = TRUE)`;
columns include `wage`, `education`, `sex`, `occupation`). They march through the whole course arc on
**one dataset** — SLR → inference → additive MLR/ANOVA → interactions/diagnostics — so they're the most
faithful preview of exam-style questions. Each activity's coefficient table is read with
`moderndive::get_regression_table()`.

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

### The one-liner that ties it together

> Regression estimates the **average of Y given X**, `lm` fits it by **least squares**, we quantify
> uncertainty with **SEs from theory or bootstrap**, we **check LINE + multicollinearity** before trusting
> the numbers, and we only claim **causation when the design (randomization) earns it.**
