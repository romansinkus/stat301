# Practice 09 — Comprehensive Midterm Practice Exam

*All topics. Time yourself (~75 min). Solutions:
[`solutions/practice-exam-solutions.md`](solutions/practice-exam-solutions.md).*

A researcher studies county-level cancer mortality with `US_cancer_data`
(`TARGET_deathRate` = deaths per 100 000; `povertyPercent`; `PctPrivateCoverage`; `state`, a
categorical with several levels). Unless told otherwise, use `alpha = 0.05`.

---

## Section A — Quick concepts (short written answers, ~1–2 marks each)

*(The real exam has no multiple choice — state each answer and give the one-line reason.)*

**A1.** In `E[Y|X] = b0 + b1*X`, what does the left-hand side `E[Y|X]` represent — a single
individual's value at `X`, or something else? State it precisely.

**A2.** A 95% confidence interval for a slope is `(2.1, 4.8)`. Give the **correct** interpretation of
this interval (in the repeated-samples sense), and state whether the slope is significant at the 5%
level and how you can tell.

**A3.** `anova(lm(TARGET_deathRate ~ state))` returns `p = 2e-16`. State the correct conclusion —
what does it say about the association between death rate and state (and what does it *not* say)?

**A4.** A residuals-vs-fitted plot shows a widening funnel. Which assumption is violated, and what is
the problem called?

**A5.** State the primary consequence of strong multicollinearity on the coefficients' standard
errors, and say whether it biases the slope estimates.

---

## Section B — Short answer / interpretation

**B1 [4].** `lm(TARGET_deathRate ~ povertyPercent)` gives a slope of `1.52` with a 95% CI of
`(1.40, 1.64)` and `p ≈ 0`. (a) Interpret the slope in one careful sentence. (b) Is it statistically
significant, and how do the CI and p-value each show that? (c) Rewrite the interpretation the way a
classmate might *incorrectly* phrase it, and say what's wrong.

**B2 [3].** Explain the difference between the **error term** and a **residual**, including which one
is observable and why they differ.

**B3 [4].** Compare **theory-based** inference (what `lm()` does) with **bootstrapping** for getting
the SE of a slope. State one assumption each relies on, and describe how bootstrap resampling works
(with replacement, size `n`).

**B4 [4].** The model `lm(TARGET_deathRate ~ povertyPercent + state)` is additive.
(a) Geometrically, what does this describe (lines and their relationship)? (b) Interpret the
`povertyPercent` coefficient. (c) The same `povertyPercent` slope differs from the SLR version — why?

**B5 [4].** For `lm(TARGET_deathRate ~ povertyPercent * state)` (Alabama = reference), the row
`povertyPercent:stateCalifornia` has `p = 0.28`. (a) What does this row test? (b) What do you
conclude about the two states' poverty slopes? (c) Which model (additive or interaction) is
justified, and why?

**B6 [3].** State the LINE assumptions. For each of L, I, E, give the consequence of violating it.

---

## Section C — Longer / applied

**C1 [5].** A newspaper headline: "Counties with more private health coverage have *lower* cancer
death rates — so buying private insurance prevents cancer deaths." Critique this causal claim using
at least two distinct ideas from Topic 3 (e.g. confounding, observational vs. experimental,
reverse causality). What kind of study *would* license a causal claim, and why?

**C2 [5].** You fit `lm(TARGET_deathRate ~ povertyPercent + PctPrivateCoverage + medIncome)` and find
huge standard errors on all three coefficients, though the model's overall fit is good. (a) Name the
likely problem and the intuition for why it inflates SEs. (b) How would you *diagnose* it (name the
metric and threshold, including the categorical-safe variant)? (c) Give two possible fixes and a
trade-off of each.

**C3 [4].** `lm(TARGET_deathRate ~ povertyPercent)` residuals-vs-fitted plot shows a funnel, and the
Q-Q plot bends away from the diagonal at the tails. (a) Name both violations. (b) Propose a single
transformation likely to help both, and explain the mechanism. (c) After the fix, what should the two
diagnostic plots look like?
