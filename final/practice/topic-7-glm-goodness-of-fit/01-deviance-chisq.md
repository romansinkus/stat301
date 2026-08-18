# Practice 01 (Topic 7) — Goodness of Fit for GLMs (Deviance)

*Topic 7. Solutions: [`solutions/01-deviance-chisq-solutions.md`](solutions/01-deviance-chisq-solutions.md).*

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Justify
> every true/false, and respect any word limits. 

---

## Problem 1 (15 pts) — The deviance concept

**(a) (4 pts)** A student fits `glm(survived ~ fare, family = binomial)` and asks for its `R²`. (i) What
is the single most important fact from this topic about `R²`/F-tests and GLMs, and what should they
compute **instead**? (ii) Define the **deviance** — it is described as "RSS for GLMs," so what gap does it
measure, what is the **saturated model**, and is lower or higher deviance a better fit?

**(b) (4 pts)** In `glm` output you see a **null deviance** and a **residual deviance**. What does each one
correspond to (which model), and what does it mean if the residual deviance is much **smaller** than the
null deviance?

**(c) (4 pts)** "A model that passes exactly through every data point (the saturated model) is the best
possible model." True or false? Explain the concept of **overfitting** and why the course prefers
'good-but-not-perfect' models.

**(d) (3 pts)** Complete the **cheat-sheet mapping**: for a **linear** model, RSS leads to which fit
measures and which test? For a **GLM** (logistic/Poisson), deviance leads to which test? Which single
likelihood-based criterion works for **both** kinds of model?

---

## Problem 2 (16 pts) — The deviance test

`anova(model_reduced, model_full, test = "Chisq")` on two nested logistic models reports a **deviance drop
of 18.7** on **3** degrees of freedom, with `p = 0.0003`.

**(a) (5 pts)** Describe the **deviance test** for comparing two nested GLMs. State (i) the null and
alternative hypotheses, (ii) the test statistic, (iii) its reference distribution and the degrees of
freedom `d`, and (iv) the R command.

**(b) (4 pts)** For the output above: (i) what does the deviance drop of 18.7 represent? (ii) what is
`d = 3`? (iii) state the conclusion — is the larger model justified?

**(c) (3 pts)** The deviance test "is a large-sample result." What does that caveat mean in practice, and
when might you distrust the χ² p-value?

**(d) (4 pts)** Why can't we just use the F-test (from Topic 6) to compare two nested logistic models?
What has to change, and what stays the same (in workflow)?
