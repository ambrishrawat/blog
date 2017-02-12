---
layout: post
title:  "Create to understand"
date:   2017-02-07 22:56:35 +0000
categories: 
comments: true
use_math: true
---

## Where does the story begin?

Generative modelling is one of the most fascinating paradigms of AI. And its story begins at observations of what we perceive as *phenomena*. Colloquially, we associate the word phenomenon with an object, when that object is believed to exist. Furthermore, it exists because it got created. Often, in order to understand such a phenomemnon and its subsequent evolution, we attempt to recreate or mimic its underlying processes. For instance, the phenomenon of light. Through few centuries of reserch explorations, with experimental and theoretical conjecturing of laws of physics, we now have a *generative model* for understanding light. Similarly, the generative paradigm of AI imparts understanding to an AI agent if it succeeds in mimicing a phenomenon. 

Let's say an AI agent is faced with the following observation - an image of a bird. Depending on its response we would impart different degree of intelligence to it. 

- (Of the choices I had,) I know this is a bird.

With traditional discriminatively strategies I would be rather dubious about the whole notion of intelligence. There were limited choices and the agent was made to pick one. The hestiation to ascribe intelligence sources from cross-questioning. What's the confidence of this choice? What's the limit of agent's capacity (any unseen images? imagge of objcets it previously did't know of? or beyond) How did the agent arrive at its decision?

In short, if the agent discards more options in arriving at a decision, and gives confidence measuress on its decision, then perhaps it is more intelligent. Mathematically, this could involve discrinimating in high-dimensionlal spaces, or regressing to continous space. From an approximate reasoning perspective, this could involves choosing better priors. These could be explicit priors by incorporating appropriate relaxations or smoothening assumtioptions or implicit ones theough more data and better model defintions. 

- Another image of a bird. 

Suppose an agent responded with an image. Since it succeeded in mimcing the phenomenon, it can be intuitively expected to showcase better intelligent behaviour. One such phenomemon where AI has had tremendous success is natural speech. AI claims to 'understand' spoken speech through its recreation. It achieves this via a surgical analysis of how elemental forms like sound waves, phonemes, words and sentences are strung together in its coherent synthesis.

- Birds have feathers and wings. So does the animal in this picture. Hence, perhaps this is a bird.

The third leg of intelligence lies in the agents capacity to reason. This is highly intricate as a generalised model. However simplified versions of this are attainable through hybrid approaches of generative and discriminative modelling. Most deployed AI systems are minaturised versions of reasoning machines designed for specific tasks.

## The classical origins}

The overall objective of generative modelling can be summarised as writing a model $G$, such that one can sample $x_s$ from this model.

$$ x_s \sim G(\theta)$$

### Sampling from distributions

This $G$ often takes the form of a distribution. In data science, often a kneejerk reaction to a large set of real numbers is computing their mean and variance. Although mathematically grounded, implicit to this computation is a notion of existence. It is believed that there exists a 'true' distribution from which the numbers were generated. In such cases, when $G$ is a distribution, generative modelling can be summarised as modelling for $p$, where,

$$x_s \sim p(x;\theta)$$

Once the parameters have been inferred, this model has various use cases. First, it can be used to sample new observations. And second, it allows us to compute predictive-likelihood for any new observations. 

### Inference in Generative models

Principled inference in these models can be arbitrarily hard. In fact, complexities start popping in even for the favourites like Gaussians. In practice, we tend to take MLE estimates as substitues for sufficient statistics of distributions of exponential family. However, if were to embark on the principled Bayesian approach, the journey is not that jolly. But with appropriate conjugate priors one can get significant distance.

### Implicit generative models

Prescribing a probabilistic model is not the only way to generate observations. When extensive physical mechanisms are known to govern a phenomenon, complex stochastic procedures can be written to directly generate observations. These implicit generative model are common approaches in climate, genetics and other physical systems. Inference methods used in these systems are clubbed under Approximate Bayesian Computation. Implicit models have garnered considerable traction with the introduction of Generative Adversarial Networks, which create instance by merely observing. In particular, they have been extremely successful in creating natural images without any mechanistic specification for creation og image-phenomenon.

### How to validate model-efficacy?

A central concern to generative modelling is in validation of their efficiay. Why do its samples make sense? If the model is explicilt probabilistic, one could compute density estimates on the generated samples. This is non trivial and the doors only lead to echo chambers. The samples could be made sense of if there is a metric available for comparison. Again, for high dimensional spaces, this is not the case. 

In this blog, I have attempted to entertain different paradigms and recent research advances under the umbrella of generative modelling. I plan to expand on the nuances through later blogs.