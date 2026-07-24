# Practice 07 — Multicollinearity

*Topic 3 (Multicollinearity). Solutions: [`solutions/02-multicollinearity-solutions.md`](solutions/02-multicollinearity-solutions.md).*

---

**Q1 [SA].** Define **multicollinearity**. Why does it make a model unable to "isolate the individual
effects" of the involved predictors?

---

**Q2 [SA].** You put both `income` (in \$1000s) and `incomeUSD = income * 1000` into one model and R
returns `NA` for one coefficient. Explain *why* R can't estimate both — what is true about the SSR
across many coefficient combinations?

---

**Q3 [SA].** Explain the "two identical employees" analogy for perfect collinearity, and what it says
about the *individual* contributions of collinear predictors.

---

**Q4 [SA].** What is the main *statistical* consequence of strong (but not perfect) multicollinearity
— on the standard errors, CIs, and hypothesis tests of the **individual** coefficients? Does it bias
the point estimates or hurt the overall `R^2`? Explain.

---

**Q5 [TF].** "Multicollinearity can only occur between two variables at a time." True or false?
Justify with the idea of one predictor being collinear with a *combination* of others.

---

**Q6 [SA].** Why are **pairwise correlations** between predictors helpful but **not sufficient** for
detecting multicollinearity? What tool catches what pairwise correlations miss?

---

**Q7 [SA].** Define **VIF** conceptually (what ratio does it capture?), and state the common
guideline thresholds. When there are categorical predictors, which variant do you use and how do you
compare it?

---

**Q8 [CALC].** A GVIF table reports, for a categorical predictor, `GVIF = 12.4`, `Df = 2`, and
`GVIF^(1/(2*Df)) = 1.87`. Is this predictor's collinearity "concerning" by the `sqrt(5) ≈ 2.23`
rule? Show the comparison and state your conclusion.

---

**Q9 [SA].** Name the two standard **fixes** for multicollinearity and one trade-off of each. In the
penguins example, which variable had the highest VIF, and what happened when it was removed?
