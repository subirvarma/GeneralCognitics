---
layout: default
title: " An Energy based Language Model with Hierarchical Memory"
---

# An Energy based Language Model with Hierarchical Memory


## Introduction

This is the third in a series of papers for models of cognition based on the energy minimization principle. The first paper [Generative AI as an Effective Theory of Cognition](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html) proposed the Latent Energy based Predictive Processing or LEPP model for perception as a process of flow on energy landscapes.
The following paper [A Hierarchical Energy-Based Model for Multimodal Cognition](https://subirvarma.github.io/GeneralCognitics/2026/08/07/statmech5.html) built on the IM-LEPP model and proposed the Integrated Multimodal LEPP or IM-LEPP model as a model for cognition that integrates both perception and language processing. In this paper we build on the IM-LEPP work and propose a more comprehensive and detailed model for language processing, in particular:

- The next word prediction module in the IM-LEPP language model was based on the minimization of an energy function $E_W$. We propose a neural network model for $E_W$, the output of which can be used for process of energy minimization using Langevin base diffusion sampling.
- The prediction module in IM-LEPP interfaces with the central ATL hub whose state gets updated with information coming in from other sensory modules, the amygdala, as well the main memory storage system. We supply the mechanism by which the contents of the memory storage are accessed as a function of the current language system state and get incorporated into a resulting state that provides a context for the generation of the next word.

All language models involve two basic operations: 

- Creation of a context vector which serves as a conditional for next word prediction.
- The next word prediction operation, which involves accessing memory to choose the word that best serves as a continuation for the already generated sequence.

Context vectors in Transformer based LMs are generated using the self attention operation, and this operation is repeated over several layers. Context generation at the bottom layer is based on the input prefix and the transformers generated output so far, while in the upper layers it is based on latent representations of these inputs (which also are the initial predictions made by the Transformer).
Self attention is engineered to dynamically focus on part of the context that is most relevant to the generation of the next word, by making the key and values a learnt function of the context (rather than the context itself). 
Transformers do next word prediction using their FFN network, which is a two stage fully connected feed forward system, and this functions as its parametric (key,value) memory storage . It can be shown that the parameters of the first stage encode the key values from the training data, while the parameters of the second state encode the distribution of the values for a given key (see [Geva et.al.](https://arxiv.org/abs/2012.14913)). Note that this parametric memory is frozen after training, and is distributed across the multiple stages of the Transformer.
In fact two-thirds of the parameters in a Transformer go into the FFN modules.
Even though Transformers have multiple stages, they use a single latent state representation across all the stages, and this state serves as a residual value that gets modified as the data flow progresses across the stages.

The IM-LEPP language model differs from that of Transformers in the following respects:

- IM-LEPP also features a latent state that is subject to change during the process of prediction just as in Transformers. However unlike Transformers, this latent state also flows across successing word predictions. Transformers on the other hand use the generated word as a bridge between successive generations.
- IM-LEPP also generates a context vector that it uses for prediction, however this context is created from information that is stored in its long term memory. Hence the prediction model in IM-LEPP is decoupled from memory storage, and the two modules can evolve independently over time, for example new memories can be added using other sensory modalities such as vision or smell, and this is done using a process of continuous learning. In Transformers on the other hand, prediction and parametric memory are coupled in its FFN, and in order to incorporate more memory, the system has to undergo re-training. In other words memory in transformers is frozen at the time of training, while it is de-coupled from the prediction module in IM-LEPP, and can change continuously.
- IM-LEPP uses an energy based diffusion model to do prediction, as opposed to the FFN used in Transformers. This makes the prediction operation more flexible, and it can be adapted to the level of difficulty involved.

## The IM-LEPP Model

![](https://subirvarma.github.io/GeneralCognitics/images/stat170.png) 

Figure 1: The IM-LEPP Model


![](https://subirvarma.github.io/GeneralCognitics/images/stat183.png) 

Figure 2: The IM-LEPP Language Module



Figure 3: Generating $zzz_n$ at the ATL Hub using kNN and Attention Modules



Figure 4: Computation of the energy function $E_W$ 

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
