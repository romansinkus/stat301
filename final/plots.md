# STAT 301 — Plots Reference (all topics)

*Every plot you may need to **read or draw**, with the topic it's from, its axes, what it shows, and the
good-vs-bad patterns. Plain-text (no LaTeX) for CLI printing. "Sketch?" = could the exam ask you to draw
it by hand (label both axes!).*

---

## Master table — all plots

| Plot | Topic | Axes (x → y) | Purpose / what it checks | Key features (good vs bad) | Sketch? |
|---|---|---|---|---|---|
| Scatterplot + fitted line | 1 (SLR) | X (cont.) → Y (cont.) | show linear relationship + LS line; residuals = vertical gaps | line through cloud; slope = direction | **Yes** |
| Bootstrap distribution (histogram) | 1 | bootstrap b̂1 → frequency | sampling distribution of the slope; 2.5/97.5 pctile = CI | roughly bell-shaped; spread = SE | maybe |
| Boxplot (categorical predictor) | 2 (MLR) | category → Y (cont.) | compare group means/spread; = regression w/ categorical X | box = IQR, line = median; gaps = group diffs | maybe |
| Grouped scatter + line per group | 2 | X (cont.) → Y, colored by group | additive vs interaction | **parallel = additive; non-parallel/crossing = interaction** | **Yes** |
| Scatterplot matrix / `ggpairs` | 2 (tut) | all pairs | EDA: pairwise scatter + correlations | spot strong pair correlations | read |
| **Residuals vs fitted** | 3 (diag) | fitted ŷ → residual ê | checks **L** (linearity) & **E** (equal var) | **good = flat random band at 0; curve = L bad; funnel = E bad** | **Yes** |
| **Q-Q plot** | 3 | theoretical Normal quantiles → residual quantiles | checks **N** (Normality) | **good = points on diagonal; off/curved tails = non-Normal** | **Yes** |
| Histogram of residuals | 3 | residual → frequency | checks Normality (symmetry) | good = bell-shaped, centered 0; skew = bad | maybe |
| (Independence) | 3 | — no plot — | **I** judged from study design | temporal/repeated data → likely violated | n/a |
| **Logistic S-curve** | 4 (logistic) | X → probability P(Y=1) | fitted probability, bounded (0,1) | **S-shape (sigmoid); flattens near 0 and 1** | **Yes** |
| Log-odds line | 4 | X → log-odds (logit) | the linear predictor L | straight line (range −∞..∞) | maybe |
| Group probability curves | 4 | X → P(Y=1), per group | additive vs interaction on prob scale | additive = non-crossing S-curves; interaction = can cross | maybe |
| Logistic residual plot | 4 | fitted → residual | why it's **useless** | **residuals collapse onto 2 lines** (Y is 0/1) → use binned/Pearson | read |
| Poisson mean curve | 5 (Poisson) | X → count | fitted mean λ = e^(…), always > 0 | exponential-shaped, never negative | maybe |
| Poisson residual plots | 5 | fitted → Pearson/deviance resid | diagnostics (limited use) | lean on overdispersion instead | read |
| Sums-of-squares diagram | 6 (GoF) | X → Y with mean line + fit line | visualize TSS/ESS/RSS as vertical gaps | point→mean = TSS; fit→mean = ESS; point→fit = RSS | maybe |
| Deviance residual plots | 7 (GLM GoF) | fitted → deviance resid | GLM diagnostics | same caveats as logistic residuals | read |
| **LASSO coefficient path** | 8 (selection) | log(λ) → coefficient values | shrinkage + selection as λ grows | **lines shrink toward 0, peel off to exactly 0**; top axis = # nonzero | read |
| **Cross-validation curve** | 8 | log(λ) → CV MSE (± 1 SE) | choosing λ | **U-shape; min = `lambda.min`; `lambda.1se` = simplest within 1 SE** | read |
| Bias–variance curve | 8 | complexity / λ → error | why we accept bias | total MSE = bias² + variance → **U-shaped total** | maybe |
| **Regression line + CIP & PI bands** | 9 (pred) | X → Y | prediction uncertainty | **two nested hourglass bands: narrow CIP (mean), wide PI (new Y); both narrowest at x̄** | **Yes** |

---

## The must-draw sketches (label both axes!)

### Residuals vs fitted — Topic 3 (the single most important diagnostic)
```
GOOD (assumptions hold)     CURVE = L violated          FUNNEL = E violated
 e|                          e|      __                  e|            . .
  |  . . .  .  .              |    /    \                 |        .  .  . .
 0|--.--.--.--.--.--         0|--/------\--.--           0|--.--.--.--.------
  |   .  . .  .               | .        \  /             |   . . .
  |______________ŷ            |___________\/___ŷ          |______________ŷ
 flat random band            arch/U-shape (nonlinear)    spread widens (heterosced.)
```
Good = structureless cloud around 0. **Curve → add X²/log (Linearity).** **Funnel → log(Y)/transform (Equal variance).**

### Q-Q plot — Topic 3 (Normality)
```
GOOD                         BAD (heavy tails)
 r|         .                 r|            .
  |      . .                   |         .
  |   . .                      |     . .
  | . .                        | . .
  |.___________ theo. quant.   |._________  (points curve off at the ends)
 points on the diagonal       tails veer off the line → non-Normal
```

### Additive vs interaction — Topic 2 / 4 (grouped lines)
```
ADDITIVE (parallel)          INTERACTION (different slopes / crossing)
Y|      ___ group B          Y|        /group B
 |   ___/                      |    ___/
 |__/___ group A               |___/____ group A     (lines can cross)
 |__________ X                 |__________ X
 same slope, shifted           slopes differ → effect depends on group
```

### Logistic S-curve — Topic 4
```
P(Y=1)
 1|            ______
  |          /
0.5|        /
  |       /
 0|______/___________ X      bounded in (0,1); linear on the LOG-ODDS scale
```

### LASSO path & CV curve — Topic 8
```
COEFFICIENT PATH                 CV CURVE (pick λ)
b|\  \                          MSE|  .              .
 | \  \___                         |   .           .
0|--\----\----=====-- 0             |     .       .
 |   \____\___                      |       . _ .   <- min = lambda.min
 |________________ log λ            |_______________ log λ
 lines shrink to exactly 0          U-shape; lambda.1se = largest λ within 1 SE
 (more λ → fewer nonzero)           of the min (simpler model)
```

### CIP vs PI bands — Topic 9
```
Y|          . PI (wide)  .
 |        .-----------.              two nested bands around the fitted line:
 |      .   CIP (narrow) .            - inner (narrow) = CIP  (the AVERAGE E[Y|X])
 |  .  .===== line =====.  .          - outer (wide)   = PI   (a single new Y, +e)
 |    .-----------.                  both PINCH at x̄ and FLARE at the extremes;
 |          . (wide) .               geom_smooth(se=TRUE) draws the CIP band, NOT the PI
 |__________________________ X
             x̄
```

---

## Quick lookup — "which plot checks which assumption?" (Topic 3)

| Assumption | Plot to inspect | Bad pattern |
|---|---|---|
| **L** — Linearity | residuals vs fitted | a curve / U-shape |
| **I** — Independence | *(no plot)* — study design | temporal / repeated-measures data |
| **N** — Normality | Q-Q plot (or residual histogram) | points off the diagonal / skew |
| **E** — Equal variance | residuals vs fitted | funnel (spread widens) |

*(Reminder: for **logistic/Poisson** the raw residual plot is nearly useless — residuals collapse onto lines and variance changes with the mean by design — so lean on the **overdispersion** check, not residual plots.)*

---

## By-topic index

- **Topic 1 (SLR):** scatter + line; bootstrap histogram.
- **Topic 2 (MLR):** boxplot; grouped scatter with per-group lines (additive vs interaction); ggpairs.
- **Topic 3 (Diagnostics):** residuals-vs-fitted (L, E); Q-Q (N); residual histogram; independence = design.
- **Topic 4 (Logistic):** S-curve (probability); log-odds line; group probability curves; the useless 2-line residual plot / binned.
- **Topic 5 (Poisson):** exponential mean curve; Pearson/deviance residual plots.
- **Topic 6 (GoF linear):** sums-of-squares decomposition diagram (mostly a metrics topic).
- **Topic 7 (GoF GLM):** deviance residual plots (mostly a metrics topic).
- **Topic 8 (Selection):** LASSO coefficient path; cross-validation curve; bias–variance U.
- **Topic 9 (Prediction):** regression line with CIP + PI bands (hourglass); `geom_smooth` band = CIP.
