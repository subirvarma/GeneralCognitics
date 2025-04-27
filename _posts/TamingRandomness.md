---
layout: default
title: "Encounters with Randomness: The Story of Brownian Motion"
---

# Encounters with Randomness: The Story of Brownian Motion

## Introduction

![](https://subirvarma.github.io/GeneralCognitics/images/weiner1.png) 

Figure 1: Brownian Motion

In 1827 the Scottish botanist Robert Brown was peering through his microscope at minute particles of pollen suspended in a drop of water, when he noticed something strange. The pollen particles seemed to be moving about randomly, with no preferential direction. That being the age of Newtonian Mechanics, Brown looked for a force that might be causing the particles to move, but he couldn't find any that was visible. This phenomenon was named after him, and in fact most of us have seen particles of dust dancing around in a beam of sunlight in a darkened room, which is another example of Brownian Motion. 

The cause of the random motion remained a mystery until 1905, when the young Albert Einsten came up with a satisfactory explanation in his very first published paper. Einstein theorized that the pollen particles where being pushed around by the molecules of water, which are too tiny to be seen under a microscope. At any point in time, there are slight imbalances in the number of water molecules extering pressure on the pollen grain in various directions, as a result of which it gets pushed in random directions as time goes on. Einstein also derived the average distance the particle moves in time $t$, which he showed was proportional to $\sqrt{t}$. In order to get these results Einstein utilized the then newly discovered science of Statistical Mechanics, which is used to obtain laws that govern the Physics of a large assemblage of tiny particles. But in this case, we are not interested in the behavior of millions of particles acting together to create macroscopic quantities such as pressure, but in the random motion of a single particle at a time, and this was something new to Physics. Unbeknownst to Einstein, Brownian Motion had already been analyzed five years earlier by Louis Bachelier in the context of a model for the stock market.

### Two New Sciences

At the dawn of the 20th century, there were two new sciences that were launched. One of them of course, was Quantum Mechanics, that came into existence with Max Planck's 1901 paper on Black Body Radiation. The other less well known one, was the science of Random Processes, and this was launched in a PhD Thesis by the French mathematician Louis Bachelier, also around the same time. Quantum Mechanics of course went on the upend our ideas of Physics and reality in general, but what about Bachelier's discovery? This article is on precisely this topic.

The science of random events, or Probability Theory, was founded in the 17th century by the French mathematician and philosopher Blaise Pascal who was the first one assign numbers to notions such as the probability of winning at a game of chance. 
This was further developed in the 18th century, with the name most associated with it being the Swiss mathematician Jacob Bernoulli. Bernoulli initiated the idea of a repeated random trial, which was the first step towards the definition of a Random Process. For example if we toss a coin N times, he gave a formula for the probability that $n$ of those are heads and the remaining $N-n$ are tails, now called the Binomial Distribution. 

![](https://subirvarma.github.io/GeneralCognitics/images/weiner4.png) 

Figure 2: Discrete Time Random Processes

But what if we were to look at an infinite sequence of coin tosses, this then becomes a (discrete valued) Random Process. An example of such a random process is shown above, it is created by tossing a coin multiple times, with Heads represented by 1 and Tails by 0. 

![](https://subirvarma.github.io/GeneralCognitics/images/weiner2.png) 

Figure 3: Continuous Time Random Processes

Extending this idea further, what if the random quantity evolves continuously in time? This then becomes a continuous time Random Process, and an example of this is shown the above figure. You can think of these graphs as being created by the Brownian Motion of a pollen particle whose movement is confined to just one dimension, either up or down along the y-axis, or the variation in the stock price for a company over time. Note that there are several curves shown in the figure, and each of them represents a possible evolution of the random process when starting from the origin  $t=0$, also called a sample path. These sample paths constitutes the different outcomes in time for the Random Process and just as we assign a probability to an individual event, for example getting a Heads whena when tossing a coin, we now assign a probability to the entire sample path as a whole. 

The analysis of a continuous time Random Process is exponentialy harder than the discrete time version since the set of possible outcomes is the space of continuous functions which is very hard to analyze. Consequently very little progress had been made in this area by 1900 and part of the reason was that there was no connection made between Probability Theory and the rapidly developing methods in analysis that had resulted in developments such as the Borel Measure and the Lebesgue Integral towards the end of the 19th century.
The major contribution that the 20th century made to the science of randomness, is precisely this connection. It laid the science of Random Processes on a firm mathematical foundation, by connecting it with the rest of mathematical analysis. This process started with Bachelier, and was completed two decades later with great Russian mathematician Andrei Kolmogorov's axiomatization of Probability Theory which made it possible to talk about quantities that evolve randomly and continuously in time, which is precisely what a Random Process is. This has an interesting echo with Quantum Mechanics that also took about two decades two mature from Planck to Heisenberg and Schrodinger. 

Kiyosi Ito was a Japanese mathematician who made the next important advance in the theory of Random Processes. Working in wartime Tokyo during the 1940s, he came up with the idea of extending the idea of the integral to the case when the integration is done with respect to Brownian Motion, and this is now called the Ito Integral in his honor. I found this to be a totally mind blowing concept when I first learnt about in grad school in the late 1980s, and even today I consider it a privilage that I understand what it means.
This idea was very influential since it allowed mathematicians to build more complex Random Processes by using Brownian Motion as a basic building block. This laid the foundation for several important applications of Random Processes that happened in the following decades.

But how important are these Random Processes? Well, the most famous example of a randomly evolving continuous time process is the stock market, and this is precisely what Bachelier studied in his 1900 paper. His work was essentially lost until the 1950s, when it came to the attention of the  eminent economist Paul Samuelson, who built on Ito's work and applied it to create a model for the stock market called the Logarithmic Brownian Motion.
Later in the 1960s the economists Fischer Black and Myron Scholes extended Ito and Samuelson's theories to create a model for stock options trading. This resulted in a Partial Differential Equation named after them, whose solution is probably the most important mathematical result in use in Wall Street trading today. In fact I recently came acrosss a list of the most imprtant equations in science, and the Black-Scholes equation was listed along with others such as Maxwell Equations for electromagnetism and Schrodinger's Equation for the quantum wave function.

![](https://subirvarma.github.io/GeneralCognitics/images/weiner6.png) 

Figure 6: Signals in Noise

Brownian Motion has evolved into a powerful tool for modeling random phenomena. Whenever the need arises to capture the randomness that exists in fields such as communications system or electrical circuits, Brownian Motion is the go-to model that engineers use. An example of a deterministic signal subject to random noise is shown in the above figure. The clean signal is transmitted, while the noise is added during the course of transmisssion over a communications channel. The Filtering Problem looks at ways in which the signal can be extracted from the noise which is usually modeled as a Brownian Motion. Norbert Weiner (more about him in the next section) and Richard Kalman are names associated with the solution to the filtering problem.

![](https://subirvarma.github.io/GeneralCognitics/images/weiner7.png) 

Figure 6: Training a Neural Network to generate images

But the most interesting, and surprising, application of Brownian Motion has happened during the last decade, when it was used to create a Neural Network model that can generate realistic images and videos. This model ouperformed all competing methods, and it has become the most prevalent image/vdeo generation model in use today. This topic is treated in greater detail later, but a rough idea of how it done can be seen in the above figure. The top row shows the process of adding incremental random numbers to an image, until it becomes indistinguishable from noise. The bottom row trains the Neural Network by learning how to recover the original image from noise. Once the network is trained, it can generate new images by starting from a noise sample.

## From Brownian Motion to the Weiner Process

There was one name that I didn't mentioned in my brief survey of mathematicians who have contributed to the theory of the Brownian Motion, and it is that of Norbert Weiner. This is quite a big omission since the terms Brownian Motion and Weiner Process are often used inter-changeably. Strictly speaking Brownian Motion is the physical phenomenon that Robert Brown discovered and Einstein analyzed, while the Weiner Process is a mathematical model for it and this is the terminology that I will use in the rest of this article. Norbert Weiner was the first one to do a rigorous mathematical analysis of Brownian Motion in the early 1920s, and abstracted it to create the mathematical notion of a Weiner Process. He proved several important properties for it, such as the fact that its sample paths are continuous in time, while at the same time its derivative does not exist anywhere.
Weiner was a child prodigy who got his PhD from Harvard at age 19 and spent his career teaching at MIT. His work spanned mathematics, both pure and applied, as well philosophy and towards the latter part of his life what we call Artificial Intelligence (he called it Cybernetics). He contributed more than anyone else to the emerging field of Signal Processing, and was a big influence on the later work of Claude Shannon and John von Neummann.

The theory of a random process in continuous time was not sufficiently well developed when Weiner was working on the problem in the early 1920s, and had to wait for Kolmogorov's axiomitization of Probability Theory ten years later. During the 1950s Monroe Donsker gave a highly intuitive explanation of how the Weiner Process arises as a limiting case of simpler Random Processes, and this is what I am going to describe in this section.

![](https://subirvarma.github.io/GeneralCognitics/images/weiner9.png) 

Figure: Outcome of a Coin Tossing Experiment

Lets start with a very simple process, that of tossing a coin. Let the Random Variable $X_n$ be the result of the $n^{th}$ toss, and assign $X_n =  1$ if the result is a Heads and $-1$ to Tails. Define $S_n$ to be the Random Sum given by

$$ S_n = X_1 + X_2 + ...+ X_n $$

If we interpolate linearly between successive values of $S_n$, then it results in the continuous valued Random Process shown in the above figure.
The figure shows one possible sample path that results from the tosse sequence $THHTHT$. This process is known as a Random Walk and it has the interesting property that once we know the value of $S_n$, the future evolution of the process is completely independent of what happened prior to the $n^{th}$ toss. These type of processes, in which the the future is independent of the past given the present, form an important category called Markov Processes and the Weiner Process also belongs to this. 

So we have a continuous time process that seems to be moving about randomly, but it is not quite a Brownian Motion yet. 
How can we go about creating a model for Brownian Motion? First of all we need to introduce time as a variable. Also compared to the Random Sum, Brownian Motion exhibits much faster changes in direction, and also successive changes happen much quicker in time. One way to accomplish all these goals is by doing the following:

- Scale the Random Sums by ${1\over{\sqrt{n}}}$ so that as $n$ increases, the jumps in the $S_n$ values become smaller, i.e., the particle covers smaller and smaller distances before it changes direction.
- In order to introduce a time dependence, restrict the Random Walk to the time interval interval $[0,1]$ such that changes in the Random Sum occur at at the $n$ time instants given by ${1\over n}, {2\over n},...,{n-1\over n}, 1$
- Define a random function $W_n(t), 0\le t\le 1$ such that it is equal to the scaled sum ${S_i\over{\sqrt n}}$ at the point ${i\over n}$ and then interpolate between successive sums to create a continuous function over $0\le t\le 1$ whose value at time $t$ is given by:

$$ W^n(t) = {S_{i-1}\over{\sqrt{n}}} + \left[{t - {(i-1)\over n}\over{1\over n}}\right] {1\over{\sqrt{n}}} X_i\ \ \ for\ \ \
t\in \left[{i-1\over n}, {i\over n}\right]$$

![](https://subirvarma.github.io/GeneralCognitics/images/weiner10.png) 

Figure: Scaled and Interpolated Random Sums over $0\le t\le 1$ for n = 100 (blue), n = 400 (red) and n = 10000 (green)

The figure above three different sample paths for $W_n(t)$ over the interval $[0,1]$, with the gap between successive changes in direction becoming smaller and smaller as $n$ increases. As $n\rightarrow\infty$, Donsker's Theorem says that $W_n(t), 0\le t\le 1$ converges to a Weiner Process. What does it mean to take the limit $n\uparrow\infty$ for the interpolated Random Sums? Since we are constrained to be in the interval $[0,1]$, it means that successive coin tosses are happening faster and faster, and in the limit they are being done over the continuum. Since each coin toss results in a change of direction for $W_n(t)$, it follows that in the limit, the change of direction is happening at each instant! This is a bit difficult to visualize, but essentially this also means that in the limit the Weiner Process $W(t), 0\le t\le 1$ does not have a derivative at any point in the interval $[0,1]$ (since the derivative is not defined at points at which the direction of a function changes). 

There is a bit of ambiguity in the notation since $W^n(t)$ can refer both to the sample path of the Random Process over the interval $[0,1]$, as well the Random Variable $W^(t)$ at time $t$. We will use the convention that $W^n(t)$ refers to the function $W^n(t)$ defined over an interval such as $[0,1]$, while we will use $W^n_t$ to refer to the Random Variable at time $t$.

There is another way to analyze a Random Process and that is by fixing the time instants $t_1,t_2,..,t_n$ at which we sample the random process. This avoid the necessity of considering the space of continuous sample paths, and instead we now have a vector of Random Variables ${W_{t_1}, W_{t_2},...,W_{t_n)}}$, and these can be analyzed by assigning a joint Probability Density Function to the vector, which is a much easier proposition. Kolmogorov showed that if we are able to assign probabilities to all possible vectors of the resulting Random Variables, then this uniquely determines the Probability Measure that exists over the space of continuous functions, and this is called the Kolmogorov Extension Theorem. Most of the work in practical applications of Random Processes is done using joint distributions over vectors.

We now provide some heuristic arguments to show that the Random Process $W^n(t)$ converges to the Weiner Process $W(t)$ as $n\uparrow\infty$. We start by showing a couple of important properties for the Random Process $W^n(t)$. In the following we will refer to the vector $W^n_{j\over n} - W^n_{i\over n}$ as an increment of the Random Process $W^n(t)$.

**The Independent Stationary Increment (ISI) Property**
   
Note that the increment $W^n_{j\over n} - W^n_{i\over n}$ can be written as

$$ W^n_{j\over n} - W^n_{i\over n} = {1\over\sqrt n}\sum_{k=i}^j X_k $$

Hence overlapping increments are the sum of distinct independent Random Variables $X_k$. From this we can conclude that non-overlapping increments of $W^n(t)$ form independent Random Variables, which is known as the Independent Stationary Increment (ISI) property. The stationarity refers to the fact that the distribution of an increment in only a function of its length and is indpendent of where it islocated over the time interval.

**Distribution for Increments of $W^n(t)**

We established that increments of $W^n(t)$ are stationary and independent, we now given expression for their distribution.
We start with

$$ W^n_{j\over n} - W^n_{i\over n} = {1\over\sqrt n}\sum_{k=i}^j X_k = {1\over\sqrt n}(S_j - S_i) $$

Note that $E(S_k) = 0$ while 

$$  E(S_k^2) = E(\sum_{i=1}^k\sum_{j=1}^k X_i X_j) = k\ \ \ since\ \ \ E(X_i^2) = 1\ \ \ and\ \ \ E(X_i X_j) = 0\ \ \  for\ \ \ i\ne j  $$ 

so that for $j > i$

$$ E(S_j - S_i)^2 = E(S_j^2) + E(S_i^2) - 2E(S_i S_j) = j + i - 2i = j - i $$

It follows that

$$ E[W^n_{j\over n} - W^n_{i\over n}]^2 = {1\over n}E(S_j - S_i)^2  = {j\over n} - {i\over n}  $$

Also note that

$$ E[W^n_{j\over n} - W^n_{i\over n}] = 0 $$

Setting $t_j = {j\over n}$ and $t_i = {i\over n}$, 
as $n\uparrow\infty$, it follows from the Central Limit Theorem that the increment $W^n_{j\over n} - W^n_{i\over n}$ converges in distribution to a Normal distribution with mean 0 and variance $t_j - t_i$. 

But, what is the definition of the Weiner Process? A Random Process $W(t), 0\le t\le 1$ is called a Weiner Process if it satisifes the following conditions:

1. The sample paths of $W(t)$ are continuous with $W_0 = 0$.
2. The increments $W_{t_1} - W_{t_0},...,W_{t_m} - W_{t_{m-1}}, 0 = t_0 < t_1 < ...<t_{m-1} < t_m$ are independent Random Variables. This is called the Independent Stationary Increment (ISI) property.
3. Over finite time increments $t_{j-1}$ to $t_j$, $W_{t_j} - W_{t_{j-1}}$ is Normally distributed with mean 0 and variance $t_j - t_{j-1}$, and this can be written as:

$$ P(a\le W_{t_j}-W_{t_{j-1}}\le b) = {1\over\sqrt{2\pi}}\int_a^b e^{-{x^2\over 2(t_j - t_{j-1})}} dx $$

A question that arises is: What does convergence mean when the objects we are talking about are Random Processes? 
Lets first consider what consider what convergence means in the context of the Random Sum $S_n$. Can we say anything about the convergence of the scaled version of this sum given by ${S_n\over\sqrt{n}}$? We certainly can, and this is one of the most famous results in Probability Theory called the Central Limit Theorem or CLT. It says that the distribution of ${S_n\over\sqrt{n}}$ converges to the Standard Gaussian Distribution $N(0,1)$. More precisely

$$ {S_n\over\sqrt{n}} \rightarrow  {1\over\sqrt{2\pi}}e^{-{x^2\over 2}}\ \ \ as\ \ \ n\uparrow\infty $$

This kind of convergence for Random Variables is called Convergence in Distribution or Weak Convergence. It basically says that in the limit, we may not be able to tell the precise number to which ${S_n\over\sqrt{n}}$ will converge to (which is the traditional idea of convergence for determinitic series), but we can give precise estimates of the probability of the Random Sum falling within an interval, say $[a,b]$, and this is given by the Normal Distribution. 

Can we define a similar type of Weak Convergence result for Random Functions $W_n(t), 0\le t\le 1$ as $n\uparrow\infty$? Hence if $P_n$ is a probability measure over the space of Random Functions $W_n(t), 0\le t\le 1$, and if $P_W$ is the probability measure for the Weiner Proces $W(t), 0\le t\le 1$, then does $P_n\rightarrow P$ as $n\uparrow\infty$? It turns that this is indeed the case, and this is the content of Donsker's Theorem.
Note that there is a whole bunch of mathematical subtleties that I have swept under rug, for instance: What does it mean to define a probability space consisting of functions (as opposed to numbers) and what is the metric for that space? What is the appropriate notion of events for this space and lastly what does it mean to define a probability measure for those events? For those of you wanting to get deeper, there are several excellent books available, in particular "Convergence of Probability Measures" by Patrick Billingsley is standard reference for the theory of weak convergence.

There are some intuitive arguments to show how the interpolated random sums $W_n(t)$ converge to the Weiner process

The notion of a probability measure over spaces of functions is a convenient mathematical abstraction, but in practice we use something that is easier to deal with, namely multi-dimensional distributions at a finite number of time instants. For example the distribution for the Weiner Process at the finite set of time instants $(t_1,t_2,...t_n)$ is given by

$$ P(x_1\le W_{t_1}\le y_1, x_2\le W_{t_2}\le y_2,...,x_n\le W_{t_n}\le y_n) = \int_{x_1}^{y_1} \int_{x_2}^{y_2} \int_{x_n}^{y_n} N(0,t_1)N(0,t_2-t_1),...,N(0,t_n-t_{n-1})dx_1 dx_2...dx_n  $$

There is a result known as the Kolmogorov Extension Theorem which states that if these distributions exist for all possible finite time instants in the interval $[0,1]$, gthen it implies the existence of a corresponding probability measure over the space of functions $x(t), 0\le t\le 1$.

- Absolute Sum of variations

## Stochastic Calculus and the Ito Integral

- [ ] Go through the signal + noise model, as per page 15 of Oksendal's book. How this naturally leads to the Ito Integral.
- [ ] dx/dt = Ax + B dW/dt equivalent to x = int(Ax dt) + int(B dW).  The latter is the Ito integral. 
- [ ] Rough derivation of the existence proof of the Ito Integral

## Adding Randomness to Models

- [ ] Why is it important? A convenient way to add randomness to a model. WP is analytically tractable. 
- [ ] Applications: Stock Market, image generation, noise filtering
- [ ] Processes that can be modeled as signal plus noise
- [ ] Great interest in extracting the signal, the filtering problem, Kalman Filtering
- [ ] Processes that can be modeled as a function of a Random Process
- [ ] Example: Financial Derivatives
- [ ] Modeling the space of Latent Variables
- [ ] Example: Diffusion based Image Generation

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


## My Personal Encounters with Randomness

- Reflected Brownian Motion, as part of my PhD Thesis
- Russian probabilists at UMD in the late 1980s
- Stock Market prediction using a Neural Network model






      
