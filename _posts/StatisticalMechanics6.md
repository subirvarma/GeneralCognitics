---
layout: default
title: " An Energy based Language Model with Hierarchical Memory"
---

# An Energy based Language Model with Hierarchical Memory


## Introduction

This is the third in a series of papers for models of cognition based on the energy minimization principle. The first paper [Generative AI as an Effective Theory of Cognition](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html) proposed the Latent Energy based Predictive Processing or LEPP model for perception as a flow process on energy landscapes.
The following paper [A Hierarchical Energy-Based Model for Multimodal Cognition](https://subirvarma.github.io/GeneralCognitics/2026/08/07/statmech5.html) built on the LEPP model and proposed the Integrated Multimodal LEPP or IM-LEPP as a more detailed model for perception and language processing. In this paper we build on the IM-LEPP work with further development of the language processing module, in particular:

- The prediction module in IM-LEPP interfaces with the central ATL hub whose state gets updated with information coming in from other sensory modules, the amygdala, as well the main memory storage system. We describe the mechanism by which the contents of the memory storage are accessed and get incorporated into a resulting state that provides context for the generation of the next word.
- The next word prediction module in the IM-LEPP was based on the minimization of an energy function $E_W$. This process is laid out in more detail in this paper, and it involves an alternating process of memory access followed by energy minimization. We also propose some specific models for $E_W$.

All language models involve two basic operations: 

1. Starting with the system latent state, creation of a context state which serves as a conditional for next word prediction and this may involve long term memory access in order to create a suitable context. Incorporation of the information in the context leads to a modification of the system latent state.
2. The next state prediction operation, which matches the modified system latent state with information stored in its parametric memory in order to create a new system latent state.

These two operations may be repeated in sequence several times before the latent state for the next word is predicted, and this corresponds to the 'thinking' process. This model corresponds to the 'Production System' framework used in cognitive science.

The Production System framework also applies to Transformer based LMs.
Even though a Transformers has multiple stages, it uses a single system latent state that is created anew for each column, and it runs across all the stages.
This state serves as a residual value that gets modified as the data flow progresses across the stages.
The two Production System operatios in Transformers are as follows:
 
1. The context in Transformers corresponds to the initial prefix as well as the words that have been generated. The system latent state serves as a query into this context using the self attention operation. Self attention is engineered to dynamically focus on part of the context that is most relevant to the generation of the next word.

2. Self attention is followed by next state prediction and this done using a fully connected two-layer feed forward network (FFN). The parameters of this network function as a frozen (key,value) memory storage that are learnt during the training process. The system latent state serves as query into this storage, and the corresponding value is the predicted next state.

These two operations, self-attention followed by FFN, are repeated multiple times and are responsible for properties such as in context learning (ICL) in the Transformer.

Even though Transformers and the proposed IM-LEPP language model are both based on the Production System framework, they differ in the following respects:

- IM-LEPP features a system latent state that is subject to modification during the process of prediction just as in Transformers. However unlike Transformers, this latent state also flows across successive word predictions and is recurrent in nature. Transformers on the other hand use the discrete generated word as a bridge between successive predictions and instead of using a recurrent state, they use the entire past history for future predictions. The recurrent state design is more biologically plausible, since for example humans rarely keep for than 4-5 words in working memory when deciding on the next word.
- The context in IM-LEPP is created from information that is stored in its long term memory, while in a Transformer the context is given by words generated so far. In the latter case since the context grows as the generation proceeds, it can become very large, and since attention has quadratic complexity, it leads to high processing requirements (in practice the context is cut off after some length is reached, which leads to forgetting in Transformers). IM-LEPP on the other hand can handle a much larger memory storage with lower processing complexity by using more efficient search algorithms.
- Instead of using a FFN for prediction, IM-LEPP uses an energy based diffusion model, in which the context serves as a conditioning variable for the generation. This is again a more biologically plausible prediction mechanism since it is based on the physical principle of energy minimization.

There are other differences in language generation in the two models that were pointed out in [A Hierarchical Energy-Based Model for Multimodal Cognition](https://subirvarma.github.io/GeneralCognitics/2026/08/07/statmech5.html) that make the IM-LEPP model more biologically plausible.

## The IM-LEPP Model

![](https://subirvarma.github.io/GeneralCognitics/images/stat170.png) 

Figure 1: The IM-LEPP Model

Notes for Figure 1:

- This is the figure from the previous paper, no changes.


![](https://subirvarma.github.io/GeneralCognitics/images/stat192.png) 

Figure 2: The IM-LEPP Language Module

Notes for Figure 2:

- The prediction module is invoked a variable number of times. During inference a constant amount of noise is added for the diffusion step.
- Before the first invocation $zz_m(1)$ is sent to the ATL hub, where it is changes to $zzz'_m(1)$ using the predictive coding pipeline. This is then used to invoke items from memory (described in figure 3 below), and this results in a change in $zzz'_m(1)$ to $zzz_m(1)$.
- $zzz_m(1)$ is fed back into the prediction module to condition the minimization of $E_W(x;zz_m(1),zzz_m(1))$ using L steps of the Langevin iteration, which results in  $zz_m(2)$.
- $zz_m(2)$ is then fed back into the ATL hub to undergo another round of memory access etc, which in turn is fed back and results in $zz_m(3)$. This is repeated $K$ times, and the final value $zz_m(K) = xx_{m+1}$ is fed into the generation module to generate $yy_{m+1}$.
- The multiple loops through the prediction module have been put in to handle complex queries with intermediate outputs, it serves the same function multiple stages in a Transformer. It can be considered to be a thinking operation that the model engages in latent space.


![](https://subirvarma.github.io/GeneralCognitics/images/stat193.png) 

Figure 3: Generating $zzz_n(i)$ at the ATL Hub using kNN based search and a predictive processing pipeline

- All memories are of the episodic kind and get stored in the long term memory. The break up into episodes uses the surprisal based mechanism described in the previous paper.
- A certain number, say M of these are retrieved after matching using $zzz'_m(i)$ using kNN perhaps. I will get into more details of this mechanism in the detailed write-up.
- These M episodes are then run through a predictive processing pipeline to generate $zzz_m(i)$. Alternatively an attention based mechanism can be used for this purpose, with $zzz'_m(i)$ serving as the query. The details for this have to be worked out.

![](https://subirvarma.github.io/GeneralCognitics/images/stat194.png) 

Figure 5: Computation of the energy function $E_W(x;zz_m(k),zzz_m(k))$ 

![](https://subirvarma.github.io/GeneralCognitics/images/stat194.png) 

Figure 6: A single DiT Block

Figures 5 and 6 show a diffusion Transformer based design for computing the energy function.

