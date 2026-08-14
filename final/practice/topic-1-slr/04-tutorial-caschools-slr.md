# Practice 04 (Topic 1) — Tutorial 01: Generative Modelling, EDA & SLR (CASchools)

*Topic 1 (SLR + inference). Source: `tutorials/tutorial_01.ipynb`. Solutions:
[`solutions/04-tutorial-caschools-slr-solutions.md`](solutions/04-tutorial-caschools-slr-solutions.md).*

Dataset: **CASchools** — `read` (avg district reading score) vs `income` (district avg income, \$1000s).

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Respect
> the word limits.

---

## Problem 1 (15 pts) — The generative model and EDA

**(a) (4 pts)** The course calls linear regression **"generative modelling."** Explain what that phrase
means: what is the model an approximation *of*, and what role do the coefficients `b` play in it?

**(b) (4 pts)** "In a simple linear regression, the response is an **exact** linear function of the
input, `Y_i = b0 + b1*X_i`." True or false? Justify, and write the correct model.

**(c) (4 pts)** The error term `e_i` in `read_i = b0 + b1*income_i + e_i` — name the **two** kinds of
things it absorbs, and explain why we can never observe `e_i` directly.

**(d) (3 pts)** Before modelling, the tutorial runs `GGally::ggpairs()`. Give **two** reasons `ggpairs()`
is preferred over base `pairs()` for a first look at several variables.

---

## Problem 2 (15 pts) — Fitting and inference for `read ~ income`

For `lm(read ~ income)` the slope estimate is `≈ 1.94`, with a 95% CI of `≈ (1.75, 2.13)` and
`p < 0.05`.

**(a) (4 pts)** Write a **correct** one-sentence interpretation of the slope (mind the units of
`income`), and say why "each extra \$1000 of income **raises** a district's score by 1.94 points" would
be marked wrong.

**(b) (4 pts)** (i) State whether `income` is significantly associated with `read`, and how *both* the CI
and the p-value show it. (ii) Are the `lm` p-values based on classical theory or on bootstrapping?

**(c) (3 pts)** Fill in the blank correctly and explain: "One of the *sampling distributions* in SLR is
the distribution of ___." Say why it is **not** the distribution of `Y`, of the true slope `b1`, or of
`X`.

**(d) (4 pts)** Describe how to use bootstrapping to approximate the sampling distribution of the slope:
what do you resample, how many times (the tutorial used `B = 10000`), and how do you read a **90%** CI
off the stored `boot_slope` values?
