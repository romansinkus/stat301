# Practice 01 (Topic 6) — Computing the F-statistic & Model-Selection Criteria

*Gap-filler for Topic 6. Solutions: [`solutions/01-computing-f-and-aic-solutions.md`](solutions/01-computing-f-and-aic-solutions.md).
Companion to `../../practice/topic-6-goodness-of-fit/` (which *reads* F off `glance` but never computes
it). Here you build F by hand.*

> **Exam-style.** Show key steps (70% procedure, 30% answer). Circle final numbers. Calculator allowed.

---

## Problem 1 (17 pts) — Computing F two ways

**(a) (6 pts)** Two **nested** linear models on `n = 100`:
- reduced (`q = 2` predictors): `RSS_reduced = 500`
- full (`p = 4` predictors): `RSS_full = 400`

Using `F = [(RSS_red − RSS_full)/k] / [RSS_full/(n − p − 1)]`, compute `F`. State `k` and the two degrees
of freedom explicitly, and name the R function that runs this exact test.

**(b) (5 pts)** A model with `p = 4` predictors reports `R² = 0.60` on `n = 100`. Compute the
**model-vs-null** F from `R²` using `F = [R²/p] / [(1 − R²)/(n − p − 1)]`. Which R output (`glance` field)
would show this same number?

**(c) (3 pts)** For part (a), the p-value comes out `≈ 0.00003`. State the conclusion precisely: what does
rejecting `H0` tell you, and — per the protein~mRNA punchline — what does it **not** tell you?

**(d) (3 pts)** Why must the two models be **nested** for the F-test to be valid? What breaks if they
aren't?

---

## Problem 2 (13 pts) — `F = t²` and choosing between models

**(a) (4 pts)** In a **single-predictor** model, the coefficient's t-statistic is `t = 3.5`. Compute the
model's F-statistic, and explain why `F = t²` holds here (what makes the two hypotheses identical when
`p = 1`?).

**(b) (5 pts)** You compare three nested models by AIC:

| Model | # predictors | R² | AIC |
| --- | --- | --- | --- |
| A | 2 | 0.55 | 520 |
| B | 4 | 0.60 | 512 |
| C | 8 | 0.62 | 518 |

(i) Which model does **AIC** prefer, and by what rule (bigger or smaller)? (ii) Why can't you use **raw
R²** to make this choice? (iii) What did adding predictors 5–8 (B→C) evidently do, and how does AIC
"see" it?

**(c) (4 pts)** In one line each: what is **AIC** (its two parts), how does **BIC** differ, and which
criterion is what **`step()`** optimizes?
