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

Context vectors in transformers are generated using the self attention operation, and this operation is repeated over several layers. Context generation at the bottom layer is based on the input prefix and the transformers generated output so far, while in the upper layers it is based on latent representations of these inputs (which also are the initial predictions made by the Transformer).
Self attention is engineered to dynamically focus on part of the context that is most relevant to the generation of the next word, by making the key and values a learnt function of the context (rather than the context itself). 
Transformers do next word prediction using their FFN network, which is a two stage fully connected feed forward system, and this functions as its parametric (key,value) memory storage. . It can be shown that the parameters of the first stage encode the key values from the training data, while the parameters of the second state encode the distribution of the values for a given key. Note that this parametric memory is frozen after training, and is distributed across the multiple stages of the Transformer.
Even though Transformers have multiple stages, they use a single latent state representation across all the stages, and this state serves as a residual value that gets modified as the data flow progresses across the stages.

The IM-LEPP language model differs from Transformers in the following respects:

- 
- Memory in transformers is frozen at the time of training, and is captured in the parameters of the feed forward network or FFN (see [Geva et.al.](https://arxiv.org/abs/2012.14913)), in fact two-thirds of the parameters in a Transformer go into the FFN modules. Memory storage in IM-LEPP on the other hand is de-coupled from the prediction module



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
