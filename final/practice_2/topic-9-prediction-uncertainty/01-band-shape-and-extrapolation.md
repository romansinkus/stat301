# Practice 01 (Topic 9) — The Interval Band Shape & Extrapolation

*Gap-filler for Topic 9. Solutions: [`solutions/01-band-shape-and-extrapolation-solutions.md`](solutions/01-band-shape-and-extrapolation-solutions.md).
Companion to `../../practice/topic-9-prediction-uncertainty/` (CIP vs PI concepts). This set adds the
**shape** of the bands — why they pinch at `x̄` and flare at the edges — and the extrapolation angle.*

> **Exam-style.** Show key steps (70% procedure, 30% answer). Circle final answers.

---

## Problem 1 (16 pts) — Why the confidence band is an "hourglass"

The shaded confidence band around a fitted SLR line is **narrowest at `x̄`** (the mean of the predictor)
and **flares outward** as `X` moves away from `x̄` in either direction.

**(a) (5 pts)** Explain *why* the band pinches at `x̄` and widens at the extremes. Refer to how the
uncertainty in the fitted value `ŷ` depends on the distance `(X − x̄)` — which part of the line is
"anchored" most firmly by the data?

**(b) (4 pts)** The **CIP** (confidence interval for the prediction) and the **PI** (prediction interval)
are **both** widest at the extremes, but the PI is wider everywhere. Decompose each interval's width into
its **two ingredients**, and say which ingredient the PI has that the CIP does not — and whether that extra
ingredient depends on `(X − x̄)`.

**(c) (4 pts)** A realtor predicts an assessed value for a house whose size is **far larger than any in the
data**. Beyond the usual "extrapolation" warning about the point estimate, what happens to the **width** of
both intervals out there, and why does that make the prediction doubly untrustworthy?

**(d) (3 pts)** True/false, justify: "The band that `geom_smooth(se = TRUE)` draws shows where ~95% of the
individual data points fall." If false, what does the band actually show, and which interval *would*
capture individual points?

---

## Problem 2 (14 pts) — Reading `predict()` at two locations

For `lm(assess_val ~ BLDG_METRE)` with mean size `x̄ ≈ 200 m`, `predict()` gives 95% intervals:

```
At X = 200 m (near x̄):
  confidence: (671944, 748198)
  prediction: (454519, 965622)

At X = 340 m (far from x̄):
  confidence: (past printout) — WIDER than at 200
  prediction: (past printout) — WIDER than at 200
```

**(a) (4 pts)** Compute the **width** of the confidence interval and of the prediction interval at
`X = 200`. Which is wider, and by roughly what factor?

**(b) (4 pts)** Without the numbers, state whether each interval at `X = 340` is **wider or narrower** than
at `X = 200`, and explain the mechanism (tie back to `(X − x̄)`).

**(c) (3 pts)** Which interval (confidence or prediction) should the realtor give a **single client**
asking about **their specific** 340 m house? Which should the **city** use to budget the **average**
assessed value of all 340 m houses? One sentence each.

**(d) (3 pts)** Both intervals at `X = 200` are centered on the same fitted value — roughly what is it
(show the midpoint calc for the confidence interval)? Why do CIP and PI share the same center?
