---
layout: default
title: " An Energy based Language Model with Hierarchical Memory"
---

# An Energy based Language Model with Hierarchical Memory


## Introduction

This is the third in a series of papers for models of cognition based on the energy minimization principle. The first paper [Generative AI as an Effective Theory of Cognition](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html) proposed the Latent Energy based Predictive Processing or LEPP model for perception as a flow process on energy landscapes.
The following paper [A Hierarchical Energy-Based Model for Multimodal Cognition](https://subirvarma.github.io/GeneralCognitics/2026/08/07/statmech5.html) built on the LEPP model and proposed the Integrated Multimodal LEPP or IM-LEPP as a more detailed model that intergrated perception with language processing. In this paper we build on the IM-LEPP work with further development of the language processing module, in particular:

- The prediction modules in IM-LEPP interface with the central ATL hub whose state gets updated with information coming in from sensory modules, the amygdala, as well the main memory storage system. We describe the mechanism by which the contents of the memory storage are accessed and get incorporated into a resulting state that provides context for the prediction modules.
- The next word prediction module in the IM-LEPP was based on the minimization of an energy function $E_W$. This module is described in greater detail in this paper, and it involves the following:
  (1) Energy minimization through a process of gradient descent.
  (2) A description of the training process for the computation of the energy function parameters.
  (3) Interleaving of energy optimization with episodic memory access which results in a conditional minimization process.

The IM-LEPP language model defines a system latent state, which can be likened to a thought state, and is used to generate the next word. This state gets modified over time as a result of the following events: 

- New language sensory input that comes in, either through reading or through sound (also in latent form),
- Modification of the latent state as a result of episodic memory recall from the past history of the language agent.
- Modification of the latent state as a result of other sensory modalities such as vision or sound.
- The latent state variables can be used to define an energy function. New sensory data or memory access causes the energy level to rise, and it subsequently settles back to a minimum, and this results in a new latent state from which the next word is generated. Energy minimization is done through a variable number number of steps until it gets to a minimum. The number of steps is a function of the amount of thinking involved in generating the next word. The parameters of the energy function are specialized to the task of predicting the next word and are estimated during the training process, 

These operations are repeated in sequence and result in the evolution of the though state as new sensory data comes in memories are accessed.
Even though Transformers and the proposed IM-LEPP language model are both are both doing language generation, they differ in the following respects:

- IM-LEPP features a system latent state that is subject to modification during the process of prediction. However unlike Transformers, this latent state flows across successive word predictions and is recurrent in nature. Transformers on the other hand use the discrete generated word as a bridge between successive predictions and instead of using a recurrent state, they use the entire past history for future predictions. The latent state in Transformers is localized to the 'column' that is used to generate the next word, and does not cross column boundaries.
The recurrent state design in IM-LEPP is more biologically plausible, since clearly human's don't keep the entirety of their past word generations in mind when generating the next word.
- The context in IM-LEPP is created from information that is stored in its episodic memory, as well an information from other modalities. In a Transformer the context is given by the initial prefix and the entire past history of word generations, which causes the context to grow with time. It can become very large, and since attention has quadratic complexity, it leads to high processing requirements (in practice the context is cut off after some length is reached, which leads to forgetting in Transformers). 
- Prediction in IM-LEPP is based on a multistep minimization of an energy function, in which the context serves as a conditioning variable. Transformers do prediction using a feed forward network or FFN, and they also carry out multiple passes through the FFN when a predicting the next word. However the number of steps or stages in a Transformer is fixed, while IM-LEPP can adjust the number of steps depending upon the difficulty of the prediction.

There are other differences in language generation in the two models that were pointed out in [A Hierarchical Energy-Based Model for Multimodal Cognition](https://subirvarma.github.io/GeneralCognitics/2026/08/07/statmech5.html) that make the IM-LEPP model more biologically plausible.

The rest of this paper is organized as follows: Section 2 has a high level description of IM-LEPP language generation, where the main modules, their functions and inter-module dependencies are described. 
Since language generation is intimately related to memory mechanisms, we start in Section 3 with a description of what is known about how memory works in humans.
Section 4 compares IM-LEPP with other language models, in particular with the Transformer, along the following axes: (a) Memory mechanisms, (b) Latent State definitions, (c) Prediction techniques. There have been several suggestions for modifications to improve the Transformer design over the years, including, Universal Transformers, Looped Transformers, Full Bandwidth Transformers etc. We will discuss the relationship between these models and IM-LEPP in Section 5.
Recently there has been a resurgence of interest in updated forms of recurrent neural networks or RNNs for language modeling, these are discussed in Section 6 along with the connections to IM-LEPP.
In Section 7, we discuss the recent literature on reasoning models, and how the IM-LEPP model fits within this framework.
In Section 8 we go into details of the specific algorithms used in the IM-LEPP language model for (a) Episodic Memory access, (b) Design of the energy function and its training algorithm, (c) Halting techniques for determining number of steps in energy minimization


## The IM-LEPP Model

![](https://subirvarma.github.io/GeneralCognitics/images/stat170.png) 

Figure 1: The IM-LEPP Model

Notes for Figure 1:

- This is the figure from the previous paper, no changes.


![](https://subirvarma.github.io/GeneralCognitics/images/stat198.png) 

Figure 2: The IM-LEPP Language Module

Notes for Figure 2:

- The energy module $E_W$ is invoked a variable number of times using schemes such as in the Du, Li, Tenenbaum, Mordatch paper. I will experiment with either no noise added in each E_W step or a constant amount of noise as in the Gladstone paper.
- Before the first invocation $zz_m(1)$ is sent to the ATL hub, where it is changes to $zzz'_m(1)$ using the predictive coding pipeline. This is then used to invoke items from memory (described in figure 3 below), and this results in a change in $zzz'_m(1)$ to $zzz_m(1)$.
- $zzz_m(1)$ is fed back into the prediction module to condition the minimization of $E_W(x;zz_m(1),zzz_m(1))$, which results in  $zz_{m+1}$.
- $zz_{m+1}$ is then fed back into the ATL hub to undergo another round of memory access etc, which in turn is fed back and results in $zz_{m+2}$ etc. Note that memory access is done once per E_W module invocation, so in cases such as the Martha Washington example, either (1) Multi-step reasoning happens to to repeated access to the parametric memory in E_W, and/or (2) Multi-step reasoning ha[[ends over multiple invocations of the E_W module, each time conditioned by a different episodic memory match.
- Comparison to Transformers: (1) IM-LEPP uses a recursive structure unlike Transformers, (2) Episodic memory in IM-LEPP is selectively chosen depending upon current state, unlike Transformers where the entire past history is used as context, (3) Each invocation of the E_W module is like a Transformer Block in which attention and FFN are invoked a variable number of times while using the same parameters in each invocation.
- Comparison to the TRM model: The (z,y) variables in TRM area analogous to the (zz,zzz) variables in IM-LEPP.
- Question: Can RL be done on the IM-LEPP model? Can't think of a way to do it, it would involve changing the parameters of E_W in response to a reward. On the other hand perhaps humans don't learn using RL, rather they memorize algorithms instead.



![](https://subirvarma.github.io/GeneralCognitics/images/stat193.png) 

Figure 3: Generating $zzz_n(i)$ at the ATL Hub using kNN based search and a predictive processing pipeline

- All memories are of the episodic kind and get stored in the long term memory. The break up into episodes uses the surprisal based mechanism described in the previous paper.
- A certain number, say M of these are retrieved after matching using $zzz'_m(i)$ using kNN perhaps. I will get into more details of this mechanism in the detailed write-up.
- These M episodes are then run through a predictive processing pipeline to generate $zzz_m(i)$. Alternatively an attention based mechanism can be used for this purpose, with $zzz'_m(i)$ serving as the query. The details for this have to be worked out.

![](https://subirvarma.github.io/GeneralCognitics/images/stat199.png) 

Figure 5: Computation of the energy function $E_W(x;zz_m(k),zzz_m(k))$ 

I have used the cross attention mechanism for doing the conditioning. There are two other ways of doing this described in the DiT paper.

![](https://subirvarma.github.io/GeneralCognitics/images/stat195.png) 

Figure 6: A single DiT Block

Figures 5 and 6 show a diffusion Transformer based design for computing the energy function.

