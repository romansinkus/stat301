* Models make assumptions -> they assume that nothing goes wrong
* EDA:
  * If there are outliers, you should remove them -> otherwise everything will be wrong. You must first perform a visualization to determine this.
  * plot y vs x1, y vs x2, 
  * For logistic regression, create box plots for y vs. X1 where y is on the x axis and x1 is on the y-axis
  * x2 vs. x1 shows multi-collinearity -> should put the R value inside of the plot
  * 2x2 table to summarize EDA for logistic regression
* Conclusions from the model should be consistent with the EDA
  * e.g. if you find significant predictors, then you should be able to point back to the EDA
* Requirement is 6-10 pages
  * Include the most important materials inside the actual report and put the others in the appendix
* Put the R code in the appendix
* Summarize the R output in your own words -> this is to show that you understand what it means and understand what parts are actually relevant
* Include good picture ("good picture makes your report looks a lot better -> should be an informative one and it's worth 1000 words")
* Models
  * You should justify why you're using each of the predictors that you're using
  * Conclusions from the models section should match the conclusions from the EDA


### Questions
* Should we default to including the variables and remove them only if they have poor correlation with the response or if they exhibit collinearity?
  * 
* What if after fitting our model, there are very low significace levels for most of the input variables?
* How many input variables make the most sense to include?
* How do we justify whether we use log, log-odds, or probability for the project?

### Answers
* Use the step function with the full model (all predictors) -> it will select the relevant ones for us during the model creation process
  * We can then corroborate these results with the EDA section
* Try to avoid units that are too large or too small (the magnitudes of each input variable should be similar)
  * You can choose different units -> instead of minutes do per hour or per second -> this way we keep the interpretation
  * Don't need to do normalization across all variables since they become less interpretable
* We can just choose log, log-odds, prob to talk about the model -> we don't need to add justification as to which one we use to discuss the model. We also don't need to include all three in our discussion (we can just choose one).
* You can keep predictors in the model even if they aren't significant
  * Not-significant is still important
  * We just need to include justification in the conclusion for keeping them in the model
* Our model can have a single input variable if the other ones we determine are not significant
---

* Should not use units that are too large or too small
* 