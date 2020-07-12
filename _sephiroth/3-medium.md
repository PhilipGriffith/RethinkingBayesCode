---
layout: page
title: "3. Sampling the Imaginary"
date: 2000-12-24
---

# Medium

**3M1.** Suppose the globe tossing data had turned out to be 8 water in 15 tosses. Construct the posterior distribution, using grid approximation. Use the same flat prior as before.

<hr>

**3M2.** Draw 10,000 samples from the grid approximation from above. Then use the samples to calculate the 90% HPDI for p.

<hr>

**3M3.** Construct a posterior predictive check for this model and data. This means simulate the distribution of samples, averaging over the posterior uncertainty in p. What is the probability of observing 8 water in 15 tosses?

<hr>

**3M4.** Using the posterior distribution constructed from the new (8/15) data, now calculate the probability of observing 6 water in 9 tosses.

<hr>

**3M5.** Start over at 3M1, but now use a prior that is zero below p = 0.5 and a constant above p = 0.5. This corresponds to prior information that a majority of the Earth’s surface is water. Repeat each problem above and compare the inferences. What difference does the better prior make? If it helps, compare inferences (using both priors) to the true value p = 0.7.