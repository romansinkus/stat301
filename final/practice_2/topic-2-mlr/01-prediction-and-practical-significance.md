# Practice 01 (Topic 2) — Prediction by Hand & Practical vs. Statistical Significance

*Gap-filler for Topic 2. Solutions: [`solutions/01-prediction-and-practical-significance-solutions.md`](solutions/01-prediction-and-practical-significance-solutions.md).
Companion to `../../practice/topic-2-mlr/` (additive/interaction concepts).*

> **Exam-style.** Show key steps (70% procedure, 30% answer). Circle final numbers.

---

## Problem 1 (16 pts) — Computing predictions from a multi-predictor fit

An additive model `lm(wage ~ education + experience + sex)` (female = reference) gives:

```
term          estimate
(Intercept)     -2.00
education        0.60
experience       0.10
sexmale          1.50
```

**(a) (4 pts)** Write the fitted equation with the `sexmale` dummy shown explicitly. State what value the
dummy takes for a female and for a male.

**(b) (4 pts)** Predict the average wage for a **female** with **12 years education** and **10 years
experience**. Show every term of the substitution and circle the answer.

**(c) (4 pts)** Predict for a **male** with the same education and experience. What is the male–female
difference, and which coefficient equals it? Explain why the difference is the *same* at every
education/experience combination (name the assumption).

**(d) (4 pts)** Now suppose the model were `lm(wage ~ education * sex)` with an added
`education:sexmale = 0.15` term. In ≤ 30 words, explain why you could **no longer** say "the male–female
gap is the same at every education level," and how the gap now depends on education.

---

## Problem 2 (14 pts) — Statistical vs. practical significance

A retailer fits `lm(spend ~ app_notifications)` on **n = 500,000** customers and reports:

```
term                estimate   std_error   p_value
app_notifications     0.004      0.0008     3e-7
```

(`spend` in dollars; `app_notifications` = number sent per month.)

**(a) (4 pts)** Is `app_notifications` **statistically significant** at the 5% level? Justify from the
p-value (and note how the huge `n` drove the SE).

**(b) (5 pts)** Interpret the estimate `0.004` in plain language. Is the effect **practically** important —
would 100 extra notifications change spending in a way a manager should care about? Show the arithmetic.

**(c) (3 pts)** In ≤ 30 words, state the general lesson: why does a very large sample make "statistically
significant" a **weak** claim, and what should you report alongside the p-value?

**(d) (2 pts)** Name one thing you would check about the *sign and size* of a confidence interval to judge
practical significance, rather than relying on the p-value alone.
