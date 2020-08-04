---
layout: page
title: "4. Linear Models"
date: 2000-12-21
use_math: true
---

# Easy.

**4E1.** In the model definition below, which line is the likelihood?

$$ \begin{align}
y_i &\sim Normal(\mu, \sigma) \\
\mu &\sim Normal(0, 10) \\
\sigma &\sim Uniform(0, 10)
\end{align} $$

$y_i \sim Normal(\mu, \sigma)$ is the likelihood.

<hr>

**4E2.** In the model definition just above, how many parameters are in the posterior distribution?

There are two parameters in the posterior distribution: $\mu$ and $\sigma$.

<hr>

**4E3.** Using the model definition above, write down the appropriate form of Bayes’ theorem that includes the proper likelihood and priors.

$$ Pr(\mu, \sigma \mid y) = \frac{\prod_i Normal(y_i \mid \mu, \sigma) \, Normal(\mu \mid 0, 10) \, Uniform(\sigma \mid 0, 10)}{\iint \prod_i Normal(y_i \mid \mu, \sigma) \, Normal(\mu \mid 0, 10) \, Uniform(\sigma \mid 0, 10) \, d \mu d \sigma} $$

<hr>

**4E4.** In the model definition below, which line is the linear model?

$$ \begin{align}
y_i &\sim Normal(\mu, \sigma) \\
\mu_i &= \alpha + \beta x_i \\
\alpha &\sim Normal(0, 10) \\
\beta &\sim Normal(0, 1) \\
\sigma &\sim Uniform(0, 10)
\end{align} $$

$\mu_i = \alpha + \beta x_i$ is the linear model.

<hr>

**4E5.** In the model definition just above, how many parameters are in the posterior distribution?

There are three parameters in the posterior distribution: $\alpha$, $\beta$ and $\sigma$.