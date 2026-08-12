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
* If independence is violated, then the **standard errors** of the estimators are biased (the coefficient estimates themselves stay unbiased), so the confidence intervals and hypothesis tests are invalid. (Slide 1.2.2 — same holds for a homoscedasticity violation, slide 1.3.2.)
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
* Confounder: a variable that causes changes in both the response and at least one input variable

  * Example: does smoking cause cancer?
    * lifestyle could be a confounding variable since lifestyle could affect if someone smokes and affect their probability of having cancer
* If you want to establish a causal effect, you need to think about HOW the data was collected

  * Example: testing to see if a new drug helps.
    * Split everyone into two groups: group 1 takes the drug and group 2 gets the placebo. People are randomly assigned into groups (through a process called "randomization"). Then you compare the results.
    * The randomization eliminates confounders
* Experimental designs

  * Completely Randomized Desgin (CRD)
    * Experimental units are randomized throughout the data layout (no correlation between observations)
  * Randomized Block Design (RBD)
    * Splits experimental units into homogenous blocks to remove the variance from the nuisance factors. Then randomly assigns treatments to each block. Blocks are similar in all aspects except treatment
* 

# Topic 4: Logisitc Regression

* The types of regression models are determined by the types of the responses, not the predictors
* For linear regression models, we assume that teh response is continuous and normally distributed
* In practice, many responses are binary (only take two values)
* Variance is completely determined by the mean
  * E(y) = P(y=1) and Var(y)=P(y=1)(1-P(y=1)) if a RV y is binary, taking only two values (0 and 1)
* What are you supposed to do if you want regression model of y on x?
  * A: odds
* For logistic regression, you use the binomial distribution
* Note, there is no error ter since we are modeling a function of the conditional expectation
* Logistic regression model can ve written as h(E(y_i)) = beta_0 + beta_1*X_1i where h(.) is called a link function. h(x) = log(x/(1-x)) -> logit function
  * A linear model is h(x)=x, i.e. E(y_i) = beta_0 + beta_1X_1i
* A model in the form of h(E(y_i)) = beta_0 + beta_1X_1i is called the generalized linear model (GLM)
  * `h` is the link function and `beta_0 + beta_1*X_1i` is the linear part
  * You link the meaning of the response to the linear predictor
  * Though this part doesn't have to be linear, but we will start with linear for now
* In logistic regression, you assume a Bernoulli distribution
* Gaussian = normal distribution
* Least squares is easier to explain than MLE (maximum likelihood estimators)
* In your model, if you choose binomial, it assumes you choose logit link
* Keep in minds that for the interpretation it's in the log-odds scale, though it exhibits the same relationship as the interpretation of linear regression
* When you exponentiate the coefficients, you can interpret the odds rather than the log-odds
* In the final, we will have 1 or 2 mathematical application of logistic regression -> "why can you interpret it that way" 
* You can interpret in the exponential or the non-exponential scale
  * If you don't take the exponential, the interpretation will be of the log-odds
  * You can choose which one you want to interpretation
* (1) Central limit theorem (CLT): If x1, x2, ..., xn which are iid, then you x_bar ->d-> N(mu, sigma^2/n) as n->inf
  * sqrt(n)(x_bar - mu) ->d-> N(0, sigma^2)
* (2) MLE beta_hat
  *  `sqrt(n)(beta_hat-beta) ->d-> N(0, I^-1(beta)) as n-> inf <==> (beta_hat - beta) / SE(beta_hat) ->d-> N(0,1)`
  *  MLE is optimal
*  The two things that are most important are estimate and SE
*  If the p-value is close to the significance level, you have to be careful and look at other things in order be sure about statistical significance
   *  Statistics is approximate (unlike math) -> Statistical thinking
*  The default is log-odd, but you can also do odds or probability
*  On the final, we will need to calculate the log-odd, probability, and log by hand, but typically you can just use software to do this
*  In a bernoulli distribution, the mean and variance depend on each other, so we cannot compare residuals across observations
*  **Pearson residuals**: divides the raw residuals by the standard deviation of the response
   *  More reliable than the raw residual
   *  we are scaling by the variance because it depends on the variance
* If you want to create a residual plot while using logistic regression, you should use **pearson residuals** or **standardized residuals**
* For logistic regression, you should likely just not use the residual plot
* **Overdispersion** is more important for logistic regression compared to residual plots
  * The variance in the data is larger than the theoretical variance
* Interpretation: similar to linear regression models except that the covariate effects are on log(odds) of the response, rather than the response itself
* Estimation: MLE


### Topic 4 Questions
* Why don't we always just use the probability? Isn't this the most useful for the real-world?

### Topic 4 TO STUDY
* MLE
* What is link function
  * what's the difference between the different links
* When do you treat the predictors as an additive function vs. interaction? I saw that on some slides stuff was added, however on other slides it was multiplied
* Variance stuff - why can't we use QQ plots for Log Reg?
  * var(y) = E(y)(1-E(y))

# Topic 5: Poisson Regression
* Poisson dist: P(Y=k) = (e^(-lambda)*lambda^k)/k!, k=0, 1, 2, 3, ...
  * E(Y) = lambda
  * Var(Y) = lambda
* Overdispersion problem:
  * In linear models, you don't have to worry about overdispersion since you have Var(Y_i|X_i = sigma^2) -> indep of B's
* Range problem:
  * Counts are nonnegative. If you use linear regression, we might have a range problem by predicting negative counts.
* You can skip the X in E[Y_i|X_i] as long as you understand that it's there
* The interpretation of the coefficients will be very similar to those of the logistic regression case, except that the covariate effects are on the log-scale instead of the log(odds) scale
* When you take the exponential, the model becomes multiplicative
* If you want to use the residuals, you have to use the Pearson residuals
  * Residual plots in general are not very useful though
  * Overdispersion is  abetter way of evaluating
* If the dispersion parameter is far from 1, then we know that the Poisson Distribution DOES NOT hold
* 

### Topic 5 Questions
* Why do we drop the e? I understand this has something to do with e, but I'm not entirely sure.
* On slide 26 of the topic5.1 notes, why do we need separate models for leisure and working days?
* 

### Topic 5 TO STUDY
* Link function
* Dispersion and overdispersion
  * Why is a dispersion parameter of 1 significant?
  

# Topic 6: Model Evaluation (Goodness of Fit)
* Common issues with models are multicollinearity and interaction
* R^2: percent of variation in the response that can be explained by the linear model
  * y = beta_0 + beta_1*X + e
  * Objective: Where does the variation in y come from
  * Example: 
    * y is the score
    * X is someone's EQ
  * An r^2value of 20-50% is considered useful. In an observational study, it's more difficult to get a higher r^2 value since there is more noise in these models
* Null model: model with the intercept only -> no predictions are useful
* In R, you can use stepwise variable selection using the `step(model)` -> this automatically chooses the useful predictors for you
  * It doesn't actually understand which predictors are important and which are not
* `drop1` is also a useful function for variable selection
  * Works for `glm` and `lm` models
* Final model should be reasonable
  * As long as your model is reasonable, you can stop there -> use your judgement.
  * Do model diagnostics only on the final model
* If there are outliers, you should remove these (i.e. the residual is massive)
* How do we know if our model is "better than nothing" (i.e. the null model)
* R^2 will increase with the number of inputs
  * It takes into account the number of predictors you have in your model
  * Therefore, `adjusted R^2` is a more useful metric for your model
    * It takes into account how many predictors you have
    * Only for linear models (linear regression) -> NOT for logistic regression
* R^2: percent of variation in the response TODO (Slide 4)
* TODO TODO (Slide 4)
* In R, stepwise variable selection
  * Forward: start with null model and add predictors
  * Backward: start with all predictors and remove them
  * Don't blindly trust the results of this process -> "there is no perfect model"
    * It's fine if everyone ends up with different models, as long as there are associated justification to go with them
* Residual: `what you observe` - `what oyu predict`
* Your model should be at least as good as the null model
* Explained Sum of Squares (ESS)
  * y_hat is the predicted value based on a model
    * y_hat = beta0_hat + beta1_hat*X_i
  * y_bar is the predicted value based on the null model
  * variation explained by your model
* Residual Sum of Squares (RSS)
  * variation that cannot be explained by the model (or variation from noise)
  * y = beta_0 + beta_1*X + e -> the RSS aims to explain the error 
* Total Sum of Squares (TSS)
  * Total variation
  * Q: How much is the total variation in the data (response data) that can be explained by your model?
    * A: Sample variance (S^2): 1/n * sum (from i=1 to n) of (y_i - y_bar)^2 (TODO slide 25)
* Sum of squares decomposition:
  * TSS = ESS + RSS
  * Decomposition of total variation
  * ANOVA is a similar idea
  * Q: How to show that your model is more useful than the null model?
    * A: Compare the ESS to RSS 
      * If ESS is much higher than RSS, then the model is useful -> you can also just look at the TSS since this value is comprised of ESS and RSS
* The coefficient of determination: R^2
  * R^2 = ESS/TSS = 1 - (RSS/TSS) = proportion of total variation that can be explained by the model
  * Number between 0 and 1
  * R^2 increases as the number of predictors in the model increases BUT we don't like large models since you will get a large penalty in AIC
* AIC: Akaike Information Criterion
  * (goodness of fit) + (penalty for large model or large number of predictors)
  * Choose a model with small AIC values
  * BIC is similar
* Adjusted R^2: usefulness of your model in linear models
  * Penalized for large number of covariates in the model
* Residual standard error
  * Intuitively, a DF is how much free direction you can use
  * RSE = sqrt((1/(n-p-1)) * RSS)
  * RSE is the variation in the noise
* Mean squared error
* R^2 cannot be used to check if the model is "significantly" better than another model -> you need hypothesis testing in order to measure significance
* What does significant mean?
  * In hypothesis testing, significant means that what you observe is unlikely to have occurred due to chance
* Goodness of fit = how good your model fits the data
* You can split the variation into different sources -> decomposition
* You cannot use R^2 for hypothesis testing
* F-Test: used for testing nested models
  * Use when one model is larger than the other
  * Example:
    * model 1: `y = beta_0 + beta_1*X_1 + e`
    * model 2: `y = beta_0 + beta_1*X_1 + beta_2*X_2 + e`
    * Model 1 is nested within model 2
    * Q: Which model is significantly better?
      * A: To answer this question, we need to use F-test
* WE WILL NOT NEED TO CALCULATE THE F-STATISTIC
* To calculate the F-statistic:
  * RSS of the reduced model divided by the RSS of the full model
* Previously, using an F-table was necessary which has df on the x and y axis of the table which indicates the F value of interest
  * This is not done anymore
* Should just use the anova() command
* R^2 is not a test
  * In order to compare two different models, we must use F-test (using anova) -> tests if one of the predictors can be removed
* F-Test can only be used to compare nested models, not non-nested models
  * If the model is not nested, you cannot use F-test to compare these (e.g. if one of the model uses X1 and the other uses X2)

### Topic 6 Questions:
* What is the difference between drop1() and step()

### Topic 6 TO STUDY:

# Topic 7: Model Evaluation (Goodness of Fit for Logistic and Poisson)
* A "perfect" model goes through all of the points
  * This is not useful even though R^2 = 1 -> it is not useful intuitively since you overfit the data
  * If you get another sample from the same population, the model will likely make many mistakes
  * This is why we prefer non-perfect models that are considered to be "good"
* Deviance is composed of very complex mathematical formulas
* Perfect fit = BAD
  * "Anything that goes to the extreme becomes bad"
* Deviance to test
  * H_0: models I and II are equally good
  * H_1: one model is better
  * For GLM, deviance measures the difference of the two log-likelihoods
  * Deviance ~ X^2(d), where d is the difference of the number of predictors in the two models
    * The test statistic is the deviance
    * ~ under H_0
    * This only works well for large sample. You want an infinite sample size, however in practice this is not possible
* R^2 cannot be used for logistic regression models
* F-Test cannot be used for logistic regression models
* "The most important thing to remember for topic 7":
  * R^2, adj. R^2, RSE, and MSE ONLY apply for linear regression.
  * For logistic regression and poisson regression, we use deviance instead
  * Deviance mathematical formula is ugly, but you can think of Deviance as a generalization of RSS for linear regression
  * Deviance test allows you to compare models

### Topic 7 Questions
* What does generalized linear model (glm) mean?

# Topic 8: Regularization Methods for Variable Selection
* We have already talked about stepwise function
  * start with null model and add x1 and check the R^2 or AIC, then add x2 and check R^2 or AIC, etc.
  * The problem with this method is that it depends on which variables are selected first for this process
  * This results in a model being either kept or left out, however, in real life we also want something in between these two discrete options -> this would be called "smooth"
* Should split your data into training data and testing data
  * Training data is used to get your estimate
  * Testing data is used to check prediction accuracies (y_i - y_i_hat)
    * From the predictions, you can then calculate your MSE
  * This process is called cross-validation
  * You'll likely need to keep updating your training data and therefore updating your estimating
  * You can split the data in many different ways
    * Common approach is to split the data in several different ways
      * e.g. split it in 10 ways = 10-fold cross-validation
      * Pick the model that is the most accurate out of all these possible models that have been created
  * Training data simply refers to the data that you use to get your estimate
* Regularization shrinks coefficients in a continuous way by adding a penalty
* Regularization techniques:
  * Ridge: uses an L2 norm to measure the size of the coefficients
    * We prefer squared rather than abs value since it is smooth and therefore it is differentiable
  * Lasso: uses an L1 norm to measure the size of the coefficients
* Lambda is called a penalty parameter -> this controls how much penalty you give to each coefficient
* We will skip ridge and instead only focus on LASSO
* LASSO
  * High dimensionality problem: number of predictors is much larger than the sample size
  * It is not unbiased
  * Tradeoff between variance and bias
* LASSO has been originally used for high dimensionality problem, but now it's used in other cases since it has "good prediction power"
* LASSO is biased (not unbiased) -> the goal is to minimize the mean squared error
  * MSE = Var(b_j_hat) + bias^2
  * Bias variance tradeoff
* Lambda Selection by CV with LASSO
  * You want to select the number of predictors associated with a small MSE but while selecting the fewest predictors possible
  * Lambda is the penalty -> the graph shows how to best choose the best lambda value
  * You can use R to find the lambda for you
* 69-95-99.7 rule
  * 1SD - 2SD - 3SD away from the mean
* LASSO smoothly selects variables and trains the corresponding model for the values of lambda in the grid -> this differs from stepwise which is instead completely discrete (either 0 or 1 for each of the predictors)
* LASSO is used to build strong predictive models
* Using LASSO for interference is biased -> you get a better prediction, but at the price of having a large bias
* Map function is useful for doing simulation
* Can we use the data to first estimate the parameters then use the same data for inference?
  * Probably not, because you're using the data TWICE
* Parametric vs. non-parametric
  * Parametric model is easier to interpret
* Prediction vs. Inference
  * **inference** is about generalizing your conclusions to the whole population
  * prediction 
* Any smooth and differentiable function can be approximated by a taylor polynomial
* Q: If we use data to select a model, can we fit the selected model using the same data to make inference -> suppose this is the research question. How do we prove it?
  * (1) Mathematical proof -> It is very difficult to prove mathematically
    * You often assume that the sample size is infinite which is not a realistic assumption
  * (2) Can do simulation
    * R is very slow with simulation
    * You repeat the same scenario multiple times to quantify error rates
* Simulation design
  1. Setting (variables): a response variable Y and a p=10 covariates with Normal Distribution
  2. Setting (coefficients): set all coeffs to 0, so none of the generated covariates will have an effect on Y
     * b1=b2=...=b10=0 -> imply that none of the predictors should be selected
  3. generate 100 observations (n) for this setting
  4. Apply the forward selection alg to select at most 3 variables among the 10 available, using the adj R^2
  5. ~~Use the selected model and the same dataset to make inference about the population~~
  6. Replicate this study 1,000 times and compute the type 1 error rate
  * The issue with this setup is step 5 since we are using the same dataset to calculate the p-value. All other parts are fine. Since we are repeating this 1,000 times, this cannot be explained by random chance.
* For loops in R are quite slow -> should use C to do anything computationally demanding
  * R is mostly for interface

### Topic 8 questions
* What is LASSO used for now if it's not used for reducing the size of models?
* Why did we not want small p-values in the simulation experiment?

### Topic 8 TOSTUDY
* Parametric vs. non-parametric
* Prediction vs. inference
* Types of error rates

# Topic 9: Prediction Uncertainty
* `add1()` and `drop1()` can be used when doing stepwise variable selection
* 