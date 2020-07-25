---
layout: page
title: "4. Linear Models"
date: 2000-12-20
use_math: true
---

# Medium.

**4M1.** For the model definition below, simulate observed heights from the prior (not the posterior).

$$\begin{align}
y_i &\sim Normal(\mu, \sigma) \\
\mu &\sim Normal(0, 10) \\
\sigma &\sim Uniform(0, 10)
\end{align}$$

<hr>

**4M2.** Translate the model just above into a `map` formula.

<hr>

**4M3.** Translate the `map` model formula below into a mathematical model definition.

{% highlight r %}
flist <- alist(
	y ~ dnorm( mu , sigma ),
	mu <- a + b*x,
	a ~ dnorm( 0 , 10 ),
	b ~ dunif( 0 , 1 ),
	sigma ~ dunif( 0 , 50 )
)
{% endhighlight %}

<hr>

**4M4.** A sample of students is measured for height each year for 3 years. After the third year, you want to fit a linear regression predicting height using year as a predictor. Write down the mathematical model definition for this regression, using any variable names and priors you choose. Be prepared to defend your choice of priors.

<hr>

**4M5.** Now suppose I tell you that the average height in the first year was 120cm and that every student got taller each year. Does this information lead you to change your choice of priors? How?

<hr>

**4M6.** Now suppose I tell you that the variance among heights for students of the same age is never more than 64cm. How does this lead you to revise your priors?