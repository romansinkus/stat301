# Intro/Admin

* The course focusing on "understanding" and "analyzing"
* In the exam, you have to show the key steps of your solution
* People say that your future success is largely because of your EQ and only a portion is because of your IQ
  * Emotional Intelligence: ability to manage your emotions

---

# Topic 1: Simple Linear Regression (SLR)

### Topic 1 Notes

* Pretty much all models are approximations (and therefore cannot be considered exact)
* **Least Squares Method** minimizes the sum of the squares of the residuals
  * Residual of an observation is the difference between its response value and its predicted response on the line ("represented by the dotted vertical line")
* SLR can be used to describe association but not necessarily establish a causal relationship between covariate and response
* Stoichastic -> uncertain, deterministic -> certain
* Sometimes models that are only able to describe a small amount of variation (e.g. 40%), they can still be useful
* The **response** is the variable that you are interested in
* Xi and Yi denote the values of X and Y for observation i
  * You can think of it as `n` pairs: (X1, Y1), (X2, Y2), ..., (Xn, Yn)
* The error term (epsilon) is the variation in y that cannot be explained by X
  * `Yi = B0 + B1Xi + Ei`
  * B0= intercept, B1 = slope, Ei = error term
* Uncertainty is measured by the standard error
* Intuition and understanding are very important
* An unbiased estaimte means that E(B1_hat = B1) -> the estimate should be equivalent to the true value
* YOU NEED TWO THINGS:
  * 1. Unbiased estimate
    2. Uncertainty (SE)
* If we want to test if there exists a linear association between cancer mortality and poverty **the null hypothesis** is `B1 = 0`.
* We treat `Ei` as a random variable
  * It has a distribution -> we assume it to be normal
  * It has a mean -> we safely assume it to be 0
  * It has a variance -> unknown and denoted by sigma^2
* Interpretation of B0 and B1
  * B1 is the slope
  * B0 is the average value of Y when X = 0
    * Note: we don't care as much about this parameter
* The parameters of B0 and B1 (*slide 51*)
  * B0_hat and B1_hat depend on the sample, therefore we will need their **sampling distribution**
* Inference for B0_hat (*slide 51*):
  * **Inference** means... can we generate results for a single dataset to a larger population?
  * Two approaches:
    * 1. Confidence interval for B0
      2. Hypothesis testing for B0
* Confidence intervals for B0 and B1 (*slide 56*)
  * They are derived based on the assumption that E is normally distributed
  * Q: What if the normal assumption does NOT hold?
    * A: We can use **bootstrap**. This is like "advil" in statistics because it does not need a formula and we can use it if nothing else is working. It will still give you a confidence interval. You don't need any sort of assumptions.
      * Q: If we have bootstrap, why even learn to use the formula?
        * A: Bootstrap works, but it may not give you a narrow confidence interval. If you want the most narrow confidence intervals, using the formula is better to use.
* In other hypothesis tests, the null hypothesis claims a null state (status quo), but in SLR the status quo is the absense of a relation between the reponse and the input variable(s)
* In statistics, we do not prove that the null hypothesis is true or false, we can only reject or fail to reject the null hypothesis based on the evidence in the data
* Alternative hypothesis:
  * H_1 = B_1 > 0
* In statistics, bootstrapping refers to sampling from our original sample with replacement to generate a bootstrap sampling distribution. The idea is to use the original sample as an estimate of the unknown population.

### Topic 1 Questions:

* Why is the residual different than the error term?
* Why do we first consider a linear relationship?
  * A: Because we want to start with something simple. We can later use a more complex models.
  * `y = B0 + B1X`
* How do you esimate the values of B0 and B1?
  * A: You first get the data, then you find a line that is closest to all data points.
    * Q: How do you find the line that is closest to all the data points?
      * A: Optimization problem. Minimuze the the sum of `(yi - (B0 + B1Xi))^2`. You must solve `dQ/dB0 = 0`and`dQ/dB1 = 0`. Solutions: B0_hat and B1_hat are estimates of B0 and B1. Note: the estimates are not the same as B0 and B1. The B0 and B1 values are never known.
        * Q: How do you know if B0_hat and B1_hat are good?
          * A: True value of B1 may be between B1_hat - 1.96xSE(B1_hat) and B1_hat + 1.96xSE(B1_hat). Hypothesis testing is equivalent to confidence intervals. SE(B1_hat) is the unceratinty of the estimate.

---

# Topic 2 Notes:

### Topic 2 Questions:
