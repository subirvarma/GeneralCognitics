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
- The context vector in Transformers is created using the input prefix as well as already generated text using the attention operation. IM-LEPP on the other hand summarizes the past in its state vector, hence its operation is closer to a recurrent neural network or RNN. Humans clearly don't hold the entirety of past generations in their memory while deciding on the next word, and it is thought that this information is captured in the system state, which is closer to how IM-LEPP operates.

## The IM-LEPP Model

![](https://subirvarma.github.io/GeneralCognitics/images/stat170.png) 

Figure 1: The IM-LEPP Model

Notes for Figure 1:

- This is the figure from the previous paper, no changes.


![](https://subirvarma.github.io/GeneralCognitics/images/stat185.png) 

Figure 2: The IM-LEPP Language Module

Notes for Figure 2:

- I have added a loop for the prediction module, hence it is invoked K times
- Before the first invocation $zz_m$ is sent to the ATL hub, where it changes to $zzz_m$. This is then used to invoke items from memory (described in figure 3 below), and this results in a change in $zzz_m$ to $zzz'_m$.
- $zzz'_m$ is fed back into the prediction module to condition the minimization of $E_W(x;zz_m,zzz'_m)$ which results in  $xx_{m+1}(1)$.
- $xx_{m+1}(1)$ is then fed back into the ATL hub to undergo another round of memory access etc, which in turn is fed back and results in $xx_{m+1}(2)$. This is repeated $K$ times, and the final value $xx_{m+1}(K)$ is fed into the generation module to generate $yy_{m+1}$.
- The multiple access has been put in to handle complex queries with intermediate outputs, it serves the same function multiple stages in a Transformer.


![](https://subirvarma.github.io/GeneralCognitics/images/stat184.png) 

Figure 3: Generating $zzz_n$ at the ATL Hub using kNN and Attention Modules

![](https://subirvarma.github.io/GeneralCognitics/images/stat189.png) 

Figure 4: Memory Access + Prediction Stack

![](https://subirvarma.github.io/GeneralCognitics/images/stat187.png) 

Figure 5: Computation of the energy function $E_W$ 

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
