---
layout: page
title: "3. Sampling the Imaginary"
date: 2000-12-25
---

# Easy

The code used to answer the questions below relies on these Python libraries:

{% highlight python %}
import numpy as np
import scipy.stats as stats
import matplotlib.pyplot as plt
import arviz as az

# I'm using this code to make plotting easy in a Jupyter notebook
%matplotlib inline
%config InlineBackend.figure_format = 'retina'
plt.style.use(['seaborn-colorblind', 'seaborn-darkgrid'])
{% endhighlight %}

As in Chapter 2, we'll compute and plot the grid approximation of the posterior distribution using these helper functions written by the wonderful people at PyMC3:

{% highlight python %}
def compute_grid_approximation(prior, success=6, tosses=9):
	"""
	Parameters:
		prior: np.array
			A distribution representing our state of knowledge
			before seeing the data. The number of items
			should be the same as the number of grid points.
		success: integer
			Number of successes.
			The default is 6.
		tosses: integer
			Number of tosses (i.e. successes + failures).
			The default is 9.
	Returns: 
		p_grid: np.array
			An evenly-spaced parameter grid between 0 and 1.
		posterior: np.array
			The posterior distribution.
	"""
	# First, define the parameter grid
	p_grid = np.linspace(0, 1, prior.shape[0])
	# Then compute the likelihood at each point in the grid
	likelihood = stats.binom.pmf(success, tosses, p_grid)
	# Compute the product of the likelihood and the prior
	unstd_posterior = likelihood * prior
	# Finally, standardize the posterior so that it sums to 1
	posterior = unstd_posterior / unstd_posterior.sum()

	return p_grid, posterior, success, tosses

def plot_grid_approximation(p_grid, posterior, success, tosses, x_label):
    """
    This function plots a grid approximation of the posterior distribution.
    """
    plt.plot(p_grid, posterior, 'o-', label=f'Success = {success}\nTosses = {tosses}')
    plt.xlabel(x_label)
    plt.ylabel('Posterior Probability')
    plt.legend(loc=0)
{% endhighlight %}

The questions below rely on a set of samples specified in the R code 3.27 box found on p. 69 of _Statistical Rethinking_. We'll generate the samples using the following code:

{% highlight python %}
# Setting a random seed allows the results to be reproducible
np.random.seed(3)
size = 1000
# Create a prior distribution of 1000 1's
# This will also create a posterior distribution with 1000 points
prior = np.ones(size)
pg, po, s, t = compute_grid_approximation(prior, success=6, tosses=9)
# Take 1000 samples (with replacement) from the posterior
# The posterior provides the probability for each value in the parameter grid
samples = np.random.choice(pg, p=po, size=size, replace=True)
{% endhighlight %}

[`Documentation for np.random.seed`](https://numpy.org/doc/stable/reference/random/generated/numpy.random.seed.html){:target="_blank"}
<br>
[`Documentation for np.random.choice`](https://numpy.org/doc/stable/reference/random/generated/numpy.random.choice.html){:target="_blank"}

<hr>

**3E1.** How much posterior probability lies below p = 0.2?

{% highlight python %}
np.mean(samples < 0.2)
{% endhighlight %}
[`Documentation for np.mean`](https://numpy.org/doc/stable/reference/generated/numpy.mean.html){:target="_blank"}

**p = 0.001**

<hr>

**3E2.** How much posterior probability lies above p = 0.8?

{% highlight python %}
np.mean(samples > 0.8)
{% endhighlight %}

**p = 0.119**

<hr>

**3E3.** How much posterior probability lies between p = 0.2 and p = 0.8?

{% highlight python %}
np.mean((samples > 0.2) & (samples < 0.8))
{% endhighlight %}

**p = 0.88**

<hr>

**3E4.** 20% of the posterior probability lies below which value of p?

{% highlight python %}
np.percentile(samples, 20)
{% endhighlight %}
[`Documentation for np.percentile`](https://numpy.org/doc/stable/reference/generated/numpy.percentile.html){:target="_blank"}

**p = 0.522**

<hr>

**3E5.** 20% of the posterior probability lies above which value of p?

This is equivalent to asking the value of p that lies below 80%.

{% highlight python %}
np.percentile(samples, 80)
{% endhighlight %}

**p = 0.758**

<hr>

**3E6.** Which values of p contain the narrowest interval equal to 66% of the posterior probability?

{% highlight python %}
az.hdi(samples, hdi_prob=0.66)
{% endhighlight %}
[`Documentation for az.hdi`](https://arviz-devs.github.io/arviz/generated/arviz.hdi.html){:target="_blank"}

**p = [0.519, 0.782]**

<hr>

**3E7.** Which values of p contain 66% of the posterior probability, assuming equal posterior probability both below and above the interval?

If there is an equal posterior probability both below and above the interval, then the remaining intervals comprise the lowest and highest 17% of the posterior. We need to compute the interval between those two percentiles.

{% highlight python %}
np.percentile(samples, [17, 83])
{% endhighlight %}

**p = [0.504, 0.774]**