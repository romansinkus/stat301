# Solutions — Practice 01 (Topic 4): Logistic Prediction by Hand

## Problem 1

**(a)** Female → `sexmale = 0`. `L = −1.00 + 0.015×100 + (−2.50)×0 = −1.00 + 1.50 + 0 = **0.50**`. `L` is
on the **log-odds** scale (the linear predictor / logit).

**(b)** `p = e^0.5 / (1 + e^0.5) = 1.649 / (1 + 1.649) = 1.649 / 2.649 = **0.622**`. Since `0.622 > 0.5`,
the classifier predicts **survived (1)**. *(3 pts conversion, 2 pts classification.)*

**(c)** Male → `sexmale = 1`. `L = −1.00 + 1.50 + (−2.50)×1 = **−2.00**`.
`p = e^−2 / (1 + e^−2) = 0.135 / 1.135 = **0.119**` → `< 0.5` → predicts **did not survive (0)**.
Log-odds difference (male − female) = `−2.00 − 0.50 = **−2.50**` = the `sexmale` coefficient ✓.
It is **not** −2.50 on the probability scale because the logit→probability map (the S-curve) is
**nonlinear** — the same −2.50 log-odds drop moves probability from 0.622 to 0.119, a change of about
−0.50, not −2.50. A constant log-odds effect is a *non*-constant probability effect. *(2 pts arithmetic,
2 pts diff = coef, 1 pt nonlinearity.)*

**(d)** Because a probability is trapped in `(0, 1)` — a straight-line model for `p` would predict
impossible values below 0 / above 1; the logit link stretches `(0,1)` onto the whole real line so a linear
predictor is valid, then we map back with `e^L/(1+e^L)`.

## Problem 2

**(a)** log-odds `= 0.5`. (i) **odds** `= e^0.5 = **1.649**`. (ii) **probability** `= odds/(1+odds) =
1.649/2.649 = **0.622**` (equivalently `e^0.5/(1+e^0.5)`).

**(b)** `p = 0.80`. (i) **odds** `= p/(1−p) = 0.80/0.20 = **4**`. (ii) **log-odds** `= ln(4) = **1.386**`.

**(c)** (i) OR `= e^−2.5 = **0.082**`. (ii) `OR < 1` → decrease `= (1 − 0.082)×100 = **91.8%**`: males have
about **91.8% lower odds** of survival than females (holding fare constant). (iii) Yes — it's the same
significance statement: "significant if the CI excludes **0** on the **log-odds** scale," which is the same
as excluding **1** on the odds/exponentiated scale. *(Watch the subtract-from-1 step: 0.082 → 91.8% lower,
not "8% lower.")*

**(d)** raw `glm` coefficients → **log-odds**; `exponentiate = TRUE` → **odds (odds ratio)**;
`predict(type = "response")` → **probability**.
