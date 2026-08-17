# STAT 301 — Final Practice Set 2 (Gap-Filler)

A **companion** to [`../practice/`](../practice/). That set already covers the core concepts of every
topic; **this set deliberately does NOT repeat them.** Instead, `practice_2` targets the angles the first
set left thin — mostly **by-hand computation** (which `master_notes.md` flags as "likely exam tasks") and
a handful of untested nuances.

> **Same exam format.** Written short answer only, **70% procedure / 30% answer**, show key steps, circle
> final numbers, respect word limits, simple calculator allowed. Final: **Wed Aug 19, 2026**, cumulative,
> two cheat sheets.

## What this set adds (and how it differs from `practice/`)

| Topic | `practice/` already drills | **`practice_2` adds (the gap)** |
| --- | --- | --- |
| 1 — SLR | model, LS, residuals, inference table, bootstrap | **estimation formulas** `β̂₁ = r·Sy/Sx`, `β̂₀ = ȳ − β̂₁x̄`, `R² = r²` by hand; **SD vs SE vs RSE** |
| 2 — MLR | additive/interaction concepts, ANOVA | **prediction by hand** from a multi-predictor fit; statistical vs **practical** significance |
| 3 — Diagnostics | LINE, VIF, causality | **interpreting log-transformed models** (`log(Y)`, `log(X)`, log–log) — the fix that's never interpreted |
| 4 — Logistic | 3 scales, odds ratios, overdispersion | **prediction by hand**: `L → p = e^L/(1+e^L)`, classify at 0.5; numeric scale conversions |
| 5 — Poisson | rate ratios, `factor()`, mean=variance | **prediction by hand**: `λ = e^(b0+b1x)`; comparing predicted counts across covariate values |
| 6 — GoF (linear) | R², adj R², F-test concepts | **computing F by hand** from RSS / from R²; the `F = t²` numeric check; AIC/BIC decision |
| 7 — GoF (GLM) | deviance concept, χ² test | **computing the deviance-test statistic & df by hand**; AIC model comparison; pseudo-R² |
| 8 — Selection | LASSO/ridge, double-dipping | **reading a coefficient-path plot & a CV plot**; counting selected variables at a given λ |
| 9 — Prediction | CIP vs PI concepts | the **band shape** (narrowest at `x̄`, widens away); extrapolation and interval width |

## How to use

Do a topic's Problem, then check `solutions/`. If you get one wrong, the *first* set (`../practice/`) has
the conceptual version — come back here for the computation drill. These are short, focused sets (usually
2 problems), not full 47-point papers.
