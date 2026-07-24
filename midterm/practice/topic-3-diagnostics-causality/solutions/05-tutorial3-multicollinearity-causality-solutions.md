# Solutions 05 (Topic 3) — Tutorial 03: Multicollinearity Workflow & Causality

*Questions: [`../05-tutorial3-multicollinearity-causality.md`](../05-tutorial3-multicollinearity-causality.md).*

---

## Part 1 — Multicollinearity in practice

**Q1.** Workflow: (1) **Visualize** predictor correlations — `GGally::ggpairs()` and a **correlation
heatmap** (`geom_tile()` over a melted `cor()` matrix) — flagging pairs with `|r| > 0.6`; (2) **fit the
full model** and compute **VIF** (`car::vif()`); (3) **drop** the higher-VIF variable from the
most-correlated pair; (4) **refit and recompute VIF** to confirm the values dropped below the threshold.
Visual tools = `ggpairs` + heatmap; numeric tool = **VIF**.

---

**Q2.** (a) The `.` means "**use all other columns** in the data frame as predictors" (i.e.
`score ~ everything else`). (b) **VIF = 1** means no multicollinearity for that variable; the rule of
thumb is **VIF > 5 (or > 10)** signals a problem.

---

**Q3.** Rule: find the pair with the **largest absolute correlation**, and of that pair **drop the
variable with the larger VIF** (it's the more redundant one). Here `calworks`–`lunch` had the top
correlation (0.74), and `lunch` had the larger VIF (≈ 5.7 vs `calworks`'s ≈ 2.6), so `lunch` is removed.

---

**Q4.** The coefficients of the variables **most correlated with `lunch`** changed the most — `income`,
`calworks`, and `english` (all had `|r| > 0.6` with `lunch`). A variable barely correlated with `lunch`
(like `stratio`, r ≈ 0.14) barely moved. This is the signature of multicollinearity: collinear variables
share information, so removing one **re-allocates** that shared explanatory weight onto its correlated
partners.

---

**Q5.** **False.** The SEs decreased **only for the variables that were collinear with `lunch`**
(`calworks`, `english`, `income`) — removing their collinear partner **de-inflated** their SEs. For the
**non-collinear** variables (`stratio`, `computer`, `expenditure`) the SEs actually **increased slightly**,
because dropping a strong predictor (`lunch`) **raises the model's residual variance**, which pushes all
SEs up; only the collinear variables get enough collinearity relief to net *decrease*.

---

**Q6.** Compare the **before vs. after VIF tables** against the threshold: if the previously-high VIFs
(and all others) are now **below 5 (or 10)**, the problem is solved. Here every VIF dropped below ~2 after
removing `lunch`, so **yes** — resolved.

---

## Part 2 — Causality & confounders

**Q7.** **`Y` = ad dwell time** (continuous response); **`X` = ad type** (Current vs New, the treatment);
**`C` = athlete** (the confounder). `athlete` is a confounder because it is associated with **both** the
treatment (athletes disproportionately choose the New ad) **and** the response (athletes have longer dwell
times regardless of ad) — the two arrows `C → X` and `C → Y`.

---

**Q8.** With a **simulation** you **know the true data-generating process and the true effect (+8)**, so
you can check whether each analysis recovers it and *see* exactly how confounding biases the estimate. In
real data the true effect is unknown and many confounders are unmeasured, so you couldn't grade the
methods this way.

---

**Q9.** (a) The **naive** estimate **9.83** is biased **upward** (above the true 8). In the observational
data athletes **self-select** the New ad and also dwell longer, so the New group is loaded with high-dwell
athletes → the athlete effect **inflates** the apparent ad effect. (b) The **adjusted** MLR (7.92) and the
**randomized** experiment (8.03) both land **≈ 8**, recovering the true effect — two different ways of
removing the confounding.

---

**Q10.** (1) **Adjust for the confounder** — include `athlete` in the model (gives 7.92). **Limitation:**
it only works if you **know about and have measured** the confounder; unknown/unmeasured confounders still
bias you. (2) **Randomize** — randomly assign the ad (gives 8.03). **Advantage:** randomization balances
the confounder across groups **by design, even confounders you never measured**, so it needs no confounder
in the model. (Observational alternative when you can't randomize: **stratification** — compare within
subgroups sharing the confounder's value.)

---

**Q11.** Random assignment makes the ad a customer receives **independent of `athlete`** (and of every
other trait). So athletes and non-athletes end up **balanced across both ad groups** — the `athlete → ad`
link is broken. With nothing systematically differing between the groups except the ad, the estimate is
unbiased **without** needing to model `athlete`.

---

**Q12.** The caveat: adjustment only removes bias from **confounders you actually included**. You can
never be sure you've measured *every* confounder, so an adjusted observational estimate is only "causal"
**conditional on there being no remaining unmeasured confounders** — an assumption you generally can't
verify. That's precisely why **randomization** (which handles unknown confounders too) is the gold
standard, and why observational studies usually warrant only **association**, not causation.
