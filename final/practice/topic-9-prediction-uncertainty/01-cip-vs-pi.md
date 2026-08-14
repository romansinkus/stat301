# Practice 01 (Topic 9) — Prediction Uncertainty (CIP vs. PI)

*Topic 9. Solutions: [`solutions/01-cip-vs-pi-solutions.md`](solutions/01-cip-vs-pi-solutions.md).
Course dataset: Strathcona property tax (`assess_val ~ BLDG_METRE`).*

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Justify
> every true/false, and respect any word limits.

---

## Problem 1 (16 pts) — The two targets: CIP vs. PI

**(a) (3 pts)** Why is a prediction `ŷ = b̂0 + b̂1·X` itself a **random variable**? What is the source of
its randomness?

**(b) (4 pts)** For a house of a given size `X`, you might predict two different targets. Name them, give
the symbol for each (`E[Y|X]` vs. `Y`), and explain how they differ (which one includes the individual
error `e`?).

**(c) (5 pts)** Complete the table:

| | Confidence Interval for Prediction (CIP) | Prediction Interval (PI) |
| --- | --- | --- |
| Predicting | ? | ? |
| Sources of uncertainty | ? | ? |
| Width | ? | ? |
| Interpret with the word... | ? | ? |
| `predict(interval = ?)` | ? | ? |

**(d) (4 pts)** The three stacked equations `Y = E[Y|X] + e` → `Y = b0 + b1X + e` → `ŷ = b̂0 + b̂1X` are
"the one diagram to carry." Explain which **target** the CIP aims `ŷ` at, and which target the PI aims `ŷ`
at, using these equations.

---

## Problem 2 (16 pts) — Reading and applying `predict()` output

For a house of size 220 m, `predict()` gives:
- `interval = "confidence"`: `(671944, 748198)`
- `interval = "prediction"`: `(454519, 965622)`

**(a) (4 pts)** Explain **why the PI is always wider than the CIP**. Refer to the "two sources of
uncertainty" and why predicting one actual value is harder than predicting the average.

**(b) (3 pts)** Why does the CIP use the language of **"confidence"** while the PI uses the language of
**"probability"**? Tie your answer to whether the target is a **fixed number** or a **random variable**.

**(c) (5 pts)** (i) Which interval above is which type, and how can you tell at a glance? (ii) Write the
correct one-sentence interpretation of **each**. (iii) Both are centred at the same fitted value — roughly
what is it?

**(d) (4 pts)** (i) "The shaded band that `geom_smooth(se = TRUE)` draws around a regression line shows
where about 95% of the individual data points fall." True or false? Explain what the band actually
represents. (ii) A realtor wants to advise a single client on the likely assessed value of **their
specific** 220 m house — CIP or PI, and why? What if instead the city wants the **average** value of all
220 m houses for budgeting?
