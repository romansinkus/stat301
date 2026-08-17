# Solutions — Practice 01 (Topic 3): Log-Transformed Models

## Problem 1

**(a)** Logging `Y` often fixes **(1) non-constant variance (Equal-variance / heteroscedasticity — the
funnel)** and **(2) non-Normal, right-skewed residuals (the Q-Q drift)** simultaneously, and it can also
straighten mild curvature (Linearity). It's still **linear regression** because "linear" means **linear in
the parameters** (`b0 + b1·something`) — transforming the *variables* (`log`, `X²`, `√X`) is fine; the
model is linear in the `b`'s.

**(b)** Slope `0.08` on `log(wage)`:
- (i) **Exact:** `(e^0.08 − 1)×100 = (1.0833 − 1)×100 = **8.33%**`.
- (ii) **Approx:** `≈ 100×0.08 = 8%`. The approximation is good for **small** coefficients (roughly
  `|β| < 0.1`); it drifts as `β` grows.
- (iii) **"Each additional year of education is associated with an ~8.3% higher wage, holding else
  constant."** *(Percentage, multiplicative, "associated with.")*

**(c)** Two errors: (1) **wrong scale** — the coefficient is on `log(wage)`, not dollars, so it's **not**
"+$0.08"; (2) **additive vs. multiplicative** — a `log(Y)` coefficient means a **percentage/multiplicative**
change, not a fixed dollar add. Corrected: *"each extra year is associated with an ~8.3% increase in
wage."*

**(d)** A constant **percentage** effect means a **bigger dollar gap at high wages**: 8.3% of a $10 wage is
~$0.83, but 8.3% of a $50 wage is ~$4.15. Same percentage, larger absolute effect where wages are higher.

## Problem 2

**(a)** The coefficient is the **elasticity**. In a log–log model, a **1% increase in price** is associated
with approximately a **−1.5% change in sales** (a 1.5% *decrease*). Since `|−1.5| > 1`, demand is
**elastic** (sales respond more than proportionally to price).

**(b)** Level–log: dividing the coefficient by 100 gives the effect of a **1%** change. A **1% increase in
weight** → about `−6/100 = **−0.06 mpg**`. A **doubling** of weight (×2) → `−6 × ln(2) = −6 × 0.693 =
**−4.16 mpg**`. *(Level–log: 1% change → β/100; a factor-`c` change → β·ln(c).)*

**(c)**
| Model | `β` interprets as… |
| --- | --- |
| `Y ~ X` | a 1-**unit** rise in X → **β-unit** change in Y (level change) |
| `log(Y) ~ X` | a 1-**unit** rise in X → **~100·β %** change in Y (exact `(e^β−1)·100%`) |
| `Y ~ log(X)` | a **1%** rise in X → **~β/100 unit** change in Y |
| `log(Y) ~ log(X)` | a **1%** rise in X → **~β %** change in Y (**elasticity**) |

**(d)** Because the log–log coefficient is an **elasticity** — a **unit-free** "% per %" number — it doesn't
depend on the units of X or Y, so effects are directly comparable across variables measured on totally
different scales.
