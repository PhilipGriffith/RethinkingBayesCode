---
layout: page
title: "4. Linear Models"
date: 2000-12-19
use_math: true
---

# Hard.

**4H1.** The weights listed below were recorded in the !Kung census, but heights were not recorded for these individuals. Provide predicted heights and 89% intervals (either HPDI or PI) for each of these individuals. That is, fill in the table below, using model-based predictions.

\begin{array}{c|c|c|c}
\text{Individual} & \text{weight} & \text{expected height} & \text{89% interval} \\\
\hline
1 & 46.95 & & \\\
2 & 43.72 & & \\\
3 & 64.78 & & \\\
4 & 32.59 & & \\\
5 & 54.63 & & \\\
\end{array}

<hr>

**4H2.** Select out all the rows in the `Howell1` data with ages below 18 years of age. If you do it right, you should end up with a new data frame with 192 rows in it.

(a) Fit a linear regression to these data, using `map`. Present and interpret the estimates. For every 10 units of increase in weight, how much taller does the model predict a child gets?

(b) Plot the raw data, with height on the vertical axis and weight on the horizontal axis. Superimpose the MAP regression line and 89% HPDI for the mean. Also superimpose the 89% interval for predicted heights.

(c) What aspects of the model fit concern you? Describe the kinds of assumptions you would change, if any, to improve the model. You don’t have to write any new code. Just explain what the model appears to be doing a bad job of, and what you hypothesize would be a better model.

<hr>

**4H3.** Suppose a colleague of yours, who works on allometry, glances at the practice problems just above. Your colleague exclaims, “That’s silly. Everyone knows that it’s only the _logarithm_ of body weight that scales with height!” Let’s take your colleague’s advice and see what happens.

(a) Model the relationship between height (cm) and the natural logarithm of weight (log-kg). Use the entire `Howell1` data frame, all 544 rows, adults and non-adults. Fit this model, using quadratic approximation:

$$\begin{align}
h_i &\sim Normal(\mu_i, \sigma) \\
\mu_i &= \alpha + \beta \, log(w_i) \\
\alpha &\sim Normal(178, 100) \\
\beta &\sim Normal(0, 100) \\
\sigma &\sim Uniform(0, 50)
\end{align}$$

where $h_i$ is the height of individual _i_ and $w_i$ is the weight (in kg) of individual _i_. The function for computing a natural log in R is just `log`. Can you interpret the resulting estimates?

(b) Begin with this plot:

{% highlight r %}
plot( height ~ weight , data=Howell1 , col=col.alpha(rangi2,0.4) )
{% endhighlight %}

Then use samples from the quadratic approximate posterior of the model in (a) to superimpose on the plot: (1) the predicted mean height as a function of weight, (2) the 97% HPDI for the mean, and
(3) the 97% HPDI for predicted heights.