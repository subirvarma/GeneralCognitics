---
layout: default
title: "Energy Based Models Part 3: Recent Developments"
---

# Energy Based Models Part 3: Recent Developments

**Contents**        
  

## Introduction

All of modern Generative AI systems, such as LLMs for generating text and diffusion models for generating images, are based on the idea of sampling from a probability distribution that represents the statistics of the training data. Hinton and Sejnowski were the first ones to realize the power of this idea, and showed how to obtain a model for the probability distribution by choosing the interaction strengths in a Sherrington-Kirkpatrich type spin glass model, that they called a Boltzmann machine. These systems worked well, but failed to scale up and also suffered from long convergence times. On the other hand these systems had the benefit that they could serve as plausible models for biological neural networks. Also their training methodology was based on statistical ampling and not on the backprop algorithm, so potentially they could be used to create more energy efficient systems. 
So the question arises whether sampling based EBM models can scale up to node sizes that are comparable to non-EBM based modern artificial neural networks and with comparable or better performance, while being faster and more energy efficient. Modern EBMs are not quite there yet, but have made a good deal of progress in the last decade or so, and this is described in this article.

Modern EBMs are also based on the idea of approximating the training data distribution by a Boltzmann distribution that is parametrized by the interaction strengths of multiple Ising type nodes. This can also be considered to be be the same as the problem of approximating the energy function implied by the training data with the energy function of the EBM model. The original Boltzmann machines were restricted to using fairly simple quadratic enery functions and one way to create a more powerful EBM would be by using more sophistictaed energy functions. The modern theory of on artificial neural networks (ANNs) comes to the rescue here, since it provides us with a way to create very complex parametrized functions that can be used to approximate arbitrarily comples functions. 
The parameters of the ANN play the role of interaction strengths in the original model and moreover they can be estimated by using the powerful backprop algorithm.
Using this idea it becomes possible to replace the quadratic energy function in the original Boltzmann machine, with an ANN which can potentially have hundreds of millions of parameters and results in an enormous increase in the modeling power of the resulting EBM. This also enables modern EBMs to piggyback on the advances in ANNs in recent years with powerful models such as convolutional neural networks (CNNs) and transformers.
With the introduction of ANN based energy functions and the use of the backprop algorithm for training, the question arises whether these modern EBMs are still biologically plausible. I will have a few remarks to say on this topic in the next section.

In order to carry out this agenda, there are two problems that have to be solved:

- How to sample from these EBM models since clearly the Gibbs sampling used in classical Boltzmann machines no longer applies.
- How to train these EBM models, since again the Contrastive Divergence or CD algorithm used in Boltzmann machines cannot be used anymore.

I am going to spend the the bulk of this article talking about proposed solutions to these problems, so lets get into the next level of detail.

EBM models entered a winter phase following the success of backprop driven neural network models, heralded by the the AlexNet model of 2012, and more recently with the LLM models from OpenAI and others.
However beginning in 2019 there has been a renewed interest in EBMs, led by research coming from academia, such as by Stefano Ermon's group at Stanford University. This has led to considerable progress in the
theory for Boltzmann Machines. The original Boltzmann Machines never became commercially viable due to a couple of problems:

- They were not able to scale up to beyond a few hundred nodes since the training process became too time consuming. This was due to the fact that the sampling alsgorithm was not able to handle multi-model distributions very well. It took an excessive amount of time to move between valleys in the energy landscape during the training process.
- The original Boltzmann Machine was limited to the quadratic energy function with per node state values of 0 and 1 (or -1 and 1). In order to compete with modern neural networks there was a need to extend node values that are real numbers and more general energy functions.

The second issue was easier to solve, and was resolved with the introduction of Langevin Monte Caro Markov Chain (MCMC) sampling. This enabled the system nodes to have real valued 'spin' values, and these were updated using an iteration that caused the system state to converge to values distributed according to a specified probability distribution. The origins of Langevin sampling lie in the theory of stochastic diffusion processes, and I touched upon this topic in [my post on Brownian Motion](https://subirvarma.github.io/GeneralCognitics/2025/05/23/TamingRandomness.html). 
Once we use Langevin sampling, it becomes possible to handle energy functions that are more complex than quadratic, indeed te becomes possible use completely arbitrary functions of three or higher orders. This takes us back to the modern developments in neural networks, which basically used these networks to model arbitrary functions of the input variables using regression techniques. This opens up the use of powerful systems such as convolutions neural networks and transformers to model energy functions.

There also has been progress in training algorithms for EBMs. Hinton's original algorithm for training Boltzmann Macines was based on the concept of maximizing the likelihood function for the training data (or equivalently minimizing the KL divergence between the training data distribution and the model provided distribution). This algorithm runs into the problem that it requires an estimate of the partition function, which has traditionally been a difficult task. Hinton tried to resolve this problem with the contrastive divergence (CD) algorithm, however it still runs into scaling problems in model sizes larger than a few hundred nodes. The resolution to this problem required some fundamental advances in theory, and interestingly enough the core idea that finally solved it is related to the idea of simulated annealing that was described in Part 1. It was recognized that the problem had to do with the inefficient sampling of multi-modal distributions, and the solution involved mixing Gaussian noise to the input values in order to make the distribution closer to unimodal. More important was the idea of introducing this noise at various levels and then gradually reducing it from high to low values as part of the sampling process. It was shown that this indeed solved the multi-modality problam and led to model outputs that are currently the state of the art in image generation. These models generally go by the name of diffusion models and can be considered to be the modern versions of the Boltzmann Machines from the 1980s with upgraded energy functions and training algorithms.

All these advances in EBM models are impressive, but is there any fundamental benefit to using them over non-EBM models since it seems that both types of models are equally good at various tasks. The current generation of non-EBM models are based on the backprop algorithm for training, and this can be considerably accelerated with the help of GPUs. However this comes with the issue of sky-rocketing energy consumption for large model sizes which has become a major problem. If EBM models can be engineered for lower energy consumption then this would constitute a major benefit. Since EBM models are based on the operation of sampling from distributions they are not able to enjoy the same acceleration with the use of GPUs as backprop driven non-EBM models. However if the hardware substrate on which these systems run is optimized for the sampling operation then it can potentially lead to huge savings in energy consumption. There are a number of efforts underway in this direction and we will describe a couple of them:

- A startup called Normal Computers has been working on silicon based chips that can be used to accelerate Langevin sampling.
- Extropic is another startup which is trying to produce that can be used to acclerate the Gibbs sampling used in Boltzmann machines.

These and similar systems are based on the idea of using the physical properties of the substrate on which the chip is built to introduce noise into calculations, which are required as part of the samploig process. So for exmple, in the Extropic system, the states of all the nodes in the Boltzmann machine can be updated in parallel in a single cycle, rather then on a serial one-by-one basis in digital implementations.
These sytems are still in the reserach phase and they have a long way to go until they approach the performance of modern dititally implemented non-EBM systems.

The holy grail of modern generative systems are LLMs, and the question arises whether EBMs can be used to implement LLMs. The current generation of LLMs are based on auto-regressive sampling using transformers, and generate one word at a time. It turns out that diffusion models can also be used to generate text, which clears the path to using EBM based diffusioins to generate text. Stefano Ermon has founded a start-up called Inception that is working of diffusion based LLMs. These are still implemented in traditional GPU based architectures, and their selling point is faster text generation compared to auto-regressive models as opposed to lower energy consumption.

There is another branch in modern EBM development called Thermodynamic Computing  which derives its inspiration from the original Hopfield network as opposed to the Boltzmann machine. Recall that the Hopfield network generated specific node configuratoins as opposed to distribution of configurations, and potentially can be used as a computational tool. This wasd actyually pointed out by Hopfield himself, who showed how combinatorial optimization problems such as the Travelling Salesman Problem can be mapped on to the Hopfield network. This work has been updated by reserach groups at Purdue University and UCSB, who have shown how Hopfield networks can be scaled to much larger sizes, using both theoretical advances such as more efficient sampliong techniques, as well new hardware devices that can implemenent this sampling more efficiently. This work is also in its reserach phase at the present time, and its maon driver has been to serve as an alternative to quantum computers for  probabilistic algorithms.


## EBMs with ANN Based Energy Functions

![](https://subirvarma.github.io/GeneralCognitics/images/stat54.png) 

Figure 1: Computing the energy functions for EBMs

The original Ising model for paramagnetism featured a simple energy function, shown in part (a) of the above figure. The interaction strength between nodes was uniform across the entire network, and this resulted in an energy landscape with a couple of minima corresponding to net magnetization of the system. Sherrington and Kirkpatrick modified this model by making the interaction strengths random, ans also each node to interact with every other node in the system, shown in part (b). This led to a complex energy landscape with a large number of minima that scaled up with the number of nodes.
The SK model was subsequently used by Hopfield and Hinton to create the first computational and generative models, namely the Hopfield network and the Boltzmann machine, as described in Part 2 of this article series. 
A way for EBMs to transition to the modern era is shown in the lower part of the figure. Part (c) shows an energy function that is described by convolutional neural network or CNN. These were originally introduced as a way to process images, and given the 2D nature of the nodes in the EBM, there seems to be a good fit for designing EBMs which can be used to generate images. Part (d) of the figure shows an EBM that uses the transformet network for computing energy functions. Transformers are another powerful way to approximate energy functions, traditional LLMs use them as a way to sample from conditional probability distributions.

Note that in the original EBMs shown in parts (a) and (b), the energy function was parametrized by the interaction strengths between nodes. 
On the other hand, if we use either a CNN or transformer (or any other ANN) to model the energy function, then the energy function is parametrized by the weights in the ANN. If the EBM is being used as a model for neural processing in biological brains, then what is the connection between the ANN weights and the interaction strengths between nodes? Clearly the interactions are more complex than the two node interactions in the SK model, and involve multiple nodes interacting with one another, and thus closer to the P-Spin or PSM type models described in Part 1. Are these more complex interactions biologically plausible? Interactions between biological neurons seem to be of the two node type, however one way to reduce higher node interactions to two node interactions is by introducing hidden nodes into the model, as first pointed out by Krotov and Hopfied. I haven't seen examples in the literature for this program of converting an EBM with a CNN or transformer based energy function into an equivalent EBM with hidden nodes in which all interactions are of the two node type.
This doesn't mean that biological brains are not designed this way, indeed biological neurons have a very complex interconnection topology (called the connectome) in which each neuron may be connected to thousands of other neurons, and we have very little knowledge about the nature of this network.
Another way to look at this problem is by recognizing that a complete understanding of the connectome is probably out of our reach at the present time, but we can ignore the details of the node interconnections and focus on the resulting energy function instead. This energy function is also a very complex beast, but fortunately we have a tool at our disposal to model complexity of this magnitude, name the ANN.


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

![](https://subirvarma.github.io/GeneralCognitics/images/stat53.png) 

Figure 1: Computing the energy function using a neural network

- The state variables $(x_1,...,x_N)$ are no longer restricted to $+1,-1$ but can take on any real value.
- The energy function $E_W(x_1,...,x_N)$ is described by a neural network whose input is $(x_1,...,x_N)$ and has parameters given by the vector $W$.

Since a neural network can be trained to approximate any possible function, it follows that the new EBM is capable of modeling a much wider variety of energy
landscapes. This opens up the possibility of using moden neural networks such as convolutional networks and transformers as models for the energy function.
The new design raises the following questions:

- How can we sample from these networks, since Gibbs sampling clearly does not apply here.
- How do we train these networks? Do Contrastive Divergence (CD) type algorithms still work?

![](https://subirvarma.github.io/GeneralCognitics/images/stat52.png) 

Figure 2: The energy landscape in Boltzmann Machines

The first question is answered in the next subsection in which we introduce a powerful MCMC type sampling algorithm called Langevin sampling. The answer to the training
question is more involved and occupies the following sections. Not only do we have to come up with training schema that applies to more complex energy landscapes, but the new algorithm also has to avoid the issues that plagued the older Boltzmann Machine system, namely that Boltzmann Machine and related systems could not be scaled beyond a few thousand nodes since the computational cost of sampling became excessive, since it took a very long time to converge. This problem has to do with the difficulty in sampling from a multi-model landscapes, as illustrated in figure 2.






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
