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
\begin{align*}
\text{posterior: } &p(\mu|X,\sigma_0,\eta) = \mathcal{N}(\mu|\mu_n,\sigma_n^2), \quad \mu_n = \frac{\frac{1}{\sigma_0^2}\sum_{x \in X} x + \frac{\eta_\mu}{\eta_\sigma^2}}{\frac{1}{\eta_\sigma^2} + \frac{n}{\sigma_0^2}} \quad \sigma_n^2 = \frac{1}{\frac{1}{\eta_\sigma^2} + \frac{n}{\sigma_0^2}}\\
\text{predictive distribution: } & p(x^*|X,\sigma_0,\eta) = \mathcal{N}(x^*|\mu_n,\sigma_n^2+\sigma_0^2), \quad \mu_n = \frac{\frac{1}{\sigma_0^2}\sum_{x \in X} x + \frac{\eta_\mu}{\alpha_\sigma^2}}{\frac{1}{\eta_\sigma^2} + \frac{n}{\sigma_0^2}} \quad \sigma_n^2 = \frac{1}{\frac{1}{\eta_\sigma^2} + \frac{n}{\sigma_0^2}}
\end{align*} 
$$


**Basic Model 2**: With $$\mu_0$$ as a hyperamater. 

$$
\begin{align*}
\text{posterior: } &p(\sigma^2|X,\mu_0,\beta) = \text{IG}(\sigma^2|\alpha_n,\beta_n), \quad \alpha_n = \zeta_\alpha + \frac{n}{2} \quad \beta_n = \zeta_\beta + \frac{1}{2}\sum_{x\in X}(x-\mu_0)\\
\text{predictive distribution: } & p(x^*|X,\mu_0,\zeta) = \frac{\Gamma(\zeta_\alpha + \frac{1}{2})}{\Gamma(\zeta_\alpha)} \frac{1}{(2\pi\zeta_\beta)^{\frac{1}{2}}}\frac{1}{\big(1+\frac{1}{2\zeta_\beta}(x^*-\mu_0)^2\big)^{\zeta_\alpha+\frac{1}{2}}}
\end{align*} 
$$

**Joint-prior Model 1**: With a joint prior on both $\mu$ and $\sigma$ (Normal-Gamma prior)


$$
\begin{align*}
\text{posterior: } &p(\mu,\sigma^2|X,\gamma) = \text{NIG}(\mu,\sigma^2|\mu_n,\kappa_n,\alpha_n,\beta_n)\\
& \mu_n = \frac{\gamma_\kappa\gamma_\mu + \sum_{x \in X}x}{\frac{1}{\gamma_\kappa}+n}\\
& \frac{1}{\kappa_n} = \frac{1}{\gamma_\kappa} + n, \\
& \alpha_n = \gamma_\alpha + \frac{n}{2}\\
& \beta_n = \gamma_\beta + \frac{1}{2}\Big(\gamma_\mu^2\gamma_\kappa + \sum_{x\in X}(x-\mu_n^2\kappa_n)\Big)\\
\text{predictive distribution: } & \text{this is \textit{pending}}
\end{align*}
$$


