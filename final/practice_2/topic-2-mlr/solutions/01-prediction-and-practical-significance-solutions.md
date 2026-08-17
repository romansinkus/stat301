# Solutions — Practice 01 (Topic 2): Prediction & Practical Significance

## Problem 1

**(a)** `ŵage = −2.00 + 0.60·education + 0.10·experience + 1.50·sexmale`, where **`sexmale = 0` for
females, `= 1` for males**.

**(b)** Female (`sexmale = 0`): `−2.00 + 0.60×12 + 0.10×10 + 1.50×0 = −2.00 + 7.20 + 1.00 + 0 = **$6.20/hr**`.

**(c)** Male (`sexmale = 1`): `−2.00 + 7.20 + 1.00 + 1.50 = **$7.70/hr**`. Male–female difference =
`7.70 − 6.20 = **1.50**`, which equals the **`sexmale` coefficient**. It's constant across all
education/experience values because this is an **additive** model — the dummy just *shifts the intercept*
by 1.50 (parallel lines), so the vertical gap never changes. *(4 pts: 2 arithmetic, 2 explanation.)*

**(d)** With `education:sexmale = 0.15`, the male line's **slope** on education becomes `0.60 + 0.15 =
0.75` while the female's stays `0.60`. So the male–female gap **grows by 0.15 for each extra year of
education** — it's no longer a fixed 1.50. The interaction lets the effect of sex *depend on* education
(non-parallel lines), so "same gap everywhere" fails.

## Problem 2

**(a)** **Yes — statistically significant.** `p = 3e-7 ≪ 0.05`, so reject `H0: β = 0`. Note the SE
(0.0008) is tiny largely *because* `n = 500,000` — SE shrinks like `1/√n`, so even a minuscule effect
clears the significance bar. *(Significance here is about the huge sample, not a big effect.)*

**(b)** Each additional monthly notification is associated with **$0.004 (0.4 cents)** more spending,
holding nothing else (simple model). Over **100** extra notifications: `100 × 0.004 = **$0.40**` — forty
cents. **Not practically important**: spamming 100 notifications to move spending by 40 cents is
negligible (and likely annoys customers). Statistically real, practically trivial.

**(c)** With huge `n`, SEs become so small that *any* nonzero effect turns "significant," so a small
p-value no longer implies a **meaningful** effect — you should always report the **effect size** (and its
CI), not just the p-value.

**(d)** Look at whether the **confidence interval** lies entirely within a range you'd consider
*negligible* — e.g. if the whole 95% CI for the effect is a few tenths of a cent, then even the most
optimistic end is practically meaningless. (Judge practical importance by the *magnitude* the CI covers,
not by whether it excludes 0.)
