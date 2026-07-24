# Solutions 08 — Causality & Study Designs

*Questions: [`../03-causality-designs.md`](../03-causality-designs.md).*

---

**Q1.** Whether you can claim causation depends on **(1) how the data were collected** (experimental
vs. observational) and **(2) the methods used** to analyze it. A good model fit alone never earns a
causal claim.

---

**Q2.** A **confounder** `C` causes changes in **both** the predictor `X` **and** the response `Y`:
```
      C
     / \
    v   v
    X → Y
```
Because `C` moves both `X` and `Y`, they appear associated even if `X` doesn't cause `Y` — the
`C → X` and `C → Y` paths make `X` and `Y` rise and fall together, tangling the true `X → Y` effect
with the confounder's influence.

---

**Q3.** The flaw is **reverse causality**: struggling students probably *receive* more help *because*
they're already doing poorly, so the causal arrow more plausibly runs **grades → help** (low grades
cause more help), not **help → grades**. The negative association is real, but the stated causal
direction is backwards.

---

**Q4.** **Simpson's Paradox:** an association's **direction reverses** when you split the data by a
subgroup. **UC Berkeley 1973:** aggregate admissions looked biased *against* women, but **within
almost every department** there was no such bias — women applied disproportionately to **more
competitive departments** (lower admit rates). Lesson: **aggregated and stratified data can disagree**,
so a lurking grouping variable can flip conclusions; always consider relevant subgroups.

---

**Q5.**

| | Experiment (randomized) | Observational study |
| --- | --- | --- |
| Treatment set by | **researcher, randomly assigned** | just **measured** as it naturally occurs |
| Unobserved confounders | **balanced on average** by randomization | **remain** — can't be adjusted for |
| Causal claim | **Yes** — gold standard | **No** (not naively) — association only |

---

**Q6.** **False.** Randomization balances the groups **on average across *all* variables — including
ones you never measured or thought of.** That's precisely why it's "magic": you don't need to know or
measure the confounders for them to be balanced. (Adjusting/matching only handles **observed**
confounders; randomization handles unobserved ones too.)

---

**Q7.** **CRD:** units are randomized **freely** across treatments; balances **observed AND
unobserved** confounders → gold standard for causal inference. **RBD:** first split units into
**homogeneous blocks** (to remove a known nuisance factor), then randomize **within each block**;
this balances **only observed** confounders (the blocking variable), so only average treatment
effects are estimated with appropriate methods. You'd choose RBD to **control a known, strong nuisance
factor** and gain precision, when it's practical to block on it.

---

**Q8.**
(a) The true causal effect of the new ad is **+8** (23−15 for non-athletes, 28−20 for athletes) —
consistent **within each stratum**.
(b) In an observational study athletes disproportionately pick the **new** ad, and athletes also have
**higher baseline dwell times**. So the "new ad" group is loaded with high-dwell athletes and the
"current" group with lower-dwell non-athletes; the **athlete effect gets added on top of** the true
+8, inflating the apparent ad effect. `athlete` **confounds** the comparison.
(c) **Randomizing** the ad assignment breaks the `athlete → ad choice` link, so athletes and
non-athletes are **balanced across both ad groups**; the athlete effect cancels out and the estimate
recovers the true **+8**.

---

**Q9.**
(a) **Causal claim justified.** It's a **randomized trial**, so groups are balanced (even on
unobserved confounders); the difference in blood pressure can be attributed to the drug.
(b) **Not justified.** It's **observational** — coffee drinkers may differ systematically (income,
social activity, health behaviors) that also affect depression (confounding), and reverse causality
is possible (depressed people may drink less coffee). Association only.
