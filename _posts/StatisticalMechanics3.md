---
layout: default
title: "Energy Based Models Part 3: Recent Developments"
---

# Energy Based Models Part 3: Recent Developments

**Contents**        
  

## Introduction



## EBMs with Complex Energy Functions

Early EBMs from the 1980s, such as the Boltzmann Machine, feature relatively simple energy functions

$$  E = -\sum_i\sum_{j\lt i} w_{ij} \sigma_i\sigma_j - \sum_i b_i \sigma_i $$

where $\sigma_i$ is the spin at node $i$, which can take values ${+1,-1}$, $w_{ij}$ is the symmetric strength of the interaction between nodes $i$ and $j$ and $b_i$ the threshold for activating node $i$. The spins in these networks are updated using Gibbs sampling

$$ p(\sigma_k = 1) = p_k = {1\over{1 + \exp(-\beta h_k)}} $$

Repeated sampling results in the network state gradually moving to an equilibrium configuration which corresponds to a local minima for the energy function.
The addition of hidden nodes enables these systems to model more complex nodal interactions by increasing the number of parameters available to the model.
Hinton and the early pioneers limited their models to quadratic energy functions since they wanted them to be biologically plausible so that they could be used as models
of the brain. This has become less of a requirement for modern AI systems, indeed modern EBMs are defined by the following equation

$$ p(x_1,x_2,...,x_N) = {e^{-E(x_1,...,x_N)}\over{Z}} $$

where $Z$ as usual is the partition function

$$ Z = \sum_{x_1,...,x_N} e^{-E_W(x_1,...,x_N)}  $$

There are two differences compared to older EBMs

- The state variables $(x_1,...,x_N)$ are no longer restricted to $+1,-1$ but can take on any real value.
- The energy function $E_W(x_1,...,x_N)$ is described by a neural network whose input is $(x_1,...,x_N)$ and has parameters given by the vector $W$.

Since a neural network can be trained to approximate any possible function, it follows that the new EBM is capable of modeling a much wider variety of energy
landscapes. This opens up the possibility of using moden neural networks such as convolutional networks and transformers as models for the energy function.
The new design raises the following questions:

- How can we sample from these networks, since Gibbs sampling clearly does not apply here.
- How do we train these networks? Do Contrastive Divergence (CD) type algorithms still work?

![](https://subirvarma.github.io/GeneralCognitics/images/stat52.png) 

Figure 1: The energy landscape in Boltzmann Machines

The first question is answered in the next subsection in which we introduce a powerful MCMC type sampling algorithm called Langevin sampling. The answer to the training
question is more involved and occupies the following sections. Not only do we have to come up with training schema that applies to more complex energy landscapes, but the new algorithm also has to avoid the issues that plagued the older Boltzmann Machine system, namely that Boltzmann Machine and related systems could not be scaled beyond a few thousand nodes since the computational cost of sampling became excessive, since it took a very long time to converge. This problem has to do with the difficulty in sampling from a multi-model landscapes, as illustrated in figure 1.






### MCMC Sampling Using the Langevin Equation



## Training EBMs with Complex Energy Functions



### Training Using MCMC Sampling



### Training Using Score Matching and Denoised Score Matching (DSM)



### NCSN: A Multi-Stage DSM Training Algorithm





## Implementation of  Boltzmann Machines



### P-Bit Based Systems: UCSB, Purdue

Probabilistic bits


### Multistage P-Bit Implemntation: Extropic



## Implemntation of the Langevin Equation: Normal Computing

Analog circuitry
