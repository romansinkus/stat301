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
* Relationship between 2 sample T-test and regression
  * TODO
* If it is not continous, you cannot use linear regression
* You will never know B_1, but you can determine B1_hat
* What is the difference between SD and SE?
  * SD(y_bar) = sigma / sqrt(n)
  * SE(y_bar) = sigma_hat / sqrt(n)
  * SE is an ESTIMATION of the SD since SD has something that is unknown (since sigma is unknown)
* When you have several different values for B0_hat and B1_hat from different samples, you cannot tell which one is the best estimate, however you can use them to create a sampling distribution
* Inference: althought we don't know the value of B1, we can be 95% confident that the number is between the cofidence interval. For a 95% confidence interval, 95% of the time the value would lie between these two intervals
* One way of conducting inference is confidence intervals and the other way is by using hypothesis testing
* The smaller the p-value, the stronger the evidence against H_0
* Two ways for inference of B_1
  * 95% C.I. for B1 (note: 95% is most commonly used, but you can use different numbers for this)
  * Test hypotheses: H0: B1 = 0 vs. H1: B1 != 0 (d=0.05)
* What is the relationship between CI and hypothesis testing?
  * 95% CI of B1 covers 0 *is equivalent to* fail to reject H0 at 5% level
* Just use Z instead of using a t-test ("don't worry about T")
* How do we know the sampling distribution of the estimators of the regression coefficients?
  * We have different wats of answering this question:
    * Use a theoretical result. This is what lm does.
      * You need assumptions such as normal distribution.
    * Use boostrapping.
* Note: When doing exercises that use bootstrap, you should try writing this code independently
* This course will not emphasize too much on bootstrap
* Q: What is the SE for sample mean (y_bar)?
  * A: SE(y_bar) = s/sqrt(n) where s = simga_bar
* Q: What is the SE of correlation r?
  * A: Use bootstrap
* Q: What is the SE of median?
  * A: Use boostrap
* Code example for using bootstrap:

```R
data = c(1, 3, 4, 9)
median(data)
boot1 = sample(data, 4, replace=T)
boot1
m1 = median(boot1)
m1
boot2 = smaple(data, 4, replace=T)
boot2
m2 = median(boot2)
m2
```

* Does the number of replicates matter?

  * The approximated sampling distribution becomes smoother.
  * If B >= 100, then this is typically sufficient. Making it much larger than this may require significant computational power.
* A lot of models rely on iterative algorithms (TODO)
* Types of models (TODO):

  * Frequestist <- likelihood methods
  * Bayesian
* `Bayes formula = f(theta | y) = (f(y | theta)f(theta)) / f(y)`

  * f(y) can be calculated using integral of f(y|theta)f(theta)dtheta
* MCMC (TODO)

  * Not easy to implement -> requires significant computing power
* EM algorithm (TODO)
* CLT says....

  * `sqrt(n)*(y_bar - mu) ->d-> N(0, sigma^2) as n goes to inf`
* Bootstrap methods work for ANY SAMPLE SIZE and ANY DISTRIBUTION (no matter how complicated the estiamte may be)
* Boostrap confidence intervals

  * Standard error method: use the list of bootstrap estimates to approximate (only) the SE of the estimator
  * Percentile method: use the list of bootstrap estimates to the ratnge using quantiles
* The p-values computed by the function `lm` are based on classical theoretical approximations or experimen

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

### Clicker Questions

* If x and y has a positive correlation, the regression of y on x has a positive slope
  * A: TRUE
  * `B1_hat = correlation * s_y/s_x` therefore we can rewrite this in terms of correlation
* If x and y has a positive correlation, the higher the correlation, the larger the slope of teh regression of y on x
  * A: Poorly designed question
* The regression of y on x is the same as the regression of x on y.
  * A: FALSE
  * `y = B0 + B1X` therefore `x = -B0/B1 + (1/B1)*y` these two equations are not the same
* 

---

# Topic 2 Notes: Multiple Linear Regression

* Categorical variables when using MLR are separated out into differnt
* y = beta_0 + beta_1(state) + epilson and t_test are equivalent with SIMPLE LINEAR REGRESSION
* The first level in MLR is the reference level. The default is 0, but you can change this in R. When you have 2 categories, the default reference level is 0.
* Linear regression can be written using conditional expection in addition to the typical linear regression formula
* When you are using two different categories, the slope that the linear model defines is the difference level between the response varibale in category 1 and the response variable in category 2
* If you have two categories, you can simply have one variable ->  0 and 1. When there are more than 2 levels, this gets more complicated.

  * We have 2 dummy variables for 3 levels. The reference level is 0 by default.
  * `e.g.` X = 0 -> Indiana, 1 -> Washington, 2-> Kansas. X = 0 would mean Kansas
* When you have 2 groups, you can simply use a t-test, but what can you use when there are 3 groups?

  * A: ANOVA is used or you can use SLR with state
* Additive model: `beta_0 + beta_1 * X_1 + beta_2 * X_2 + ep`
* TODO: Additive vs. non-additive models
* One hot encoding gives `k` columns whereas dummy variable encoding gives `k-1` columns
* TODO: interaction vs. non-interaction and how to determine it visually
* Question: How do we know there is an interaction?

  * A: You test the null hypothesis (`H_0: beta_3 = 0 (no interaction)` `H_1 :beta_3 != 0 (there is an interaction))`
  * If H_0 is rejected at 5% level, interaction **may** exist
  * Z = beta_3/SE(beta_3) ~ N(0,1) calculate the p-value based on the standard normal distribution
  * TODO: "power"
* **In a MLR the response is always a continuous variable**

### Topic 2 Questions:

### Topic 2 Tutorial/Worksheet:

---

### Topic 3 Notes:

* Review from topic 2:

  * MLR models are the most commonly used models (this is why they are especially important)
  * You can't draw pictures as the number of predictors grows
  * Input variables = predictors, covariates, independent variables
  * y=beta_0 + beta_1X_1 +  beta_2X_2 + eps

    * y must be continuous
    * Once you let R know that a particular variable is a factor, it can differentiate the different categories rather than treating it like numerical data
      * `factor(x2)` `as.factor(x2)`
    * R will automatically choose the first category as the reference category
  * We use **additive** models because they are simple

    * The types can be continuous or categorical
  * Interaction

    * y = beta_0 +beta_1X1 + beta_2X2 + beta_3X1X2 + eps
    * The product term is the interaction term
    * To determine if you actually need the interaction term, you use a hypothesis test
      * H_0: beta_3 = 0
      * H_1: beta_3 != 0
    * One of the interpretation difficulties is **interaction**
* All models need assumptions

  * Without assumptions, you **cannot do anything** since the derivations are all derived based on assumptions
  * y = beta_0 + beta_1X1 _ beta_2X2 + eps ==> y = f(x1, x2) + eps
  * You must assume the distribution of the error. In order to get the probability, you have to get the distribution.
  * When you are assuming a distribution, the most common is a **normal distribution**
  * LINE acronym. Without these assumptions, you cannot get the p-value or estimates.

    * Linear
    * Independence
    * Normality
    * Constant variance (i.e. variance doesn't change)
* A linear model is defined by the parameters (the beta values)
* If independence is violated, then the estimates would be biased. The hypothesis tests would be invalid.
* TODO: constant variance assumption
* "A model should be simple, but not TOO simple"
* Log(Y) and sqrt(Y) can be used to stabalize the function. Note that log is typically better than sqrt
* Without normal distribution, it would be difficult to compute the p-value
* Multicollinearity

  * strong association between two or more covariates
  * multicollinearity inflates the standard errors of our estimates
  * Pairwise correlation: correlation between each pair of covariates
* VIF: variance inflation factor -> formal way to check the multicollinearity

  * If it is higher than 5 or 10, this suggests collinearity might be a problem
  * Generalized VIF is preferred because the VIF of categorical covariates are affected by the number of categories they have
* Degrees of freedom  = # of predictors - 1
*
