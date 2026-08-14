# Practice 02 (Topic 3) — Multicollinearity

*Topic 3 (Multicollinearity). Solutions: [`solutions/02-multicollinearity-solutions.md`](solutions/02-multicollinearity-solutions.md).*

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Circle
> final numeric answers and respect the word limits.

---

## Problem 1 (15 pts) — What multicollinearity is and does

**(a) (4 pts)** Define **multicollinearity**. Why does it make a model unable to "isolate the individual
effects" of the involved predictors?

**(b) (4 pts)** You put both `income` (in \$1000s) and `incomeUSD = income * 1000` into one model, and R
returns `NA` for one coefficient. Explain *why* R cannot estimate both — what is true about the SSR
across many coefficient combinations?

**(c) (4 pts)** (i) Explain the "two identical employees" analogy for perfect collinearity, and what it
says about the *individual* contributions of collinear predictors. (ii) What is the main *statistical*
consequence of strong (but not perfect) multicollinearity on the SEs, CIs, and tests of the
**individual** coefficients? Does it bias the point estimates or hurt the overall `R²`?

**(d) (3 pts)** "Multicollinearity can only occur between two variables at a time." True or false?
Justify with the idea of one predictor being collinear with a *combination* of others.

---

## Problem 2 (16 pts) — Detecting and fixing multicollinearity

**(a) (4 pts)** Why are **pairwise correlations** between predictors helpful but **not sufficient** for
detecting multicollinearity? What tool catches what pairwise correlations miss?

**(b) (4 pts)** Define **VIF** conceptually (what ratio does it capture?), and state the common guideline
thresholds. When there are categorical predictors, which variant do you use and how do you compare it?

**(c) (4 pts)** A GVIF table reports, for a categorical predictor, `GVIF = 12.4`, `Df = 2`, and
`GVIF^(1/(2*Df)) = 1.87`. Is this predictor's collinearity "concerning" by the `sqrt(5) ≈ 2.23` rule?
Show the comparison and state your conclusion (be explicit about *which* number you compare).

**(d) (4 pts)** Name the two standard **fixes** for multicollinearity and one trade-off of each. In the
penguins example, which variable had the highest VIF, and what happened when it was removed?
