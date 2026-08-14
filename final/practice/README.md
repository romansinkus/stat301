# STAT 301 — Final Practice Questions (Cumulative)

Practice sets **organized by topic**, spanning the **entire course (Topics 1–9)**, built from the
[final study guide](../master_notes.md), the in-class activities, the tutorials, and the worksheets.
**Interpretation is the priority in this course**, so most questions ask you to *explain what a result
means* in plain language, not just compute a number.

> **These sets are written in the real exam's format** — modelled on the actual `STAT301-midterm.pdf`
> and its solutions. Instead of a flat list of tagged questions, each file is a small set of
> **scenario-based Problems**: a Problem gives you a dataset + a model + a table of R output (estimates &
> standard errors), then asks several lettered parts `(a)/(b)/(c)/(d)` — each worth **points**, often with
> **word limits** ("in less than 30 words"). The solution files show the **worked procedure**, the
> **marking scheme**, and **acceptable alternative answers**, exactly like the real solutions.

> **Exam logistics (confirmed from `slides/final-review.pdf`).** **Wednesday, August 19, 2026,
> 3:30–5:40pm (130 min), Life Building 2302**, in person; then up to 20 min (5:40–6:00pm) to upload a
> **single PDF** to Canvas ("Final Exam Solutions upload here"). **Picture ID checked**; Internet only
> at the end, for uploading. The **final is cumulative (Topics 1–9)** but with **more weight on the
> post-midterm material**. Format matches the midterm: **written answers only, NO multiple-choice**;
> interpret R outputs, say what model components mean, explain concepts *in the context of the given
> dataset*. **R code is not directly tested**, but you must read the R *outputs* (`lm`/`glm` summaries,
> `tidy()`/`glance()`/`anova()` tables, VIF, residual & Q-Q plots, LASSO paths, CV plots, CI/PI output).
> There will be **some simple calculations — bring a simple calculator.** **Closed book/notes**, but you
> may bring **TWO letter-size sheets (both sides)** — *two for the final, vs. one for the midterm.*
>
> **Marking philosophy (from the real exam):** **70% for correct procedures, 30% for correct answers.**
> **Show your key steps**, **circle final answers**, and **write clearly** — that is where most marks live.

## What's covered

The final is cumulative. Topics 1–3 (the midterm material) are included in full alongside the
post-midterm topics:

- **Topics 1–3 — SLR, MLR, diagnostics & causality** (pulled in and reformatted from the midterm sets).
- **The GLM bridge** — one link-function idea that ties the whole second half together.
- **Topic 4 — Logistic regression** (binary response: log-odds / odds / probability, 3 scales).
- **Topic 5 — Poisson regression** (count response: log-mean / rate ratios, overdispersion).
- **Topic 6 — Goodness of fit** for linear models (TSS/ESS/RSS, R², adjusted R², RSE, MSE, F-test).
- **Topic 7 — Goodness of fit for GLMs** (deviance, the χ² deviance test, AIC).
- **Topic 8 — Model selection** (LASSO/ridge, λ & cross-validation, the double-dipping problem).
- **Topic 9 — Prediction uncertainty** (confidence interval for a prediction vs. prediction interval).

## How to use this

1. Treat each **Problem** like the real thing: read the scenario/R output, then answer every lettered
   part in **full sentences**, watching the **word limits**. The exam grades wording (e.g. "associated
   with" vs. "causes", "log-odds" vs. "odds" vs. "probability").
2. **Show your key steps**, not just the final answer — that is 70% of the marks — and **circle** numeric
   answers.
3. Check against the matching file in that folder's `solutions/` subfolder. The solutions include a
   marking-scheme note and acceptable-alternative answers.
4. Re-do any Problem you missed a week later. When you want a timed dry run, use the
   [`mock-exam/`](mock-exam/).

## Folder structure (organized by topic)

Each topic folder has its own `solutions/` subfolder. The [`mock-exam/`](mock-exam/) is a cumulative,
deliberately mixed paper for the final dry run.

### [`topic-1-slr/`](topic-1-slr/) — Simple Linear Regression

| File | Covers |
| --- | --- |
| `01-slr-estimation.md` | SLR model, least squares, residuals vs. error, slope interpretation, correlation vs. causation, extrapolation |
| `02-slr-inference.md` | SE of a slope, reading an `lm` inference table, CI interpretation, sampling distributions, the bootstrap |
| `03-categorical-predictors.md` | Dummy variables, reference levels, group-mean interpretation, `factor()`, two-sample t-test equivalence |
| `04-tutorial-caschools-slr.md` | Tutorial 01: generative modelling, EDA (`ggpairs`), fitting & bootstrap inference on CASchools |

### [`topic-2-mlr/`](topic-2-mlr/) — Multiple Linear Regression

| File | Covers |
| --- | --- |
| `01-mlr-additive-anova.md` | Additive MLR (parallel lines), the additive assumption, omitted variables, ANOVA F-test for k-level categoricals |
| `02-interactions.md` | Interaction models, coefficient meanings, group slopes, "two SLRs in one", holding-constant caveat |
| `03-tutorial-caschools-mlr.md` | Tutorial 02: additive vs. interaction on CASchools, statistical vs. practical significance |

### [`topic-3-diagnostics-causality/`](topic-3-diagnostics-causality/) — Diagnostics, Multicollinearity & Causality

| File | Covers |
| --- | --- |
| `01-diagnostics-line.md` | The LINE assumptions, residual & Q-Q plots, consequences of each violation, transformations |
| `02-multicollinearity.md` | What collinearity is/does, VIF/GVIF, thresholds, the two fixes |
| `03-causality-designs.md` | Confounders, reverse causality, Simpson's Paradox, experiment vs. observation, CRD vs. RBD |
| `04-worksheet3-assumptions-sim.md` | Worksheet 03: studying violations by simulation; heteroscedasticity, non-Normality, collinearity histograms |
| `05-tutorial3-multicollinearity-causality.md` | Tutorial 03: the detect-and-fix VIF workflow + the TikTok confounding simulation |

### [`topic-4-logistic/`](topic-4-logistic/) — Logistic Regression (binary response)

| File | Covers |
| --- | --- |
| `01-glm-bridge-and-logistic.md` | The GLM/link idea; logit; 3 scales (log-odds/odds/prob); odds ratios; additive vs. interaction; Wald inference; prediction scale; overdispersion |

### [`topic-5-poisson/`](topic-5-poisson/) — Poisson Regression (count response)

| File | Covers |
| --- | --- |
| `01-poisson-regression.md` | log link; rate ratios; `factor()` gotcha; mean=variance; overdispersion (why Poisson usually over-disperses) |

### [`topic-6-goodness-of-fit/`](topic-6-goodness-of-fit/) — Goodness of Fit (linear)

| File | Covers |
| --- | --- |
| `01-r2-anova-ftest.md` | TSS=ESS+RSS, R² & adjusted R², RSE, MSE, the F-test (both cases), t-test vs. F-test |

### [`topic-7-glm-goodness-of-fit/`](topic-7-glm-goodness-of-fit/) — Goodness of Fit for GLMs

| File | Covers |
| --- | --- |
| `01-deviance-chisq.md` | Deviance = "RSS for GLMs", null vs. residual deviance, the χ² deviance test, why perfect fit is bad, AIC |

### [`topic-8-model-selection/`](topic-8-model-selection/) — Model Selection

| File | Covers |
| --- | --- |
| `01-lasso-and-double-dipping.md` | Stepwise vs. regularization, LASSO vs. ridge, λ & cross-validation, bias–variance, the post-inference / double-dipping problem, postLASSO |

### [`topic-9-prediction-uncertainty/`](topic-9-prediction-uncertainty/) — Prediction Uncertainty

| File | Covers |
| --- | --- |
| `01-cip-vs-pi.md` | Average vs. actual target, confidence interval for a prediction vs. prediction interval, why PI is wider, `geom_smooth` band |

### [`mock-exam/`](mock-exam/) — cumulative dry run

| File | Covers |
| --- | --- |
| `practice-exam.md` | Timed comprehensive practice exam (5 scenario-based Problems, 77 pts) spanning all nine topics, anchored on three datasets: `homes` (linear), `loans` (logistic), `clinic` (Poisson) |

## The real course datasets (recognize these on the exam)

The exam gives you *a dataset* and asks you to interpret its R output. The post-midterm course datasets:

| Model | Datasets used |
| --- | --- |
| **Logistic** | Titanic (`survived`), `Default` credit-card (tutorial 4), Wisconsin **breast-cancer** (worksheet 7), **wage → above/below average** (activities 6–7) |
| **Poisson** | Bikeshare (`bikers`), `galapagos` species (tutorial 5), horseshoe **`crabs`** (worksheet 5), **CD4** counts (activity 9) |
| **Goodness of fit** | **protein ~ mRNA** Nature case study (worksheet 6 / tutorial 6), wage F-test (activity 10) |
| **Model selection** | **Ames housing** + used cars (tutorial 7), simulations (worksheet 8), wage stepwise/LASSO (activities 11–12) |
| **Prediction uncertainty** | **Strathcona** property tax (`assess_val ~ BLDG_METRE`) |

*Numbers in these questions are realistic but sometimes invented for practice — focus on the reasoning,
not memorizing the digits. Every question is written short-answer, matching the real format (no multiple
choice).*
