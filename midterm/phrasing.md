# Phrasing Bank — how to word written answers

*Fill-in-the-blank templates for the things STAT 301 asks you to **state in words.** The exam is
written-answer and graders check wording (e.g. "associated with" vs. "causes"), so use these. Each entry:*

- **Template** — the sentence with `[slots]` to fill.
- **Example** — filled in with course data.
- **Why / caveat** — the reasoning and the trap to avoid.
- **Avoid** — the wrong version that loses marks.

Drawn from `master.md`, the tutorials/worksheets, and the notecards. Datasets: **wage** (`wage~education`),
**CASchools** (`read~income`, `grades`), **US cancer** (`TARGET_deathRate~povertyPercent`, `state`),
**TikTok** ad sim.

---

# CONTENTS
1. [Coefficient interpretation](#1--coefficient-interpretation)
2. [Inference — CIs, tests, p-values](#2--inference--cis-tests-p-values)
3. [Correlation, association & causation](#3--correlation-association--causation)
4. [ANOVA](#4--anova)
5. [Diagnostics (LINE)](#5--diagnostics-line)
6. [Multicollinearity](#6--multicollinearity)
7. [Prediction & extrapolation](#7--prediction--extrapolation)
8. [Master rules of thumb](#8--master-rules-of-thumb)

---

# 1 — COEFFICIENT INTERPRETATION

## 1.1 SLR slope (continuous predictor)
- **Template:** "A **[one-unit]** increase in **[X]** is **associated with** an expected **[increase/decrease]**
  of **[b̂ + units]** in **[Y]**, on average."
- **Example:** "A one-year increase in education is associated with an expected increase of about \$0.75/hour
  in wage, on average."
- **Why:** it's an *average* association across the data, not an individual guarantee, and observational data
  can't support causation. "Associated with" is the safe verb.
- **Avoid:** "Each extra year of education **causes** / **raises your** wage by \$0.75." (causation + individual)

## 1.2 Intercept
- **Template:** "The expected **[Y]** when **[X] = 0** is **[b̂0 + units]**."
- **Example:** "The model's expected wage at 0 years of education is [b̂0]; this is an extrapolation and not
  meaningful on its own."
- **Why:** often `X = 0` is outside the data / nonsensical (a 0 mm flipper), so flag it.
- **Avoid:** interpreting the intercept as meaningful when `X = 0` never occurs in the data.

## 1.3 MLR slope ("holding others constant")
- **Template:** "Holding **[all other predictors]** constant, a **[one-unit]** increase in **[X]** is
  **associated with** an expected change of **[b̂]** in **[Y]**."
- **Example:** "Holding grade span constant, each \$1000 increase in district income is associated with an
  estimated 1.93-point increase in reading score."
- **Why:** MLR coefficients are *partial* effects — only interpretable relative to the other predictors in
  the model. In an **additive** model, "holding constant" works at *any* value of the others.
- **Avoid:** dropping "holding others constant"; or claiming it in an **interaction** model (see 1.9).

## 1.4 Two-level categorical (reference vs. other)
- **Template:** "The mean **[Y]** for **[level]** is **[b̂]** **[higher/lower]** than for **[reference level]**
  (the baseline)."
- **Example:** "Mean mortality in California is 34.63 lower than in Alabama (the reference level)."
- **Why:** the coefficient is a **difference of group means**, not a group's absolute mean. Testing it = a
  two-sample t-test.
- **Avoid:** "The mean mortality in California is 34.63." (that's a *difference*, not the level's own mean)

## 1.5 k-level categorical
- **Template:** "Relative to **[reference]**, the mean **[Y]** for **[level j]** is **[b̂j]** **[higher/lower]**."
- **Example:** "Relative to occupation 1, occupation 3 has a mean wage that is [b̂] higher."
- **Why:** every non-reference coefficient is a comparison **against the baseline**, never an absolute mean,
  and never a comparison between two non-reference levels directly.
- **Avoid:** comparing two non-reference levels by reading a single coefficient.

## 1.6 Additive model (parallel lines)
- **Template:** "`b0` = intercept of the **[reference]** line; `b1` = the **vertical gap** between the lines
  (**[other]** minus **[reference]**); `b2` = the **common slope** shared by both groups."
- **Example:** "For `read ~ income + grades`: KK-06's line has intercept b0, KK-08's line is shifted by b1,
  and both share the income slope 1.93."
- **Why:** additive ⇒ **parallel lines** (same slope, different intercepts); 3 coefficients describe 2 lines
  because the slope is forced equal.
- **Avoid:** saying the groups have different slopes in an additive model (they don't).

## 1.7 Interaction — reference-group slope (main continuous term)
- **Template:** "In the **[reference group]**, a one-unit increase in **[X]** is associated with a **[b2]**
  change in **[Y]**."
- **Example:** "In KK-06 schools (the reference), each \$1000 of income is associated with a 2.02-point
  increase in reading score."
- **Why:** in an interaction model the main continuous coefficient is **only the reference group's slope**,
  not everyone's.
- **Avoid:** "Each \$1000 of income raises reading by 2.02 **for all schools**." (that's ref group only)

## 1.8 Interaction — slope gap & other-group slope
- **Template:** "`b3` = the **difference in slopes** (**[other]** minus **[reference]**); the **[other
  group]**'s actual slope is **`b2 + b3`**."
- **Example:** "`income:gradesKK-08 = −0.11` is the slope gap, so KK-08's income slope is 2.02 + (−0.11) =
  1.91."
- **Why:** `b3` alone is a *gap*, not a slope; you must **add** it to the reference slope.
- **Avoid:** reporting `b3` (−0.11) as KK-08's slope.

## 1.9 Interaction — the "cannot hold constant" caveat
- **Template:** "Because the model includes an interaction, the effect of **[X]** on **[Y]** **depends on the
  value of [the other variable]**, so it cannot be interpreted 'holding the other constant.'"
- **Example:** "Since `income` interacts with `grades`, income's effect on reading differs by school type,
  so we can't state a single income effect 'holding grades constant.'"
- **Why:** interaction = the whole point is the effect *changes* across the other variable.
- **Avoid:** "holding all else constant" wording in an interaction model.

---

# 2 — INFERENCE: CIs, TESTS, p-VALUES

## 2.1 Confidence interval
- **Template:** "We are **[95]%** confident that the true **[parameter, e.g. slope β1]** lies between
  **[lower]** and **[upper]** **[units]**."
- **Example:** "We are 95% confident that the true slope for education lies between 0.596 and 0.905 dollars
  per hour."
- **Why / caveat:** the "95%" refers to the **procedure over repeated samples** — across many samples, 95%
  of intervals built this way contain the truth. Once computed, **this** interval is fixed: it either
  contains the true value or it doesn't.
- **Avoid:** "There is a 95% **probability/chance** that the true value is in this interval." (the interval
  is fixed after computing; the randomness is in the sampling, not the parameter)

## 2.2 Hypothesis test — stating the hypotheses
- **Template:** "`H0: [β_j] = 0` (no linear association between [X] and [Y]) vs. `H1: [β_j] ≠ 0` (there is
  an association)."
- **Example:** "H0: β_income = 0 vs. H1: β_income ≠ 0."
- **Why:** hypotheses are always about the **population parameter** (β), never the estimate (β̂, a computed
  number). Use two-sided unless a direction is given.
- **Avoid:** writing `H0: β̂ = 0` (never hypothesize the estimate).

## 2.3 Reject H0
- **Template:** "Since **p = [value] < α = [0.05]** (equivalently the 95% CI excludes 0 / |z| > 1.96), we
  **reject H0**: **[X]** is **statistically associated** with **[Y]**."
- **Example:** "Since p ≈ 0 < 0.05, we reject H0: education is statistically associated with wage."
- **Why:** rejecting means the data are inconsistent with "no association."
- **Avoid:** "we **accept H1** / **prove** there is an association." (we never prove/accept)

## 2.4 Fail to reject H0
- **Template:** "Since **p = [value] > α**, we **fail to reject H0**: there is **not enough evidence** of an
  association between **[X]** and **[Y]**."
- **Example:** "The interaction p = 0.273 > 0.05, so we fail to reject H0 — no evidence the education–wage
  slope differs by sex."
- **Why:** failing to reject ≠ proving H0 true; it means insufficient evidence.
- **Avoid:** "we **accept H0** / there **is no** association / H0 is **true**." (absence of evidence ≠
  evidence of absence)

## 2.5 p-value meaning
- **Template:** "The p-value is the probability, **if H0 were true**, of observing a test statistic at least
  as extreme as the one we got. **p = [value]** ⇒ **[strong/weak]** evidence against H0."
- **Example:** "p = 1e-9 is overwhelming evidence against H0; p = 0.049 is weak."
- **Why:** magnitude of p = **strength of evidence**, not size of effect.
- **Avoid:** "the p-value is the probability that **H0 is true**" / "the probability the results are due to
  chance" / "the effect size." (all false)

## 2.6 Statistical significance
- **Template:** "At the **[5]%** level, **[X]** is **statistically significantly** associated with **[Y]**
  (p < α)."
- **Example:** "At the 5% level, income is significantly associated with reading score."
- **Why:** "significant" = evidence the effect is **not zero**, nothing about its size.
- **Avoid:** equating "significant" with "large" or "important."

## 2.7 Statistical vs. practical significance
- **Template:** "The association is **statistically significant** (evidence it is not zero), but whether it is
  **practically significant** depends on whether **[b̂]** is **large enough to matter** in context."
- **Example:** "With a large sample, a 0.002-point change in reading per \$1000 could be statistically
  significant yet too small to matter practically."
- **Why:** big `n` can make trivial effects significant; read **both** the p-value and the estimate.
- **Avoid:** treating a small p-value as proof the effect is big/important.

## 2.8 Standard error / sampling distribution
- **Template:** "The standard error measures how much **[β̂]** would **vary from sample to sample** (the SD of
  its sampling distribution)."
- **Example:** "The SE of 0.079 means the education slope estimate would wobble by about that much across
  repeated samples."
- **Why:** SE = wobble of the **estimate**, NOT the scatter of data points around the line (that's σ).
- **Avoid:** "the SE measures how spread out the data points are around the line." (that's σ, not SE)

## 2.9 Bootstrap / sampling-distribution description
- **Template:** "We **resample the data with replacement** (same size n) many times, refit each time, and use
  the **spread of the estimates** to approximate the sampling distribution of **[β̂]**."
- **Example:** "Bootstrapping `read ~ income` 10,000 times gives a distribution of slopes whose 2.5th and
  97.5th percentiles form the 95% CI."
- **Why:** the bootstrap **empirically builds** the sampling distribution without assuming Normal errors.
- **Avoid:** "we take **new samples from the population**" (bootstrap resamples your **one** sample) or
  sampling **without** replacement.

---

# 3 — CORRELATION, ASSOCIATION & CAUSATION

## 3.1 Correlation coefficient
- **Template:** "**[X]** and **[Y]** have a **[weak/moderate/strong]** **[positive/negative]** linear
  correlation (r = **[value]**)."
- **Example:** "Education and wage are weakly, positively correlated (r ≈ 0.38)."
- **Why:** r measures **strength + direction of linear** association only; symmetric (no response/predictor).
- **Avoid:** implying correlation shows causation, or that low r means "no relationship" (could be nonlinear).

## 3.2 Association ≠ causation (the default caveat)
- **Template:** "This shows **[X]** and **[Y]** are **associated**, but **not** that **[X] causes [Y]** —
  the data are **observational**, so confounders or reverse causality could explain the relationship."
- **Example:** "Higher private-coverage districts have lower cancer death rates, but this is association
  only; wealth could drive both."
- **Why:** causation needs the right **design**, not a good fit.
- **Avoid:** "causes," "the effect of," "leads to," "improves/reduces" on observational data.

## 3.3 Causal claim — when it IS justified
- **Template:** "Because **[treatment]** was **randomly assigned** (a randomized experiment), the difference
  in **[Y]** can be attributed to **[treatment]** — a **causal** effect."
- **Example:** "In the randomized ad experiment, the ~8-second difference in dwell time is the causal effect
  of the new ad."
- **Why:** randomization balances **observed AND unobserved** confounders, so only the treatment differs.
- **Avoid:** making a causal claim from an observational study, even after adjusting (see 3.4).

## 3.4 Confounding
- **Template:** "**[C]** is a **confounder**: it is associated with both **[X]** and **[Y]**, creating a
  misleading association between them; omitting it **biases** the estimate."
- **Example:** "Athlete status confounds ad→dwell-time: athletes both dwell longer and prefer the new ad, so
  ignoring it inflates the ad effect (9.83 vs. true 8)."
- **Why:** confounder → `C→X` and `C→Y`; adjustment fixes it **only if the confounder is known & measured**.
- **Avoid:** "adjusting for the confounder makes the estimate **causal**." (only if ALL confounders measured)

## 3.5 Reverse causality
- **Template:** "The association may reflect **reverse causality**: rather than **[X]→[Y]**, it may be that
  **[Y] causes [X]**."
- **Example:** "Struggling students receive more parental help, so low grades cause help, not help causing
  low grades."
- **Why:** direction of the arrow isn't settled by a correlation.
- **Avoid:** assuming the arrow runs the way the sentence is phrased.

## 3.6 Simpson's paradox
- **Template:** "The direction of the **[X]–[Y]** association **reverses** when we account for **[subgroup]**,
  so the aggregate result is misleading."
- **Example:** "UC Berkeley 1973 admissions looked biased against women overall, but within departments they
  weren't — women applied to more competitive departments."
- **Why:** aggregated and stratified data can disagree.
- **Avoid:** trusting an aggregate association without checking relevant subgroups.

## 3.7 Experiment vs. observational (summary phrasing)
- **Template:** "This is an **[observational study / randomized experiment]**, so we can conclude
  **[association only / a causal effect]**."
- **Example:** "The cancer data are observational, so we can only conclude association, not causation."
- **Why:** the design determines the strength of claim.
- **Avoid:** upgrading observational association to causation.

---

# 4 — ANOVA

## 4.1 ANOVA F-test conclusion
- **Template:** "The ANOVA F-test gives **p = [value]**; since **p < α**, we conclude **at least one**
  **[group]**'s mean **[Y]** differs — i.e. **[categorical variable]** is associated with **[Y]**."
- **Example:** "For `wage ~ factor(occupation)`, ANOVA gives p ≈ 4.12e-21, so at least one occupation's mean
  wage differs; wage is associated with occupation."
- **Why:** ANOVA tests **all group means equal** jointly; a small p means *some* differ, not *which* — use
  the coefficient table for pairwise detail.
- **Avoid:** "**every** occupation differs from **every** other" or "occupation X is highest" from ANOVA
  alone.

---

# 5 — DIAGNOSTICS (LINE)

## 5.1 Linearity (L)
- **Template:** "The residuals-vs-fitted plot shows **[no pattern / a systematic curve]**, so the linearity
  assumption **[appears satisfied / is violated]**."
- **Example:** "The residuals show a U-shaped curve, so linearity is violated; a quadratic term may help."
- **Why:** a good model gives a **structureless cloud** around 0; a curve = wrong functional form.
- **Avoid:** calling a clear curved pattern "fine."

## 5.2 Independence (I)
- **Template:** "Because the data are **[e.g. repeated measures / over time]**, the errors may be
  **correlated**, violating independence; this would **bias the SEs** and invalidate CIs/tests."
- **Example:** "Repeated measurements on the same customer make the errors dependent, so the usual SEs are
  unreliable."
- **Why:** independence is often judged from the **study design**, not just a plot.
- **Avoid:** assuming independence without considering how the data were collected.

## 5.3 Normality (N)
- **Template:** "The Q-Q plot points **[lie on / deviate from]** the diagonal, so the normality of errors
  **[appears satisfied / is questionable]**."
- **Example:** "The Q-Q points drift off the line at the tails, suggesting non-Normal errors."
- **Why:** normality is the **least severe** violation — with large n the **CLT** (or bootstrap) rescues
  inference.
- **Avoid:** over-worrying about mild non-normality when n is large.

## 5.4 Equal variance (E) / heteroscedasticity
- **Template:** "The residuals-vs-fitted plot shows **[constant spread / a funnel shape]**, so the
  equal-variance assumption **[holds / is violated (heteroscedasticity)]**; a violation makes the **SEs
  wrong**, so CIs and p-values are invalid."
- **Example:** "The residual spread widens with fitted values (a funnel), indicating heteroscedasticity; a
  log(Y) transform may stabilize it."
- **Why:** the SE formula assumes constant σ²; heteroscedasticity breaks it (point estimates stay fine).
- **Avoid:** claiming the constant-variance assumption "doesn't affect the SEs." (it does — it's built into
  them)

## 5.5 Overall assumption check
- **Template:** "Before trusting the inference, we check **LINE**; here **[which hold / which are violated]**,
  and **[fix]** addresses the violation."
- **Example:** "The additive wage model shows a funnel and off-diagonal Q-Q; refitting with log(wage) fixes
  both."
- **Why:** `lm` assumes the assumptions — **checking them is the analyst's job.**
- **Avoid:** reporting p-values/CIs without checking assumptions.

---

# 6 — MULTICOLLINEARITY

## 6.1 VIF conclusion
- **Template:** "**[Variable]** has **VIF = [value]**, which **[exceeds / is below]** the rule-of-thumb
  threshold of 5 (or 10), indicating **[problematic / acceptable]** multicollinearity."
- **Example:** "`lunch` has VIF ≈ 5.7 (> 5), indicating a multicollinearity problem; after dropping it all
  VIFs fall below 2."
- **Why:** multicollinearity **inflates the SEs** of the involved coefficients (estimates stay ~unbiased,
  R² can stay high). For categoricals use **GVIF**: compare `GVIF^(1/(2·Df))` to √5 ≈ 2.23.
- **Avoid:** "multicollinearity is correlation between a predictor and the **response**." (it's **among
  predictors**)

## 6.2 Effect of dropping a collinear variable
- **Template:** "Removing **[collinear variable]** most changed the coefficients of the variables
  **correlated with it** and **lowered their p-values** (their SEs were de-inflated)."
- **Example:** "Dropping `lunch` shifted `income`, `calworks`, `english` the most and lowered their p-values."
- **Why:** collinear variables share information; removing one re-allocates it to its partners.
- **Avoid:** "dropping the variable lowered **all** SEs." (only the collinear partners'; unrelated ones can
  rise)

---

# 7 — PREDICTION & EXTRAPOLATION

## 7.1 Prediction
- **Template:** "For **[X = value]**, the model predicts an **average** **[Y]** of **[ŷ]** **[units]**."
- **Example:** "For a district with 14% poverty, the predicted average death rate is [ŷ]."
- **Why:** the prediction is the **conditional average**, not a guarantee for any single unit (individuals
  scatter by the error term).
- **Avoid:** presenting a prediction as an exact value for one individual.

## 7.2 Extrapolation caveat
- **Template:** "**[X = value]** lies **outside the observed range** of the data, so this prediction is an
  **extrapolation** and is unreliable."
- **Example:** "Predicting body mass for a 500 mm flipper (observed range 172–231) is extrapolation."
- **Why:** the relationship may not hold beyond the data; "all models are wrong, but some are useful."
- **Avoid:** trusting predictions far outside the data range.

---

# 8 — MASTER RULES OF THUMB

- **Observational data ⇒ "associated with," never "causes"/"effect of."**
- **CI:** "95% confident the true parameter is in [range]" — NOT "95% probability the truth is in this
  interval."
- **Tests:** "reject / fail to reject H0" — never "accept," "prove," or "H0 is true."
- **p-value** = strength of **evidence** against H0, not effect size, not P(H0 true).
- **Effect size** lives in the **estimate**; **evidence** lives in the **p-value** — cite both.
- **MLR coefficients:** "holding the other predictors constant" (additive: at any value; interaction: cannot).
- **Categorical coefficients** are **differences from the reference**, not group means.
- **Interaction:** main continuous term = **reference group's slope**; other group = sum with the interaction.
- **Multicollinearity** = correlation **among predictors**; inflates **SEs**.
- **Equal-variance / independence violated ⇒ SEs invalid ⇒ CIs & p-values invalid** (estimates still OK).
- **Randomization** earns causation (balances even unmeasured confounders); **adjustment** only fixes
  **known, measured** confounders.
