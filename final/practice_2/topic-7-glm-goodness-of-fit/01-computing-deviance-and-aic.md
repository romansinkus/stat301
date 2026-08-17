# Practice 01 (Topic 7) — Computing the Deviance Test & Pseudo-R²

*Gap-filler for Topic 7. Solutions: [`solutions/01-computing-deviance-and-aic-solutions.md`](solutions/01-computing-deviance-and-aic-solutions.md).
Companion to `../../practice/topic-7-glm-goodness-of-fit/` (deviance concept, χ² test — conceptual).
Here you compute the statistic and df by hand.*

> **Exam-style.** Show key steps (70% procedure, 30% answer). Circle final numbers. Calculator allowed.
> χ² 5% critical values: `χ²₁ = 3.84`, `χ²₂ = 5.99`, `χ²₃ = 7.81`, `χ²₄ = 9.49`.

---

## Problem 1 (16 pts) — Reading and testing a `glm` deviance output

A logistic fit `glm(default ~ balance + income + student + limit, family = binomial)` on `n = 200`
reports:

```
    Null deviance: 900.0  on 199  degrees of freedom
Residual deviance: 750.0  on 195  degrees of freedom
```

**(a) (4 pts)** Which model does the **null deviance** correspond to, and which does the **residual
deviance** correspond to? What does deviance play the role of, relative to linear regression?

**(b) (5 pts)** Run the **model-vs-null** deviance test by hand: (i) compute the deviance drop (the
statistic); (ii) compute its degrees of freedom from the two df lines; (iii) compare to the χ² critical
value and state the conclusion.

**(c) (4 pts)** Compute a **McFadden pseudo-R²** = `1 − residual/null deviance`. Interpret it in one
sentence, and say why it is *not* the same thing as the linear-model R² (why "proportion of variance
explained" doesn't literally apply).

**(d) (3 pts)** The residual deviance (750) is still large. In ≤ 30 words, why is driving the residual
deviance to **0** (a saturated / perfect fit) a *bad* goal, not a good one?

---

## Problem 2 (14 pts) — Nested deviance test + AIC

Two **nested** logistic models:

```
reduced:  residual deviance 780.0 on 197 df    AIC = 790
full:     residual deviance 750.0 on 195 df    AIC = 764
```

**(a) (5 pts)** Test whether the **extra block** of predictors helps. Compute (i) the deviance drop, (ii)
`d` (the df), (iii) compare to χ² and conclude. Name the R command.

**(b) (3 pts)** The two models agree with **AIC** here. Which model does AIC pick (smaller = better), and
does it agree with the deviance test? Why is AIC usable when raw deviance (which always drops with more
predictors) is not, for comparing sizes?

**(c) (3 pts)** Why can't you use the **F-test** from Topic 6 on these two logistic models? What replaces
it, and what stays the same in the workflow?

**(d) (3 pts)** The deviance/χ² test is a **large-sample** result. What does that caveat mean, and when
would you distrust the χ² p-value?
