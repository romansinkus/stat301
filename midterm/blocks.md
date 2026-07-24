# Dense Blocks — copy-paste study snippets

*All the dense blocks generated for the midterm, grouped by **Topic 1 / Topic 2 / Topic 3 / General**.
Each is a compact, copy-paste-ready summary. No emojis; `[slots]` = fill-in.*

---

# INDEX (44 blocks)

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

**Topic 3 — Diagnostics, Multicollinearity & Causality (10)**
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

**General — cross-cutting (4)**
- G.1 Phrasing bank (dense) — G.1a Coefficients · G.1b Inference · G.1c Causation · G.1d ANOVA/diagnostics/multicollinearity
- G.2 Equations (dense) — G.2a SLR · G.2b MLR · G.2c assumptions & collinearity · G.2d quick calc
- G.3 Reading a regression output table
- G.4 Terminology / synonyms

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

**G.3 Reading a regression output table**
In `tidy()` / `get_regression_table()` output, each **row = one coefficient**, each **column = a piece of its inference**. `term` = which coefficient (intercept, a slope, or a **dummy** like `speciesGentoo`); `estimate` = **b̂**; `std.error` = **SE(b̂)** (its sample-to-sample wobble); `statistic` = **z = estimate / SE**; `p.value` = p; `lower_ci` / `upper_ci` = **b̂ ± 1.96·SE**. **Read a row:** the effect is **significant** if `p < α` ⇔ `|z| > 1.96` ⇔ **CI excludes 0**. **Continuous row:** "a 1-unit rise in `[X]` is associated with a `[b̂]` change in Y, holding others constant." **Categorical/dummy row** (e.g. `sexmale`): b̂ = the mean-Y **difference from the reference** level, **not** that group's own mean. Watch scientific notation (`1.66e-14` ≈ 0 ⇒ report **`< 0.001`**). The **intercept** row = fitted Y when all X = 0 (often not meaningful).

**G.4 Terminology / synonyms**
Same idea, different word — the exam may not match your notes. **Inputs:** `predictor = covariate = input variable = independent/explanatory variable = X` (all the RHS variables). **Output:** `response = outcome = dependent variable = Y` (must be **continuous** for linear regression). **Fit pieces:** `fitted = predicted = ŷ`; `error = ε = disturbance` (**true, unobservable**) **≠** `residual = ê` (**observed** `y − ŷ`); `SSR = SSE = RSS` (sum of squared residuals). **Parameters:** `coefficient = parameter = β` (true) vs `b̂ / β̂` (estimate). **Others:** `slope = b̂1`; `intercept = b̂0`; `σ̂ = residual standard error` (scatter of points) vs `SE(b̂) = standard error` (wobble of the estimate); `multicollinearity` = association **among predictors** (not predictor-with-response); `homoscedasticity = constant/equal variance`, `heteroscedasticity = non-constant variance`.

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
