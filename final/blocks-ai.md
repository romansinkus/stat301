# Dense Blocks — copy-paste study snippets

*All the dense blocks for the **cumulative final**, grouped by **Topic 1 / Topic 2 / Topic 3 / GLM Bridge /
Topic 4 / Topic 5 / Topic 6 / Topic 7 / Topic 8 / Topic 9 / General**. Each is a compact,
copy-paste-ready summary. No emojis; `[slots]` = fill-in. Notation: β = true parameter, b̂ = estimate,
e = error, ŷ = fitted.*

> **Final exam (confirmed — `slides/final-review.pdf`):** Wed **Aug 19, 2026, 3:30–5:40pm (130 min),
> Life Building 2302**. Cumulative (Topics 1–9), **more weight post-midterm**. You may bring **TWO
> letter-size sheets** (both sides) — twice the midterm's one, so there's room for the second-half
> blocks below. Written answers only; R code not tested but its **outputs** are. Bring a calculator.
> **Prioritize the post-midterm blocks (GLM Bridge, T4–T9) for your second sheet.**

---

# INDEX (91 blocks)

**Topic 1 — SLR & Inference (18)**
- T1.1 Least squares (LS)
- T1.2 Error vs. Residual (exam trap)
- T1.3 Role of `e` in the SLR
- T1.4 `y = β0+β1X+ε` vs `E[Y|X]` (+ extrapolation)
- T1.5 Correlation vs. regression
- T1.6 z-statistic
- T1.7 Variance vs. SD vs. SE
- T1.8 Role of the t-distribution
- T1.9 CI ⇔ test equivalence + t ≈ Normal
- T1.10 Theory-based vs. Bootstrap
- T1.11 Two ways to build a CI
- T1.12 SSE vs. SE vs. CI
- T1.13 p-value literacy
- T1.14 Hypothesis test for a coefficient
- T1.15 Statistical vs. practical significance
- T1.16 Interpreting the slope & intercept
- T1.17 b̂ is a random estimator (unbiased + sampling dist.)
- T1.18 R² — goodness of fit

**Topic 2 — MLR (9)**
- T2.1 Interaction term (meaning + when to remove)
- T2.2 Testing an interaction
- T2.3 Plot choice (continuous vs categorical predictor)
- T2.4 Categorical predictors & dummy variables
- T2.5 Interpreting categorical coefficients
- T2.6 Additive model (parallel lines)
- T2.7 ANOVA — comparing 3+ group means
- T2.8 Additive vs. Interaction (side-by-side)
- T2.9 "Common slope" (and why not to assume it)

**Topic 3 — Diagnostics, Multicollinearity & Causality (11)**
- T3.1 LINE assumptions
- T3.2 Model diagnostics (residual & QQ plots)
- T3.3 Fixing assumption violations (3 tools)
- T3.4 Independence (I) assumption
- T3.5 Multicollinearity
- T3.6 Experimental designs (CRD vs RBD)
- T3.7 Experimental vs. Observational
- T3.8 Confounding
- T3.9 Reverse causality
- T3.10 Simpson's paradox
- T3.11 Interpreting log-transformed models (log-level / level-log / log-log elasticity)

**GLM Bridge — Topics 4 & 5 in one idea (3)**
- GB.1 The link-function idea (the whole trick)
- GB.2 The three GLM families (pick by response type)
- GB.3 Two structural facts (no `e`; MLE not LS)

**Topic 4 — Logistic Regression (binary response) (10)**
- T4.1 When to use it + why not ordinary linear regression
- T4.2 The logit model — three equivalent forms (prob / log-odds / odds)
- T4.3 Interpreting coefficients — the THREE scales
- T4.4 Categorical predictor = odds ratio between groups
- T4.5 Additive vs. interaction (log-odds scale; the parallel-curve trap)
- T4.6 Inference — the Wald statistic
- T4.7 Prediction & fitted values — WHICH scale?
- T4.8 Residuals — why the residual plot is useless
- T4.9 Overdispersion (the key diagnostic)
- T4.10 Overdispersion — the deeper mechanics (variance-locked; individual vs grouped; √φ; quasi trade-off)

**Topic 5 — Poisson Regression (count response) (6)**
- T5.1 When to use it + two problems that rule out linear regression
- T5.2 The log-link model
- T5.3 Interpreting coefficients — TWO scales (rate ratios) + the multiplicative derivation
- T5.4 The `factor()` gotcha
- T5.5 Overdispersion — Poisson USUALLY over-disperses
- T5.6 Logistic vs. Poisson (one-line contrast)

**Topic 6 — Goodness of Fit, linear models (9)**
- T6.1 "Better than nothing?" — the null (intercept-only) model
- T6.2 The three sums of squares (TSS = ESS + RSS)
- T6.3 R² — coefficient of determination
- T6.4 Adjusted R² (fixing the "always increases" flaw)
- T6.5 RSE & MSE (training vs. test)
- T6.6 F-test Case A — model vs. the null
- T6.7 F-test Case B — any nested pair (extra block)
- T6.8 t-test vs. F-test
- T6.9 AIC / BIC + `glance()` vs `anova()`

**Topic 7 — Goodness of Fit for GLMs (5)**
- T7.1 Deviance = "RSS for GLMs" (null vs. residual deviance)
- T7.2 The deviance test (χ²) — comparing nested GLMs
- T7.3 Why a perfect fit is BAD (saturated model / overfit)
- T7.4 Cheat-sheet mapping (linear vs. GLM)
- T7.5 Deviance in R — the worksheet-07 workflow (breast-cancer logistic)

**Topic 8 — Model Selection (7)**
- T8.1 Stepwise vs. regularization (greedy jumps vs. smooth shrinkage)
- T8.2 Ridge vs. LASSO (the two penalties)
- T8.3 The penalty λ + choosing it by cross-validation
- T8.4 Bias–variance tradeoff (why accept a biased estimator)
- T8.5 The post-inference / double-dipping problem (+ the simulation proof)
- T8.6 postLASSO + the fix (split the data)
- T8.7 Stepwise in R — the tutorial-07 workflow (`regsubsets` / `stepAIC`)

**Topic 9 — Prediction Uncertainty (5)**
- T9.1 What are you predicting? (average vs. actual)
- T9.2 CIP vs. PI (side-by-side)
- T9.3 Why the PI is always wider
- T9.4 Interpretation templates + the `geom_smooth` band
- T9.5 The interval band shape (hourglass) & extrapolation

**General — cross-cutting (5)**
- G.1 Phrasing bank (dense) — G.1a Coefficients · G.1b Inference · G.1c Causation · G.1d ANOVA/diagnostics/multicollinearity
- G.2 Equations (dense) — G.2a SLR · G.2b MLR · G.2c assumptions & collinearity · G.2d quick calc · G.2e Topics 4–9
- G.3 Reading a regression output table
- G.4 Terminology / synonyms
- G.5 Inference distributions — data vs. inference; t vs z; the null yardstick

**Notes — handwritten review (3)**
- N.1 Topic 1 review points
- N.2 Topic 2 review points
- N.3 Topic 3 review points

---

# TOPIC 1 — SLR & INFERENCE

**T1.1 Least squares (LS)**
Choose the `b`'s to **minimize the sum of squared *vertical* distances** = **SSR = Σ(yᵢ − ŷᵢ)² = Σ(yᵢ − (b̂0 + b̂1x1ᵢ + … + b̂pxpᵢ))²** (sum of squared residuals; = SSE = RSS). Writing ŷ out shows SSR is a **function of the coefficients you're choosing** — LS picks the b's that make it smallest. The distances are **vertical** (in the Y direction, since we're explaining Y). We **square** the residuals to (1) **remove signs** (so + and − don't cancel) and (2) **penalize large misses** more heavily.

**T1.2 Error vs. Residual (exam trap)**
Same idea (a point's vertical gap from a line), **different line**. **Error `e_i = y_i − (b0 + b1x_i)`:** gap from the **TRUE** line; lives in the **population** (true model); **unknowable** (you never see the true line). **Residual `ê_i = y_i − ŷ_i = y_i − (b̂0 + b̂1x_i)`:** gap from the **FITTED** line; lives in the **sample**; **observable** (computed from data). They differ because `b̂ ≠ b`; the residual is the observable **stand-in** for the invisible error.

**T1.3 Role of `e` in the SLR (`Yᵢ = b0 + b1Xᵢ + eᵢ`)** — `e` = **everything affecting Y that X doesn't capture** = **omitted variables + pure random noise** (not just "measurement error").
- **Makes the model stochastic, not deterministic:** without `e` every point sits exactly on the line; `e` is why two obs with the **same X** can have **different Y**, and it produces the **scatter around the line.** *Deterministic* (`E = mc²`, `A = πr²`) = X **completely fixes** Y, **no uncertainty**; *stochastic* = only a **tendency** with scatter (taller people **tend to** weigh more) — regression models the stochastic world.
- **Separates average from individual:** `E[Y|X] = b0 + b1X` = the line (the *average* Y at each X); `eᵢ` = how far individual `i` sits **off** that line.
- **Not a value you plug in:** `e` is **random and unobservable** — you use the **residual** as its observable stand-in, and when **predicting you drop `e`** (it averages to 0), leaving `ŷ = b̂0 + b̂1·x`.
- **Assumptions ride on `e`** (LINE: independent, Normal, constant variance σ²); **σ = SD of `e`.**
- **One-liner:** `e` = all of Y not explained by X (other variables + noise); it makes the model stochastic and creates the scatter around the line.

**T1.4 `y = β0 + β1X + ε` vs `E[Y|X] = β0 + β1X` (NOT equal)**
`E[Y|X] = β0 + β1X` is **the line** — the **average of Y over all individuals at a given X** (smooth, **no error term**). `Yᵢ = β0 + β1Xᵢ + εᵢ` describes **one specific observation**, which **includes the error εᵢ** (the true relationship *plus* its messiness) and sits **off the line** by that error. The line is the **center of the cloud**; individual points **scatter around it** — the model predicts the **center of the cloud, not one point**. Also: the fitted line is **valid only within the observed range of X** (**no extrapolation**).

**T1.5 Correlation vs. regression**
**Correlation** treats **both variables as random/stochastic** (symmetric — no response/predictor role); it measures the strength + direction of linear association. **Regression** treats **X as fixed / non-stochastic** and models the conditional average **E[Y|X]** (asymmetric — one response Y, one predictor X). In **SLR**, the **slope and the correlation always share the same sign** (both carry the sign of the covariance) — so `r > 0 ⇔ slope > 0`. **Regression is directional: `Y on X` ≠ `X on Y`** — you **cannot** algebraically invert `y = b̂0 + b̂1x` to get the X-on-Y line, because that line minimizes *horizontal* residuals and has a different slope (`r·s_x/s_y`, not `1/b̂1`); the two coincide only if `r = ±1` (all points collinear). **Scope:** the response **Y must be continuous** to use linear regression.

**T1.6 z-statistic**
`z = b̂ / SE(b̂)` = **estimate ÷ uncertainty**. Numerator `b̂` = the **estimate**; denominator `SE(b̂)` = the **SE of the estimate** = **how stable/precise it is** (its sample-to-sample wobble). So z = **how many SEs your coefficient sits from 0** → it measures whether the effect is **real or just noise**. **Big |z| (> 1.96)** ⇒ far from 0 relative to its uncertainty ⇒ **significant / real effect**; **small |z|** ⇒ could be noise.

**T1.7 Variance vs. SD vs. SE ("SD of *what*?")**
`SD = √variance`; `SE = the SD of an *estimate*` (a special SD). **Variance** = spread of the **data**, squared (units²). **SD** = spread of the **data points**, original units (`SD = √variance`). **SE** = spread of an **estimate across samples** = its **precision**, original units of the estimate (`SE = SD/√n` for a mean). **Key trap:** SE is **NOT the scatter of points around the line** (that's σ / SD) — it's the **wobble of the coefficient/estimate.**

**T1.8 Role of the t-distribution**
`z = b̂/SE`, where `SE = σ̂/√Σ(x−x̄)²` uses the **estimated σ̂**, not the true σ. If σ were **known** → z is exactly **Normal**; because σ is **estimated**, the denominator is also random → more spread → **heavier tails → t-distribution**. Heavier tails = extra uncertainty ⇒ true cutoff slightly **above 1.96** for small samples. Shape set by **df = n − k**: small df ⇒ fatter tails; large df ⇒ σ̂ ≈ σ ⇒ **t → N(0,1)** (cutoff → 1.96). Course uses **Normal/1.96 always**. **One line: known σ = Normal; estimated σ = t; t → Normal as df grows.**

**T1.9 CI ⇔ test equivalence + t ≈ Normal**
*"A 95% CI for β3 contains 0"* ⟺ *"fail to reject H0: β3 = 0 at 5%"* ⟺ **not significant** ⟺ true β3 may be 0. Flip side: **CI excludes 0 ⟺ reject ⟺ significant.** **Confidence level + α = 100%** (95% CI ↔ 5% test; 90% ↔ 10%; 99% ↔ 1%; so confidence = 1 − α). The exact sampling distribution of `z = β̂/SE` is a **t with df = n − k**, but **t → N(0,1) as df → ∞** (already ≈ Normal for df ≥ 10), so this course uses the **standard Normal (1.96) for all regression inference.**

**T1.10 Theory-based vs. Bootstrap**
Both target the **same thing** — the **sampling distribution of b̂** (→ SE, CI, p) — but differ in whether they **assume its shape** or **build it from data**. **Theory-based:** gets the sampling dist. from a **formula** (assumes a shape); key assumption = **errors Normal** (or large-n **CLT**); best when **assumptions hold / n large**; SE & CI from the **t/z distribution** (`n−k` df); **instant**. **Bootstrap:** **resamples** the data empirically to build the sampling dist.; **no assumption** about error shape; best for **non-Normal errors / small n**; SE from the **spread**, CI from **percentiles** (2.5/97.5); costs **many refits** (B ≈ 10,000). **Three nuances:** (1) some estimands have **no SE formula** — the **median** and the **correlation r** — so bootstrap is the **only** option, not just an alternative; (2) when assumptions **do** hold, the **formula CI is narrower** (more precise) than the bootstrap one — that's the reason to still use it; (3) the **CLT** (`√n(ȳ−μ) → N(0,σ²)`) is what lets theory use the Normal even with non-Normal errors, **provided n is large**.

**T1.11 Two ways to build a CI**
Both give a CI for the **true parameter** and are **read identically**; they differ in how it's built. **Theory / formula:** `b̂ ± 1.96·SE` (95%); assumes **Normal errors / CLT**; SE from the **formula** `σ̂/√Σ(x−x̄)²`; best when **assumptions hold / large n**; **symmetric** about b̂. **Bootstrap percentile:** **2.5 / 97.5 percentiles** of resampled estimates; **no assumption** about error shape; SE from the **spread of resampled estimates**; best for **non-Normal errors / small n**; **not necessarily symmetric** (follows the data's shape). `z*` = 1.96 (95%), 1.645 (90%), 2.576 (99%). Read (either): "across many samples, 95% of such intervals contain the true parameter" — NOT "95% probability the truth is in this one interval."

**T1.12 SSE vs. SE vs. CI**
Three stages: **fit → precision → inference**. **SSE/SSR = `Σ(yᵢ−ŷᵢ)²`** = total squared residuals; measures **fit of the line to the data**; units (Y)²; what **LS minimizes**; **one per model**; bigger ⇒ worse fit. **SE = SD of the sampling dist. of an estimate**; measures **wobble/precision of `b̂`**; coefficient's units; **quantifies** uncertainty; **one per coefficient**; bigger ⇒ less precise. **CI = `b̂ ± 1.96·SE`** = plausible **range for the true parameter**; about **inference**; coefficient's units; **expresses** uncertainty as a range; **one per coefficient**; bigger ⇒ more uncertain (wider). Chain: **SSE → σ̂ → SE → CI** (SSE = data/fit; SE & CI = the estimate/inference).

**T1.13 p-value literacy**
The p-value = the probability, **if H0 were true**, of a test statistic **at least as extreme** as the one observed. **Small p = strong evidence against H0** (magnitude = *strength of evidence*). It is **NOT**: the **effect size** (that's the estimate), **NOT** P(H0 is true), **NOT** "probability the results are due to chance", **NOT** P(H1 is false). With large n a **tiny** slope can have a **microscopic** p. Report "**< 0.001**", never "0".

**T1.14 Hypothesis test for a coefficient**
`H0: β = 0` (no linear association) vs `H1: β ≠ 0` (association) — always about the **population parameter β**, never `β̂` (a computed number). Statistic `z = b̂/SE`; **reject if |z| > 1.96 / p < α / CI excludes 0**. Say "**reject H0**" or "**fail to reject H0**" — **never "accept"/"prove"** (fail to reject ≠ H0 true; absence of evidence ≠ evidence of absence). One-sided `H1: β > 0` only with a directional prior; default is two-sided.

**T1.15 Statistical vs. practical significance**
**Statistical** significance = evidence the effect is **not 0** (small p / CI excludes 0) — says nothing about size. **Practical** significance = the effect is **big enough to matter** (magnitude of the estimate). With **large n**, a tiny, trivial effect can be highly statistically significant. Always read **both**: evidence (p / CI) **and** effect size (the estimate).

**T1.16 Interpreting the slope & intercept**
The core skill of the course. **Slope b̂1:** "a 1-unit increase in `[X]` is **associated with** an expected [increase/decrease] of `[|b̂1| units]` in `[Y]`, **on average**." Always **"associated,"** never "causes"/"leads to"/"effect of" (SLR = association only), and it's about the **average** Y (E[Y|X]), not any one individual. **Intercept b̂0:** the **expected Y when X = 0**; often not meaningful — **flag it** when X = 0 is outside the data range or physically impossible (the course "doesn't care as much" about b̂0). Always state the **units**, and pair the estimate b̂ (a number) with its **uncertainty** (SE / CI) before concluding.

**T1.17 b̂ is a random estimator (unbiased + sampling distribution)**
b̂0, b̂1 are computed **from the sample**, so a different sample gives different values → each is a **random variable** with a **sampling distribution**. **Unbiased: `E[b̂1] = β1`** — averaged over samples the estimate lands on the true value (centered on the truth, not systematically high/low). Inference needs **two things: (1) an unbiased estimate** (b̂) **and (2) its uncertainty** (SE). You never observe β — only ever b̂ and a CI around it. **Frequentist view:** the true β (and any prediction of the mean) is a **fixed unknown constant** — only the **estimator b̂ is random**; that's why a CI's randomness is in the **interval**, not β (contrast Bayesian, where parameters *are* random — out of scope). This sampling distribution is exactly what SE, z, CI, and bootstrap all describe (theory **assumes** its shape; bootstrap **builds** it from data).

**T1.18 R² — goodness of fit**
`R² = 1 − SSR/SST` = the **fraction of the variation in Y explained by the model** (0 to 1; higher = tighter fit). Say: "the model explains `[R²·100]`% of the variation in `[Y]`." **Traps:** a **low R² (e.g. 40%) can still be a useful model**; a **high R² does NOT** mean the model is correct, the assumptions hold, the relationship is causal, or the slope is significant (**significance is about z/p, not R²**). R² **never decreases** when you add predictors, so a bigger R² alone does not mean a better model.

---

# TOPIC 2 — MLR

**T2.1 Interaction term (meaning + when to remove)**
`y = β0 + β1x1 + β2x2 + β3(x1·x2) + e`. A **significant** interaction (β3 ≠ 0) means the association between `y` and `x1` **depends on the value of `x2`** (and vice versa) — you **can't state x1's effect without knowing x2**. It complicates interpretation, so **if the interaction (β3) is NOT statistically significant, remove it** and use the simpler **additive** model. **If β3 IS significant → keep it and interpret by fitting/plotting two separate lines** (one per group): reference-group slope = **β2**, other-group slope = **β2+β3** (β3 = the *slope gap*, not a slope). An interaction can occur between **any two predictors**.

**T2.2 Testing an interaction**
`H0: β3 = 0` (no interaction) vs `H1: β3 ≠ 0` (interaction). Test statistic **`z = β̂3 / SE(β̂3)`**, compared to the **standard normal**. **If |z| > 1.96 → reject H0 ⇒ there IS an interaction** (p < 0.05); otherwise fail to reject (drop it, use additive). Equivalently, use the **95% CI for β3 = `β̂3 ± 1.96·SE(β̂3)`**: if it **excludes 0**, significant. (**CI excludes 0 ⇔ |z| > 1.96 ⇔ p < 0.05**.)

**T2.3 Plot choice (continuous vs categorical predictor)**
**Continuous X + continuous Y → scatterplot + line** (shows the relationship/slope; visualizes a continuous-predictor SLR). **Categorical X + continuous Y → boxplot** (compares Y's distribution across groups). A boxplot isn't a model, but it **visualizes a linear regression with a categorical predictor** (`Y = b0 + b1·D`: b0 = reference mean, b1 = difference of means) — **no line, but still linear regression** ("linear" = in the *parameters*, not a straight line). So **scatter+line ↔ continuous predictor (slope); boxplot ↔ categorical predictor (group means).** **Cat + continuous together:** colored scatterplot with **one line per group** — parallel (additive) or non-parallel (interaction).

**T2.4 Categorical predictors & dummy variables**
A categorical predictor enters MLR as **0/1 dummy variables**, not as its raw labels; R must be told it is categorical (`factor()` / `as.factor()`) or it treats the codes as **numbers**. **The first level is the reference** (its dummy is all 0; R picks it alphabetically by default, changeable). An **L-level** categorical needs **L−1 dummies** (one 0/1 column per non-reference level) — a **2-level** one needs just **one** dummy. **Dummy encoding = L−1 columns** (drops the reference); **one-hot = L columns** (one per level). MLR uses **L−1** to avoid perfect collinearity with the intercept. Each dummy's coefficient is read **relative to the reference** (see T2.5).

**T2.5 Interpreting categorical coefficients**
For a pure categorical model `Y = β0 + β1D` (2 levels): **b̂0 = mean Y in the reference group**, **b̂1 = the difference in mean Y** (other − reference). b̂1 is a **difference of means, NOT the other group's mean** (that mean is b̂0 + b̂1). For **L levels**: b̂0 = reference mean; **each dummy coefficient = that level's mean minus the reference mean**. Testing `H0: β1 = 0` on a 2-level categorical is **exactly the two-sample t-test** of the group means. Phrasing: "mean `[Y]` for `[level]` is `[b̂]` higher/lower than `[reference]`," never "the mean for `[level]` is `[b̂]`."

**T2.6 Additive model (parallel lines)**
`Y = β0 + β1X1 + β2X2 + … + e` — **no product terms**, so each predictor's effect is the **same regardless of the others' values**. Interpret every slope **"holding the other predictors constant"**: a 1-unit rise in X1 is associated with a b̂1 change in Y **at any fixed** value of the others. For a **categorical + continuous** additive model (`Y = β0 + β1D + β2X`) the groups get **parallel lines** — **b̂1 = the constant vertical gap** between them (intercept shift), **b̂2 = the common slope** shared by both groups. The additive model is the **default** MLR and the baseline an interaction is tested against (T2.1/T2.2); "holding constant" is valid **only** when there is **no interaction**.

**T2.7 ANOVA — comparing 3+ group means**
A categorical predictor with **2 levels** → two-sample **t-test**; with **3+ levels** → **ANOVA** (equivalently, regression on the L−1 dummies). ANOVA's **F-test**: `H0: all group means equal` vs `H1: at least one differs`. **Reject (small p) ⇒ at least one group mean differs** — the categorical variable **is associated** with Y. It does **NOT** say **which** groups differ or **which is highest** (that needs the individual coefficients / pairwise comparisons). It is **one overall test** for the whole categorical variable, not one per level.

**T2.8 Additive vs. Interaction (side-by-side)**
Same predictors, one difference: the **product term `β3·(X1·X2)`**. **In one line (cat×cont):** additive = **same slope, different intercepts** (parallel); interaction = **different slopes, different intercepts** (non-parallel). *Both* let the **intercept** differ (that's the `β1·D` term, in both models) — the interaction **only** adds the freedom for **slopes** to differ, so the intercept is never the distinguishing feature. **Additive** `Y = β0 + β1X1 + β2X2 + e` — each effect is the **same regardless of the other** ⇒ **parallel lines** (cat×cont: common slope β2, intercept gap β1); you **CAN** say **"holding the other constant."** **Interaction** `Y = β0 + β1D + β2X + β3(DX) + e` — one predictor's effect **depends on** the other ⇒ **non-parallel lines** (ref slope **β2**, other slope **β2+β3**; β3 = *slope gap*); you **CANNOT** say "holding constant." **Which to use:** default to additive (simpler); **test `H0: β3 = 0`** (T2.2) — **keep** the interaction only if β3 is **significant** (`|z|>1.96` / CI excludes 0), else **drop it**. Visual tell: draw one line per group — **parallel ⇒ additive, crossing/fanning ⇒ interaction.**

**T2.9 "Common slope" (and why not to assume it)**
The **slope** = how much Y changes per 1-unit rise in the continuous X. A **common slope** means **every group shares the same X-effect** — the additive model (`Y = β0 + β1D + β2X`) forces this: only the **intercept** differs (β1), the slope β2 is **shared** ⇒ **parallel lines**. *"Extra experience is worth the same wage bump for everyone."* **Not assuming a common slope** = let **each group have its own slope** via an interaction (`+ β3·DX`): ref slope **β2**, other slope **β2+β3** ⇒ **non-parallel lines**; β3 = how much the slopes **differ**. Assuming a common slope is a **restriction** — if the true slopes really differ, the additive model is **misspecified** and its single slope misleads. **Don't assume it blindly: fit the interaction and test `H0: β3 = 0`** — not significant ⇒ common slope is fine (simplify to additive); significant ⇒ slopes genuinely differ, keep the interaction (and you can **no longer** say "X's effect, holding group constant" — the effect *depends on* the group).

---

# TOPIC 3 — DIAGNOSTICS, MULTICOLLINEARITY & CAUSALITY

**T3.1 LINE assumptions**
The 4 assumptions (stated about the errors `e`). **One sentence: `e₁…eₙ` iid `N(0,σ²)`** — iid = **I**ndependent + identically distributed (constant variance, E); N(0,σ²) = **N**ormal + **mean 0** (=E(e)=0, the L part) + constant **σ²** (E). **L — Linear** (E[Y|X] linear *in the parameters*; E(e)=0): diagnose via residuals-vs-fitted (want no curve); violation ⇒ **model dubious**; fix by `X²`/`log`/interaction. NB *"linear in the parameters, not the predictors"* — `y=β0+β1x+β2(1/√x)+e` is **still linear regression.** **I — Independent** errors: judge from **study design** (temporal/repeated-measures breaks it); violation ⇒ **SEs biased ⇒ CIs & tests invalid**. **N — Normal** errors: Q-Q plot (on diagonal) + histogram; **least severe** (CLT/bootstrap rescue). **E — Equal variance** (constant σ²): residuals-vs-fitted (**funnel = bad**); violation ⇒ **SEs wrong ⇒ CIs & p invalid**. **Consequences:** estimates fine under I/E/N; **I & E break the SEs**; **L** breaks the model. `lm` assumes these — **checking them is YOUR job.**

**T3.2 Model diagnostics (residual & QQ plots)**
After fitting, you must check the assumptions (else results misleading/biased). Two tools: **(1) Residual plot** = residuals vs **fitted values ŷ** → checks **Linearity** (want no curve) and **Equal variance** (want constant spread, no funnel); good model ⇒ structureless cloud around the horizontal 0 line. **(2) QQ plot** = residual quantiles vs normal quantiles → checks **Normality**; good ⇒ points on the diagonal. **Why plot vs fitted ŷ (not observed y or x)?** Because **Corr(residual, ŷ) = 0** by the least-squares construction → a correct model shows **no trend**, so any pattern signals a problem. `Corr(residual, y) ≠ 0`, so plotting vs y would show a **spurious trend even for a good model**.

**T3.3 Fixing assumption violations (3 tools)**
**(1) Variable transformations** — transform X and/or Y (e.g. `log(y)`, `√y`, `1/y`, `log(x)`, `x²`, `1/x`) → can fix **non-linearity, non-normality, AND non-constant variance**. **(2) Add terms** — **interaction** or **quadratic (`x²`)** terms → mainly for **non-linearity**, when a transformation isn't enough. **(3) Bootstrap** — for **non-normal data or small n**; gives more **reliable SEs** without the Normality assumption. (Maps to LINE: transforms hit L/N/E, adding terms fixes L, bootstrap handles N / small n.)

**T3.4 Independence (I) assumption**
If the response data are **not independent** (e.g. **repeated measurements** on the same subject, **longitudinal / time-series data**), you should **not use the usual linear regression** — instead use specialized **longitudinal / correlated-data methods** (out of scope). Judge independence **informally** by **(i) how the data were collected** and **(ii) common sense** — often there's no plot; it's a design question. Violation ⇒ **biased SEs ⇒ invalid CIs & tests.**

**T3.5 Multicollinearity**
Predictors highly correlated **with each other** ⇒ **SEs and p-values inflated** (larger than necessary ⇒ imprecise estimates; point estimates stay ~unbiased). **Perfect vs. near:** *perfect* collinearity (one predictor an exact linear function of others, e.g. income in \$ and in \$1000s) makes the coefficients **non-identifiable** — infinitely many coefficient sets give the **identical SSR**, so R returns **`NA`**; in practice you see only *near* collinearity ⇒ inflated SEs. **Detect:** (1) **pairwise correlations** among continuous predictors (informal — if two are highly correlated, keep one), but **pairwise is NOT enough** (a *common mistake*): collinearity can involve **3+ variables** with no single high pair; (2) **VIF** / **GVIF** (categoricals) — the **more formal** check — flag if **too large (> 5, or √5 for `GVIF^(1/(2Df))`)**. **VIF intuition:** how much a coefficient's SE is inflated when fitted **with** the other predictors vs. **alone** (`VIF_j = 1/(1−R²_j)`, R²_j from regressing X_j on all other predictors). **Fix:** **drop** one collinear variable (`y = β0 + β1X1 + e`) **or combine** them (`y = β0 + β1·((X1+X2)/2) + e`).

**T3.6 Experimental designs (CRD vs RBD)**
**CRD (Completely Randomized):** randomize units **freely** across treatments; balances **observed AND unobserved** confounders ⇒ **gold standard**; use as the **default**. **RBD (Randomized Block):** first split units into **homogeneous blocks** (on a known nuisance factor), then randomize **within** each block; balances **observed only** (just the blocking factor — **not** unobserved); estimates **average** treatment effects; use when there's a **known strong nuisance factor** to control. Both beat an **observational** study (which balances **nothing** — you can only adjust for confounders you measured).

**T3.7 Experimental vs. Observational**
Whether you can claim **causation** depends on **how the data were collected — not the p-value or model fit.** **Experimental (randomized):** treatment **assigned by researcher, randomly**; **observed AND unobserved confounders balanced** (on average); handle via **randomization (the design)**; ⇒ **causal claim = YES (gold standard)**; but often **impractical/unethical**. **Observational:** treatment **occurs naturally / self-selected**; observed confounders **adjusted for (only if measured)**, but **unobserved ones remain (can't adjust)**; handle via **adjustment / stratification**; ⇒ **causal claim = NO, association only**; always available. *Course example:* randomize the ad ⇒ recovers true **+8**; customers self-choose ⇒ **confounded (9.83, inflated)**.

**T3.8 Confounding**
A **confounder** is a variable associated with **both** the response Y **and** at least one predictor X. It manufactures a **spurious/misleading association** between X and Y, so **leaving it out biases** the estimate of X's effect — the classic engine behind "correlation ≠ causation." *Example:* smoking vs. cancer — **lifestyle** affects **both** whether someone smokes **and** their cancer risk. **Two fixes:** (1) **adjust** for it (add it to the model / stratify) — but this only works for confounders you **measured** (and thought to collect — **unknown** ones can't be adjusted for), so **unmeasured** ones still bias you ⇒ an observational study can **never fully rule out** confounding; (2) **randomize** the treatment (experiment) — balances **all** confounders, **measured and unmeasured**, which is exactly why randomization licenses a **causal** claim. Bottom line: adjusting for known confounders **reduces** bias but does **NOT** prove causation from observational data (ties to T3.6/T3.7).

**T3.9 Reverse causality**
A second reason association ≠ causation (besides confounding, T3.8): the **causal arrow may run backwards** — instead of X causing Y, **Y causes X**. So a real association gives **no clue** which way causation flows. *Slide example:* kids who get regular **homework help** tend to score **worse** — not because help hurts, but because **struggling kids are the ones who receive help** (outcome → treatment). Randomization / knowing the data's time order rules it out; a pure cross-sectional observational association cannot. Flag it whenever the "cause" could plausibly be a **response to** the outcome.

**T3.10 Simpson's paradox**
An association can **reverse sign** when you go from the **aggregate** data to **within-group strata** (i.e. after conditioning on a lurking third variable). *Slide example:* 1973 **UC Berkeley** admissions looked biased **against women** overall, yet **within almost every department** women were admitted at rates **as high or higher** — because women applied more to **competitive (low-admission) departments**. Lesson: an unadjusted/marginal association can be **misleading or backwards**; the "right" grouping (here, department — itself a confounder) can flip the conclusion. A vivid case of why **observational associations need the confounders accounted for** (ties to T3.8).

**T3.11 Interpreting log-transformed models (log-level / level-log / log-log elasticity)**
When diagnostics (T3.3) push you to `log(Y)` or `log(X)`, the **coefficient's meaning changes** — and interpretation is the graded skill, so know all four forms. Let `b` = the slope. **(1) level–level `Y ~ X`:** +1 unit in X → a **b-unit** change in Y (ordinary). **(2) log–level `log(Y) ~ X`** (semi-log): +1 unit in X → Y changes by **(e^b − 1)·100 %** (exact), ≈ **100·b %** for small b (good for |b| < ~0.1). E.g. b = 0.08 → about **+8.3%** per unit — a **percentage / multiplicative** change, NOT "+0.08 dollars" (two errors: wrong scale, and additive-vs-multiplicative). **(3) level–log `Y ~ log(X)`:** +**1%** in X → a **b/100-unit** change in Y; a **doubling** of X → **b·ln2 ≈ 0.693b** change. **(4) log–log `log(Y) ~ log(X)`:** b = the **elasticity** — +**1%** in X → about **b %** change in Y (unit-free, comparable across variables; |b| > 1 = elastic). **Why log at all:** `log(Y)` often fixes the funnel (E) **and** right-skew (N) at once, and it's **still linear regression** ("linear" = in the parameters). A constant **%** effect on the log scale means a **bigger absolute effect where Y is large** (8% of a big number > 8% of a small one).

---

# GLM BRIDGE — Topics 4 & 5 in one idea

**GB.1 The link-function idea (the whole trick)**
So far Y was **continuous** and we modelled its average **directly**: `E[Y|X] = β0 + β1X1 + …`. But many responses aren't continuous — **binary** (survived/died) or **counts** (number of rentals) — and a straight line for them has a **range problem**: a line runs off to ±∞, but a probability must stay in **(0,1)** and a count can't be **negative**. **The fix:** don't model `E[Y|X]` directly — model a **function `h(·)` of it** (the **link function**) and set *that* equal to the linear part: **`h(E[Y|X]) = β0 + β1X1 + … + βpXp`**. `h` is chosen so the **left side can roam over all of (−∞,∞)** to match the linear right side, while the **untransformed `E[Y|X]` stays legal** (0–1 for a probability, positive for a count). A model of this form is a **Generalized Linear Model (GLM)**, fit with **`glm(…, family=…)`**. **Ordinary linear regression is the special case `h(x)=x`** (the "identity link") — so MLR is itself a GLM. **Why this is great for the exam:** once the link is applied the right side is *just a linear model*, so **every Topic 1–2 skill transfers** (adding predictors, dummies, additive vs. interaction, counting coefficients `k−1` per `k`-level factor). The **only** change: coefficients are interpreted on the **transformed scale** (log-odds or log-mean), and — after exponentiating — on a **multiplicative** scale.

**GB.2 The three GLM families (pick the model by the RESPONSE type, not the predictors)**

| Response | Distribution | Link `h` (canonical) | Models | `glm(family=)` | Var(Y\|X) |
|---|---|---|---|---|---|
| **Continuous** | Normal/Gaussian | **identity** `h(x)=x` | the mean `E[Y]` | `gaussian` (default) | `σ²` (constant) |
| **Binary 0/1** | Bernoulli/Binomial | **logit** `log(p/(1−p))` | the **log-odds** | `binomial` | `p(1−p)` |
| **Count 0,1,2…** | Poisson | **log** `log(λ)` | the **log-mean** | `poisson` | `λ` (= mean) |

The response decides the model. In R the logistic response must be **numeric 0/1 or a 2-level factor** (convert a string: `y <- if_else(y=="success",1,0)`).

**GB.3 Two structural facts that surprise people (memorize)**
(1) **There is NO error term `e` in a GLM.** We model a *function of the conditional expectation* directly, not `Y = … + e`. (Randomness still exists — it's baked into the Bernoulli/Poisson distribution of Y — but there's no additive `e` written in the equation.) (2) **Estimation is by Maximum Likelihood (MLE), not Least Squares**, and there's **no closed-form formula** — R runs an **iterative algorithm** ("Fisher Scoring iterations" in the summary), **which may occasionally not converge**. *(For Normal errors, MLE and LS give the identical answer — that's why `lm` and `glm(family=gaussian)` agree.)*

---

# TOPIC 4 — LOGISTIC REGRESSION (binary response)

**T4.1 When to use it + why not ordinary linear regression**
Use logistic regression when the **response is BINARY** (two outcomes): survived/died, default/no-default, disease present/absent. (Course dataset: **Titanic**, `survived ~ fare, sex, …`.) For a binary Y the conditional expectation **IS a probability**: `E[Y|X] = P(Y=1|X)`. A straight line for that probability produces **fitted values below 0 and above 1** (nonsense) — the **range problem**. So we model a *function* of the probability whose range is all of (−∞,∞): the **logit**.

**T4.2 The logit model — three equivalent forms (know all three)**
Let `p = P(Y=1|X)`. Fit with `glm(survived ~ fare, family=binomial)` (logit = default/canonical link).
- **probability:** `p = e^(β0+β1X) / (1 + e^(β0+β1X))` — always between 0 and 1 (the **S-curve**).
- **log-odds (logit):** `log(p/(1−p)) = β0 + β1X` — the **LINEAR** one; range = all reals ⇒ cures the range problem.
- **odds:** `p/(1−p) = e^(β0+β1X)` — exponentiate to get here.

**odds** = `p/(1−p)` = "successes per failure" (odds of 3 ⇒ success 3× as likely as failure ⇒ `p=0.75`). **logit** = `log(odds)` = the quantity set equal to the linear part.

**T4.3 Interpreting coefficients — the THREE scales (this is the whole topic)**
Take a slope `b̂ = 0.0152` (raw), so `e^0.0152 ≈ 1.015`:

| Scale | Report | Titanic `fare` example |
|---|---|---|
| **raw b̂ (log-odds)** | "+1 in X is associated with a **change of b̂ in the log-odds** of success" | +\$1 fare → **+0.0152 log-odds** of surviving |
| **e^b̂ (odds ratio)** | "+1 in X **multiplies the odds** by e^b̂" | odds of surviving **× 1.015** per \$1 |
| **(e^b̂−1)·100%** | "+1 in X changes the odds by that **percent**" | odds **+1.5%** per \$1 |

**Raw coefficients are on the log-odds scale; exponentiated are on the odds scale** (`tidy(model, exponentiate=TRUE)`). You *choose* which to report — both correct. **Intercept:** raw β0 = log-odds of success when all X=0; `e^β0` = **baseline odds**. **`e^b̂` is literally an odds ratio.** *(Log-odds = "same wording as MLR"; odds = the more natural interpretation.)*

**T4.4 Categorical predictor = odds ratio between groups (Titanic `sex`)**
`glm(survived ~ sex)` with **female = reference** gives `sexmale = −2.514` (raw). Then `e^(−2.514) = 0.081`: a male's **odds of surviving are 0.081× a female's** — only **8.1%** of a female's odds, a **91.9% decrease** (`(0.081−1)·100`). **Flip it for a cleaner sentence:** males' **odds of *dying*** were `e^2.514 = 12.35×` those of females. (Same story from either direction — good exam phrasing.)

**T4.5 Additive vs. interaction (identical logic to MLR — on the log-odds scale)**
- **Additive** `glm(survived ~ sex + fare)`: **same fare-slope for both sexes, different intercepts** → "two logistic curves, same shape, shifted." You **CAN** say "holding sex constant / for either sex" and "keeping fare constant at any value"; the fare odds-ratio (`e^b̂`) applies to **both** groups. **TRAP:** the **probability curves will NOT look parallel** even though the log-odds components are parallel — the S-shape squashes them. **Parallel-ness lives on the log-odds scale, not the probability scale.**
- **Interaction** `glm(survived ~ sex * fare)`: **different slopes AND intercepts.** Now you **CANNOT** say "holding constant" — the effect of fare **depends on** sex. Read the four coefficients like the MLR interaction table (`b2` = reference-group log-odds slope, `b2+b3` = other group's). To get a group's **odds** ratio you **multiply** exponentiated coefficients (`e^(b2+b3) = e^b2·e^b3`) — exponentiation turns additive log-odds into multiplicative odds.

**T4.6 Inference — the Wald statistic**
GLM inference rests on the **CLT** (large-sample), so with large n: **`z = b̂/SE(b̂) ~ N(0,1)`** (the "Wald statistic"); CI `b̂ ± 1.96·SE`. Same reading as SLR/MLR: **|z|>1.96 ⇔ 95% CI excludes 0 ⇔ p<0.05.** `tidy(model, conf.int=TRUE, exponentiate=TRUE)` gives **odds-ratio CIs** directly. An odds-ratio CI for `fare` of (1.008, 1.015) reads: "95% confident a \$1 fare rise is associated with a **0.8%–1.5% rise in the odds** of surviving." (Excludes 1 on the odds scale ⇔ excludes 0 on the log-odds scale ⇔ significant.)

**T4.7 Prediction & fitted values — WHICH scale?! (a favourite trap)**
A logistic model predicts on **whichever scale you ask for**:
- `predict(model, newdata, type="link")` → **log-odds** (the default — the linear part is log-odds).
- `predict(model, newdata, type="response")` → **probability**.
- **By hand:** compute log-odds `L = b̂0 + b̂1X1 + …`, then `p = e^L / (1+e^L)`. *(The exam may ask exactly this for one observation, e.g. a male paying \$7.25 → log-odds −1.694 → p = 0.155.)*
- **Fitted-value gotcha:** `augment(model)`'s **`.fitted` = log-odds**, but the model object's **`fitted(model)`/`$fitted` = probabilities**. Know which one you hold.

**T4.8 Residuals — why the residual plot is useless here**
**Raw residual** `r = y − p̂`. Two problems: (1) **variance is not constant** — for a Bernoulli response `Var(Y)=p(1−p)`, which changes with `p`, so residuals aren't comparable; (2) because y is only **0 or 1**, raw residuals collapse onto **two parallel lines** (`−p̂` and `1−p̂`) in any residual plot. So residuals-vs-fitted is **not informative**. **Fixes:** **Pearson residual** `r = (y−p̂)/√(p̂(1−p̂))` (divide by the SD); also **deviance** and **standardized** versions — you won't compute by hand, but know which you're using. Even with Pearson the two-lines problem persists → use a **binned residual plot** (`binnedplot()` averages within bins). **Bottom line: don't lean on residual plots for logistic — overdispersion is the more important diagnostic.**

**T4.9 Overdispersion (the key logistic/Poisson diagnostic)**
The model **assumes** `Var(Y)=p(1−p)`. **Overdispersion** = the data's actual variability is **larger than the model assumes**. This **misspecifies the SEs (not the point estimates)** ⇒ CIs and p-values become unreliable. **Detect:** refit with `family=quasibinomial` and read the **dispersion parameter** — correctly specified ⇒ ≈ **1**; **>1 = over-, <1 = under-dispersion** (Titanic ≈ **0.98** ⇒ no problem). **Fix:** the **quasi-likelihood** approach (`quasibinomial`) estimates dispersion and **corrects the SEs**; **coefficient estimates are unchanged.**

**T4.10 Overdispersion — the deeper mechanics (logistic AND Poisson)**
Extends T4.9/T5.5 with the "why" (heavily tested). **Variance is "locked"** because Bernoulli/Poisson each have **one parameter** (p, λ), so fixing the mean fixes the whole distribution — variance included (`p(1−p)`, `λ`); no free σ² knob, so real data can carry **more spread than the formula allows** = overdispersion. *(Same reason GLMs have no `+e`; the Normal's separate σ² is why linear regression **can't** overdisperse — its analog is heteroscedasticity, a variance-**shape** not **magnitude** issue.)* **Logistic "sometimes" vs Poisson "usually":** individual 0/1 data (n=1/row) is variance-locked → basically can't overdisperse (Titanic ≈0.98), so logistic needs **grouped/binomial** data (hidden heterogeneity) **or clustering** ("sometimes"); a count is **unbounded** and `Var=λ` is a rigid bet real counts break via clustering/bursts ("usually", Bikeshare ≈90.6). **Damages the SEs/p-values, NOT the estimates** (coefficients come from the untouched mean structure; too-small SEs → false significance). **Fix quantitatively:** quasi estimates φ and **multiplies SEs by √φ** (√90.6 ≈ 9.5× wider); φ≈1 → no change; **φ<1 = under-dispersion = safe** (SEs conservative), **φ≫1 = dangerous.** **Why not always quasi / just inflate variance?** Goal is **calibrated** SEs, not big ones (over-inflating → CIs so wide nothing's detectable, no power) → φ is **estimated**; and plain binomial/Poisson is a **real distribution** (→ likelihood → AIC/BIC/LRT, prediction intervals) while **quasi has no likelihood → AIC=NA, no LRT.** Workflow: **fit plain → check φ → quasi only if φ≫1.** **Overdispersion ≠ bad predictions:** overdispersion is a *variance* problem (fix: quasi); wrong predictions is a *mean/accuracy* problem (fix: better predictors, diagnose via deviance/AIC) — the dispersion parameter watches **spread, not correctness.**

---

# TOPIC 5 — POISSON REGRESSION (count response)

**T5.1 When to use it + two problems that rule out linear regression**
Use it when the **response is a COUNT** (non-negative integers 0,1,2,…): customer arrivals, disease occurrences, accidents, **bike rentals**. (Course dataset: **Bikeshare**, `bikers ~ temp, season, workingday, windspeed`.) **Everything mirrors logistic regression** — only the link and interpretation scale change. Two problems kill ordinary linear regression: (1) **Range** — counts are ≥0 but a line predicts **negative** counts; (2) **Non-constant variance** — Poisson has **mean = variance** (`λ = E[Y|X] = Var(Y|X)`), so anything that shifts the mean **also shifts the variance**, automatically violating the constant-variance (E) assumption.

**T5.2 The log-link model**
Let `λ = E[Y|X]` be the **mean count**. Model: **mean** `E[Y|X] = λ = e^(β0+β1X1+…)` (always positive ⇒ cures the range problem); **log-mean** `log(λ) = β0 + β1X1 + …` (the **LINEAR** one; log = canonical link). Fit with `glm(bikers ~ ., family=poisson)`. Again: **no error term** (we model a function of the conditional mean), estimated by **MLE / iterative algorithm**.

**T5.3 Interpreting coefficients — TWO scales (rate ratios)**
Take `b̂ = 2.688` (raw), so `e^2.688 ≈ 14.7`:

| Scale | Report | Bikeshare example |
|---|---|---|
| **raw b̂ (log-mean)** | "+1 in X is associated with a **change of b̂ in the log-mean** count, holding others constant" | +1 in `temp` → **+2.688 log-mean** bikers |
| **e^b̂ (rate ratio)** | "+1 in X **multiplies the mean count** by e^b̂" | mean bikers **× 14.7** per unit temp |
| **(e^b̂−1)·100%** | percent change in the mean count | `season2` `e^b̂=1.065` → **+6.5%** vs season 1 |

**Raw = log-mean scale; exponentiated = mean-count scale** (multiplicative). A **dummy** `e^b̂` = **ratio of mean counts** vs. the reference (e.g. `season3` `e^(−0.141)=0.868` → season 3 has **86.8%** of season 1's mean usage = **13.2% decrease**). **Why multiplicative (derivation you may be asked for):** compare `log λ` at `temp` and `temp+1`; everything else is held constant and cancels, leaving `log λ_(t+1) − log λ_t = b`; by the log-of-a-ratio rule `log(λ_(t+1)/λ_t)=b`, so `λ_(t+1)/λ_t = e^b` ⇒ `λ_(t+1) = e^b·λ_t`. **Additive vs. interaction:** same as logistic/MLR on the log-mean scale — additive ⇒ "keep others constant at any value"; interaction ⇒ effect **depends on** the other variable, **multiply** exponentiated coefficients for a group's rate ratio.

**T5.4 The `factor()` gotcha (bites people constantly)**
R only makes dummy variables out of **factors**. If a categorical variable is stored as a **number** (e.g. `season`=1,2,3,4 or `workingday`=0/1), `glm` **silently treats it as continuous** and fits **one meaningless slope on the codes**. Wrap it **before** fitting: `mutate(season = as.factor(season))` so you get `season2, season3, season4` dummies.

**T5.5 Overdispersion — Poisson USUALLY over-disperses**
Same residual issues as logistic (discrete response, non-constant variance): raw & **Pearson** residuals (`r = (y−λ̂)/√λ̂`), residual plots not very useful ⇒ lean on **overdispersion**. **Poisson regression usually exhibits overdispersion** because the "mean = variance" straitjacket is rarely true in real data — **a much bigger deal for Poisson than for logistic.** **Detect:** refit `family=quasipoisson`, check dispersion (want ≈1). **Bikeshare: dispersion ≈ 90.6** — *wildly* above 1 ⇒ **severe overdispersion**, the Poisson assumption clearly fails. *(Contrast Titanic logistic ≈0.98 — that's what "fine" looks like.)* **Fix:** **quasi-likelihood** (`quasipoisson`) re-estimates dispersion and **corrects the SEs**; point estimates unchanged. If dispersion is far from 1, the plain Poisson SEs/p-values **can't be trusted.**

**T5.6 Logistic vs. Poisson (one-line contrast to lock in)**
**Logistic** → **log-odds / odds** (odds ratios), `Var = p(1−p)`, overdispersion *sometimes*. **Poisson** → **log-mean / mean** (rate ratios), `Var = λ`, overdispersion *usually*. **Both:** no error term, MLE, Wald inference, `factor()` your categoricals, exponentiate for a multiplicative interpretation.

---

# TOPIC 6 — GOODNESS OF FIT (linear models, fit by LS)

**T6.1 "Better than nothing?" — the null (intercept-only) model**
"Nothing" = the **null model** = **intercept-only** `Y = β0 + e`, whose best guess for every observation is just the **sample mean ȳ** (no predictors). The question: **does using X beat just predicting the average?** We compare our fitted `ŷ` (estimate of `E[Y|X]`) against `ȳ` (estimate of `E[Y]`). *(Course case study: predicting **protein from mRNA** — biology's "Central Dogma" says they should track, but real data shows only a weak association ⇒ a natural "is this model any good?" story.)*

**T6.2 The three sums of squares (know all three cold)**
`TSS = Σ(yᵢ − ȳ)²` **Total** — total variation; residuals from the NULL model. `ESS = Σ(ŷᵢ − ȳ)²` **Explained** — variation the model explains (fit vs. mean). `RSS = Σ(yᵢ − ŷᵢ)²` **Residual** — variation the model misses (leftover; LS minimizes this). **The decomposition** (holds with an **intercept** + **LS** fit): **`TSS = ESS + RSS`** ("total = explained + unexplained"). A good model makes **ESS large, RSS small** relative to TSS.

**T6.3 R² — coefficient of determination**
**`R² = 1 − RSS/TSS = ESS/TSS`** (the two forms are equal only with intercept + LS) = the **proportion of total variation in Y the model explains.** Range **0 to 1** (larger = better). In **SLR it equals the square of the correlation: `R² = r²`.** *(protein~mRNA: R²≈0.09 ⇒ only 9% of protein variation explained; in observational data even 20–50% can be useful — high R² is rare, noisy data is normal.)* **CRITICAL caveats (all exam-worthy):** (a) R² is **in-sample (training)** — says nothing about **out-of-sample** prediction; (b) R² is **NOT a test** — no known distribution, so you can't use it to declare one model "significantly" better; (c) R² **always increases when you add a predictor**, relevant or not ⇒ it **can't compare models of different sizes** and it tempts overfitting.

**T6.4 Adjusted R² (fixing the "always increases" flaw)**
**`adj R² = 1 − [RSS/(n−p−1)] / [TSS/(n−1)]`** (p = #covariates excluding intercept). Dividing RSS by `n−p−1` **penalizes extra variables**: adding a useless predictor lowers RSS only a little but costs a degree of freedom, so **adj R² can go DOWN.** Use **adj R² (not R²) to compare models of different sizes.** *(Linear models only — there is no adj R² for logistic/Poisson; that's Topic 7's job.)*

**T6.5 RSE & MSE (training vs. test)**
- **RSE (Residual Standard Error)** `= √(RSS/(n−p−1))` — called **`sigma`** in `glance()`. Estimates **σ = √Var(e)**, the size of the *irreducible* error; it's what classical theory uses to compute the coefficient SEs. Smaller = better.
- **MSE (Mean Squared Error)** `= (1/n)Σ(yᵢ−ŷᵢ)²`. **Training MSE** uses the fitting data; **testing MSE** uses **new/held-out** data to judge **out-of-sample** prediction (the honest measure). Smaller = better.
- **`glance(model)`** prints `r.squared`, `adj.r.squared`, `sigma`, the **F-statistic + its p-value**, `AIC`, `BIC`, `deviance` in one row.

**T6.6 F-test Case A — model vs. the null ("is the model better than nothing?")**
`R²` is *descriptive*, not a test. For a yes/no significance question use an **F-test** (requires the two models to be **nested**). Case A: reduced = intercept-only `Y=β0+e`; full = `Y=β0+β1X1+…+βpXp+e`. **`H0: β1=β2=…=βp=0`** (NONE of the predictors help, simultaneously) vs **H1: at least one βj≠0.** Statistic (read from R, **don't compute by hand**): `F = [(RSS_red − RSS_full)/p] / [RSS_full/(n−p−1)] ~ F(p, n−p−1)`. Big RSS drop ⇒ big F ⇒ small p ⇒ **reject H0 ⇒ the model beats the null.** In R: **`glance(model)`** reports this (its reduced model is *always* the intercept-only model).

**T6.7 F-test Case B — any nested pair ("does an EXTRA block of variables help?")**
reduced = q covariates; full = the same q **plus** `k = p−q` extra. **`H0: β_(q+1)=…=βp=0`** (the k extra coefficients are all 0 — the extra block adds nothing) vs H1: at least one ≠0. `F = [(RSS_red − RSS_full)/k] / [RSS_full/(n−p−1)] ~ F(k, n−p−1)`. In R: **`anova(model_reduced, model_full)`** compares **any** nested pair. *(protein example: adding `gene` to `prot ~ mrna` gave F=9.9, p=0.001 ⇒ the bigger model is significantly better.)* **Must-remember caveat:** a significant F-test means the bigger model **fits significantly better** — it does **NOT** mean "we can predict Y from X," and it does **NOT** mean a *specific* predictor matters (in the example, **`gene`, not mRNA**, carried the signal). **Significance of a model ≠ good prediction ≠ a given predictor being useful.**

**T6.8 t-test vs. F-test (a clean exam contrast)**
- **`lm`'s t-test** on a coefficient tests **one** `βj=0` at a time, **with the other variables still in the model** — "does *this* variable add anything, given the rest?"
- **The F-test** tests **many** coefficients **simultaneously** — "does this *whole block* (or the whole model) add anything?"
- **Special case p=1:** with a single predictor the two hypotheses are identical, and **`F = t²`** with the same p-value. Both rest on Normality / large-sample approximations.

**T6.9 AIC / BIC + `glance()` vs `anova()`**
**`AIC = (goodness of fit) + (penalty for model size)`; smaller AIC = better.** BIC is similar with a **heavier** size penalty. Like adj R², they trade off fit against complexity, and they're what **stepwise selection** optimizes (Topic 8). **`glance(model)`** = one-model metrics (R², adjR², sigma, F vs. null, AIC, BIC). **`anova(reduced, full)`** = the F-test for any nested pair. **Model-selection warning (leads into Topic 8):** using F-/t-tests to *pick* significant variables and then refit on the **same data** = the **post-inference / "double-dipping"** problem ⇒ inference is no longer valid.

---

# TOPIC 7 — GOODNESS OF FIT FOR GLMs (deviance)

**T7.1 Deviance = "RSS for GLMs" (null vs. residual deviance)**
**The single most important fact:** `R²`, `adj R²`, `RSE`, `MSE` — and the F-test — are **for LINEAR regression only.** They **do NOT apply to logistic or Poisson regression.** For GLMs the analogous quantity is the **DEVIANCE**: it measures the gap between the **log-likelihood of your fitted model** and that of a **"perfect" (saturated) model** (one parameter per observation, fits every point exactly). **Think of deviance as RSS for GLMs** — in fact, for a linear model with Normal errors the deviance is **proportional to RSS.** **Lower deviance = better fit.** `glm` output shows **null deviance** (fit of the intercept-only model) and **residual deviance** (fit of your model) — a smaller residual deviance means your predictors helped. **AIC** also works (it's likelihood-based, so valid for both linear and GLMs).

**T7.2 The deviance test (χ²) — comparing nested GLMs**
Just as the F-test compares nested **linear** models, the **deviance test** compares nested **GLMs**. **`H0`: the two (nested) models are equally good** (the extra coefficients add nothing) vs **H1: the larger model is better.** **test statistic = difference in deviance ~ χ²(d)** under H0, where **d = difference in the number of predictors.** A **large deviance drop** ⇒ large χ² ⇒ small p ⇒ the extra terms significantly improve the fit. **This is a large-sample result** — reliable only when n is big. In R: **`anova(reduced, full, test="Chisq")`** — same workflow as the F-test, different reference distribution.

**T7.3 Why a perfect fit is BAD (saturated model / overfit)**
A model that passes through **every** point (the **saturated model**; the R²=1 analogue in linear regression) has **overfit** — it **memorized noise** and will make big errors on a *new* sample from the same population. We deliberately prefer **good-but-not-perfect** models. *"Anything taken to the extreme becomes bad."*

**T7.4 Cheat-sheet mapping (linear vs. GLM)**
**Linear model:** RSS → **R² / adjR² / F-test.** **GLM (logistic/Poisson):** deviance → **deviance χ²-test** (and **AIC**, which works for both). **If a question gives you a `glm` and asks about R², the answer is "you can't — use deviance."**

**T7.5 Deviance in R — the worksheet-07 workflow (breast-cancer logistic)**
Fit `glm(target ~ ., family=binomial)` (recode response to 0/1 first; drop `ID`). **Residuals:** `augment(model)` gives **deviance** residuals by default; `residuals(model, type=...)` gives **`"response"`, `"pearson"`, `"deviance"`** (use Pearson/deviance, not raw). **Residual deviance = "RSS for GLMs":** equals `sum(deviance_resid^2)` and matches **`model$deviance`**. **`glance(model)`** reports **`null.deviance`** (intercept-only) and **`deviance`** (residual = your model); `model$null.deviance` matches. **For the intercept-only model, null deviance = residual deviance** (there are no predictors to add, so the fitted model *is* the null). **Compare nested GLMs:** `anova(reduced, full, test="Chisq")` — the **`Resid. Dev`** column = each model's residual deviance; small p ⇒ the extra terms significantly improve fit. Same workflow for Poisson (`family=poisson`).

---

# TOPIC 8 — MODEL SELECTION

**T8.1 Stepwise vs. regularization (greedy jumps vs. smooth shrinkage)**
Two big questions: **(1)** how to pick which variables belong (smoothly), and **(2)** why it's dangerous to **select and infer on the same data**. (Course dataset: **Ames Housing**, predicting `SalePrice`.) **Stepwise selection** (`step()`, `regsubsets(…, method="forward")`) adds/removes variables one at a time — a **greedy** algorithm: results **depend on the order** variables enter, and a variable is **fully in or fully out**, its coefficient **jumping** from 0 to a value in one discrete step. **Regularization** does the selection **smoothly**: add a **penalty** on coefficient size to the objective so coefficients **shrink toward 0 continuously**: minimize `Σ(Yᵢ − β0 − Xᵢ·β)² + λ·penalty(β)` (usual fit + shrinkage term).

**T8.2 Ridge vs. LASSO (the two penalties)**

| Method | Penalty | Norm | Shrinks to exactly 0? | Selects variables? |
|---|---|---|---|---|
| **Ridge** | `λ·Σβⱼ²` | **L2** (squared) | **No** (never quite 0) | **No** |
| **LASSO** | `λ·Σ\|βⱼ\|` | **L1** (absolute) | **Yes** | **Yes** — selects *and* trains at once |

*(Course focuses on **LASSO** = **L**east **A**bsolute **S**hrinkage **a**nd **S**election **O**perator, Tibshirani 1996. Ridge, Hoerl & Kennard 1970, is a multicollinearity remedy.)* The L1 (absolute) penalty is what lets LASSO hit exactly 0; L2 (squared) can't.

**T8.3 The penalty λ + choosing it by cross-validation**
**λ = 0** ⇒ no penalty ⇒ objective is just RSS ⇒ **you get back the ordinary LS estimates.** **As λ grows**, coefficients shrink: **LASSO drives them to *exactly 0* one by one** (that's how it *selects* — 0 means "dropped"); **Ridge shrinks toward 0 but never reaches it** (so Ridge can't select). *(A LASSO path plot shows lines peeling off to 0 as `log λ` rises; the top axis counts how many coefficients are still non-zero.)* **Choosing λ ("tuning"):** pick the λ that **minimizes the test MSE**, estimated by **cross-validation** (CV splits the *training* data into internal train/test folds so **no real test data is touched**). **`k`-fold CV:** chop the training data into `k` folds, train on `k−1` and test on the held-out one, rotating so **every point is tested once**, then average the `k` errors per λ (`k=10` typical). **`cv.glmnet()`** reports two choices: **`lambda.min`** = the λ with the smallest CV MSE; **`lambda.1se`** = the **largest** λ whose CV MSE is still within **1 standard error** of the minimum ⇒ **more shrinkage / a simpler model at almost no cost in error.**

**T8.4 Bias–variance tradeoff (why we'd accept a biased estimator)**
Shrinkage **biases** the coefficients (pulls them toward 0), so `E[b̂] ≠ β`. Why do it? Because **`MSE = Variance + Bias²`**, and **paying a little bias buys a big drop in variance**, which **improves prediction.** LASSO was designed for **prediction**, especially the **high-dimensional** case where `p` (predictors) `>> n` (sample size). **Because the penalty depends on coefficient *size*, you must STANDARDIZE the inputs first** (`glmnet` does this by default). **In R (`glmnet`):** needs a **matrix `x`** of predictors + a response **vector `y`** (not a formula/data-frame); `alpha=1` ⇒ **LASSO**, `alpha=0` ⇒ **Ridge**, in between = **Elastic Net**; `coef(cv_fit, s="lambda.min")` pulls coefficients (dropped ones show as `.`); `predict(cv_fit, newx=X_test, s="lambda.min")` predicts.

**T8.5 The post-inference / double-dipping problem (+ the simulation proof)**
**The core sin:** using the **same data** to (a) **select** which variables go in the model **and** (b) **test/estimate** those variables. Selection cherry-picks variables that look good **in this sample**, so the follow-up inference is **over-optimistic** — you **reject H0 far too often.** **The simulation proof (know the design):** generate data where **ALL true coefficients are 0** (so the intercept-only model is genuinely correct — nothing should look significant). On each of 1000 datasets: **forward-select** up to 3 variables using **adj R²**, then **F-test** the selected model on the **same** data. Result: in a **large fraction** of datasets the F-test **wrongly rejects H0** — the **Type I error rate is badly inflated** (should be ~5%, comes out much higher). *Selecting on the data inflated adj R², which then fooled the test.* **The fix — split the data:** use **one part to select** the model and a **separate part to fit and test** it; because the inference part never saw the selection, its Type I error is back to **~5%.**

**T8.6 postLASSO + the takeaway**
LASSO's coefficients are **biased** (shrinkage). But if you take the variables **LASSO selected** and refit **ordinary LS on just those variables**, that **postLASSO** estimator is **unbiased.** **However** — to make **valid inference** with postLASSO you **still must split the data** (selecting and inferring on the same data is the same double-dipping sin). **Takeaway: you cannot select variables and do valid inference on the same data — split it, or use more advanced methods (beyond this course).** *(R tooling from the worksheets: `map`/`map_dbl`/`map2` apply a function across a list of datasets; `update()` refits a model with a tweaked formula.)*

**T8.7 Stepwise in R — the tutorial-07 workflow (`regsubsets` / `stepAIC`)**
Two functions for **stepwise/best-subset** selection. **`regsubsets()` (`leaps`):** `regsubsets(y ~ ., data=train, nvmax=p, method="forward")` (or `"backward"`). **`nvmax` = largest model size to search** — set it to the number of predictors so every size 1…p is evaluated (**default is only 8!**). `summary(fit)` returns the best model per size + vectors **`$rsq, $rss, $adjr2, $cp` (Mallows' Cp), `$bic`** and `$which`; pick the size by **max `adjr2`** or **min `Cp`/`BIC`**. **`stepAIC()` (`MASS`):** `direction = "forward"/"backward"/"both"`, with **`k=log(n)` ⇒ BIC**, **`k=2` ⇒ AIC** (smaller = better). **Categoricals:** `regsubsets` evaluates **each dummy column separately** (can split a factor, and *which* level depends on the arbitrary reference) — awkward; **`stepAIC` adds/removes a whole categorical at once** (usually what you want). **`step` / `drop1` / `add1` (base R, work on `lm` AND `glm`):** `drop1(model)` = a **one-move** table showing AIC/test for **removing each** variable; `add1(model, scope)` = for **adding each** candidate; **`step(model)`** = runs the **whole** forward/backward/both search to the end (repeated best-AIC moves until none improve). So `drop1`/`add1` = single step, `step` = full loop. **Predictive evaluation = TEST set:** `MSE_test = (1/n_new)Σ(y_new − ŷ_new)²`, `RMSE_test = √MSE_test` — compute by hand (`sqrt(mean((y−pred)^2))`) or `yardstick::metrics()`/`rmse()`; **never evaluate on the training data.** **Caveat:** `summary()`/`step` p-values on a stepwise-selected model are **invalid** (double-dipping — see T8.5).

---

# TOPIC 9 — PREDICTION UNCERTAINTY (CIP vs PI)

**T9.1 What are you predicting? (average vs. actual)**
An estimated model gives `ŷ = b̂0 + b̂1X + …`. But `b̂` came from a **random sample**, so a different sample gives different coefficients and a different prediction — **predictions are random variables.** (Focus is **MLR**; extending intervals to GLMs is hard and out of scope. Course dataset: **Strathcona property tax**, `assess_val ~ BLDG_METRE`.) For a house of size `X` you might predict either **(a)** the **AVERAGE** value of *all* houses of that size, `E[Y|X]` (a point on the population line), or **(b)** the **ACTUAL** value of *one specific new* house of that size, `Y = E[Y|X] + e` (the average **plus** its own random error). Different targets, **different amounts of uncertainty ⇒ different intervals.**

**T9.2 CIP vs. PI (side-by-side)**

| | **Confidence Interval for Prediction (CIP)** | **Prediction Interval (PI)** |
|---|---|---|
| **Predicting** | the **average** `E[Y\|X]` | an **actual new** value `Y` |
| **Sources of uncertainty** | **ONE** — sample-to-sample wobble in `b̂` | **TWO** — wobble in `b̂` **+** the random error `e` |
| **Width** | narrower | **wider** (extra `e` term) |
| **Centred at** | the fitted value `ŷ` | the same fitted value `ŷ` |
| **Interpret with** | "**confidence**" (target is a fixed number) | "**probability**" (target is a random variable) |
| **R** | `predict(model, interval="confidence")` | `predict(model, interval="prediction")` |

**T9.3 Why the PI is always wider (the exam's favourite question)**
The **CIP** only accounts for **uncertainty 1**: our estimated line `b̂0+b̂1X` **approximates** the true average line `β0+β1X` (sample-to-sample wobble). The **PI** must **also** account for **uncertainty 2**: even if we knew the true average line perfectly, an **individual** house still scatters around it by its own error `e`. **Two sources > one, so PI ⊃ CIP — the PI is always wider.** Predicting **one actual value is harder** (more uncertain) than predicting **the average.** **The one diagram:** `Y = E[Y|X] + e` (truth) → `Y = β0 + β1X + e` (linearity) → `ŷ = b̂0 + b̂1X` (our prediction). **CIP** aims at the **middle part** `β0+β1X` (the average); **PI** aims at the **whole** `Y` (average + e). Same `ŷ`, different target, different width.

**T9.4 Interpretation templates + the `geom_smooth` band**
- **CIP:** "With **95% confidence**, the **average** assessed value of houses of size **220 m** is between **\$671,944 and \$748,198**." *(Confidence — the average is a fixed unknown number; once computed the interval either contains it or not.)*
- **PI:** "With **95% probability**, the value of **a (single) house** of size **220 m** is between **\$454,519 and \$965,622**." *(Probability — an individual house's value is itself random. Note how much wider — that's the `e` term.)*
- **`geom_smooth(se=TRUE)` band:** the shaded band `ggplot` draws around a regression line is the **CIP band** (uncertainty of the *fitted line / average*) — **NOT** a PI, and **NOT** the scatter of the points. (Same "SE of the line ≠ scatter of the points" idea from Topic 1 inference.)

**T9.5 The interval band shape (hourglass) & extrapolation**
Both the **CIP and PI bands are narrowest at x̄** (the predictor mean) and **flare outward** as X moves away in either direction — an hourglass/bowtie. **Why:** the fitted line effectively **pivots around (x̄, ȳ)** (LS always passes through it), so slope wobble barely moves ŷ near the center but swings it more and more at the extremes; the uncertainty in ŷ grows with the distance **(X − x̄)**. The **PI adds the constant σ² floor** (the individual error e) on top, so it's wider everywhere and stays wide even at x̄ (its extra ingredient does **not** depend on (X − x̄)). **Extrapolation** far outside the data makes BOTH the point estimate *and* the band width untrustworthy — the interval balloons, so even taking the model at face value the prediction is nearly uninformative. The `geom_smooth(se=TRUE)` shaded band is this **CIP band** (uncertainty of the mean line), narrowest at x̄ — **NOT** where 95% of individual points fall (that's the wider PI).

---

# GENERAL (cross-cutting)

**G.1 Phrasing bank (dense)**
`[slots]` to fill; "NOT" = wording to avoid. Four sub-banks: **G.1a** coefficients · **G.1b** inference · **G.1c** causation · **G.1d** ANOVA/diagnostics/multicollinearity.

**G.1a Coefficients**
- *SLR slope:* "A 1-unit increase in `[X]` is **associated with** an expected [increase/decrease] of `[b̂ units]` in `[Y]`, on average." NOT "causes"/"effect of"/"raises your".
- *MLR slope:* same + "**holding [other predictors] constant**" (additive: at any value; interaction: can't).
- *Intercept:* "expected `[Y]` when `[X]`=0 is `[b0]`" (flag if X=0 is meaningless).
- *2-level categorical:* "mean `[Y]` for `[level]` is `[b̂]` higher/lower than `[reference]`" = **difference of means**, NOT the level's own mean.
- *k-level:* "relative to `[ref]`, `[level]` is `[b̂]` higher/lower."
- *Additive:* "b0 = ref intercept, b1 = intercept gap, b2 = **common slope** (both groups)" — parallel lines.
- *Interaction:* "b2 = **ref-group slope only**, b3 = slope gap, other slope = **b2+b3**"; CANNOT say "holding constant."
- *Interaction (in words):* "the effect (slope) of `[X1]` on `[Y]` **depends on** `[X2]`" — i.e. the `[Y]`–`[X1]` slope **differs across** `[X2]` (for cat×cont: slope `[b2]` for `[reference]`, `[b2+b3]` for `[other group]`). NOT "`[X1]`'s effect is `[b]`, holding `[X2]` constant."

**G.1b Inference**
- *CI:* "We are `[95]`% confident the true `[param]` lies between `[L]` and `[U]`." NOT "95% probability/chance the truth is in this interval."
- *Reject:* "Since p < α (CI excludes 0 / |z| > 1.96), **reject H0**: `[X]` is **statistically associated** with `[Y]`." NOT "accept H1"/"prove".
- *Fail to reject:* "Since p > α, **fail to reject H0**: **not enough evidence** of association." NOT "accept H0"/"no association"/"H0 is true".
- *Hypotheses:* about the population param — `H0: β=0` (never β̂).
- *p-value:* "prob, **if H0 true**, of a statistic this extreme"; small p = **strong evidence** vs H0. NOT effect size, NOT P(H0 true). Report "< 0.001" not "0".
- *Statistical vs practical:* significant = effect ≠ 0 (evidence); practical = big enough to matter (magnitude). Big n ⇒ tiny effects significant. Read **both**.
- *SE:* "how much `[b̂]` varies sample-to-sample." NOT the scatter of points (that's σ).

**G.1c Causation**
- *Default caveat:* "`[X]` and `[Y]` are **associated**, NOT that `[X]` causes `[Y]` — observational, so confounders/reverse causality possible." Avoid causes/effect of/leads to.
- *Causal (when justified):* "because `[treatment]` was **randomly assigned**, the difference in `[Y]` is a **causal** effect."
- *Confounder:* "`[C]` is associated with **both** `[X]` and `[Y]`, creating a misleading association; omitting it **biases** the estimate."
- *Adjusting ≠ causal:* only if **ALL** confounders measured.
- *Exp. vs observational:* a causal claim depends on **how the data were collected** (randomized ⇒ causal; observational ⇒ association only), **not** the p-value or model fit.
- *Reverse causality:* the arrow may run **backwards** (`[Y]` drives `[X]`, not `[X]`→`[Y]`); a cross-sectional association can't tell direction.
- *Simpson's paradox:* an aggregate association can **reverse** within subgroups; the marginal result misleads unless you condition on the `[lurking variable]`.
- *Correlation:* "`[X]`,`[Y]` have `[weak/mod/strong]` `[pos/neg]` linear correlation (r = `[val]`)"; r = linear only, symmetric. Rough scale: `|r|` ≲ 0.3 weak, 0.3–0.6 moderate, ≳ 0.6 strong (Tut 03: `|r| > 0.6` = "high" for flagging collinearity).

**G.1d ANOVA / diagnostics / multicollinearity**
- *ANOVA:* "p < α ⇒ **at least one** `[group]` mean differs; `[variable]` is associated with `[Y]`." NOT "every pair differs"/"which is highest".
- *LINE diagnose:* L & E via residuals-vs-fitted (curve = L bad, funnel = E bad); N via Q-Q (off diagonal = bad). **I & E violated ⇒ SEs invalid ⇒ CIs/p invalid.**
- *VIF:* "`[var]` VIF = `[val]` > 5 (/10) ⇒ problematic multicollinearity" (categorical: compare `GVIF^(1/(2Df))` to √5 ≈ 2.23). NOT correlation with response (it's **among predictors**).
- *Prediction:* "for `[X=val]`, predicted **average** `[Y]` is `[ŷ]`"; flag **extrapolation** if outside the data range.
- *R²:* "the model explains `[R²·100]`% of the variation in `[Y]`." NOT a sign the model is correct/causal or that the slope is significant.

**G.2 Equations (dense)**
β = true, b̂ = estimate, e = error, ê = residual, ŷ = fitted, n = obs, k = #coefs, p = #predictors, σ = error SD, s = sample SD. Four sub-banks: **G.2a** SLR · **G.2b** MLR · **G.2c** assumptions & collinearity · **G.2d** quick calc.

**G.2a Equations — Topic 1 (SLR)**
- Model `Y_i = β0 + β1·X_i + e_i`; line `E[Y|X] = β0 + β1X`; fitted `ŷ = b̂0 + b̂1x`
- Residual `ê = y − ŷ`; LS: minimize `SSR = Σ(y−ŷ)²`
- Slope `b̂1 = Σ(x−x̄)(y−ȳ) / Σ(x−x̄)² = r·(s_y/s_x)`; intercept `b̂0 = ȳ − b̂1·x̄`
- Correlation `r = Σ(x−x̄)(y−ȳ) / √[Σ(x−x̄)²·Σ(y−ȳ)²] = cov(x,y)/(s_x·s_y)`
- Noise `σ̂² = SSR/(n−k)` (SLR: n−2); `SE(b̂1) = σ̂ / √Σ(x−x̄)²`
- Test `z = b̂/SE(b̂)`; reject if **|z| > 1.96**; CI `b̂ ± 1.96·SE` (z*=1.645 @90%, 2.576 @99%); bootstrap CI = 2.5/97.5 percentiles
- `R² = 1 − SSR/SST`, `SST = Σ(y−ȳ)²`

**G.2b Equations — Topic 2 (MLR)**
- Model `Y = β0 + β1X1 + … + βpXp + e`; #dummies = **L−1**; #interaction coefs = (coefs A)×(coefs B); **df = n − k**
- 2-level `Y = β0 + β1D`: ref mean = β0, other = β0+β1
- Additive `Y = β0 + β1D + β2X`: ref line `β0 + β2X`, other `(β0+β1) + β2X` (**parallel**, common slope β2)
- Interaction `Y = β0 + β1D + β2X + β3DX`: ref slope = **β2**, other slope = **β2+β3**; other intercept = β0+β1
- Predict `ŷ = b̂0 + b̂1x1 + …` (drop e)

**G.2c Equations — Topic 3 (assumptions & collinearity)**
- LINE: `E[Y|X]` linear / `E(e)=0`; e independent; `e ~ N(0,σ²)`; `Var(e)=σ²`. One line: `e₁…eₙ iid N(0,σ²)`
- `VIF_j = 1/(1−R²_j)`; **>5 or 10** concerning; =1 none
- GVIF (categoricals): compare `GVIF^(1/(2·Df))` to **√5 ≈ 2.23** or √10 ≈ 3.16

**G.2d Equations — Quick calc (the ones you'll actually do)**
`ŷ=b̂0+b̂1x` · `ê=y−ŷ` · `z=b̂/SE` (|z|>1.96 ⇒ reject) · `CI=b̂±1.96·SE` (excludes 0 ⇒ sig) · group slope `β2+β3` · group means `β0`, `β0+β1` · dummies `L−1` · `σ̂²=SSR/(n−k)`

**G.2e Equations — Topics 4–9 (the second half)**
- **Logistic:** logit `log(p/(1−p)) = β0+β1X`; prob `p = e^(β0+β1X)/(1+e^(β0+β1X))`; odds `= e^(β0+β1X)`. Odds ratio `= e^b̂`; % change in odds `= (e^b̂−1)·100`. By-hand predict: `L=b̂0+b̂1x`, `p=e^L/(1+e^L)`.
- **Poisson:** `log(λ)=β0+β1X`; mean `λ=e^(β0+β1X)`. Rate ratio `= e^b̂`; `λ_(x+1)=e^b̂·λ_x`.
- **GLM inference:** Wald `z=b̂/SE ~ N(0,1)`; |z|>1.96 ⇔ CI excludes 0 (or odds/rate-ratio CI excludes **1**) ⇔ p<0.05.
- **Overdispersion:** refit `quasibinomial`/`quasipoisson`, dispersion ≈ 1 good; >1 over. (Titanic ≈0.98; Bikeshare ≈90.6.)
- **GoF (linear):** `TSS=ESS+RSS`; `R²=1−RSS/TSS=ESS/TSS` (=`r²` in SLR); `adjR²=1−[RSS/(n−p−1)]/[TSS/(n−1)]`; `RSE=√(RSS/(n−p−1))` (=`sigma`); `MSE=(1/n)Σ(y−ŷ)²`.
- **F-test:** `F=[(RSS_red−RSS_full)/k]/[RSS_full/(n−p−1)] ~ F(k,n−p−1)`; Case A `k=p` (vs null, `glance()`); Case B any nested pair (`anova(red,full)`); `F=t²` when p=1.
- **GLM GoF:** null vs residual **deviance** (lower=better); deviance test stat = ΔDeviance `~ χ²(d)` (`anova(red,full,test="Chisq")`); AIC works for both.
- **LASSO/Ridge:** minimize `Σ(Y−Xβ)² + λ·penalty`; LASSO `λΣ|βⱼ|` (L1, → exactly 0, selects), Ridge `λΣβⱼ²` (L2, ≠0). `λ=0`⇒LS. `MSE=Var+Bias²`. Tune λ by CV (`lambda.min`, `lambda.1se`); `alpha=1`=LASSO, `0`=Ridge.
- **Prediction:** CIP (`interval="confidence"`) = average `E[Y|X]`, 1 source, narrower, "confidence"; PI (`interval="prediction"`) = actual `Y`, 2 sources (+e), wider, "probability". Both centred at `ŷ`; **PI ⊃ CIP always**.

**G.3 Reading a regression output table**
In `tidy()` / `get_regression_table()` output, each **row = one coefficient**, each **column = a piece of its inference**. `term` = which coefficient (intercept, a slope, or a **dummy** like `speciesGentoo`); `estimate` = **b̂**; `std.error` = **SE(b̂)** (its sample-to-sample wobble); `statistic` = **z = estimate / SE**; `p.value` = p; `lower_ci` / `upper_ci` = **b̂ ± 1.96·SE**. **Read a row:** the effect is **significant** if `p < α` ⇔ `|z| > 1.96` ⇔ **CI excludes 0**. **Continuous row:** "a 1-unit rise in `[X]` is associated with a `[b̂]` change in Y, holding others constant." **Categorical/dummy row** (e.g. `sexmale`): b̂ = the mean-Y **difference from the reference** level, **not** that group's own mean. Watch scientific notation (`1.66e-14` ≈ 0 ⇒ report **`< 0.001`**). The **intercept** row = fitted Y when all X = 0 (often not meaningful).

**G.4 Terminology / synonyms**
Same idea, different word — the exam may not match your notes. **Inputs:** `predictor = covariate = input variable = independent/explanatory variable = X` (all the RHS variables). **Output:** `response = outcome = dependent variable = Y` (must be **continuous** for linear regression). **Fit pieces:** `fitted = predicted = ŷ`; `error = ε = disturbance` (**true, unobservable**) **≠** `residual = ê` (**observed** `y − ŷ`); `SSR = SSE = RSS` (sum of squared residuals). **Parameters:** `coefficient = parameter = β` (true) vs `b̂ / β̂` (estimate). **Others:** `slope = b̂1`; `intercept = b̂0`; `σ̂ = residual standard error` (scatter of points) vs `SE(b̂) = standard error` (wobble of the estimate); `multicollinearity` = association **among predictors** (not predictor-with-response); `homoscedasticity = constant/equal variance`, `heteroscedasticity = non-constant variance`.

**G.5 Inference distributions — data vs. inference; t vs z; the null yardstick**
**Data distribution ≠ inference distribution:** the *data* distribution = shape of one Y (Normal/Bernoulli/Poisson); the *inference* distribution = sampling distribution of a statistic (b̂/SE) across samples (t or z) — they needn't match, e.g. **Poisson data is nothing like Normal yet inference is z**, because the **CLT / MLE asymptotic normality** makes *estimates* ≈ Normal even when raw data isn't. **Linear → t, GLM → z** (same statistic b̂/SE, different reference): linear estimates a **separate σ²** → extra uncertainty → **t** (fatter tails, df=n−k); GLMs have **no free σ²** → straight to **Normal z**, but only **large-sample (MLE)** → GLM inference is *approximate*, linear's t *exact*; t→Normal as df grows (cutoff→1.96). **t vs Normal:** same bell, t has **fatter tails** because it *estimates* σ (Normal assumes σ known); small df = bigger cutoff than 1.96. **Reference dist centered at 0 = the NULL yardstick, not a belief β=0:** you standardize against 0 (z=(b̂−0)/SE) and ask "if β were 0, would a z this extreme surprise me?" — far tail → reject 0. **r→R² trap:** given a correlation, **square it** — r=0.3 → R²=0.09 (9%), NOT 30% (cousin of the odds-ratio %-change slip — don't skip the transformation).

---

# NOTES (handwritten review)

**N.1 Topic 1 review points**
- **SE of b̂1 = 0 only if no sampling variability** → you've observed the **whole population**, or the data are **perfectly deterministic**.
- **Scatter of points** around the line reflects **residual error variance**, while **SE of b̂1** measures how much the **coefficient estimate itself wobbles** across related samples.
- Because b̂1 comes from a **random sample**, `lm()` assumes **Normal errors** and uses theory to say the **standardized estimate follows a t-distribution with n−k df**, which gives the SE. So we can **approximate the t-distribution with the Normal**.
- We are **95% confident** the true slope lies in this interval because the **procedure that built it captures the true parameter 95% of the time across repeated samples** — NOT because this specific interval has a 95% probability.
- The **95% CI excludes zero** (reject), the **statistic exceeds the critical value ~1.96** (reject), and the **p-value falls below 0.05** (reject) — **all three approaches reach the same conclusion** about significance.
- **P-value cannot be zero.** If it appears to be zero, just claim it is **< 0.001**.
- **Evidence strength lives in the p-value, effect size lives in the estimate** — you need **both** to judge whether a finding is truly important.
- **Bootstrapping must sample WITH replacement** so that resamples differ and you get variability; **without replacement** just reproduces the original sample every time, **collapsing the distribution to a single point**.
- With **continuous predictors** we often ignore the **intercept**, because it just means "the value when x is zero," which is **often nonsensical**.
- Testing **b1 = 0 in a two-group regression is mathematically identical to a two-sample t-test** — both compare the same group means and produce the exact same estimate and test statistic.
- You would **change the reference level** to get a more **meaningful baseline** (e.g. a control group or the most common category), so the coefficients tell you the **differences you actually care about**.
- **Real data always has scatter** around the line ∴ a correct model **must include an error term**.
- **Research in linear models focuses on:**
  - **Estimation:** how to estimate the true (but unknown) relation between the response and the input variables.
  - **Inference:** how to use the model to infer information about the unknown relation between variables.
  - **Prediction:** how to use the model to predict the value of the response for new observations.
- **Degrees of freedom = n − k** (observations minus number of estimated coefficients) = the **independent information left over after fitting**; it matters because it's the **divisor in σ̂² = SSR/(n−k)** (so it sets your SEs) and controls the **t-distribution's shape** for inference.

**N.2 Topic 2 review points**
- If the relation between the **continuous predictor and the response changes for each level of the categorical variable**, the model should have **different slopes AND different intercepts** for each level ∴ we need to **add interaction term(s)**.
- **Think of it as 2 SLRs in one** (2-level dummy X): Alabama (X=0) → `Y = β0 + β1·0 + ε = β0 + ε`, so `E[Y|X=0] = β0`; California (X=1) → `Y = β0 + β1·1 + ε = β0 + β1 + ε`, so `E[Y|X=1] = β0 + β1`.
- **Reference level** is chosen **alphabetically** (by default).
- **Dummy variables are comparisons to the reference level.**
- **In additive models:** (a) we **assume** the association between each input and the response **does not vary across values of other variables**; (b) each estimate is interpreted as the **association of the input variable with the response, keeping all other inputs in the model constant**.
- An **additive model** with one continuous + one categorical input has a **common slope and different intercepts** for each level of the categorical variable.
- If the relationship between an input and the response **differs across the levels** of the categorical variable, we **add interaction terms** — we allow input variables to **interact with** the association between other variables and the response.
- **Omitting a correlated predictor dumps its effects into the error term, biasing the included coefficient** — until you add it back to the model.
- **Multiple t-tests inflate the false-positive rate;** one **ANOVA F-test controls it** while answering "does the variable matter at all?"
- **`lm()` fits by least squares (not a test)**, then reports a **t/z-test on each coefficient** (`H0: βj = 0`); regressing **Y on a single 2-level categorical = a 2-sample t-test**, while **3+ levels = ANOVA / F-test**.
- **Interaction-term example:** "Since p < 0.001 < 0.05, we **reject H0**: there is a significant interaction between income and state. The effect of income on cancer mortality **depends on** the state — the slope is −0.42 for the reference state and −0.68 (= −0.42 + −0.26) for the other. We therefore **keep the interaction** and **cannot** report a single income effect holding state constant." (**"significant interaction" = keep it, report two slopes.**)

**N.3 Topic 3 review points**
- **QQ plot checks one thing: are your residuals normally distributed.**
  - **x-axis:** theoretical quantiles (where each point **should** fall under normality).
  - **y-axis:** your actual (sorted) residual quantiles (where each point **does** fall).
  - It compares the quantiles of your residuals against the quantiles you'd expect **if they came from a normal distribution**.
  - **How to read:** points fall on the **straight diagonal line** → residuals match the normal pattern (**normality looks fine**). Points **curve or veer off** the line (especially bending away at the **ends/tails**) → residuals are **non-Normal** → assumption violated.
- **Residual plot checks linearity + variance** (whereas the QQ plot only did one).
  - **x-axis:** the fitted y-values ŷ (the model's predictions).
  - **y-axis:** the residuals ê = y − ŷ (how far off each prediction was).
- **Diagnostic summary:**

  | Plot | Checks | Bad sign |
  |---|---|---|
  | Residuals-vs-fitted | L and E | curve (L), funnel (E) |
  | Q-Q plot | N | points off the diagonal |
  | (no plot — design) | I | temporal/repeated data |

- **Why collinearity inflates SEs:** correlated predictors move together, so the data **cannot isolate each one's separate effect** → the estimates **trade off and swing from sample to sample** → that instability shows up as a **larger SE**, quantified by **VIF = 1/(1−R²_j)**.
- **1.96 is the standard-normal cutoff for 95% confidence** — reject `H0: β = 0` if `|z| > 1.96`, and build a 95% CI as `b̂ ± 1.96·SE`.
