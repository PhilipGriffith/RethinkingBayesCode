---
layout: page
title: "2. Small Worlds and Large Worlds"
date: 2000-12-27
use_math: true
---

# Hard.

**2H1.** Suppose there are two species of panda bear. Both are equally common in the wild and live in the same places. They look exactly alike and eat the same food, and there is yet no genetic assay capable of telling them apart. They differ however in their family sizes. Species A gives birth to twins 10% of the time, otherwise birthing a single infant. Species B births twins 20% of the time, otherwise birthing singleton infants. Assume these numbers are known with certainty, from many years of field research. Now suppose you are managing a captive panda breeding program. You have a new female panda of unknown species, and she has just given birth to twins. What is the probability that her next birth will also be twins?

We first need to compute the probability that our panda will have twins, then use that information to compute the probability that our panda will have twins again, _given_ that she's already had one set.

$$ Pr(twins) = Pr(twins \mid A) \cdot Pr(A) + Pr(twins \mid B) \cdot Pr(B) \tag{1} \label{1} $$

$$ Pr(A) = Pr(B) = 0.5 \tag{2} \label{2} $$

$$ Pr(twins \mid A) = 0.1 \tag{3} \label{3} $$

$$ Pr(twins \mid B) = 0.2 $$

$$ Pr(twins) = 0.1 \cdot 0.5 + 0.2 \cdot 0.5 = 0.15 $$

We can now update the probabilities that our panda is a member of species A or species B, given that she has had twins:

$$ Pr(A \mid twins) = \frac{Pr(twins \mid A) \cdot Pr(A)}{Pr(twins)} = \frac{0.1 \cdot 0.5}{0.15} = \frac{0.05}{0.15} = \frac13 \tag{4} \label{4} $$

$$ Pr(B \mid twins) = 1 - Pr(A \mid twins) = 1 - \frac13 = \frac23 $$

We can see that, after the birth of twins, we now believe our panda is twice as likely to be a member of species B than species A. We'll use these new estimates about her species membership to update the probability that she will have twins. Given $\eqref{1}$:

$$ \mathbf{ Pr(twins) = 0.1 \cdot \frac13 + 0.2 \cdot \frac23 = \frac16 } \tag{5} \label{5} $$

<hr>

**2H2.** Recall all the facts from the problem above. Now compute the probability that the panda we have is from species A, assuming we have observed only the first birth and that it was twins.

We computed this probability while solving 2H1. It is simply $\eqref{4}$:

$$ \mathbf{ Pr(A \mid twins) = \frac13 } $$

<hr>

**2H3.** Continuing on from the previous problem, suppose the same panda mother has a second birth and that it is not twins, but a singleton infant. Compute the posterior probability that this panda is species A.

We can compute this probability by using the information we learned in 2H1. The key is to use the probabilities computed _after_ observing our panda has had her first set of twins.

$$ Pr(A \mid singleton) = \frac{Pr(singleton \mid A) \cdot Pr(A)}{Pr(singleton)} $$

$$ Pr(singleton \mid A) = 1 - Pr(twins \mid A) = 1 - 0.1 = 0.9 \tag{$\mathit{v.s.}$ \ref{3}} $$

$$ Pr(A) = \frac13 = 0.\bar3 \tag{$\mathit{v.s.}$ \ref{4}} $$

$$ Pr(singleton) = 1 - Pr(twins) = 1 - \frac16 = \frac56 = 0.8\bar3 \tag{$\mathit{v.s.}$ \ref{5}} $$

$$ \mathbf{ Pr(A \mid singleton) = \frac{0.9 \cdot 0.\bar3}{0.8\bar3} = 0.36 } \tag{6} \label{6} $$

<hr>

**2H4.** A common boast of Bayesian statisticians is that Bayesian inference makes it easy to use all of the data, even if the data are of different types. So suppose now that a veterinarian comes along who has a new genetic test that she claims can identify the species of our mother panda. But the test, like all tests, is imperfect. This is the information you have about the test:

* -- The probability it correctly identifies a species A panda is 0.8.
<br>
* -- The probability it correctly identifies a species B panda is 0.65.

The vet administers the test to your panda and tells you that the test is positive for species A. First ignore your previous information from the births and compute the posterior probability that your panda is species A. Then redo your calculation, now using the birth data as well.

It will be helpful to compute a table to show the possible results of the veterinarian's test:

\begin{array}{c|c|c}
& \text{Test=A} & \text{Test=B} \\\
\hline
A & 0.8 & 0.2 \\\
B & 0.35 & 0.65 \\\
\end{array}

To complete the first part of the question, we can use our initial estimates about whether our panda is a member of species A or species B to compute the updated probability, given the results of the veterinarian test:

$$ Pr(A \mid Test=A) = \frac{Pr(Test=A \mid A) \cdot Pr(A)}{Pr(Test=A)} $$

$$ Pr(A) = 0.5 \tag{$\mathit{v.s.}$ \ref{2}} $$

$$ Pr(Test=A \mid A) = 0.8 $$

$$ Pr(Test=A) = Pr(Test=A \mid A) \cdot Pr(A) + Pr(Test=A \mid B) \cdot Pr(B) $$

$$ Pr(Test=A) = 0.8 \cdot 0.5 + 0.35 \cdot 0.5 = 0.4 + 0.175 = 0.575 $$

$$ \mathbf{ Pr(A \mid Test=A) = \frac{0.8 \cdot 0.5}{0.575} = \frac{0.4}{0.575} \approx 0.70 } $$

By including the information about our panda's births, we can gain a better estimate of her species membership. All we need to do is use the information we learned in 2H3. The key is to use the probabilities computed _after_ observing our panda has had twins and then a singleton.

$$ Pr(A) = 0.36 \tag{$\mathit{v.s.}$ \ref{6}} $$

$$ Pr(B) = 1 - Pr(A) = 1 - 0.36 = 0.64 $$

$$ Pr(Test=A) = 0.8 \cdot 0.36 + 0.35 \cdot 0.64 = 0.288 + 0.224 = 0.512 $$

$$ \mathbf{ Pr(A \mid Test=A) = \frac{0.8 \cdot 0.36}{0.512} = \frac{0.288}{0.512} = 0.5625 } $$