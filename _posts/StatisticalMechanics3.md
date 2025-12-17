---
layout: default
title: "Energy Based Models Part 3: Recent Developments"
---

# Energy Based Models Part 3: Recent Developments

**Contents**        
  

## Introduction



## EBMs with Complex Energy Functions

Early EBMs from the 1980s, such as the Boltzmann Machine, feature relatively simple energy functions

$$  E = -\sum_i\sum_{j\lt i} w_{ij} \sigma_i\sigma_j - \sum_i \sigma_i b_i $$

where $\sigma_i$ is the spin at node $i$, which can take values ${+1,-1}$, $w_{ij}$ is the symmetric strength of the interaction between nodes $i$ and $j$ and $b_i$ the threshold for activating node $i$. The spins in these networks are updated using Gibbs sampling

$$ p(\sigma_k = 1) = p_k = {1\over{1 + \exp(-\beta h_k)}} $$

Repeated sampling results in the network state gradually moving to an equilibrium configuration which corresponds to a local minima for the energy function.
The addition of hidden nodes enables these systems to model more complex nodal interactions by increasing the number of parameters available to the model.
Hinton and the early pioneers limited their models to quadratic energy functions since they wanted them to be biologically plausible so that they could be used as models
of the brain. This has become less of a requirement for modern AI systems, indeed modern EBMs are defined by the following equation

$$ p(\x_1,x_2,...,x_N) = {e^{-E(x_1,...,x_N)}\over{Z}} $$

where $Z$ as usual is the partition function

$$ Z = \sum{x_1,...,x_N} e^{-E(x_1,...,x_N)}  $$

There are two differences compared to older EBMs

- The state variables $(x_1,...,x_N)$ are no longer restricted to $+1,-1$ but can take on any real value.
- 

however they still
suffer from the following problems

In order to generalize this 




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
