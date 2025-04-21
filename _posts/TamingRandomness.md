---
layout: default
title: "Taming Randomness: The Story of Brownian Motion"
---

# Taming Randomness: The Story of Brownian Motion


## Introduction

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

## Adding Random Noise to Models

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
- [ ] Rough derivation of the Ito Integral

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






      
