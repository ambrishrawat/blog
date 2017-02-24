---
layout: post
title:  "Exploring Gaussians"
date:   2017-02-23 22:56:35 +0000
categories: 
comments: true
use_math: true
---

## Where does the story begin?


In this note, I wish to explore Gaussians from the first principles of Bayesian reasoning. Most of this note is just a re-iteration of [] and [].

The centrality of Gaussians in probability theory sources from the Central Limit Theorem. They exhibit a multitude of desirable properties that accounts for all the paparazzi they attarct. In particular, the correspondence between sample moments, maximum likelihood estimates and sufficient stastics makes Gaussians or more generally the exponential family distributions makes them extremely interesting.

If you are faced with a Gaussian model for observations, one of the first tasks at hand is to estimate its parameters. To begin with, suppose a set of raw observations is available as a large collection of one-dimensional real numbers. 

**Observations**: }What does they look like? And what are some of their statistical properties?

**Model**: Visual inspection and sample statiscs provide reasonble motivation to model the observations as samples from a Gaussian distribution.

$$x_s \sim p(x;\mu,\sigma)$$

In particular each $$x_i$$ is a sample,

$$ p(x_i) = (2\pi \sigma^2)^{\frac{-1}{2}} exp(\frac{-(x_i-\mu)^2}{2\sigma^2}) $$

**Inference** For principled inference, we ofcourse wish to invoke the Bayes' rule as applied to posterior of the parameters, $$\theta = \{\mu,\sigma\}$$.

$$p(\theta|X,m) = \frac{p(X|\theta,m)p(\theta|m)}{p(X|m)}$$

Ideally, we could place any joint-prior on $$\mu$$ and $$\sigma$$ and application of Bayes' rule with result in an appropriate posterior distribution. The graphical model should therefore, in its general setting should be something like this,

If we seek an actual expression of a posterior, we need to be more specific about out choice of prior. For instance, we could rely on conjugacy. Let's look at a few simplified models first to motivate these conjugate priors. 

**Basic Model 1**: With $$\sigma_0$$ as a hyperamater (like $$\gamma$$ in the previous case). 



$$
\begin{align\*}
p(\mu|X,\sigma_0,\eta) & = \\
p(\mu|X,\sigma_0,\eta) & = 
\end{align\*} 
$$


**Basic Model 2**: With $$\mu_0$$ as a hyperamater. 


**Joint-prior Model 1**: With a joint prior on both $\mu$ and $\sigma$ (Normal-Gamma prior)





