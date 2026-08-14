# Solutions 05 (Topic 3) — Tutorial 03: Multicollinearity Workflow & Causality

*Questions: [`../05-tutorial3-multicollinearity-causality.md`](../05-tutorial3-multicollinearity-causality.md).*

> Marking scheme: **70% for correct procedures, 30% for correct answers.**

---

## Problem 1 — Multicollinearity in practice (CASchools)

**(a)** Workflow: (1) **Visualize** predictor correlations — `GGally::ggpairs()` and a **correlation
heatmap** (`geom_tile()` over a melted `cor()` matrix) — flagging pairs with `|r| > 0.6`; (2) **fit the
full model** and compute **VIF** (`car::vif()`); (3) **drop** the higher-VIF variable from the
most-correlated pair; (4) **refit and recompute VIF** to confirm the values dropped below the threshold.
Visual tools = `ggpairs` + heatmap; numeric tool = **VIF**.

**(b)** (i) The `.` means "**use all other columns** in the data frame as predictors" (i.e.
`score ~ everything else`). (ii) **VIF = 1** means no multicollinearity for that variable; the rule of
thumb is **VIF > 5 (or > 10)** signals a problem. (iii) Rule: find the pair with the **largest absolute
correlation**, and of that pair **drop the variable with the larger VIF** (the more redundant one). Here
`calworks`–`lunch` had the top correlation (0.74) and `lunch` had the larger VIF (≈ 5.7 vs ≈ 2.6), so
`lunch` is removed.

**(c)** (i) The coefficients of the variables **most correlated with `lunch`** changed the most —
`income`, `calworks`, and `english` (all `|r| > 0.6` with `lunch`); a barely-correlated variable
(`stratio`, `r ≈ 0.14`) hardly moved. Collinear variables share information, so removing one
**re-allocates** that shared explanatory weight onto its correlated partners. (ii) **False.** The SEs
decreased **only for the variables collinear with `lunch`** (`calworks`, `english`, `income`) — removing
their collinear partner **de-inflated** them. For **non-collinear** variables (`stratio`, `computer`,
`expenditure`) the SEs actually **increased slightly**, because dropping a strong predictor raises the
model's residual variance, which pushes all SEs up; only the collinear ones get enough relief to net
decrease.

**(d)** Compare the **before vs. after VIF tables** against the threshold: if the previously-high VIFs
(and all others) are now **below 5 (or 10)**, the problem is solved. Here every VIF dropped below ~2 after
removing `lunch`, so **yes** — resolved.

---

## Problem 2 — Causality & confounders (TikTok simulation)

**(a)** (i) **`Y` = ad dwell time** (continuous response); **`X` = ad type** (Current vs New, the
treatment); **`C` = athlete** (the confounder). `athlete` is a confounder because it is associated with
**both** the treatment (athletes disproportionately choose the New ad) **and** the response (athletes
dwell longer regardless of ad) — the arrows `C → X` and `C → Y`. (ii) With a **simulation** you **know
the true data-generating process and the true effect (+8)**, so you can check whether each analysis
recovers it and *see* exactly how confounding biases the estimate; in real data the true effect is
unknown and confounders unmeasured, so you could not grade the methods this way.

**(b)** (i) The **naive** estimate **9.83** is biased **upward** (above the true 8): athletes
**self-select** the New ad and also dwell longer, so the New group is loaded with high-dwell athletes →
the athlete effect **inflates** the apparent ad effect. (ii) The **adjusted** MLR (7.92) and the
**randomized** experiment (8.03) both land **≈ 8**, recovering the true effect — two different ways of
removing the confounding.

**(c)** (1) **Adjust for the confounder** — include `athlete` in the model (gives 7.92). **Limitation:**
it only works if you **know about and have measured** the confounder; unknown/unmeasured confounders
still bias you. (2) **Randomize** — randomly assign the ad (gives 8.03). **Advantage:** randomization
balances the confounder across groups **by design, even confounders you never measured**. The experiment
recovers +8 without `athlete` in the model because random assignment makes the ad received **independent
of `athlete`** (and every other trait) — the groups are balanced, so nothing systematically differs
except the ad.

**(d)** Adjustment only removes bias from **confounders you actually included**. You can never be sure you
measured *every* confounder, so an adjusted observational estimate is "causal" only **conditional on
there being no remaining unmeasured confounders** — an assumption you generally cannot verify. That is
why **randomization** (which handles unknown confounders too) is the gold standard, and why observational
studies usually warrant only **association**.
