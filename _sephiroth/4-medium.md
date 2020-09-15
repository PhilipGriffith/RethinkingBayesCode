---
layout: page
title: "4. Linear Models"
date: 2000-12-20
use_math: true
---

# Medium.

The code used to answer the questions below relies on these Python libraries:

{% highlight python %}
import pymc3 as pm
import arviz as az

# I'm using this code to make plotting easy in a Jupyter notebook
%config InlineBackend.figure_format = 'retina'
az.style.use('arviz-darkgrid')
{% endhighlight %}

**4M1.** For the model definition below, simulate observed heights from the prior (not the posterior).

$$ \begin{align}
y_i &\sim Normal(\mu, \sigma) \\
\mu &\sim Normal(0, 10) \\
\sigma &\sim Uniform(0, 10)
\end{align} $$

![4M1]({{ site.baseurl }}/assets/images/4m1.png "4M1")

<hr>

**4M2.** Translate the model just above into a ~~`map`~~ `PyMC3` formula.

The PyMC3 code for both the model and the plot of simulated heights displayed in 4M1 is as follows:

{% highlight python %}
with pm.Model() as m_4M1:
    mu = pm.Normal('mu', mu=0, sd=10)
    sigma = pm.Uniform('sigma', lower=0, upper=10)
    y = pm.Normal('heights', mu=mu, sd=sigma)
    trace_4M1 = pm.sample_prior_predictive(samples=1000, var_names=['heights'],
        random_seed=4)

az.plot_trace(trace_4M1)
{% endhighlight %}

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

$$ \begin{align}
y &\sim Normal(\mu, \sigma) \\
\mu &= \alpha + \beta x \\
\alpha &\sim Normal(0, 10) \\
\beta &\sim Uniform(0, 1) \\
\sigma &\sim Uniform(0, 50)
\end{align} $$

<hr>

**4M4.** A sample of students is measured for height each year for 3 years. After the third year, you want to fit a linear regression predicting height using year as a predictor. Write down the mathematical model definition for this regression, using any variable names and priors you choose. Be prepared to defend your choice of priors.

$$ \begin{align}
height_i &\sim Normal(\mu_i, \sigma) \\
\mu &= \alpha + \beta \cdot year_i \\
\alpha &\sim Normal(171.69, 10.04) \\
\beta &\sim Normal(0, 2) \\
\sigma &\sim Uniform(0, 15)
\end{align} $$

Let's assume the students attend university and have therefore completed puberty. Data for the $\alpha$ prior comes from [Our World in Data: Human Height](https://ourworldindata.org/human-height#height-is-normally-distributed){:target="_blank"}. Data for p in the equations below comes from [Our World in Data: Gender Ratio](https://ourworldindata.org/gender-ratio#gender-ratio-across-the-world){:target="_blank"}. Assuming the height measurements are independent, the mean and standard deviation of adult height can be computed using [the following equations](https://stats.stackexchange.com/questions/205126/standard-deviation-for-weighted-sum-of-normal-distributions){:target="blank"}:

$$ \mu = p \mu_{male} + (1 - p) \mu_{female} $$

$$ \sigma = \sqrt{ p \sigma^2_{male} + (1 - p) \sigma^2_{female} + p(1 - p)(\mu_{male} - \mu_{female})^2 } $$

For the mean:

$$ \mu = \frac{51}{100} 178.4 + \frac{49}{100} 164.7 = 171.69 $$

For the standard deviation:

$$ \sigma = \sqrt{ \frac{51}{100} 7.59^2 + \frac{49}{100} 7.07^2 + \frac{51}{100} \cdot \frac{49}{100} (178.4 - 164.7)^2 } $$

$$ \sigma = \sqrt{ 29.38 + 24.49 + 46.90 } = \sqrt{ 100.78 } = 10.04 $$

Though some students will continue to grow taller while at university, the _average_ relationship between height and year for all students will likely be close to zero. Centering a narrow $\beta$ prior at zero reflects this assumption.

The $\sigma$ prior assumes that 95% of heights will fall within 30cm of the mean height, which mimics the empirical distribution of height among adults.

<hr>

**4M5.** Now suppose I tell you that the average height in the first year was 120cm and that every student got taller each year. Does this information lead you to change your choice of priors? How?

This new information implies that our assumption about the students attending university is false: according to the [CDC Growth Charts](https://www.cdc.gov/growthcharts/cdc_charts.htm){:target="_blank"}, they're likely between five and nine years old! The new model updates the mean height and uses an exponential distribution to insure that the $\beta$ prior is not only positive but has an average value of 5cm, as estimated by the growth charts.

$$ \begin{align}
height_i &\sim Normal(\mu_i, \sigma) \\
\mu &= \alpha + \beta \cdot year_i \\
\alpha &\sim Normal(120, 10) \\
\beta &\sim Exponential(5) \\
\sigma &\sim Uniform(0, 15)
\end{align} $$

<hr>

**4M6.** Now suppose I tell you that the variance among heights for students of the same age is never more than 64cm. How does this lead you to revise your priors?

This new information allows us to update the $\sigma$ prior. Because the standard deviation is simply the square root of the variance ($\sqrt{64} = 8$), we can update the model accordingly.

$$ \begin{align}
height_i &\sim Normal(\mu_i, \sigma) \\
\mu &= \alpha + \beta \cdot year_i \\
\alpha &\sim Normal(120, 10) \\
\beta &\sim Exponential(5) \\
\sigma &\sim Uniform(0, 8)
\end{align} $$