# Practice 03 (Topic 3) — Causality & Study Designs

*Topic 3 (Causality). Solutions: [`solutions/03-causality-designs-solutions.md`](solutions/03-causality-designs-solutions.md).*

> **Exam-style.** Written short answer only. **Show the key steps** (70% procedure, 30% answer). Where a
> question says *draw*, clearly label your diagram.

---

## Problem 1 (16 pts) — Confounding and causal reasoning

**(a) (3 pts)** "Association is not causation" — but *what* determines whether you can make a causal
claim? Name the two things (from lecture) that a causal claim depends on.

**(b) (4 pts)** Define a **confounder** `C` in terms of the arrows it draws to `X` and `Y`. Draw the
confounder diagram, and explain how it creates a misleading association between `X` and `Y`.

**(c) (5 pts)** (i) "Children who get more parental homework help tend to have *lower* grades, so
parental help hurts grades." Name the most likely flaw in this causal reasoning, and say in which
direction the causal arrow more plausibly runs. (ii) Explain **Simpson's Paradox** and give the UC
Berkeley 1973 admissions example. What is the general lesson about aggregated vs. stratified data?

**(d) (4 pts)** For each finding, say whether a causal claim is justified and why: (i) a randomized trial
finds a drug lowers blood pressure more than placebo; (ii) an observational survey finds coffee drinkers
have lower rates of depression.

---

## Problem 2 (16 pts) — Study designs and a confounding simulation

An ad study measures **dwell time** (seconds) by group:

| | current ad | new ad |
| --- | --- | --- |
| non-athlete | 15 | 23 |
| athlete | 20 | 28 |

**(a) (4 pts)** Fill in the contrast between an **experiment** and an **observational study** on three
rows: how the treatment is set, what happens to *unobserved* confounders, and whether a causal claim is
licensed.

**(b) (3 pts)** "Randomly assigning treatment balances the groups only on the variables the researcher
measured." True or false? Justify — this is the whole reason randomization is called "magic."

**(c) (4 pts)** Distinguish **Completely Randomized Design (CRD)** from **Randomized Block Design (RBD)**.
Which balances *unobserved* confounders, and which balances only *observed* ones? Why would you ever
choose RBD?

**(d) (5 pts)** Using the table: (i) what is the true causal effect of the *new ad* (within each athlete
stratum)? (ii) In an **observational** study where athletes disproportionately choose the new ad, why
does the apparent ad effect come out *too large*? (iii) How does randomizing the ad assignment recover
the true effect?
