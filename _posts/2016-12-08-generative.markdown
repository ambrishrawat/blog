---
layout: post
title:  "Variational Inference: a high-level overview"
date:   2016-12-10 22:56:35 +0000
categories: 
comments: true
use_math: true
---
### Where does the story begin?

Every day, on numerous occasions, we tend to take decisions based on opinions. But this is not a point of dismay, becuase contrary to our speculation, reasoning with assumptions can be achieved within the elegance of just two guiding rules - the sum and product rule of probability theory. Assumptions, opinions, approximate knowledge or beliefs - they are merely placeholders when viewed through the mathematical construct of uncertainty. Uncertainty (or equivalently degree of belief) in the variability of $$x$$, is quantified as a real number through a function $$ p(x) $$, more formally defined as probability. This function, by virtue of Cox’s axioms must uphold the rules of probability theory, in particular, the sum and product rule.

Sum-rule: 

$$ P(AB) + P(\bar{A}|B) = 1 $$

Product-rule: 

$$ P(AB|C) = P(A|BC)P(BC) $$ 

### How does this play with ML or AI?

Uncertainty has an all-pervasive presence in a statistical model - from noise in the observations, to a model’s belief about its parameters, to uncertainty in model predictions, to our belief about the model itself. But with its explicit and faithful representation in Bayesian probability theory, one can reason with it in a principled way.

Most ML tasks can be conveniently (and crudely) summarised as follows - a model, accompanied with its explicit and necessary assumptions based on prior knowledge, is capable of making predictions and performing inference in the light of some observations. In this simplistic pipeline, it is easy to examine how uncertainty factors at every step of modelling.

**Uncertainty representation**: All the the believed uncertainties in the mathematical description of a model are stated via functional definitions - prior $$p(\theta\vert m)$$ , likelihood $$p(D\vert\theta,m)$$, noise processes, among other expressions. These functional expressions and implcit conditioning, capture different conceptions of uncertainties like parametric and structural uncertainties.

**Uncertainty propagation**: All the different kinds of uncertainties, implicit or explicit in an model should be propagated for decision-making (computing utilities for prediction or parameter-setting), which in general translates to prediction or inference. Mathematically, this involves the use of marginalisation principle (a direct application of sum and product rule). 

**Inference and Prediction**: The task of inference or learning boils down to squeezing prior uncertainties $$(p(\theta))$$, (often with respect to parameters, latent variables etc.) through the data, $$D$$, to posterior uncertainties $$p(\theta\vert D,m)$$ (following Bayes’ rule).

$$ \begin{align}
p(\theta|D,m) = \frac{p(D|\theta,m)p(\theta|m)}{p(D|m)} && p(D|m) = \int p(D|\theta,m)p(\theta|m)\mathrm{d}\theta
\end{align} $$

The normalisation constant, $$p(D\vert m)$$, is referred to as *Marginal Likelihood* or *Model Evidence*. At the level of conditioning on $$m$$, Bayesian model selection is naturally implemented as Occam’s Razor. Moreover, these updated uncertainties in the posterior can be sequentially propagated while making predictions about the unobserved (new data, $$ D^*$$).

$$ \begin{align}
p(D^*|D,m) &= \int p(D^*,\theta\vert D,m)\mathrm{d}\theta\\
           &= \int p(D^*\vert\theta,D,m) p(\theta\vert D,m) \mathrm{d}\theta
           &= \int p(D^*\vert\theta,m) p(\theta\vert D,m) \mathrm{d}\theta
\end{align}$$

### Logistics can be tricky

The elegance of first principles makes Bayesian reasoning extremely compelling. However, the theory merely guides on what-to-do and often fails on the how-to front. This latter one is where the practicality and feasibility are contested, or in other words computational and analytical intractability. And more often then what one would desire, these computations are intractable. Therefore, in practice a range of approximations are used. The inexpensive point estimates, being the most common ones where one settles for solutions from optimisation of maximum likelihood and maximum a posteriori. And then there are  deterministic approximations which harness structural understanding of the model like Variational mean field and Expectation Propagation.  Lastly, there are the computationally demanding but often asymptotically exact stochastic methods (like sampling).

### Common sense reduced to calculus. More calculus.

Variational Inference appends to the set of model assumptions, a parameterised approximate posterior ,$$q_{\lambda}(\theta)$$. Thus, it encourages you to search for the posterior in a constrained space of possible choices. A space constrained by the choice of paramteric form and, spanned by the range of variational parameters. More importantly, the choice of approximate posterior is not arbitrary. The theory proposes another guiding principle - choose a distribution that most similar the exact posterior of the original model. Similarity, here, being measured via  Kullback–Leibler divergence (KL-divergence), $$ \mathcal{D}_{KL}$$, which is defined as follows,

$$ \mathcal{D}_{KL}(q_{\lambda}(\theta)\vert\vert p(\theta\vert D,m)) \equiv \int q_{\lambda}(\theta)\log \frac{p(\theta\vert D,m)}{q(\theta)}\mathrm{d}\theta $$

Thus, the VI approach can be summaried as minimising

$$ q_{\lambda^*}(\theta) = \text{argmin}  \mathcal{D}_{KL}(q_{\lambda}(\theta)\vert\vert p(\theta\vert D,m))$$

Moreover, the obtained approximate-posterior can replace the exact posterior for any further practical compuatations, like  prediction,

$$ \begin{align}
&& q(D^*|D,m) = \int p(D^*\vert\theta,m) q_{\lambda^*}(\theta\vert D,m) \mathrm{d}\theta
\end{align} $$

The obvious point of contention here is, why this particular choice of similarity measure? And what are its qualitiative properties. 

#### Why this similarity measure?

This similarity measure naturally yields a lower bound for the marginal likelihood. A quantity, we would have maximised for during model selection. Thus, (hand-wavyly) we are assured that we are not very far from the 'best-model' search we had foresaken due to intractabilities. 

$$ \begin{align}
\mathcal{D}_{KL}(q_{\lambda}(\theta)\vert\vert p(\theta\vert D,m)) &\equiv \int q_{\lambda}(\theta)\log \frac{q_{\lambda}(\theta)}{p(\theta\vert D,m)}\mathrm{d}\theta\\
                 &= \int q_{\lambda}(\theta)\log \frac{q_{\lambda}(\theta)p(D\vert m)}{p(\theta, D\vert m)}\mathrm{d}\theta\\
                 &= \int q_{\lambda}(\theta)\log \frac{q_{\lambda}(\theta)}{p(\theta, D\vert m)}\mathrm{d}\theta + \int q_{\lambda}(\theta)\log p(D\vert m) \mathrm{d}\theta\\
                 &= \int q_{\lambda}(\theta)\log \frac{q_{\lambda}(\theta)}{p(\theta, D\vert m)}\mathrm{d}\theta + \log p(D\vert m)
\end{align} $$

equivalently,

$$ \log p(D\vert m) =   \int q_{\lambda}(\theta)\log \frac{p(\theta, D\vert m)}{q_{\lambda}(\theta)}\mathrm{d}\theta + {D}_{KL}(q_{\lambda}(\theta)\vert\vert p(\theta\vert D,m))$$

### Why use VI?

- It's grounding in statistical physics

Variational Inference is viserally gratifying because of its grounding in statiscal physics. The marginal-likelihood,$$\log p(D\vert m)$$, differs from the system's free-energy $$ \mathbb{E}_{q_{\lambda}(\theta)}[\log\frac{p(\theta, D\vert m)}{q_{\lambda}(\theta)}]$$, which in simplified form is the sum of energy and entropy $$\mathbb{E}_{q_{\lambda}(\theta)}[\log p(\theta, D\vert m)] + H(q)$$.

- Intergration simplified to optimisation

VI owes its popularity to reducing an intractable integral to an optimisation problem which involves derivative computations.

- It preserves the Bayesian modelling principles

With parametric and analytical form of approximate posterior, VI compromises the least on uncertainty representation. 

- It can be coupled or extended with other (mean-field) apprxoimations

Guding principles in VI don't mandate a particular choice of $$q_{\lambda}(\theta)$$. In principle, an optimal choice of q can be obtained within any family of distributions. One extended approximation which is known to go well wioth VI, is the mean-field approximation. 

### Why not use VI?

KL divergence is not symmetric. In fact, minimising the reverse-KL is the basis of another approximate inference scheme - Expectation Propagation. Due to a specific chocie of similarity measure, VI scheme doesn't guraantee that obtained approximate posterior will have desired properties.

- What are the qualitative propoerties of obtained $$q_{\lambda^*}(\theta)$$

In high-dimensional spaces and multi-modal exact posteriors, VI often fails. The choice of KL-divergence results can result in an approximate posterior where the the optimal apprxoimationm, $$q_{\lambda^*}(\theta)$$ distributes its mass in a counter-intuitive fashion. For instance, it could place a high-mass on regions where the orignal distribution had a low or zero mass. 

- Are all the uncertainties propagated?

As VI is often extended with a new layer of structure approximation like mean-field, it often fails to propagate uncertainties. 

