---
layout: post
title:  "Create to understand"
date:   2016-12-08 22:56:35 +0000
categories: 
comments: false
use_math: true
---

## Where does the story begin?

Generative modelling is one of the most fascinating paradigms of AI. And its story begins at observations of what we perceive as *phenomena*. Colloquially, the word phenomenon is associated with an object, when that object is believed to exist. Furthermore, it exists because it got created. Often, in order to understand such a phenomemnon and its subsequent evolution, we attempt to recreate or mimic its underlying generative process. For instance, consider the phenomenon of light. Through nmuerous monumental research explorations, some experimental and some conjectured or argued through laws of physics, we now have a have *generative model* of light.

The generative paradigm of AI contests to impart understanding to an AI agent in the similar way. One such phenomemon that AI has been successfull at mimicing is natural speech. AI claims to 'understand' spoken speech through its recreation. It achieves this via a surgical analysis of how elemental forms like sound waves, phonemes, words and sentences are strung together in its coherent synthesis.

### A classical generator

Often my kneejerk reaction when faced with a large sequence of real numbers is computing some statistical properties like mean and variance. Although mathemtically grounded in law of large numbers, implicit to this computation is a notion of existence. I like to believe that there exists a 'true' distribution from which the numbers were generated. In fact, by matching the sample moments to the moments of my believed distribution, I am able to script a generator that can sample other similar numbers. These random-samplers used in various programming languages are a classical examples of generative models. With chained applications of product-rule and sum-rule, these basic generators can be further combined to represent other more complex distributions. 

Let's say we were to write generative process that could have led to $$N$$ observations, $$\{x_i\}^N_1$$. 
- If $$x$$ was a one-dimensionl entity, traditional distributions offer a reliable starting point. A large family of distributions are available, spanning both discrerte and continuous random variables.
- Multi-modality - 
- However, things can be complex as distrubtions become highly multi-modal . Moreover, there is also a challenging task is in verifying if the generated samples even make sense. 
One reliable way to validate the sample-generation process, is by estimating the density of generated samples. But there are situations when this is infeasible. There are two interesting approaches to when the generative process is intricate and  which I wish to look a closer look at.

### The a b c of simulation models

Complex phenomenon like weather, brain, genetics or the Big-Bang have been studied by humans for centuries. Their mysteriousness rarely fails to strike a chord with our curiosity. While studying these phenomenon, we often simulate their involved dynamics through large complex computer-programs. Moreover, these phenomenon also have the added baggage of complex measurements. Big Bang for instance hass everything in our -- as its measurement.

For such phenomemnon, where we have one large observation $$Y$$ or its summary statistic $$y_{sum}$$. 

### Generating by merely observing

Phenomemon of natural images. 

#### Generative Adversarial Networks

predicting without observing

#### Variational Autoencoders


