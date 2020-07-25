---
layout: page
title: "4. Linear Models"
date: 2000-12-22
---

# Overview

* 4.1 Why normal distributions are normal

	* 4.1.1 Normal by addition

	* 4.1.2 Normal by multiplication

	* 4.1.3 Normal by log-multiplication

	* 4.1.4 Using Gaussian distributions

		* 4.1.4.1 Ontological justification

		* 4.1.4.2 Epistemological justification

			* _Gaussian distribution_

			* 

* 4.2 A language for describing models

	* 4.2.1 Re-describing the globe tossing model

		* _From model definition to Bayes' theorem_

		* 

* 4.3 A Gaussian model of height

	* 4.3.1 The data

		* _Data frames_

		* _Index magic_

	* 4.3.2 The model

		* _Independent and identically distributed_

		* _A farewell to epsilon_

		* _Model definition to Bayes' theorem again_

		* 

	* 4.3.3 Grid approximation of the posterior distribution

	* 4.3.4 Sampling from the posterior

		* _Sample size and the normality of σ's posterior_

		* 

	* 4.3.5 Fitting the model with `map`

		* _Start values for `map`_

		* _How strong is a prior?_

		* 

	* 4.3.6 Sampling from a `map` fit

		* _Under the hood with multivariate sampling_

		* _Getting σ right_

		* 

* 4.4 Adding a predictor

	* _What is "regression"?_

	* 

	* 4.4.1 The linear model strategy

		* 4.4.1.1 Likelihood

		* 4.4.1.2 Linear model

			* _Nothing special or natural about linear models_

			* _Units and regression models_

			* 

		* 4.4.1.3 Priors

			* _What's the correct prior?_

			* 

	* 4.4.2 Fitting the model

		* _Everything that depends upon parameters has a posterior distribution_

		* _Embedding linear models_

		* 

	* 4.4.3 Interpreting the model fit

		* _What do parameters mean?_

		* 4.4.3.1 Tables of estimates

		* 4.4.3.2 Plotting posterior inference against the data

		* 4.4.3.3 Adding uncertainty around the mean

		* 4.4.3.4 Plotting regression intervals and contours

			* _Overconfident confidence intervals_

			* _How `link` works_

		* 4.4.3.5 Prediction intervals

			* _Two kinds of uncertainty_

			* _Rolling your own `sim`_

* 4.5 Polynomial regression

	* _Linear, additive, funky_

	* _Converting back to natural scale_

* 4.6 Summary