---
layout: page
title: "4. Linear Models"
date: 2000-12-20
---

4M1. For the model definition below, simulate observed y values from the prior (not the posterior).
yi ∼ Normal(µ, σ)
µ ∼ Normal(0, 10)
σ ∼ Exponential(1)
4M2. Translate the model just above into a quap formula.
4M3. Translate the quap model formula below into a mathematical model definition.
flist <- alist(
y ~ dnorm( mu , sigma ),
mu <- a + b*x,
a ~ dnorm( 0 , 10 ),
b ~ dunif( 0 , 1 ),
sigma ~ dexp( 1 )
)
4M4. A sample of students is measured for height each year for 3 years. After the third year, you want
to fit a linear regression predicting height using year as a predictor. Write down the mathematical
model definition for this regression, using any variable names and priors you choose. Be prepared to
defend your choice of priors.
4M5. Now suppose I remind you that every student got taller each year. Does this information lead
you to change your choice of priors? How?
4M6. Now suppose I tell you that the variance among heights for students of the same age is never
more than 64cm. How does this lead you to revise your priors?