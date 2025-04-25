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

Extending this idea further, what if the random quantity evolves continuously in time? This then becomes a continuous time Random Process, and an example of this is shown the above figure. You can think of these graphs as being created by the Brownian Motion of a pollen particle whose movement is confined to just one dimension, either up or down along the y-axis, or the variation in the stock price for a company over time. Note that there are several curves shown in the figure, and each of them represents the evolution of the random process when starting from the origin  $t=0$, also called a sample path. Each of these sample paths is deterministic as a function of time, the randomness arises from the fact that we don't know in advance at $t=0$ which of these paths will actually result once the motion starts. Hence instead of assigning a probability to an individual outcome, as when tossing a coin, we assign a probability to the entire sample path as a whole. 

The analysis of a continuous time Random Process is exponentialy harder than the discrete time version. Consequently very little progress had been made in this area by 1900 and part of the reason was that there was no connection made between Probability Theory and the rapidly developing methods in analysis that resulted in developments such as the Borel Measure and the Lebesgue Integral towards the end of the 19th century.
The major contribution that the 20th century made to the science of randomness, is precisely this connection. It laid the science of Random Processes on a firm mathematical foundation, by connecting it with the rest of mathematical analysis. This process started with Bachelier, and was completed two decades later with great Russian mathematician Andrei Kolmogorov's axiomatization of Probability Theory. This made it possible to talk about quantities that evolve randomly and continuously in time, which is precisely what a Random Process is. This has an interesting echo with Quantum Mechanics that also took about two decades two mature from Planck to Heisenberg and Schrodinger. 

Kiyosi Ito was a Japanese mathematician who made the next important advance in the theory of Random Processes. Working in wartime Tokyo during the 1940s, he came up with the idea of extending the idea of the integral to the case when the integration is done with respect to Brownian Motion, and this is now called the Ito Integral in his honor. I found this to be a totally mind blowing concept when I first learnt about in grad school in the late 1980s, and even today I consider it a privilage that I understand what it means.
This idea was very influential since it allowed mathematicians to build more complex Random Processes by using Brownian Motion as a basic building block. This laid the foundation for several important applications of Random Processes that happened in the following decades.

But how important are these Random Processes? Well, the most famous example of a randomly evolving continuous time process is the stock market, and this is precisely what Bachelier studied in his 1900 paper. His work was essentially lost until the 1950s, when it came to the attention of the  eminent economist Paul Samuelson, who built on Ito's work and applied it to create a model for the stock market called the Logarithmic Brownian Motion.
Later in the 1960s the economists Fischer Black and Myron Scholes extended Ito and Samuelson's theories to create a model for stock options trading. This resulted in a Partial Differential Equation named after them, whose solution is probably the most important mathematical result in use in Wall Street trading today. In fact I recently came acrosss a list of the most imprtant equations in science, and the Black-Scholes equation was listed along with others such as Maxwell Equations for electromagnetism and Schrodinger's Equation for the quantum wave function.

![](https://subirvarma.github.io/GeneralCognitics/images/weiner6.png) 

Figure 6: Signals in Noise

Brownian Motion has evolved into a powerful tool for modeling random phenomena. Whenever the need arises to capture the randomness that exists in fields such as communications system or electrical circuits, Brownian Motion is the go-to model that engineers use. An example of a a deterministic signal subject to random noise is shown in the above figure. The clean signal is transmitted, while the noise is added during the course of transmisssion over a communications channel. The Filtering Problem looks at ways in which the signal can be extracted from the noise which is usually modeled as a Brownian Motion. Norbert Weiner (more about him in the next section) and Richard Kalman are names associated with the solution to the filtering problem.

![](https://subirvarma.github.io/GeneralCognitics/images/weiner7.png) 

Figure 6: Training a Neural Network to generate images

But the most interesting, and surprising, application of Brownian Motion has happened during the last decade, when it was used to create a Neural Network model that can generate realistic images and videos. This model ouperformed all competing methods, and it has become the most prevalent image/vdeo generation model in use today. This topic is treated in greater detail later, but a rough idea of how it done can be seen in the above figure. The top row shows the process of adding incremental noise to an image, until it becomes indistinguishable from noise. The bottom row trains the Neural Network by learning how to recover the original image from noise. Once the network is trained, it can generate new images by starting from a noise sample.

## From Brownian Motion to the Weiner Process

There was one name that I haven't mentioned in my brief survey of mathematicians who have contributed to the theory of the Brownian Motion, and it is that of Norbert Weiner. This is quite a big omission since the terms Brownian Motion and Weiner Process are often used inter-changeably. Strictly speaking Brownian Motion is the physical phenomenon that Robert Brown discovered and Einstein analyzed, while the Weiner Process is a mathemtical model for it (this is the terminology that I will use in the rest of this article). Norbert Weiner was the first one to do a rigorous mathematical analysis of Brownian Motion in the early 1920s, and abstracted it to create the mathematical notion of a Weiner Process. He proved several important properties for it, such as the fact that its sample paths are continuous in time, while at the same time its derivative does not exist anywhere.
Weiner was a child prodigy who got his PhD from Harvard at age 19, and spent his career teaching at MIT. His work spanned mathematics, both pure and applied, as well philosophy and towards the latter part of his life what we call Artificial Intelligence (he called it Cybernetics). He contributed more than anyone else to the emerging field of Signal Processing, and was a big influence on the later work of Claude Shannon and John von Neummann.

The theory of sample paths of a continuously varying random process was not sufficiently well developed when Weiner was working on the problem in the early 1920s, and had to wait for Kolmogorov's axiomitization of Probability Theory ten years later. During the 1950s Monroe Donsker gave a highly intuitive explanation of how the Weiner Process arises as a limiting case of simpler Random Processes, and this is what I am going to describe in this section.

![](https://subirvarma.github.io/GeneralCognitics/images/weiner9.png) 

Figure: Outcome of a Coin Tossing Experiment

Lets start with a very simple process, that of tossing a coin. Let the Random Variable $X_n$ be the result of the $n^{th}$ toss, and assign $X_n =  1$ if the result is a Heads and -1 to Tails. Define $S_n$ to be the Random Sum given by

$$ S_n = X_1 + X_2 + ...+ X_n $$

The figure above graphs one possible sample path for $S_n$ resulting from the tosses $THHTHT$. This process is known as a Random Walk and it has the interesting property that once we know the value of $S_n$, the future evolution of the process is completely independent of what happened prior to the $n^{th}$ toss. These type of processes, in which the the future is independent of the past given the present, form an important category called Markov Processes. 

So we have a process that seems to be moving about randomly, but it is not quite a Brownian Motion yet. 
How can we go about creating a model for Brownian Motion? First of all we need to introduce time as a variable. Also compared to the Random Sum, Brownian Motion exhibits much faster changes in direction, and also successive changes happen much quicker in time. One way to accomplish all these goals is by doing the following:

- Scale the Random Sums by ${1\over{\sqrt{n}}}$ so that as $n$ increases, the jumps in the $S_n$ values become smaller.
- In order to introduce a time dependence, restrict the Random Walk to the time interval interval $[0,1]$ such that changes in the Random Sum occur at at the $n$ time instants given by $[{i-1\over n}, {i\over n}], i = 1, 2,...n$
- Define a random function $W_n(t), 0\le t\le 1$ such that it is equal to the scaled sum ${S_i\over{\sqrt n}}$ at the point ${i\over n}$ and then interpolate between successive sums to create a continuous function over $0\le t\le 1$ whose value at point $t$ is given by:

$$ W_n(t) = {S_{n-1}\over{\sqrt{n}}} + \left[{t - {(i-1)\over n}\over{1\over n}}\right] {1\over{\sqrt{n}}} X_i\ \ \ for\ \ \
t\in \left[{i-1\over n}, {i\over n}\right]$$

![](https://subirvarma.github.io/GeneralCognitics/images/weiner10.png) 

Figure: Scaling Random Walks for n = 100 (blue), n = 400 (red) and n = 10000 (green)

The figure above three different sample paths for $W_n(t)$ over the interval $[0,1]$, with the interval between successive changes in direction becoming smaller as $n$ increases. As $n\rightarrow\infty$, Donsker's Theorem says that $W_n(t), 0\le t\le 1$ converges to a Weiner Process. What does it mean to take the limit $n\uparrow\infty$ for the interpolated Random Sums? Since we are constrained to be in the interval $[0,1]$, it means that successive coin tosses are happening faster and faster, and in the limit they are being done over the continuum. Since each coin toss results in a change of direction for $W_n(t)$, it follows that in the limit, the change of direction is happening at each instant. This is a bit difficult ti visualize, but essentially this also means that in the limit the Weiner Process $W(t), 0\le t\le 1$ does not have a derivative at any point in the interval $[0,1]$ (since at every point where the direction of a function changes, its derivative at that point is not well defined).

But, what is the definition of the Weiner Process? A Random Process $W(t), 0\le t\le 1$ is called a Weiner Process if it satisifes the following:

- The sample paths of $W(t)$ are continuous.
- The increments $W(t_1) - W(t_0),...,W(t_m) - W(t_{m-1}), 0 = t_0 < t_1 < ...<t_{m-1} < t_m$ are independent.
- Over finite time increments $t_{j-1}$ to $t_j$, $W(t_j) - W(t_{j-1})$ is Normally distributed with mean 0 and variance $t_j - t_{j-1}$.

There is a bit of ambiguity in the notation $W(t)$ can refer both the Random Process over the interval $[0,1]$, as well the Random Variable $W(t)$ at time $t$. We will specifically specify the time range when referring to the Random Process.

A question that arises is: What does convergence mean when the objects we are talking about are Random Processes? Lets first consider what consider what convergence means in the context of the Random Sum $S_n$. Can we say anything about the convergence of the scaled version of this sum given by ${S_n\over\sqrt{n}}$? We certainly can, and this is one of the most famous results in Probability Theory called the Central Limit Theorem or CLT. It says that the distribution of ${S_n\over\sqrt{n}}$ converges to the Standard Gaussian Distribution $N(0,1)$. More precisely

$$ {S_n\over\sqrt{n}} \rightarrow  {1\over\sqrt{2\pi}}e^{-{x^2\over 2}}\ \ \ as\ \ \ n\uparrow\infty $$

This kind of convergence for Random Variables is called Convergence in Distribution or Weak Convergence. It basically says that in the limit, we may not be able to tell the precise number to which ${S_n\over\sqrt{n}}$ will converge to (which is the traditional idea of convergence for determinitic series), but we can give precise estimates of the probability of the Random Sum ending up in an interval over the Real Line, say $[a,b]$, and this is given by the Normal Distribution. 

Can we define a similar type of Weak Convergence for Random Functions $W_n(t), 0\le t\le 1$ as $n\uparrow\infty$? 

In order to do so, we will have to specify the following:

- We will have to specify the set in which $W_n(t)$ is an element, usually called $\Omega$ in Probability Theory. In the case of the Random Sums, this was quite simple, $S_n$ was an element of the set of Integers. For $W_n(t)$ the appropriate set is called $C[0,1]$, which is the set of all possible continuous functions defined in the interval $[0,1]$. We will also have to define a metric over this space, since without a metric we cannot talk about distance between elements in the set. This is given by

$$ \rho(x,y) = \sup_t|x(t) - y(t)|  $$

- We will have to define a Probability Measure over the appropriate subsets of $\Omega$. We will use the notation $P_n$ to refer to Probability Measures for the Random Functions $W_n(t)$, for the case when the interval $[0,1]$ is divided into $n$ equal parts.

Using these definitions, the sequence of Probability Measures $\{P_n\}$ is said to converge weakly to the Measure $P$ if

$$ 

Until now I haven't formally defined what a Weiner Process is, we will try to figure out its properties with the help of the fact it is the limiting case of Random Sums.
- Continuous but no derivatives anywhere, continuously changes direction. The fractal Self similarity property.
- Independent Stationary Increments
- Gaussian distribution in the limit. Estimate of how much it will wander from the origin.
- Absolute Sum of variations

Weiner's contribution

Image and Video generation using the Langevin Process.

- [ ] What is the most random thing possible?
- [ ] The drunkards walk
- [ ] Limiting case of the drunkards walk, becomes something that captures the essence of randomness in a form that is amenable to analysis ie the BM
- [ ] History of BM: Einstein, application to stock trading Bachelier, Weiner, KKL expansion
- [ ] Diffusion processes 

### Historical Notes

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

## My Personal Encounters with Randomness

- Reflected Brownian Motion, as part of my PhD Thesis
- Stock Market prediction using a Neural Network model






      
