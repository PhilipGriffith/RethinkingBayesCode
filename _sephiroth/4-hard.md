---
layout: page
title: "4. Linear Models"
date: 2000-12-19
---

4H1. The weights listed below were recorded in the !Kung census, but heights were not recorded for
these individuals. Provide predicted heights and 89% intervals for each of these individuals. That is,
fill in the table below, using model-based predictions.
Individual weight expected height 89% interval
1 46.95
2 43.72
3 64.78
4 32.59
5 54.634.7. PRACTICE 125
4H2. Select out all the rows in the Howell1 data with ages below 18 years of age. If you do it right,
you should end up with a new data frame with 192 rows in it.
(a) Fit a linear regression to these data, using quap. Present and interpret the estimates. For
every 10 units of increase in weight, how much taller does the model predict a child gets?
(b) Plot the raw data, with height on the vertical axis and weight on the horizontal axis. Superimpose the MAP regression line and 89% interval for the mean. Also superimpose the 89% interval
for predicted heights.
(c) What aspects of the model fit concern you? Describe the kinds of assumptions you would
change, if any, to improve the model. You don’t have to write any new code. Just explain what the
model appears to be doing a bad job of, and what you hypothesize would be a better model.
4H3. Suppose a colleague of yours, who works on allometry, glances at the practice problems just
above. Your colleague exclaims, “That’s silly. Everyone knows that it’s only the logarithm of body
weight that scales with height!” Let’s take your colleague’s advice and see what happens.
(a) Model the relationship between height (cm) and the natural logarithm of weight (log-kg). Use
the entire Howell1 data frame, all 544 rows, adults and non-adults. Fit this model, using quadratic
approximation:
hi ∼ Normal(µi, σ)
µi = α + β log(wi)
α ∼ Normal(178, 20)
β ∼ Log − Normal(0, 1)
σ ∼ Uniform(0, 50)
where hi is the height of individual i and wi is the weight (in kg) of individual i. The function for
computing a natural log in R is just log. Can you interpret the resulting estimates?
(b) Begin with this plot:
R code
plot( height ~ weight , data=Howell1 , 4.80
col=col.alpha(rangi2,0.4) )
Then use samples from the quadratic approximate posterior of the model in (a) to superimpose on
the plot: (1) the predicted mean height as a function of weight, (2) the 97% interval for the mean, and
(3) the 97% interval for predicted heights.
4H4. Plot the prior predictive distribution for the polynomial regression model in the chapter. You
can modify the code that plots the linear regression prior predictive distribution. Can you modify the
prior distributions of α, β1, and β2 so that the prior predictions stay within the biologically reasonable
outcome space? That is to say: Do not try to fit the data by hand. But do try to keep the curves
consistent with what you know about height and weight, before seeing these exact data.