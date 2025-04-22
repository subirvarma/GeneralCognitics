---
layout: default
title: "Taming Randomness: The Story of Brownian Motion"
---

# Taming Randomness: The Story of Brownian Motion

## Introduction

![](https://subirvarma.github.io/GeneralCognitics/images/weiner1.png) 

Figure 1: Brownian Motion

In 1827 the Scottish botanist Robert Brown was peering through his microscope at minute particles of pollen suspended in a drop of water, when he noticed something strange. The pollen particles seemed to be moving about randomly, with no preferential direction. That being the age of Newtonian Mechanics, Brown looked for a force that might be causing the particles to move, but he couldn't find any that was visible. This phenomenon was named after him,and in fact most of us would have seen particles of dust dancing around in a beam of sunlight in a darkened room, which is also another example of Brownian Motion. 

The cause of the random motion remained a mystery until 1905, when the young Albert Einsten came up with a satifactory explanation in his very first published paper. Einstein theorized that the pollen particles where being pushed around by the molecules of water, which are too tiny to be seen under a microscope. At any point in time, there are slight imbalances in the number of water molecules extering pressure on the pollen grain in various directions, as a result of which it gets pushed in random directions as time goes on. Einstein also derived the average distance the particle moves in time $t$, which he showed was proportional to $\sqrt{t}$. In order to get these results Einstein utilized the newly discovered science of Statistical Mechanics, which is used to obtain laws that govern the Physics of a large assemblage of tiny particles. But in this case, we are not interested in the behavior of millions of particles acting together to create macroscopic quantities such as pressure, but in the motion of a single particle at a time, and this was something new to Physics. Unbeknownst to Einstein, Brownian Motion had already been analyzed five years earlier in the context of a model for the Stock Market.

### Two New Sciences

At the dawn of the 20th century, there were two new sciences that were launched. One of them of course, was Quantum Mechanics, that came into existence with Max Planck's 1901 paper on Black Body Radiation. The other less well known one, was the science of Random Processes, and this was launched in a PhD Thesis by the French mathematician Louis Bachelier, also around the same time. Quantum Mechanics of course went on the upend our ideas of Physics and reality in general, but what about Bachelier's discovery? This article is on precisely this topic.

The science of random events, or Probability Theory, was founded in the 17th century by the French mathematician and philosopher Blaise Pascal who wasn the first one assign numbers to notions such as the probability of winning at a game of chance. 
This was further developed in the 18th century, with the name most associated with it being the Swiss mathematician Jacob Bernoulli. Bernoulli initiated the idea of a repeated random trial, which was the first step towards the definition of a Random Process. For example if we toss a coin N times, he gave a formula for the probability that $n$ of those are heads and the remaining $N-n$ are tails, now called the Binomial Distribution. But what if we were to look at an infinite sequence of coin or dice tosses, this then becomes a (discrete valued) Random Process. 

![](https://subirvarma.github.io/GeneralCognitics/images/weiner4.png) 

Figure 2: Discrete Time Random Processes

An example of a discrete time random process is shown above, it is created by tossing a coin multiple times, with Heads represented by 1 and Tails by 0. 

![](https://subirvarma.github.io/GeneralCognitics/images/weiner2.png) 

Figure 3: Continuous Time Random Processes

Extending this further, what if the random quantity evolves continuously in time? This is a continuous time Random Process, and an example of this is shown the above figure. You can think of these graphs as being created by the Brownian Motion of a pollen particle whose movement is confined in one dimension to up and down motions along the y-axis, or the variation in the stock price for a company over time. Note that there are several curves shown in the figure, and each of them represents the evolution of the random process when starting from the origin  $t=0$. Each of these curves is a deterministic function of time, the randomness arises from the fact that we don't know in advance at $t=0$ which of these curves will actually result once the motion starts.

The analysis of such an object is exponentialy harder than the discrete time version. Consequently very little progress had been made in this area and part of the reason was that there was no connection made between Probability Theory and the rapidly developing methods in analysis that resulted in developments such as the Borel Measure and the Lebesgue Integral towards the end of the 19th century.

The major contribution that the 20th century made to the science of randomness, is precisely this connection, and it all started with Bachelier's work from 1900. Why was this important? It laid the science of Random Processes on a firm mathematical foundation, by connecting it with the rest of mathematical analysis. This process started with Bachelier, and was completed two decades later with Russian mathematician Andrei Kolmogorov's axiomization of Prabability Theory. This made it possible to talk about quantities that evolve randomly and continuously in time, which is precisely what a Random Process is. This has an interesting echo with Quantum Mechanics that also took about two decades two mature from Planck to Heisenberg and Schrodinger. 

Kiyosi Ito was a Japanese mathematician who made the next important advance in the theory of Brownian Motion. Working in wartime Tokyo during the 1940s, he came up with the idea of extending the idea of integration to the case when the integrand is Brownian Motion, and this is now called the Ito Integral in his honor. This idea was very influential since it allowed mathematicians to build more complex Random Processes by using Brownian Motion as a basic building block. This laid the foundation for several important applications of Random Processes that happened in the following decades.

But how important are these Random Processes? Well, the most famous example of a randomly evolving continuous time process is the stock market, and this is precisely what Bachelier studied in his 1900 paper. His work was essentially lost until the 1950s, when it came to the attention of the  eminent economist Paul Samuelson, who built on Ito's work and applied it to create a model for the Stock Market called the Logarithmic Brownian Motion.
Later in the 1960s Black and Scholes extended Samuelson's work to create a model for options trading. This resulted in a Partial Differential Equation named after them, whose solution is probably the most important mathematical result in use in Wall Street today. In fact I recently came acrosss a list of the most imprtant equations in science, and the Black-Scholes equation was listed along with others such as Maxwell Equations for electromagnetism and Schrodinger's Equation for the wave function.

Talk about Image Generation using BM

### The Weiner Process Model for Brownian Motion

Talk about random sums, and how they can be scaled to create BM.

Weiner's contribution

Image and Video generation using the Langevin Process.

- [ ] What is the most random thing possible?
- [ ] The drunkards walk
- [ ] Limiting case of the drunkards walk, becomes something that captures the essence of randomness in a form that is amenable to analysis ie the BM
- [ ] History of BM: Einstein, application to stock trading Bachelier, Weiner, KL expansion
- [ ] Diffusion processes 
- [ ] Modern applications: Black Scholes equation, image generation

### Historical Notes

- [ ] Bacheliers 1900 work on Stock Market models
- [ ] Einstein’s 1905 work on Brownian Motion.
- [ ] Weiner's work in the 1920s
- [ ] Ito's work in the 1940s
- [ ] Donsker's work in the 1950s

## The Weiner Process

- [ ] Introduce RVs
- [ ] Introduce random vectors and then discrete time random process
- [ ] Talk about law of large numbers
- [ ] Go on to continuous time random process
- [ ] Can we take an infinite sequence of random processes and scale them?
- [ ] Yes we can, and the result is the Weiner Process: Donsker's Theorem
- [ ] Properties of the Weiner Process

## Adding Randomness to Models

- [ ] Why is it important? A convenient way to add randomness to a model. WP is analytically tractable. 
- [ ] Applications: Stock Market, image generation, noise filtering
- [ ] Processes that can be modeled as signal plus noise
- [ ] Great interest in extracting the signal, the filtering problem, Kalman Filtering
- [ ] Processes that can be modeled as a function of a Random Process
- [ ] Example: Financial Derivatives
- [ ] Modeling the space of Latent Variables
- [ ] Example: Diffusion based Image Generation

## Stochastic Calculus

- [ ] Go through the signal + noise model, as per page 15 of Oksendal's book. How this naturally leads to the Ito Integral.
- [ ] dx/dt = Ax + B dW/dt equivalent to x = int(Ax dt) + int(B dW).  The latter is the Ito integral. 
- [ ] Rough derivation of the existence proof of the Ito Integral

### Functions of the Weiner Process and the Ito Formula

- [ ] Why is this important? Because we want to build models for random phenomena, and a convenient way to do this is by expressing them as functionals of the Weiner process. Y_t=f(W_t).
- [ ] How do we get an expression for Y_t?
- [ ] By using the Ito formula. This involves evaluating a stochastic integral. 
- [ ] Diffusion Processes and Stochastic differential equations 
- [ ] Start with Weiner process to Brownian motion to Ito diffusion to Ito process
- [ ] Some important functions: Langevin equation, exponential Ito Process

## Stock Market Models using Geometric WP

- [ ] Is there a signal or is it all noise
- [ ] Theory 1: it is all noise, the EMH
- [ ] Hedge funds: we beg to disagree. Look up book on finance by Korean economist. Test to check if market is a BM, Andrew Lo book.
- [ ] How to extract the signal 
- [ ] Temporary trends, non stationary processes 
- [ ] Stock market model, geometric WP, Samuelson. 
- [ ] Trading using WP
- [ ] The Black Scholes stochastic PDE  for options pricing
- [ ] Is it possible to find regularities in the randomness? Using deep learning to do prediction. 
- [ ] Mandelbrot and Nicholas Taleb: The Black Swan critique of Weiner Process based stock market models

## Image Generation using the Langevin Process

- [ ] Take an image and add noise to it, until it becomes completely random 
- [ ] Pixels jointly distributed as per Gaussian distribution in the Latent Space. 
- [ ] Train a NN to convert the LV from this space into an image 
- [ ] How is this even possible?
- [ ] The noise is actually a latent vector. By using the Langevin Process to add noise, we are constraining the Latent Space to obey the Gaussian Distribution.
- [ ] During training we are mapping LVs back to images
- [ ] Create new images by interpolating in the latent space
- [ ] Text to image conversion: Map text to a latent variable using a LLM, and then map the LV to an image.






      
