# Practice 01 (Topic 5) — Poisson Regression (count response)

*Topic 5. Solutions: [`solutions/01-poisson-regression-solutions.md`](solutions/01-poisson-regression-solutions.md).
Course dataset: Bikeshare (`bikers ~ temp, season, workingday, windspeed`).*

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Circle
> final numeric answers, and respect any word limits. A simple calculator is allowed.

---

## Problem 1 (15 pts) — Why Poisson, and the model

**(a) (3 pts)** What kind of response calls for Poisson regression? Give two example responses (not from
the course) that would qualify.

**(b) (4 pts)** State the **two** problems that rule out ordinary linear regression for a count response.
For the second, explain the special Poisson property `λ = E[Y|X] = Var(Y|X)` and which **LINE**
assumption it automatically breaks.

**(c) (4 pts)** Write the Poisson model in both its **mean** form and its **log-mean** form. Which is "the
linear one," and why does the log link cure the range problem?

**(d) (4 pts)** Reproduce the **multiplicative derivation**: starting from `log λ = b0 + b1·temp`, show
why increasing `temp` by 1 **multiplies** the mean count by `e^b1` (compare `log λ` at `temp` and
`temp + 1`).

---

## Problem 2 (16 pts) — Interpreting a Bikeshare Poisson fit

`glm(bikers ~ temp + season, family = poisson)` (season 1 = reference) gives `b_temp = 2.688`,
`season2 = 0.063`, and `season3 = −0.141`.

**(a) (5 pts)** For `b_temp = 2.688`: (i) interpret the raw coefficient on the **log-mean** scale;
(ii) compute `e^2.688 ≈ 14.7` and interpret it as a **rate ratio**; (iii) if the mean count at some
temperature is 40 bikers, what is the predicted mean count one unit of `temp` higher?

**(b) (4 pts)** (i) Convert `season2` and `season3` each to a rate ratio and a percent change vs.
season 1. (ii) Which season has higher mean ridership than season 1, and which lower? (iii) In one
sentence, interpret the `season3` result in plain language.

**(c) (3 pts)** "In the Bikeshare data, `workingday` is stored as `0/1` and `season` as `1,2,3,4`, so we
can put them straight into `glm()` and get proper dummy variables." True or false? Explain the
`factor()` gotcha and what goes wrong if you forget it.

**(d) (4 pts)** An **interaction** model gives a `temp` rate ratio of `e^b_temp = 14.7` for non-working
days and an interaction term `e^b_int = 0.483`. (i) What is the `temp` rate ratio for **working** days?
(ii) Explain in words what the interaction says about how temperature affects ridership on working vs.
non-working days.

---

## Problem 3 (15 pts) — Overdispersion and inference

**(a) (4 pts)** Poisson and logistic regression share almost all their machinery. Fill in the contrast:
(i) what scale are the exponentiated coefficients on for each (odds ratio vs. ___)? (ii) what is
`Var(Y|X)` for each? (iii) which model **usually** shows overdispersion, and which only **sometimes**?

**(b) (4 pts)** Why does Poisson regression **usually** exhibit overdispersion, when logistic often does
not? Refer to the "mean = variance" assumption.

**(c) (4 pts)** Refitting Bikeshare with `family = quasipoisson` reports a **dispersion parameter of
≈ 90.6**. (i) What does this tell you about the plain Poisson fit? (ii) What specifically becomes
untrustworthy — the coefficients or the SEs/p-values? (iii) What does the quasi-Poisson fit do about it,
and how does this contrast with the Titanic logistic dispersion of ≈ 0.98?

**(d) (3 pts)** How is inference for a Poisson coefficient done (name the statistic and its reference
distribution), and what large-sample result justifies it? State the equivalence between `|z| > 1.96`, the
CI, and the p-value.
