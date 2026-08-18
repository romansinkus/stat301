# Practice 01 (Topic 8) — Model Selection (Regularization & Post-Inference) 

*Topic 8. Solutions: [`solutions/01-lasso-and-double-dipping-solutions.md`](solutions/01-lasso-and-double-dipping-solutions.md).
Course dataset: Ames Housing (`SalePrice`).*

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Justify
> every true/false, and respect any word limits.

---

## Problem 1 (14 pts) — Stepwise vs. regularization; ridge vs. LASSO

**(a) (5 pts)** **Stepwise selection** is called a "greedy" algorithm. Explain two of its limitations:
(i) the role of the **order** variables enter, and (ii) the "all-or-nothing" way a variable's coefficient
enters. What does regularization do **differently** ("smoothly")?

**(b) (4 pts)** Write the general **regularized objective** (the thing we minimize) and label its two
parts. What is the role of `λ`?

**(c) (5 pts)** Complete the comparison, then say which method the course focuses on and what "LASSO"
stands for:

| Method | Penalty | Norm | Shrinks to exactly 0? | Selects variables? |
| --- | --- | --- | --- | --- |
| Ridge | ? | L2 | ? | ? |
| LASSO | ? | L1 | ? | ? |

---

## Problem 2 (15 pts) — Tuning λ and the bias–variance trade-off

**(a) (5 pts)** Describe what happens to the coefficients as `λ` goes from `0` to large. (i) What do you
get back at `λ = 0`? (ii) How does **LASSO** produce variable *selection* as `λ` grows, and why can
**Ridge** never select?

**(b) (5 pts)** How do we **choose** `λ` ("tuning")? Name the procedure, explain what it splits and why it
does not touch the real test set, and distinguish **`lambda.min`** from **`lambda.1se`**.

**(c) (5 pts)** Shrinkage deliberately produces a **biased** estimator (`E[b̂] ≠ β`). Using
`MSE = Variance + Bias²`, explain **why we would accept bias**. In what setting (relationship between `p`
and `n`) was LASSO especially designed to shine, and why must inputs be **standardized** first?

---

## Problem 3 (16 pts) — Double-dipping / post-inference

**(a) (4 pts)** State the **post-inference / double-dipping** problem in one or two sentences. What
exactly are the "two dips," and what goes wrong with the resulting p-values / Type I error rate?

**(b) (5 pts)** Describe the **simulation** that proves the double-dipping problem. (i) How is the data
generated (what are the true coefficients)? (ii) What is done on each of the ~1000 datasets? (iii) What is
the punchline about the Type I error rate, and what does the fix (splitting the data) restore?

**(c) (4 pts)** "postLASSO — refitting ordinary least squares on the variables LASSO selected — gives
unbiased coefficients, so you can safely report its p-values from the same data." True or false? Justify
carefully.

**(d) (3 pts)** In one sentence, state the overarching takeaway of Topic 8 about selection and inference.
Then name the practical remedy.
