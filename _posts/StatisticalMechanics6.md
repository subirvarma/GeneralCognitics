---
layout: default
title: " An Energy based Language Model with Hierarchical Memory"
---

# An Energy based Language Model with Hierarchical Memory


## Introduction

This is the third in a series of papers for models of cognition based on the energy minimization principle. The first paper [Generative AI as an Effective Theory of Cognition](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html) proposed the Latent Energy based Predictive Processing or LEPP model for perception as a flow process on energy landscapes.
The following paper [A Hierarchical Energy-Based Model for Multimodal Cognition](https://subirvarma.github.io/GeneralCognitics/2026/08/07/statmech5.html) built on the LEPP model and proposed the Integrated Multimodal LEPP or IM-LEPP as a more detailed model for perception and language processing. In this paper we build on the IM-LEPP work with further details for the language processing module, in particular:

- The prediction module in IM-LEPP interfaces with the central ATL hub whose state gets updated with information coming in from other sensory modules, the amygdala, as well the main memory storage system. We supply the mechanism by which the contents of the memory storage are accessed and get incorporated into a resulting state that provides context for the generation of the next word.
- The next word prediction module in the IM-LEPP was based on the minimization of an energy function $E_W$. This process is laid out in more detail in this paper, and it involves an alternating process of memory access followed by energy minimization. We also propose some specific models for $E_W$.

All language models involve two basic operations: 

- Creation of a context state which serves as a conditional for next word prediction. This may involve memory access in order to create a suitable context.
- The next state prediction operation, which uses the context to estimate the latent value for the next word.

Context vectors in Transformer based LMs are generated using the self attention operation, and this operation is repeated over several layers. Context generation at the bottom layer is based on the input prefix and the transformers generated word output so far, while in the upper layers it is based on frozen latent representations of these inputs.
Self attention is engineered to dynamically focus on part of the context that is most relevant to the generation of the next word, by making the key and values a learnt function of the context (rather than the context itself). 
Transformers do next word prediction using their FFN network, which is a two stage fully connected feed forward system, and the parameters of this network function as a frozen (key,value) memory storage learnt during the training process. It has ben shown that the parameters of the first FFN stage encode the key values, while the parameters of the second stage encode the distribution of the values for a given key (see [Geva et.al.](https://arxiv.org/abs/2012.14913)). Note that this parametric memory is frozen after training, and is distributed across the multiple stages of the Transformer, in fact two-thirds of the parameters in a Transformer go into the FFN modules.
Even though Transformers have multiple stages, they use a single latent state representation across all the stages, and this state serves as a residual value that gets modified as the data flow progresses across the stages.

The proposed IM-LEPP language model differs from that of Transformers in the following respects:

- IM-LEPP features a latent state that is subject to modification during the process of prediction just as in Transformers. However unlike Transformers, this latent state also flows across successive word predictions. Transformers on the other hand use the generated word as a bridge between successive generations.
- IM-LEPP also generates a context vector that it uses for prediction, however this context is created from information that is stored in its memory. Hence the prediction module in IM-LEPP is decoupled from memory storage, and the two modules can evolve independently over time. For example new memories can be added using other sensory modalities such as vision or smell, and this is done using a process of continuous learning. In Transformers on the other hand, prediction and parametric memory are implemented in a coupled fashion in its FFN, and in order to incorporate more memory, the system has to undergo re-training. In other words memory in transformers is frozen at the time of training, while it is de-coupled from the prediction module in IM-LEPP, and can change continuously.
- The context vector in Transformers is generated using the input prefix as well as already generated text. IM-LEPP on the other hand summarizes the past in its state vector, hence its operation is closer to a recurrent neural network or RNN. However unlike a traditional RNN, IM-LEPP creates its context from not just its previous state, but also utilizes the entirety of its memory.
Humans clearly don't hold all of their past generations in their working memory while deciding on the next word, and it is thought that this information is captured in the system state aided by memory, which is closer to how IM-LEPP operates.


## The IM-LEPP Model

![](https://subirvarma.github.io/GeneralCognitics/images/stat170.png) 

Figure 1: The IM-LEPP Model

Notes for Figure 1:

- This is the figure from the previous paper, no changes.


![](https://subirvarma.github.io/GeneralCognitics/images/stat185.png) 

Figure 2: The IM-LEPP Language Module

Notes for Figure 2:

- I have added a loop for the prediction module, hence it is invoked K times
- Before the first invocation $zz_m(1)$ is sent to the ATL hub, where it is changes to $zzz'_m(1)$ using the predictive coding pipeline. This is then used to invoke items from memory (described in figure 3 below), and this results in a change in $zzz'_m(1)$ to $zzz_m(1)$.
- $zzz_m(1)$ is fed back into the prediction module to condition the minimization of $E_W(x;zz_m(1),zzz_m(1))$ which results in  $zz_m(2)$.
- $zz_m(2)$ is then fed back into the ATL hub to undergo another round of memory access etc, which in turn is fed back and results in $zz_m(3)$. This is repeated $K$ times, and the final value $zz_m(K) = xx_{m+1}$ is fed into the generation module to generate $yy_{m+1}$.
- The multiple loops through the prediction module have been put in to handle complex queries with intermediate outputs, it serves the same function multiple stages in a Transformer. It can be considered to be a thinking operation that the model engages in latent space, somewhat like the open loop operation described in the previous paper.


![](https://subirvarma.github.io/GeneralCognitics/images/stat190.png) 

Figure 3: Generating $zzz_n(i)$ at the ATL Hub using kNN based search and attention operations

- I have used a [Cowan](https://pmc.ncbi.nlm.nih.gov/articles/PMC2657600/) style memory classification for this module. Memories are stored as a pair $(zz_n,zz_{n+1})$, as key-value pair, provided $\vert xx_{n+1} - zz_{n+1}\vert$ exceeds some threshold.The idea here is that the next state $zz_{n+1}$ from the prior state $zz_n$ has a high surprisal value and hence gets stored. If a state similar to $zz_n$ is encountered again, then $zz_{n+1}$ can potentially be used to do prediction (similar to [Borgeaud et.al](https://arxiv.org/abs/2112.04426) or [Khandelwal et.al.](https://arxiv.org/abs/1911.00172)). In IM-LEPP all prediction are done using the $E_W$ module however, but a Khandelwal type prediction mechanism is something to think about.
- Items in long term memory are matched using L2 distance measure perhaps, with $k$ nearest neighbors sent to the STM.
- The short term memory is organized as per Cowan, with contents being flushed out periodically depending on how long they have been in there.
- Contents of the STM are used to run a traditional attention operation (as per Vaswani et.al), with learnt query, key and value vectors, with $zzz'_n(i)$ used for generating the query.

Note that I haven't used your idea of having a sequence of states stored  as a 'thought' in the memory. This may be more relevant to visual memory, what do you think?

Additional notes are in the figure.

![](https://subirvarma.github.io/GeneralCognitics/images/stat191.png) 

Figure 4: Memory Access + Prediction Stack

Shows operation of the prediction module for a two state prediction pipeline, ie.e, the case $K=2$. Has some similarities to the [Full Bandwidth Transformer](https://arxiv.org/abs/2608.08888). 
Should the different stages in the stack use the same set of parameters or should they be different? I am leaning towards using different set of parameters. If I use the same set of parameters, will this be equivalent to the Loop Transformer, with a loop length of one? Is this preferable?  I guess the benefit of adopting the same set of parameters is that we can make the number of stages $K$ variable as a function of level of difficulty. 

The other variable that can be adjusted is the number of diffusion stages within the prediction module. My current thinking is that the difficulty in language generation lies in getting hold of the right context to base the next word on. From this point of view, making $K$ variable is prefereable to making the number of diffusion stages variable.

Also what are the lessons of the Recirculation architecture by [Mozer et.al.](https://arxiv.org/abs/2608.17981)? My current thinking is that the lessons in Re-circulation may not apply here, what do you think?
Also is there a need for the residual connection? My intuition tells me that they are needed.

![](https://subirvarma.github.io/GeneralCognitics/images/stat187.png) 

Figure 5: Computation of the energy function $E_W$ 

This module can be implemented in one of several ways:

- Use a FFN, as in a Transformer.
- Use a 1D convolution.

Basically the module should be capable of processing a bunch of vectors as input and produce a scalar output. The FFN option is definitely more parameter rich which may be a plus.

## Types of Memory in the Brain





### Hierarchical Arrangement of Memory

- Based on Cowan paper


### Parametric Memory


### Object Level Memory


### Episodic Memory



## Modern Hopfield Networks for Storage



## Memory Use in Transformers




## An Hierchical Model for Memory

- Retrieval from a very large database (google deepmind paper) at Level 1
- Attention based retrieval at Level 2 (in ATL)
- Working Memory in the Prediction Module



## An Energy based Language Model

- Universal Transformers
- MoE design to Boost Parameter Count
- Variable Number of De-Noising Stages
