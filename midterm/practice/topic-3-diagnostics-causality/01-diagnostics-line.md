# Practice 06 — Assumptions & Diagnostics (LINE)

*Topic 3 (Diagnostics). Solutions: [`solutions/01-diagnostics-line-solutions.md`](solutions/01-diagnostics-line-solutions.md).*

---

**Q1 [SA].** Write out the **LINE** acronym: name each assumption and state it in one sentence.

---

**Q2 [TF] (the one from lecture).** "The assumption that all the error terms have the same variance
does **not** affect the estimator of the standard error of the LS estimators." True or false?
Justify.

---

**Q3 [SA].** The **residuals-vs-fitted plot** is the workhorse diagnostic. Explain *why* residuals
are the right thing to plot (what do they contain?), and describe what the plot should look like if
the model is good.

---

**Q4 [SA].** A residuals-vs-fitted plot shows a clear **funnel** (spread widens as fitted values
increase). Which LINE assumption is violated, what is the technical name for this problem, and what
does the plot look like when the assumption *holds*?

---

**Q5 [SA].** For each of **L, I, E**, name the consequence of violating it. Which two specifically
break your standard errors (and therefore your CIs and p-values)?

---

**Q6 [SA].** Why is **Normality** described as the "least severe" of the four violations? Name the
two things that rescue your inference when errors aren't Normal.

---

**Q7 [SA].** A model of `read ~ income` shows a curved (U-shaped) residuals-vs-fitted plot. (a) Which
assumption is violated? (b) Propose a fix. (c) Explain why adding an `income^2` term still counts as
a *linear* regression.

---

**Q8 [SA].** Which plot diagnoses the **Normality** assumption, and what does a "good"
(assumption-satisfied) version look like? What pattern signals a violation?

---

**Q9 [SA].** In-class Activity 4C: the additive wage model's residual plot funneled out and the Q-Q
plot drifted off the diagonal. Name both violations, then explain why refitting with `log(wage)`
addressed *both* at once.

---

**Q10 [SA].** When is the **Independence** assumption most likely to fail? Give two data situations,
and explain why you often assess independence from the **study design** rather than a plot.

---

**Q11 [SA].** Complete the diagnostic table — for each assumption, name the plot you'd inspect and the
*bad* pattern that signals a violation:

| Assumption | Plot to inspect | 'Bad' pattern that signals a violation |
| --- | --- | --- |
| **L** (linearity) | ? | ? |
| **E** (equal variance) | ? | ? |
| **N** (normality) | ? | ? |
