# Solutions — Practice 01 (Topic 9): Band Shape & Extrapolation

## Problem 1

**(a)** The fitted line effectively **pivots around the point `(x̄, ȳ)`**, which the data anchor most
firmly (least squares always passes through it). Small wobbles in the estimated **slope** barely move the
line near `x̄`, but they swing it up and down more and more as you go out to extreme `X`. The uncertainty
in `ŷ` grows with the distance **`(X − x̄)`** — zero-ish contribution at the center, large at the edges —
so the band pinches at `x̄` and flares outward (an hourglass/bowtie).

**(b)** Both widths come from **estimation uncertainty** (uncertainty in the fitted line, the `(X − x̄)`
term). The **PI** adds a *second* ingredient: the **irreducible noise `σ²`** (the individual error `e`) —
because it targets one *actual* `Y`, not the average `E[Y|X]`. That extra `σ²` is a **roughly constant**
floor that does **not** depend on `(X − x̄)`, which is why the PI is wider *everywhere* and stays wide even
near `x̄`.

**(c)** Far outside the data, `(X − x̄)` is huge, so **both bands flare very wide** — the estimation part
of the uncertainty balloons. So the prediction is untrustworthy twice over: (1) the point estimate relies
on an unverified extrapolation of the linear form, and (2) even taking the model at face value, the
interval is so wide it's nearly uninformative.

**(d)** **False.** `geom_smooth(se = TRUE)` draws the **confidence band for the mean line (CIP)** — where
the *average* `E[Y|X]` plausibly lies — **not** where individual points fall. The interval that captures
individual observations is the **prediction interval (PI)**, which is much wider (it includes `σ²`).

## Problem 2

**(a)** Confidence width = `748198 − 671944 = **76,254**`. Prediction width = `965622 − 454519 =
**511,103**`. The **PI is wider**, by about `511103 / 76254 ≈ **6.7×**`.

**(b)** **Both are wider** at `X = 340` than at `X = 200`. Mechanism: `X = 340` is far from `x̄ ≈ 200`, so
`(X − x̄)` is large → the estimation-uncertainty term grows → the fitted line is less pinned down there,
widening both intervals (the CIP flares proportionally more, since the PI's constant `σ²` floor dilutes the
effect).

**(c)** Single client, their **specific** 340 m house → **prediction interval** (targets one actual `Y`,
includes individual noise). City budgeting the **average** value of all 340 m houses → **confidence
interval for the prediction (CIP)** (targets `E[Y|X]`, the mean).

**(d)** Midpoint of the CIP = `(671944 + 748198)/2 = 1,420,142/2 = **≈ $710,071**`. CIP and PI share this
center because both are built around the **same fitted value `ŷ = b̂0 + b̂1·X`** — they differ only in
*width* (what uncertainty they add), not in *center*.
