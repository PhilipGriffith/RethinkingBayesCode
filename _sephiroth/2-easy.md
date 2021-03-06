---
layout: page
title: "2. Small Worlds and Large Worlds"
date: 2000-12-29
use_math: true
---

# Easy.

For some of the questions below, we'll use the [Kolmogorov definition of conditional probability](https://en.wikipedia.org/wiki/Conditional_probability){:target="_blank"}:

$$ \frac{Pr(A, B)}{Pr(B)} = Pr(A \mid B) \tag{K} \label{K} $$

<hr>

**2E1.** Which of the expressions below correspond to the statement: _the probability of rain on Monday_?

* 1) Pr(rain)

	* _The probability of rain_.
^	
* 2) **Pr(rain \| Monday)**

	* _The probability of rain, given that it's Monday_.
^
* 3) Pr(Monday \| rain)

	* _The probability it's Monday, given that it's raining_.
^
* 4) $\mathbf{\frac{Pr(rain, \, Monday)}{Pr(Monday)}}$

	* By substituting the concepts for the variables in $\eqref{K}$, we get:
		* $\frac{Pr(rain, \, Monday)}{Pr(Monday)} = Pr(rain \mid Monday)$
	* We can now see that (4) is equivalent to (2).

<hr>

**2E2.** Which of the following statements corresponds to the expression: Pr(Monday \| rain)?

* 1) The probability of rain on Monday.

	* Pr(rain \| Monday).
^
* 2) The probability of rain, given that it is Monday.

	* This is equivalent to (1).
^
* 3) **The probability that it is Monday, given that it is raining.**

	* Pr(Monday \| rain).
^
* 4) The probability that it is Monday and that it is raining.

	* Pr(Monday, rain).

<hr>

**2E3.** Which of the expressions below correspond to the statement: _the probability that it is Monday, given that it is raining_?

* 1) **Pr(Monday \| rain)**

	* _The probability it's Monday, given that it's raining_.
^
* 2) Pr(rain \| Monday)

	* _The probability of rain, given that it's Monday_.
^
* 3) $Pr(rain \mid Monday) \cdot Pr(Monday)$

	* By rearranging $\eqref{K}$, we get:
		* $Pr(A \mid B) \cdot Pr(B) = Pr(A, B)$
	* By substituting the concepts for the variables, we get:
		* $Pr(rain \mid Monday) \cdot Pr(Monday) = Pr(rain, Monday)$
	* We can now see that (3) is _the probability that it's raining and that it's Monday_.	
^
* 4) $\mathbf{\frac{Pr(rain \mid Monday) \cdot Pr(Monday)}{Pr(rain)}}$

	* Given what we learned in (3), we know that:
		* $Pr(rain \mid Monday) \cdot Pr(Monday) = Pr(rain, Monday)$
	* And so we can simplify (4) through substitution and rearrange to get:
		* $\frac{Pr(rain, \, Monday)}{Pr(rain)} = \frac{Pr(Monday, \, rain)}{Pr(rain)}$
	* Given $\eqref{K}$, we know that:
		* $\frac{Pr(Monday, \, rain)}{Pr(rain)} = Pr(Monday \mid rain)$
	* We can now see that (4) is equivalent to (1).
^
* 5) $\frac{Pr(Monday \mid rain) \cdot Pr(rain)}{Pr(Monday)}$

	* This has the same structure as (4), but the concepts have switched places.
	* This implies that (5) is the opposite of (4): _the probability of rain, given that it's Monday_.

<hr>

**2E4.** The Bayesian statistician Bruno de Finetti (1906–1985) began his book on probability theory with the declaration: "PROBABILITY DOES NOT EXIST." The capitals appeared in the original, so I imagine de Finetti wanted us to shout this statement. What he meant is that probability is a device for describing uncertainty from the perspective of an observer with limited knowledge; it has no objective reality. Discuss the globe tossing example from the chapter, in light of this statement. What does it mean to say "the probability of water is 0.7"?

According to de Finetti, probability is nothing more than a subjective report by an observer regarding the strength of their belief that an event will occur: it is an epistemological notion, not a metaphysical one. Hence, to say "the probability of water on the globe is 0.7" is _not_ to say that, given numerous future globe tossing observations, approximately 70% of them will be water. Instead, it is to say that, given what I know about the globe, the method for generating observations about it, and the observations made so far, I am 70% sure that the next observation of tossing the globe will be water. In fact, I'd put my money where my mouth is and bet on those odds being true!

You can read more about subjective probability [here](https://plato.stanford.edu/archives/sum2003/entries/probability-interpret/#3.5){:target="_blank"}.