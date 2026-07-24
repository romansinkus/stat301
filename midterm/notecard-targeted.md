# Targeted Notecard — Uncertainty & Inference Concepts

*Deep-dive on the pieces that get conflated: **SSE, σ, SE, z, CI.** They form one pipeline
(fit → noise → precision → test/interval). Companion to [`notecard-ai.md`](notecard-ai.md); belongs with
Topic 1 inference (T1.2–T1.3).*

---

## THE ONE PIPELINE (memorize this chain)

```
SSE = Σ(y−ŷ)²                          fit: how far DATA is from the LINE
   │  σ̂² = SSE / (n−k)                 estimate the noise variance
   ▼
σ̂  (residual standard error)           noise: scatter of POINTS around the line
   │  SE(b̂) = σ̂ / √Σ(x−x̄)²            precision: wobble of the ESTIMATE
   ▼
SE(b̂)
   ├─  z = b̂ / SE                      test: how many SEs b̂ is from 0
   └─  b̂ ± 1.96·SE                     interval: plausible range for true b
```

Everything downstream flows from SSE. **Noisier fit (bigger SSE) → bigger σ̂ → bigger SE → wider CI /
smaller z.**

---

## Error term vs. Residual (classic exam trap)

Same idea (point's vertical gap from a line) but a **different line**: error uses the **true** line,
residual uses the **fitted** line.

| | **Error `eᵢ`** | **Residual `êᵢ = yᵢ − ŷᵢ`** |
|---|---|---|
| Gap from | the **true** line `b0 + b1x` | the **fitted** line `b̂0 + b̂1x` |
| Lives in | the **population** (true model) | the **sample** (fitted model) |
| Known? | **unknowable** (never see true line) | **observable** (computed from data) |
| Formula | `eᵢ = yᵢ − (b0 + b1xᵢ)` | `êᵢ = yᵢ − (b̂0 + b̂1xᵢ)` |

- Differ because `b̂ ≠ b`. Residual = **observable stand-in** for the invisible error.
- **Analogy:** error = distance to the **real bullseye** (can't see it); residual = distance to **where you
  aimed** (fitted line).
- **Why it matters:** LINE assumptions are stated about **errors**; you **check** them with **residuals**
  (residuals-vs-fitted, Q-Q) since errors are unobservable. Assumptions = about errors; diagnostics = use
  residuals.
- Residuals **sum to 0** (LS constraint); true errors have mean 0 in the population but won't sum to exactly 0.

## SSE vs. SE vs. CI (compare & contrast)

| | **SSE / SSR** | **SE** | **CI** |
|---|---|---|---|
| What | `Σ(yᵢ−ŷᵢ)²` total squared residuals | SD of sampling dist. of an estimate | `b̂ ± 1.96·SE` range for true param |
| Measures | fit of line to the **data** | wobble of the **estimate** | plausible range for the **true b** |
| About | data / **fit** | **precision** of `b̂` | **inference** on the parameter |
| Units | (Y units)² — *squared* | coefficient's units | coefficient's units |
| Role | what LS **minimizes** | **quantifies** uncertainty | **expresses** it as a range |
| Bigger ⇒ | worse fit | less precise | more uncertain (wider) |
| Scope | one per **model** | one per **coefficient** | one per **coefficient** |

- **SSE vs the rest = fit vs inference.** SSE = points-vs-line (goodness of fit); SE/CI = estimate-vs-truth
  (uncertainty). You *minimize* SSE to fit; you *report* SE/CI to convey uncertainty.
- **SE vs CI = same info, two formats.** CI is just the SE scaled by 1.96 on each side of `b̂`. That's why
  **CI excludes 0 ⇔ |z|>1.96 ⇔ p<0.05.**
- **Units gotcha:** SSE is squared and grows with n (more terms); SE/CI are in the coefficient's own units.

---

## σ vs. SE vs. z (the "which SD is which" confusion)

- **σ (sigma)** = SD of the errors `e_i` = **vertical scatter of DATA POINTS around the true line**
  ("how noisy is Y"). Estimated from residuals as **σ̂** (residual standard error). The **equal-variance
  (E) assumption** is exactly "**σ is constant** across X."
- **SE(b̂)** = **wobble of the ESTIMATE** `b̂` across samples. Built from σ:
  `SE(b̂1) = σ / √Σ(x−x̄)²`. ↓ with more data / more X-spread; ↑ with more noise (σ).
- **z = b̂ / SE** = signal-to-noise for the coefficient = "how many SEs is `b̂` from 0." |z|>1.96 ⇒
  significant at 5%.

**Key distinction:** σ = scatter of the **points**; SE = scatter of the **estimate**. Different things —
but SE is *computed from* σ. (Don't equate them; the formula is how they connect.)

**z vs t:** σ known ⇒ statistic is exactly Normal (**z**). σ estimated (σ̂) ⇒ technically **t** (n−k df).
Course approximates **t ≈ Normal**, so uses z and 1.96.

---

## Variance vs. SD vs. SE ("SD of *what*?")

**SD = √variance**, and **SE = the SD of an *estimate*** (a special SD). The trick is asking "SD of what?"

| | **Variance** | **SD** | **SE** |
|---|---|---|---|
| Of what | spread of **data** (squared) | spread of **data points** | spread of an **estimate** across samples |
| Measures | variability | variability, original units | **precision** of a statistic |
| Units | (units)² | original units | original units (of the estimate) |
| Relationship | — | `SD = √variance` | `SE = SD / √n` (for a mean) |

- **SD vs SE = the `√n` difference:** SD describes the **data points** and **does NOT shrink** as n grows;
  SE describes an **estimate** and **shrinks with n** (more data ⇒ more precise estimate).
- **In regression:** σ = **SD of the errors** (point scatter), σ² = error **variance** (the "E" assumption
  is σ² constant), and `SE(b̂1) = σ / √Σ(x−x̄)²` = **SD of the estimate `b̂`.** Same pattern: an SD of the
  *data* (σ) feeds an SD of the *estimate* (SE).

## Theory-based vs. Bootstrap (two routes to inference)

Both aim for the **same thing** — the **sampling distribution of `b̂`** (→ SE, CI, p). They differ in
whether they **assume its shape** or **build it from data.**

| | **Theory-based (`lm`)** | **Bootstrap** |
|---|---|---|
| Gets sampling dist. by | a **formula**, assuming a shape | **resampling** the data empirically |
| Key assumption | **errors Normal** (or large-n **CLT**) | none about the *error shape* |
| Best when | assumptions hold, or n large | **non-Normal errors / small n** |
| SE & CI from | the **t/z** distribution (`n−k` df) | spread (SE) + **percentiles** (CI) |
| Cost | instant | many refits (B ≈ 10,000) |

- **Theory** *assumes* the shape: if errors are Normal, the sampling dist. of `b̂` is Normal/t → SE, CI, p
  from formulas. CLT rescues it for large n even if errors aren't Normal.
- **Bootstrap** *builds* the shape: resample **with replacement**, **same n**, refit many times; read SE off
  the spread and CI off the **2.5/97.5 percentiles** (5/95 for 90%).
- Nuance: bootstrap is **distribution-free, not assumption-free** — it still assumes the sample is
  **representative** and observations **independent**; it only drops the *Normal-errors* assumption.

## Fast gut-checks
- **More data (bigger n):** SSE up (more terms) but σ̂ ~stable, SE **down**, CI **narrower**, |z| **up**.
- **Data or estimate?** Points-vs-line = SSE (fit). Estimate-vs-truth = SE/CI (inference).
- **Number or range?** SE = a number; CI = a range (= SE × 1.96 each side).
- **Equal-variance (E) broken** ⇒ σ not constant ⇒ SE formula wrong ⇒ **z, CI, p all invalid** (but `b̂`
  and the SSE-based fit are still fine).

## Two ways to build a CI

Both give a CI for the **true parameter** and are **read identically**; they differ in how it's built.

| | **Theory / formula** | **Bootstrap percentile** |
|---|---|---|
| Formula | `b̂ ± 1.96·SE` (95%) | percentiles (2.5 / 97.5) of resamples |
| Assumes | Normal errors / CLT | none about error shape |
| SE from | formula (`σ̂/√Σ(x−x̄)²`) | spread of resampled estimates |
| Best when | assumptions hold / large n | non-Normal errors / small n |
| Symmetric about `b̂`? | **yes** | **not necessarily** (follows data's shape) |
| R | `get_regression_table()` / `tidy(conf.int=TRUE)` | `get_confidence_interval(type="percentile")` |

- `z*` = **1.96** (95%), 1.645 (90%), 2.576 (99%). *(Variant — bootstrap SE method: `b̂ ± 1.96·SE_boot`,
  using the SD of the bootstrap estimates as the SE.)*
- **Read (either method):** "across many samples, **95% of such intervals** contain the true parameter" —
  NOT "95% probability the truth is in this one interval."

## Role of `e` in the SLR (`Yᵢ = b0 + b1Xᵢ + eᵢ`)

- `e` = **everything affecting `Y` that `X` doesn't capture** = **omitted variables + pure random noise**
  (not just "measurement error").
- **Makes the model stochastic, not deterministic:** without `e` every point sits exactly on the line;
  `e` is why two obs with the **same X** can have **different Y**, and it produces the **scatter around the
  line.**
- **Separates average from individual:** `E[Y|X]=b0+b1X` = the line (the *average* Y at each X); `eᵢ` = how
  far individual `i` sits **off** that line.
- **Assumptions ride on `e`** (LINE: independent, Normal, constant variance σ²). σ = **SD of `e`**.
- Don't confuse with the **residual** (its observable sample stand-in) — see Error-vs-Residual above.
- **One-liner:** *`e` = all of `Y` not explained by `X` (other variables + noise); it makes the model
  stochastic and creates the scatter around the line.*

## Experimental vs. Observational (+ design types)

| Feature | **Experimental (randomized)** | **Observational** |
|---|---|---|
| Treatment assigned by | **researcher, randomly** | occurs naturally / self-selected |
| Observed confounders | balanced by randomization | can **adjust** for (if measured) |
| **Unobserved** confounders | **balanced on average** | **remain** (can't adjust) |
| Causal claim? | **Yes** — gold standard | **No** — association only |
| Handle confounders via | **randomization** (design) | **adjustment** / **stratification** |
| Feasibility | often impractical/unethical | always available |
| Course example | randomize the ad ⇒ recovers +8 | customers choose ad ⇒ confounded (9.83) |

**Kinds of experimental design:**

| | **CRD (Completely Randomized)** | **RBD (Randomized Block)** |
|---|---|---|
| How | randomize units **freely** across treatments | split into **homogeneous blocks** (known nuisance factor), randomize **within** each block |
| Balances observed conf.? | Yes | Yes |
| Balances **unobserved**? | **Yes** | **No** — only the blocking factor |
| Causal strength | **gold standard** | estimates **average** treatment effects |
| Use when | default | a **known strong nuisance factor** to control |

- **Key line:** CRD balances **observed AND unobserved** confounders (gold standard); RBD blocks a **known**
  nuisance and balances **observed only**; observational balances **nothing** (adjust known confounders
  only) ⇒ association, not causation.

## LINE assumptions

The 4 assumptions (stated about the errors, or equivalently the `y`'s):

| | Assumption (what it means) | Diagnose | If violated | Fix |
|---|---|---|---|---|
| **L** | **Linear** — `E[Y\|X]` linear in params; `E(e)=0` | residuals-vs-fitted: no pattern | model **dubious/misspecified** | add `X²` / `log` / interaction |
| **I** | **Independent** errors (uncorrelated) | study design; residual runs | **SEs biased ⇒ CIs & tests invalid** | time-series / longitudinal methods |
| **N** | **Normal** errors | Q-Q plot (on diagonal); histogram | **least severe** — CLT / bootstrap save you | transforms; or rely on CLT / bootstrap |
| **E** | **Equal variance** (constant σ², homoscedastic) | residuals-vs-fitted: **funnel = bad** | **SEs wrong ⇒ CIs & p invalid** | transform Y (`log`,`√`); WLS |

- Point estimates stay OK under **I/E/N**; it's the **SEs** that break (**I & E** ⇒ CIs & p invalid).
  **L** breaks the whole model. **N** is mildest (CLT/bootstrap).
- **Prof's key point — all 4 in one sentence:** **`e₁,…,eₙ` are iid `N(0, σ²)`.**
  - **iid** ⇒ **I**ndependent + *identically* distributed (same **constant variance**, E)
  - **N(0, σ²)** ⇒ **N**ormal, **mean 0** (correct linear mean, `E(e)=0`, the L part), constant **σ²** (E)
- **"Linear in the PARAMETERS, not the predictors":** transformed predictors are fine —
  `y = β0 + β1·x + β2·(1/√x) + e` (or `x²`, `log x`) is **still linear regression.** Only the
  interpretation changes, not the method.
