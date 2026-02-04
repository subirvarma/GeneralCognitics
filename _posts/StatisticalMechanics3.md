---
layout: default
title: "Energy Based Models Part 3: Recent Developments"
---

# Energy Based Models Part 3: Recent Developments

## Abstract

There has been considerable progress in the field of Artificial Neural Networks or ANNs in recent years, with the latest models such as ChatGPT or Gemini exhibiting human like characteristics. 
At the same time there is a lack of understanding on what makes these models so effective, and also how these models relate to biological brains. The latter
carry out the same tasks, and more, as ANNs, but are able to do so with much lower energy consumption. How is this possible? 

The field of Energy Based Models provides a possible path to answering these questions. In this article we will show that generative models, the class to which LLMs and image generation models belong, can be recast as EBMs (we will refer to them as generative EBMs), in fact as a more sophisticated version of the Boltzmann machines that we encountered in Part 2. This connects generative models to concepts from thermodynamics and the idea of energy minimization that we discussed in Parts 1 and 2. More importantly this creates a possible path by which modern generative ANNs can be connected to the operation of biological brains. 

In all likelihood biological brains operate using thermodynamic principles and it is not inconcievable that their architecture and that of generative EBMs share common principles of operation since the same physics underlies both (this is not unlike the fact that both birds and airplanes are able to fly using the Bernoulli's principle from physics, but they use different mechanisms). 
But how does this knowledge help us? One way in which it can is by helping us find more energy efficient ways of running ANNs and hopefully approach the energy efficiency of biological brains. Current ANNs run on GPUs that are not optimized for thermodynamic operations such as  sampling. However there are new ideas coming up in this area, and several companies are implementing chips that are much more efficient in this area and will be describd in this article.

![](https://subirvarma.github.io/GeneralCognitics/images/stat52.png) 

Figure 1: The energy landscape in an image generation EBM

The EBM approach to generative modeling also enables us to form an intuitive picture of how generative ANNs work and here is a high level description that will be elaborated upon later.
The probability distribution underlying real world data such as images or text can be approximated by the Boltzmann distribution as
modeled by a spin glass type EBM, with nodes with state $(x_1,...,x_N)$ in the model interacting with each other using a sophisticated energy function $E_W(x_1,...,x_N)$ where $W$ represents the parameters of the model. 
All possible images (or text) are arranged in the landscape of this energy function, in which the bottom of valleys corresponds to images that make sense to us, hence these have lower energy than images that don't make any sense (see figure 1). The process of generation consists of starting from an initial state in the state space (which may look like noise to us), and then navigating the energy landscape until we arrive at a minima, and at this point the configuration looks like an intelligible image. The process of finding the minima is a sampling operation using Langevin sampling, which is a generalization of the Gibbs sampling used for Boltzmann machines. The sampling is made efficient by using an idea that is related to that of simulated annealing that we came across in Part 1, and works by introducing noise at various levels of intensity and gradually reducing it as we approach the minima. 

## Introduction

All of modern Generative AI systems, such as LLMs for generating text and diffusion models for generating images, are based on the idea of sampling from a probability distribution that approximates the statistics of the training data. Hinton and Sejnowski were the first ones to realize the power of this idea, and showed how to obtain an EBM model for the probability distribution by choosing the interaction strengths in a Sherrington-Kirkpatrich type spin glass model, that they called a Boltzmann machine. These systems worked well, but failed to scale up and also suffered from long convergence times. On the other hand they had the benefit that they could serve as plausible models for biological neural networks. 
So the question arises whether Boltzmann machine type sampling based EBM models can scale up to node sizes that are comparable to non-EBM based modern generative ANNs and with comparable or better performance, while being faster and more energy efficient. We have made a good deal of progress in the last decade or so towards this goal, and this is described in this article.

Boltzmann machine based EBM models entered a winter phase following the success of backprop driven neural network models, heralded by the AlexNet model of 2012 (which also came out of Hinton'e research group), and more recently with the LLM models from OpenAI and others.
However beginning in 2019 there has been a renewed interest in EBMs, led by research coming from academia, such as by Stefano Ermon's group at Stanford University, which has led to considerable progress in the
modeliing capability of EBMs. 

The original Boltzmann Machines never became commercially viable due to a couple of problems:

- They were not able to scale up to beyond a few hundred nodes since the training process became too time consuming. This was due to the fact that the sampling algorithm was not able to handle multi-model distributions very well. It took an excessive amount of time to move between valleys in the energy landscape during the sampling process.
- The Boltzmann Machine was limited to the quadratic energy function with per node state values of 0 and 1 (or -1 and 1). In order to compete with modern neural networks there was a need to extend it to more general energy functions and node values that are real numbers.

Modern generative EBMs are also based on the idea of approximating the training data distribution by a Boltzmann distribution and a corresponding energy function,
but there are some critical differences. 
Whereas the Boltzmann machine attempts to model the data distribution directly  using the Boltzmann distribution

$$  p(x_1,...,x_N) = {e^{-E(x_1,...,x_N)}\over{Z}} $$

 it runs into the problem of getting an estimate for the partition function $Z$ which is a difficult problem to solve.The Contrastive-Divergent (CD) algorithm was an attempt to get around this problem, but it didn't fully succeed as exhibited by the fact that Boltzmann machines don't scale very well. Modern EBMs circumvent this problem by trying to get estimates of the energy function $E$, or to be more precise, the gradient of the energy function ${\partial E\over{\partial x_i}}$, which is called the score function. As we will see in this article, this allows us to generate samples from the probability distibution $p(x_1,...,x_N)$ *without explicity knowing what it is!*. 
This fundamental idea was discovered by several people around the turn of the millenium, and underlies all modern generative models. 

In order to fully exploit this idea, we need to overcome another weakness with the Boltzmann machine: The fact that it was restricted to using energy functions that are described by quadratic order interactions between nodes, and
one way to create a more powerful EBM would be by using more sophisticated energy functions. The modern theory of artificial neural networks or ANNs comes to the rescue here, since it provides us with a way to create very sophisticated parametrized functions that can be used to approximate arbitrarily complex functions. 
The parameters of the ANN play the role of interaction strengths in the original Boltzmann machine and moreover they can be estimated by using the powerful backprop algorithm.
Using this idea it becomes possible to replace the quadratic energy function in the Boltzmann machine, with an ANN which can potentially have hundreds of millions of parameters and this results in an enormous increase in the modeling power of the resulting EBM. This also enables modern EBMs to piggyback on the advances in ANNs in recent years with powerful models such as convolutional neural networks (CNNs) and transformers.

Note that by basing the EBM model directly on the energy function, we no longer need to specify the interaction strengths between nodes. This is a benefit since it opens the door to complex models, however at the same time we loose touch with physical picture of nodes interacting with one another. This raises 
the question whether these modern EBMs are still biologically plausible. I will have a few remarks to say on this topic in the next section.

In order to design modern EBMs there are two problems that have to be solved:

- How to sample from these EBM models since clearly the Gibbs sampling used in classical Boltzmann machines no longer applies.
- How to train these EBM models, since the Contrastive Divergence or CD algorithm used in Boltzmann machines cannot be used anymore.

I am going to spend the the bulk of this article talking about proposed solutions to these problems, so lets get into the next level of detail.

The first issue was resolved with the introduction of Langevin based Monte Carlo Markov Chain (MCMC) sampling. This enabled the system nodes to have real valued state, and these were updated using an iteration that caused the state to converge to values distributed according to a specified probability distribution. The origins of Langevin sampling lie in the theory of stochastic differential equations, and I touched upon this topic in [my article on Brownian Motion](https://subirvarma.github.io/GeneralCognitics/2025/05/23/TamingRandomness.html). 
Once we use Langevin sampling, it becomes possible to handle energy functions that are more complex than quadratic, indeed it becomes possible use arbitrarily complex energy functions such as those modeled by CNNs and transformers.

There also has been progress in training algorithms for EBMs. Hinton's original algorithm for training Boltzmann Macines was based on the concept of maximizing the likelihood function for the training data (or equivalently minimizing the KL divergence between the training data distribution and the model provided distribution). This algorithm runs into the problem that it requires an estimate of the partition function, which has traditionally been a difficult task. Hinton tried to resolve this problem with the contrastive divergence (CD) algorithm, however it still runs into scaling problems in model sizes larger than a few hundred nodes. 

The resolution to this problem required some fundamental advances in theory, and interestingly enough the core idea that finally solved it is related to the idea of simulated annealing that was described in Part 1. It was recognized that the problem had to do with the inefficient sampling of multi-modal distributions, and the solution involved mixing Gaussian noise to the state vectors in order to make the distribution closer to unimodal. More important was the idea of introducing this noise at various levels of intensity and then gradually reducing it from high to low values during the sampling process. It was shown that this indeed solved the multi-modality problam and led to model outputs that are currently the state of the art in image generation. These models generally go by the name of diffusion models and can be considered to be the modern versions of the Boltzmann Machines with upgraded energy functions and training algorithms.

All these advances in EBM models are impressive, but is there any fundamental benefit to using them over non-EBM models since it seems that both types of models are equally good at various tasks. The current generation of non-EBM models are based on the backprop algorithm for training, and this can be considerably accelerated with the help of GPUs. However this comes with the issue of sky-rocketing energy consumption for large model sizes which has become a major problem. If EBM models can be engineered for lower energy consumption then this would constitute a major benefit. Since EBM models are based on the operation of Gibbs or Langevin sampling they are not able to enjoy the same acceleration with the use of GPUs as backprop driven non-EBM models. However if the hardware substrate on which these systems run is optimized for the sampling operation then it can potentially lead to huge savings in energy consumption. There are a number of efforts underway in this direction and we will describe a couple of them:

- A startup called Normal Computers has been working on silicon based chips that can be used to accelerate Langevin sampling.
- Extropic is another startup which is trying to make a chip that can be used to acclerate the Gibbs sampling used in Boltzmann machines.

These and similar systems belong to the category of analog computers and are based on the idea of using the physical properties of the substrate on which the chip is built to aid in the sampling process. So for example in the Extropic system, the states of all the nodes in the Boltzmann machine can be updated in parallel in a single cycle, rather then in a serial node by node basis used in digital implementations.
These systems are still in the research phase and they have a long way to go until they can approach the performance of digitally implemented EBM systems.

The holy grail of modern generative systems are LLMs, and the question arises whether EBMs can be used to implement LLMs. The current generation of LLMs are based on auto-regressive sampling using transformers, and generate one word at a time. It turns out that diffusion models can also be used to generate text, which clears the path to using EBM based diffusions to generate text. Stefano Ermon has founded a start-up called Inception that is working on diffusion based LLMs. These are still implemented in traditional GPU based architectures, and their selling point is faster text generation compared to auto-regressive models (as opposed to lower energy consumption).

There is another branch in modern EBM work called Thermodynamic Computing  which derives its inspiration from the original Hopfield network as opposed to the Boltzmann machine. Recall that the Hopfield network generated specific state configurations as opposed to sampling from the distribution of the configurations, and potentially can be used as a computational tool. This was actually pointed out by Hopfield himself, who showed how combinatorial optimization problems such as the Travelling Salesman Problem can be mapped on to the Hopfield network. This work has been updated by research groups at Purdue University and UCSB, who have shown how Hopfield networks can be scaled to much larger sizes, using both theoretical advances such as more efficient sampling techniques, as well new hardware devices that can implemenent this sampling more efficiently. This work is also in its research phase at the present time, and its main driver has been to serve as an alternative to quantum computers for implementing probabilistic algorithms.


## EBMs with ANN Based Energy Functions

![](https://subirvarma.github.io/GeneralCognitics/images/stat54.png) 

Figure 1: Computing the energy functions for EBMs

The original Ising model for paramagnetism featured a simple energy function, shown in part (a) of the above figure. The interaction strength between nodes was uniform across the entire network, and this resulted in an energy landscape with a couple of minima corresponding to net magnetization of the system. Sherrington and Kirkpatrick modified this model by making the interaction strengths random, and also allowed each node to interact with every other node in the system, shown in part (b). This led to a complex energy landscape with a large number of minima that scaled up with the number of nodes.
The SK model was subsequently used by Hopfield and Hinton to create the first computational and generative models, namely the Hopfield network and the Boltzmann machine, as described in Part 2 of this article series. 

A way for EBMs to transition to the modern era is shown in the lower part of the figure. Part (c) shows an energy function that is described by convolutional neural network or CNN which were originally introduced as a way to process images. Part (d) of the figure shows an EBM that uses the transformer network for computing energy functions. Transformers are a powerful way to model energy functions, traditional auto-regressive LLMs use them as a way to sample from conditional probability distributions. 
Note that neither of the EBMs in the lower part of the figure show inter-node interaction strengths, presumably these exist but are much more complex than the ones in the upper part of the figure. 
In the original EBMs shown in parts (a) and (b), the energy function was parametrized by the interaction strengths between nodes, 
on the other hand, if we use either a CNN or transformer (or any other ANN) to model the energy function, then the energy function is parametrized by the weights in the ANN. 
Indeed the modern theory of EBMs is based entirely on the energy functions, which can be as complex as we wish, as long as they can be represented by a neural network.

Whether we use inter-node interactions or we use a ANN to model the energy function, in either case the probability of the system being in state $(x_1,x_2,...,x_N)$ is given by

$$ p_W(x_1,x_2,...,x_N) = {e^{-E_W(x_1,...,x_N)}\over{Z}} $$

where $Z$ as usual is the partition function

$$ Z = \sum_{x_1,...,x_N} e^{-E_W(x_1,...,x_N)}  $$

There are two differences compared to older EBMs

- The state variables $(x_1,...,x_N)$ are no longer restricted to $+1,-1$ but can take on any real value.
- The energy function $E_W(x_1,...,x_N)$ is described by a neural network whose input is $(x_1,...,x_N)$ and has parameters given by the vector $W$.

Since a neural network can be trained to approximate arbitrarily functions, it follows that the new EBM is capable of modeling a much wider variety of energy
landscapes. 
The new design raises the following questions:

- How can we sample from these networks, since Gibbs sampling clearly cannot be used here.
- How do we train these networks? Do Contrastive Divergence (CD) type algorithms still work?

The first question is answered in the next section in which we introduce a powerful MCMC type sampling algorithm called Langevin sampling. The answer to the training
question is more involved and occupies the following sections. 
The problem that we need to solve is that of choosing the parameters $W$ such that the probability distribution $p_W(x_1,x_2,...,x_N)$ given by the model is close to the training data distribution $p(x_1,x_2,...,x_N)$. 
Not only do we have to come up with training schema that applies to more complex energy landscapes, but the new algorithm also has to avoid the issues that plagued the older Boltzmann Machine system, namely that they and related systems could not be scaled beyond a few thousand nodes since the computational cost of sampling became excessive. This problem has to do with the difficulty in sampling from a multi-model landscapes, as illustrated in figure 1.


### Using EBMs to Generate Images

![](https://subirvarma.github.io/GeneralCognitics/images/stat56.png) 

Figure 2: Image generation using EBMs

The above figure gives a high level overview of how EBMs can be used to generate images. In this case the nodes in the EBM correspond to pixels in the image. 
Given a training data distribution consisting of a bunch of images, we will assume that the pixels in an image follow a Boltzmann distribution
$p(x_1,...,x_N)={e^{-E(x_1,...,x_N)}\over{Z}}$ for some unknown energy function $E(x_1,...,x_N)$. We can consider that the pixels in the image are 'interacting' with each other, which results in the interaction energy $E(x_1,...,x_N)$, and ultimately the interactions settle down to an equilibrium in which the distributon of the pixels is given by the Boltzmann distribution. Thus the equilibrium state, which is that of lowest energy, also corresponds to states that result in images that look like those from the training dataset.

The right hand side of the figure shows an EBM model with energy function $E_W(x_1,...,x_N)$, and if we can train the model so that $E_W(x_1,...,x_N)\approx E(x_1,...,x_N)$, then the model should be able to generate images by sampling, and these images should look like they came from the training dataset. It is easier to approximate the score functions instead,
defined as ${\partial E_W\over{\partial x_i}}\approx {\partial E\over{\partial x_i}}$, and we will show later that we can sample from the model from a knowledge of the score function alone. Image generation using EBMs is based on this idea of training the model so that it approximates the score function of the training data, and new images are generated by sampling from the model until it settles into an energy minima.

### Text to Image Generation

![](https://subirvarma.github.io/GeneralCognitics/images/stat58.png) 

Figure 2: Variation of energy functions depending on the textual context 

Hence the process of generation is like a ball rolling downhill in a hilly landscape, but how does it find the right valley to settle into?
In other words, how can we specify what image to generate? 
This is the province of text to image models which turn a textual description into the corresponding image. Image to image models or text to text models (also called LLMs) also fall into this class, hence it constitutes a very important class of AI models. 

These models can be understood as minimzation of the energy function $E_{W}(x_1,...,x_N, c)$ where the variable $c$ is the latent vector representing the textual description.  During inference sample images are generated by starting from a text description $c$ and a random state $(x_1,...,x_N)$, and then using the multistage sampling process to find the configuration that has the minimum energy. Each value of the text $c$ can led to multiple possible generated images, depending upon our choice of the initial random state configuration. 

For a given context $c$, the energy $E_W(x_1,...,x_N)$ forms a function with multiple minima, such that each minima corresponds to images similar to those in the training set, just as before (see above figure). However the presence of the context means that all these images are constrained by it. For example if the context is "Images of dogs jumping over a fence" then the energy landscape with be limited to state configurations that correspond to this text.


### Generative EBMs as Models for Biological Brains

This section consists of some speculation on my part on the subject whether the recent progress in EBMs can shed any light on the processing that goes on in our brains.
Both our brains and the latest generation of ANNs seem to be doing similar things, but efforts to find ANN type mechanisms in the brain have not yielded much success so far.
The brain itself has billions of neurons with trillions of connections between them, which is collectively referred to as the connectome. There are efforts underway to map the connectome to see whether it can offer some insight, but given the enormity of the task, the progress has been very slow. There has been one significant success though: Around 1960 the neuroscientists Hubel and Wiesel were able to map the circuitry that led from a cat's eye to its neural cortex, and twenty years later this work served as the inspiration for the design of convolutional neural networks or CNNs. However no such neural structures have been found that are similar to the transformer architecture, and nor is there any evidence that the brain uses a backprop like algorithm for training its neurons.

In my opinion looking for signs of transformers or backprop in the brain is probably not the right way to approach the problem. It is more likely that the brain operates using EBM principles since these are firmly grounded on the physics of how a large number of nodes can interact with one another and create emergent behaviors. The interconnect topology between neurons is exteremely complex and it is quite likely that its explanation will lie outside human comprehension for the forseable future. However EBM theory tells us that what is important is not the interconnect toplogy, but the resulting energy function that results from the interactions. Indeed the properties of the energy function determine the information stored in the EBM and how it can retrieved. So perhaps this provides a clue that instead of trying to exactly map the connectome, we should be studying the brain at the level of its energy function instead. Even more interesting is the speculation that transformers don't serve as a model for the connectome, but instead are really models for the energy function that emerges from the connectome. 

But what about training, since there is no evidence of backprop in the brain? It is quite likely that training happens using a sampling type of algorithm of the type that Hinton used for Boltzmann machines. These algorithms can be connected back to the synaptic learning rule that McCulloch and Pitts proposed back in the 1940s. If this indeed were to be the case, this would also explain why our brains are much more energy efficient than the current generation of ANNs, since thermodynamic based sampling can exploit the physics of the substrate, and thus can be faster as well as energy efficient.

![](https://subirvarma.github.io/GeneralCognitics/images/stat60.png) 

Figure 2: A Model for Biological Brains 

With these ideas in mind, the above figure shows a proposed architecture for part of the brain that results in visual images that we see.
The image that see in front of us does not really exist in reality, in fact it is internally generated by our mind (for more on this topic read my article [What would Kant think of LLMs](https://subirvarma.github.io/GeneralCognitics/2024/07/02/Kant-and-LLMs.html)). I am going to assume that there is a set of neurons in our brain whose state $(x_1,...,x_N)$ corresponds to an image that we see, lets call them the vision neurons. The process by which the vision neuron state actually gets converted into an image is a deep mystery into which there is no insight at the present time, also called *the hard problem of consciousness*. 
I am proposing that the vision neurons have a dense interconnection architecture of the spin glass type, and furthermore the multiple minima of its resulting energy function $E_W(x_1,...,x_N)$ correspond to states of reality in the external world. 

But how does the brain correlate the external reality with the state of the vision neurons, in other words how does it make sure that the image that it generates bears some correspondence to what is actually happening in front of us? 
A possible mechanism by which this is done is as follows, this is inpired by the text to image models discussed in the previous section: The light impinging on our retina leads to neuronal signals that are processed using the CNN like structure that Hubel and Wiesel discovered. This results in the signal getting converted into a configuration of neurons, lets call it the context $c$. These context neurons then interact with the vision neurons to create the energy function $E_W(x_1,...,x_N,c)$, and the resulting minima of this energy function results in a configuatrion of vision neurons that correspond to what we see. Hence in some sense most of the information in the image that we see is already strored in the vision neurons of our brain, the sparse signals coming to our eyes merely serve as a pointer to choose the correct configuration.

This mechanism also serves as a way in which we can conjure up images even with our eyes closed.  There are portions of our brain that store memories, mostt likely in the hippocampus. The neural configurations of these memories can also serve as the context vector $c$ that triggers the vision neurons to create images for us. 

Just like for images, there is perhaps a corresponding part of the brain that is reponsible for generating language, lets call it the language neurons. This comes with its own interconnection topology and energy function $E_W(x_1,...,x_N)$. The minima of this energy function correspond to words and sentences. But how does the brain decide what to speak? 
This leads to the idea of a context $c$ which controls the language output by controlling the minima that the energy function settles into. In this case the context can be one of several things:

- The context can be something that was uttered a moment ago, which results in a continuation of the thought.
- The context can be an image, so for example image to language conversion.
- The context can be just pure thought which may be non-verbal in nature. Clearly there have been cases in which a child bought up in the wild without access to language is nevertheless able to think and carry out intelligent actions.

These speculations lead to the idea that we can create a model of the brain by creating a dense interconnect network whose energy function corresponds to a transformer. But what does this interconnect pattern look like? This seems to be an open question at present, but it is not an insurmountable one, and I expect to see progress in this area in the coming  years.
Clearly the interactions are more complex than the two node interactions in a spin-glass type model, and involve multiple nodes interacting with one another, and thus closer to the P-Spin or PSM type models described in Part 1. Are these more complex interactions biologically plausible? Interactions between biological neurons seem to be of the two node type, however one way to reduce higher node interactions to two node interactions is by introducing hidden nodes into the model, as first pointed out by Krotov and Hopfied. 

After all this speculation, lets get down to the nuts and bolts of how modern EBMs work, and we will start with Langevin sampling followed by training algorithms.

## MCMC Sampling Using the Langevin Equation

Early EBMs from the 1980s, such as the Boltzmann Machine, feature relatively simple energy functions

$$  E_W = -\sum_i\sum_{j\lt i} w_{ij} \sigma_i\sigma_j - \sum_i b_i \sigma_i $$

where $\sigma_i$ is the spin at node $i$, which can take values ${+1,-1}$, $w_{ij}$ is the symmetric strength of the interaction between nodes $i$ and $j$ and $b_i$ the threshold for activating node $i$. The spins in these networks are updated using Gibbs sampling

$$ p(\sigma_k = 1\vert \sigma_1,..,\sigma_{k-1},\sigma_{k+1},...,\sigma_N) = p_k = {1\over{1 + e^{-\beta h_k}}} $$

where $h_k = \sum w_{ki}\sigma_i + b_k$. 
Repeated sampling results in the network state gradually moving to an equilibrium configuration which corresponds to a local minima for the energy function.
Gibbs sampling only works if we are able to compute this conditional probability, if the energy function is modeled by an ANN then clearly this procedure no longer holds. 

The discrete time Langevin equation is given by the iteration

$$ x^i_{n+1} = x^i_n -\eta {\partial \log p_W(x^1,_n,...,x^N_n)\over{\partial x^i_n}} +\sqrt{2\eta}\epsilon_n,\ \ n = 0,1,2,...  $$

Using vector notation this can also be written as

$$ X_{n+1} = X_n -\eta \nabla_x \log p_W(X) +\sqrt{2\eta}\epsilon_n,\ \ n = 0,1,2,...  $$

where $X_n = (x^1_n,...,x^N_n$ is the state vector and $\nabla = ({\partial\over{\partial x^1_n}},...,{\partial\over{\partial x^N_n}}$ is the differential operator,  at the $n^{th}$ step. 
$X_0$ is usually initialized from the Gaussian distribution, $\eta>0$ is the step size and the noise vector $\epsilon_n$ is distributed according to $N(0,I)$. It can be shown that in equilibrium, the disttribution of $X_n$ converges to $p_W(X)$  exponentially fast as $n\rightarrow\infty$. Since we want the distribution $p_W(X)$ to converge to the Boltzmann distribution, lets substitute this into the equation, which results in

$$ X_{n+1} = X_n -\eta \nabla_x E_W(X) +\sqrt{2\eta}\epsilon_n,\ \ n = 0,1,2,...  $$

The first two terms on the RHS of this equation are just the Newton method for finding the vector $X$ at which the function $E_W(X)$ is minimized (or equivalently the probability $p_W(X)$ is maximized), while the third term adds some noise to the process. Hence the overall effect is that of moving the system state to regions of higher probability, while the noise term enables the iteration to ocassionally jump out of local minima so that there is a greater probability that the iteration ends near a deeper minima.

The beauty of the Langevin diffusion is that enables us to generate samples from the distribution $p_W(X)$ without having to explicitly compute the partition function $Z$ or even the energy function $E$, all that we need are estimates of the score function ${\partial E\over{\partial x_i}}$. This frees us from the necessity of relating the energy function back to the inter-node interactions and enables us to sample from arbitrarily complex energy functions. Note that unlike the Gibbs equation the Langevin also applies to the case the states $x^i_n$ are any real nunber.
Although not very well known, the Langevin diffusion is probably the most important equation in the modern theory of generative models.

## Training EBMs with Complex Energy Functions

Given a training dataset consisting of a collection of images, we will start with the problem of training a model that generates new images that look similar to those in the training set. We will assume that the distribution of pixels in the training dataset is given by the (unknown) Boltzmann distribution

$$ p(x_1,x_2,...,x_N) = {e^{-E(x_1,...,x_N)}\over{Z}} $$

Our EBM model in turn, has an equilibrium distribution given by its own energy function

$$ p_W(x_1,x_2,...,x_N) = {e^{-E_W(x_1,...,x_N)}\over{Z}} $$

In order to make the generated images similar to those in the training set, we want to choose the model parameters $W$ so that
$p(x_1,x_2,...,x_N)\approx p_W(x_1,x_2,...,x_N)$. This was the approach taken by Hinton and Sejnowski in their training algorithm for the Boltzmann machines, and they showed that the problem reduces to finding the maximum likelihood estimates of $W$. This approach runs into the problem of estimating the partition function $Z$ which in general is a difficult one to solve.
We will pursue this approach in the next section, but for now we we will describe a more modern approach which avoids the estimation of $Z$ and is based on approximating the energy function so that
$E(x_1,...,x_N)\approx E_W(x_1,...,x_N)$. This would seem to be a straightforward application of supervised learning if we knew $E(x_1,...,x_N)$, unfortunately
that is not the case. For Langevin sampling we don't need $E_W$, but do need the score function, so perhaps we should be seeking the approximation
${\partial E_W\over{\partial x_i}}\approx {\partial E\over{\partial x_i}}$. This results in the problem of choosing the $W$ to minimize the score matching error, also called the Fischer divergence, given by 

$$ L_{SM}(W) = {1\over 2} E_{p(X)}\vert\vert\nabla_x \log s_W(X) - \nabla_x \log p(X)\vert\vert_2^2  $$

where $X=(x^1,...,x^N)$ and the score given by $s_W(X) = \nabla_x p_W(X)$$. 
This approach can be made to work, as first pointed out by Hyvarinen and Dayan, but however runs into the computational problem of computing second order derivatives or the trace of Jacobian during the training process.

The critical advance was made by Vincent in 2011 which he called denoised score matchin or DSM and the critical idea was that of introducing noise into the training process. Vincent noted that the problem with minimizing $L_{SM}$ is due to the intractibility of $\nabla_x\log p(X)$. He proposed injecting noise into the data samplex $X$ via a known conditional distribution $p_\sigma(X'\vert X)$ with scale $\sigma$. We then try to approximate the score of the noisy samples by minimizing the loss function

$$ L_{SM}(W,\sigma) = {1\over 2} E_{p(X')}\vert\vert\ s_W(X';\sigma) - \nabla_{X'} \log p_{\sigma}(X')\vert\vert_2^2  $$

where the distribution of the noisy sample is given by

$$ p_{\sigma}(X') = \int p_{\sigma}(X'\vert X) p(X) dx $$

Vincent showed that even though $\nabla_{X'} \log p_{\sigma}(X')$ is intractable, it can be replaced by a tractable objective by conditioning on the distribution $p(X)$ of the original data samples, which results in the Denoising Score Matching (DSM) loss given by

$$ L_{DSM}(W,\sigma) = {1\over 2} E_{p(X),p(X'\vert X)}\vert\vert s_W(X';\sigma) - \nabla_{X'} \log p_{\sigma}(X'\vert X)\vert\vert_2^2  $$

Vincent showed that the value of $s_W$ that minimizes $L_{DSM}$ satisfies the equation

$$ s^*(X';\sigma) = \nabla_{X'} \log p_{\sigma}(X') $$

which the same $W$ that also minimizes $L_{SM}$. When the noise level $\sigma$ is small $s^*(X';\sigma) \approx \nabla_{X} \log p_{\sigma}(X)$, so that taking a small step along the noisy score direction $s^*(X';\sigma)$ moves a noisy sample in roughly the same direction as a clean sample, which is the intuition behind why this technique works.

For the special case when $p_{\sigma}(X'\vert X)$ is Gaussian noise with variance $\sigma^2$ so that

$$ X' = X + \sigma\epsilon $$

where the noise vector $\epsilon$ is distributed according to $N(0,I)$$, so that

$$ p_{\sigma}(X'\vert X) = N(X'; X, \sigma^2 I)$$

where $I$ is the identity matrix. It can be shown that

$$ \nabla_{X'}\log p_{\sigma}(X'\vert X) = {X-X'\over{\sigma}} $$

thus making the minimization of $L_{DSM}(W,\sigma)$ computationally feasible. The DSM loss simplifies to

$$ L_{DSM}(W,\sigma) = {1\over 2} E_{p(X),p(X')}\vert\vert s_W(X';\sigma) - {X-X'\over{\sigma}}\\vert\vert_2^2  $$

$$ = {1\over 2} E_{p(X),\epsilon}\vert\vert s_W(X+\sigma\epsilon;\sigma) + {\epsilon\over{\sigma}}\\vert\vert_2^2  $$

Estimating $W$ my minimizing $L_{DSM}$ is a straightforward regression problem. The final step is to make the noise level $\sigma$ go to zero, so that

$$ \nabla_{X'} \log p_W(X') \approx \nabla_{X} \log p(X)  $$

and the two score functions match.

### Noise Conditional Score Networks (NCSN)

![](https://subirvarma.github.io/GeneralCognitics/images/stat61.png) 

Figure 2: Illustration of a NCSN

The DSM algorithm has some shortcomings; in complex high dimensional energy spaces with lots of saddle points where the score function is close to zero, the Langevin iteratiom can stuck in sub-optimal regions. Even if it eventually manages to get out, it can take a long time to converge. The solution to this problem was proposed by Song and Ermon, and is basically a version of the simulated annealing algorithm that was described in Part 1. Recall that simulated annealing worked by starting the optimization at a high temperature so that the iteration had enough energy to jump out of shallow local minima and saddle points, and then gradually reducing the temperature to allow it explore deeper regions within larger valleys. Song and Ermon proposed a similar mechanism for DSM, where the noise was varied not through temperature, but by varying the variance $\sigma$.

The NCSN algorithm is illustrated in the above figure. During training noise is injected at multiple levels $\sigma_1,...,\sigma_L$, where $\sigma_1<\sigma_2<...\sigma_L$, and the idea is to train a
score model $s_W(X,\sigma)$ that works for all $\sigma\in {\sigma_1,...,\sigma_L}$.
The NCSM objective is given by

$$ L_{NCSM}(W) = \sum_{i=1}^L \lambda(\sigma_i) L_{DSM}(W,\sigma_i)  $$

where

$$ L_{DSM}(W,\sigma) = {1\over{2}}E_{P(X),P(X'\vert X)}[\vert\vert s_W(X',\sigma) - {X-X'\over{\sigma^2}}\vert\vert^2_2 $$

where $\lambda(\sigma_i)$ is a weighing function for each noise level. Minimization leads to a score model $s^{*}(X,\sigma)$ that can be used at at each noise level to recover the true score $\nabla_X\log p_{\sigma}(X)$ for all $\sigma\in\{\sigma_i}_{i=1}^L $.

During the inference process, we start with a pure random sample $X_0$ distributed according to $N(0,I)$, and then Langevin iteration is applied successively at each noise level $\sigma_l$ to sample from the distribution $p_{W}(X';sigma_l), l=L,L-1,...,1$. At each level the algorithm is iterated $K$ times, and the output from level $\sigma_l$ is used to initialize the next lower level $\sigma_{l-1}$. The iteration at the l^{th}$ level is given by

$$ X_{n+1} = X_n + \eta_l s_W(X_n,\sigma_l) + \sqrt{2\eta}\epsilon_n $$

![](https://subirvarma.github.io/GeneralCognitics/images/stat63.png) 

Figure 2: A single step of the denoising process using Langevin sampling using the score estimate

A single step of the de-noising process is ilustrated above.
The complete inference algorithm is given below (from Song and Ermon)

![](https://subirvarma.github.io/GeneralCognitics/images/stat62.png) 

Figure 2: Illustration of NCSN

## Training Using MCMC Sampling

The score based technique described in the previous section was able to generate images which are currently the state of the art in the field. However it does come with issue that it uses feedforward ANNs such as CNNs and transformers as function approximators in order to do this. This contrasts with the earlier Boltzmann machine based image generation models whose operation was entirely based on the sampling operation. 
It would be nice if there was a way to equal the performance of the score based technique, while basing it entirely on Langevin or Gibbs sampling type operations, and without the use of feedforward ANNs.
This will open the door to avoiding the backprop algorithm for training, and potentially much more energy efficient systems. It also brings us one step closer to modeling the brain, since both it and sampling based models obey the principles of free energy minimization from thermodynamics.

### The Maximum Likelihood (MLE) Algorithm

As before let $p(X)$ and $p_W(X)$ be the probability distributions for the training examples and the model repectively. Since it is an EBM, we can write $p_W(X0$ as

$$ p_W(X) = {e^{E_W(X)}\over Z_W}$$

where $X$ is a vector $X=(x^1,...,x^N)$ and the partition function is given by $Z_W = \int e^{E_W(X)} dX$ as usual. 
Assuming we are given $m$ training samples $X_1,...,X_M$, 
in order to learn this model using MLE, we have to maximize the log-likelihood function given by

$$ L(W) = {1\over M}\sum_{i=1}^M \log p_W(X_i) = E_{p(X)}[\log p_W(X)]  $$

This can be written as

$$ L(W) =  -{1\over M}\sum_{i=1}^M E_W(X_i) - \log Z_W $$

The maximization can be done by using the gradient ascent algorithm, but in order to do this we need to estimate $\nabla_W L(W)$ which can be done using the following steps.
First differentiation $p_W(X)$ leads to

$$ \nabla_W\log p_W(X) = \nabla_W E_W(X) - \nabla_W \log Z_W $$

It can be shown that

$$ \nabla_W \log Z_W = E_{p(X)}[-\nabla_W E_W(X)] $$ 

so that

$$ \nabla_W\log p_W(X) = \nabla_W E_W(X) + E_{p(X)}[-\nabla_W E_W(X)]  $$

It follows that

$$ \nabla_W L(W) = -E_{p(X)}[\nabla_W E_W(X)] +  E_{p_W(X)}[\nabla_W E_W(X)] $$

The first term decreases the energy for data points that belong to the training set, while the second term increases the energy for data samples that are generated from from the model. 
This is basically a rederivation of the Boltzmann machine training algorithm, with the exception that $E_W(X)$ is restricted to be quadratic and also $X$ is no longer to the values 0 and 1.
In the Boltmann machine case the derivative simplifies to the average correlation between nodes, which can be understood to be a type of Hebbian learning, thus making is biologically plausible.
For the case when $E_W(X)$ is a expressed by a ANN such a transformer or a CNN, this derivative can be computed using the backprop algorithm.
Note that unlike for the score matching algorithm, we are tryingto estimate the parameters of the energy function $E_W(X)$ directly, rather than the score $\nabla_W E_W(X)$.

Recall that in Part 2 we showed that for the Boltzmann machine the gradient for the loss function is given by

$$ {\partial L(W)\over{\partial w_{ij}}}  = \beta (<\sigma_i\sigma_j>_{data} - <\sigma_i\sigma_j>_{model}) $$

This is a special case for the more general equation above, and can be recovered by noting that the energy function for the Boltzmann machine is given by

$$  E = -\sum_{i}\sum_{j\lt i}w_{ij}\sigma_i\sigma_j - \sigma_{i}\sigma_i b_i $$

This MLE based technique hinges on getting samples from the model which are distributed according to $p_W(X)$ and since we can no longer use Gibbs sampling, we resort to using Langevin sampling instead

$$ X_{n+1} = X_n - {\eta\over 2}\nabla_W E_X(X_n) +\sqrt{\eta}\epsilon _n $$

where $\epsilon_n$ is drawn from a normal distribution $N(0,I)$. The gradient $\nabla_W E_W(X)$ can be computed using backprop for ANN based energy functions.

This algorithm suffers from the same issues that plagued the Boltzmann machine and led to long sampling times thus limiting its scalability to few hundred nodes at most.
Gap, Song et.al. proposed a way to get around this problam, and this is covered in the next section.

### The Diffusion Recovery Likelihood (DRL) Algorithm

The DRL method is also used on the idea of injectine noise at various levels, just as for the NCSN algorithm used with score matching. 
Before we describe this, lets look at MLE for the case when the data samples $X_i$ are perturbed by Gaussian noise so that

$$  X' = X + \sigma\epsilon $$

where as before $\epsilon$ is distributed according to $N(0,I)$. If $p(X)$ follows the Boltzmann distribution, then using Bayes rule it can be shown that the conditional probability $p(X\vert X')$ is distributed according to

$$ p(X\vert X') = {1\over Z'_W} e^{-E_W(X) - {1\over{2\sigma^2}}\vert\vert X'-X\vert\vert^2} $$

where $Z_W = \int e^{-E_W(X) - {1\over{2\sigma^2}}\vert\vert X'-X\vert\vert} dX$ is the partition function for the conditional EBM. The extra quadratic term makes the resulting energy landscape to be localized around $X'$, thus making it less multi-modal and easier to sample from. When $\sigma$ is small, the conditional distribution is approximately single mode Gaussian.

We can define a maximum likelihood function $J(W)$ for the conditional distribution, given by

$$ J(W) = {1\over M}\sum_{i=1}^M \log p_W(X_i\vert X'_i) $$

and the objective is to recover the clean sample $X_i$ from the noisy sample $X'_i$ by maximizing this likelihood. It can be shown that the corresponding Langevin sampling is given by

$$ X_{n+1} = X_n - {\eta\over 2}[[\nabla_X E_W(X_n) + {1\over{\sigma^2}}\vert\vert X'_n-X_n\vert\vert^2] +\sqrt{\eta}\epsilon _n $$

It can be shown that given enough data, maximizing $J(W)$ leads to unbiased estimates of the parameters $W$ (see Appendix A2 in Gao, Song et.al, for a proof).

Since the recovery likelihood method described above works well only well the noise level $\sigma$ is small, we can use the same trick as in the NCSN algorithm, and learn a sequence of recovery likelihoods, each of which has a small noise level. In order to do this, a data sample $X(0)$ is perturbed in a sequence of steps to create noisy samples $X(1),...,X(T)$ given by

$$ X(t+1) = \sqrt{1-\sigma^2(t+1)} X(t) + \sigma(t+1)\epsilon_{t+1},\ \ t=0,1,...,T-1 $$

Defining $Y(t) = \sqrt{1-\sigma^2(t+1)} X(t)$, we get a sequence of conditional EBMs

$$ p(Y(t)\vert X(t+1)) = {1\over{Z'_W(X(t+1),t)}} e^{-E_W(Y(t),t) -{1\over{2\sigma^2(t)}} \vert\vert X(t+1)-Y(t)\vert\vert^2}\ \ \ \ t=0,1,...T-1 $$

where $E_W(Y(t),t)$ is defined by an ANN conditioned on $t$. 

The expression for the gradient of the loss function becomes

$$ \nabla_W L(W) = -E_{p(Y\vert X)}[\nabla_W E_W(Y)] +  E_{p_W(Y\vert X)}[\nabla_W E_W(Y)] $$

The $Y$ sample is drawn from the training data for the first expectation, while it is drawn from the distribution defined by the model with parameters $W$, for the second expectation. In both cases the distribution from which $Y$ is drawn is a conditional distribution, given some value $X$.

The corresponding Langevin sampling of the conditional distribution is given by

$$ Y^{r+1}(t) = Y^r(t) - {\eta\over 2}[[\nabla_Y E_W(Y^r(t),t) -  {1\over{\sigma^2(t)}}\vert\vert X(t+1)-Y^r(t)\vert\vert^2] +\sqrt{\eta}\epsilon _n,$$

We then follow the conditional probability recovery algorithm that was just described, which results in the DRL algorithm.

![](https://subirvarma.github.io/GeneralCognitics/images/stat64.png) 

Figure 2: DRL Training and Inference algorithms

The DRL algorithm can be applied to the Boltzmann machine as well, this is discussed in the next section.

## Hardware Implementation of EBMs

We have shown that EBMs can be used to implement state of the art generative models, and this leads to the question of whether there is any particuler benefit in using them (vs traditional generative models).
Sara Hooker, an inginner at Google, published an interesting essay [The Hardware Lottery](https://arxiv.org/abs/2009.06489) a few years ago in which she pointed out the most dominant architecture at any point in time is a result of synergy between available hardware and the software that gets written to use it. This is particularly true in AI systems as recent history shows. Until about 2010 deep learning was one of the many approaches to AI, and it was not clear whic approach would win out. In 2012, Hinton's team showed that Praphical Processing Units or GPUs are very well suited for the backprop algorithm, and as a result it became possible to scale up the size of systems that could be trained using backprop by orders of magnitudes, thus resulting in the current AI wave. 
Unfortunately GPUs do not result in the same compute acceleration when used for EBMs, since the basic operation in EBMs is sampling. As we have seen for the case of Boltzmann machines, state updates using sampling is an inherently serial node by node update, which cannot be parallelized when implmented on traditional hardware (unless we resort to architectures such as the Restricted Boltzmann machine or RBM).

Then the question arises if we can design an equivalent of a GPU for EBMs, i.e., an hardware architecture that is specialized to accelerate sampling, and thus enable us to scale EBMs to a large number of nodes.
We will look at a few approaches for doing this that is beinng pursued by start-ups and university labs. This field is in its enfancy, and current systems still have a long way to go before they can approach the performance of non-EBM systems. 

Is there any benefit of pursuing this line of work vs just sticking to GPU based systems? The holy grail is a potetntial decrease in energy consumption. GPU based systems are very energy intensive, and  it is often pointed out that biological EBM systems, such the brain, are able to do equivalent work with much lower power consumption. If the new EBM hardware implementations are able to approach state of the art performance with much lower energy consumption, then this will constitute a genuine advancement.

### Implentations of Boltzmann Machines: The Extropic System







### P-Bit Based Systems: UCSB, Purdue

Probabilistic bits




## Implemntation of the Langevin Equation: Normal Computing

Analog circuitry
