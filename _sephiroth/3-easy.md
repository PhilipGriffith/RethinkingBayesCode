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

As in Chapter 2, we'll compute the grid approximation of the posterior distribution using this helper function written by the wonderful people at PyMC3:

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
{% endhighlight %}

We'll also use this helper function to visualize the results:

{% highlight python %}
def plot_interval(samples, left=0, right=1):
    fig, ax = plt.subplots()
    ax.axvspan(left, right, facecolor='grey', alpha=0.35)
    ax.hist(samples, bins=100)
    ax.set_xlim(0, 1)
    yt = list((str(int(i)) for i in ax.get_yticks()))
    yt[0] = None
    ax.set_yticklabels(yt)
    plt.xlabel('Probability of Water')
    plt.ylabel('Frequency')
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
plot_interval(samples, right=0)
{% endhighlight %}

[`Documentation for np.random.seed`](https://numpy.org/doc/stable/reference/random/generated/numpy.random.seed.html){:target="_blank"}
<br>
[`Documentation for np.random.choice`](https://numpy.org/doc/stable/reference/random/generated/numpy.random.choice.html){:target="_blank"}

![3E]({{ site.baseurl }}/assets/images/3e.png "3E")

<hr>

**3E1.** How much posterior probability lies below p = 0.2?

{% highlight python %}
np.mean(samples < 0.2)
plot_interval(samples, right=0.2)
{% endhighlight %}
[`Documentation for np.mean`](https://numpy.org/doc/stable/reference/generated/numpy.mean.html){:target="_blank"}

**<center>0.1% lies below 0.2</center>**

![3E1]({{ site.baseurl }}/assets/images/3e1.png "3E1")

<hr>

**3E2.** How much posterior probability lies above p = 0.8?

{% highlight python %}
np.mean(samples > 0.8)
plot_interval(samples, left=0.8)
{% endhighlight %}

**<center>11.9% lies above 0.8</center>**

![3E2]({{ site.baseurl }}/assets/images/3e2.png "3E2")

<hr>

**3E3.** How much posterior probability lies between p = 0.2 and p = 0.8?

{% highlight python %}
np.mean((samples > 0.2) & (samples < 0.8))
plot_interval(samples, left=0.2, right=0.8)
{% endhighlight %}

**<center>88% lies between 0.2 and 0.8</center>**

![3E3]({{ site.baseurl }}/assets/images/3e3.png "3E3")

<hr>

**3E4.** 20% of the posterior probability lies below which value of p?

{% highlight python %}
value = np.percentile(samples, 20)
plot_interval(samples, right=value)
{% endhighlight %}
[`Documentation for np.percentile`](https://numpy.org/doc/stable/reference/generated/numpy.percentile.html){:target="_blank"}

**<center>p = 0.522</center>**

![3E4]({{ site.baseurl }}/assets/images/3e4.png "3E4")

<hr>

**3E5.** 20% of the posterior probability lies above which value of p?

This is equivalent to asking the value of p that lies below 80%.

{% highlight python %}
value = np.percentile(samples, 100-20)
plot_interval(samples, left=value)
{% endhighlight %}

**<center>p = 0.758</center>**

![3E5]({{ site.baseurl }}/assets/images/3e5.png "3E5")

<hr>

**3E6.** Which values of p contain the narrowest interval equal to 66% of the posterior probability?

{% highlight python %}
values = az.hdi(samples, hdi_prob=0.66)
plot_interval(samples, left=values[0], right=values[1])
{% endhighlight %}
[`Documentation for az.hdi`](https://arviz-devs.github.io/arviz/generated/arviz.hdi.html){:target="_blank"}

**<center>p = [0.519, 0.782]</center>**

![3E6]({{ site.baseurl }}/assets/images/3e6.png "3E6")

<hr>

**3E7.** Which values of p contain 66% of the posterior probability, assuming equal posterior probability both below and above the interval?

If there is an equal posterior probability both below and above the interval, then the remaining intervals comprise the lowest and highest 17% of the posterior (17 + 66 + 17 = 100). We need to compute the interval between those two percentiles.

{% highlight python %}
values = np.percentile(samples, [17, 100-17])
plot_interval(samples, left=values[0], right=values[1])
{% endhighlight %}

**<center>p = [0.504, 0.774]</center>**

![3E7]({{ site.baseurl }}/assets/images/3e7.png "3E7")