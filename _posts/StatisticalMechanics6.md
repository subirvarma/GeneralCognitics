---
layout: default
title: " # An Energy based Model for Language and Thinking"
---

# An Energy based Model for Language and Thinking


## Introduction

This is the third in a series of papers for models of cognition based on the energy minimization principle. The first paper [Generative AI as an Effective Theory of Cognition](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html) proposed the Latent Energy based Predictive Processing or LEPP model for perception as a flow process on energy landscapes.
The following paper [A Hierarchical Energy-Based Model for Multimodal Cognition](https://subirvarma.github.io/GeneralCognitics/2026/08/07/statmech5.html) built on the LEPP model and proposed the Integrated Multimodal LEPP or IM-LEPP as a more detailed model that intergrated perception with language processing. In this paper we build on the IM-LEPP work with further development of the language processing module. 
The next word prediction module in the IM-LEPP was based on the minimization of an energy function $E_W$. This module is described in greater detail in this paper, and it works through a process of energy minimization using multi-step gradient descent. Energy minimization is interleaved with episodic memory access and
 we describe the mechanism by which the contents of the memory storage are accessed and get incorporated into a resulting state that provides context for the prediction modules.

The IM-LEPP language module defines a system latent state, which can be likened to a thought state, and is used to generate language percepts. This state evolves with time as a result of the following events: 

- Modification as a result of new sensory data in the form of phonemes (sound) or characters (vision).
- Modification as a result of energy minimization: The latent state variables can be used to compute an energy function $E_W$ and new sensory data or memory access causes the energy level to rise. It subsequently settles back to a minimum, and this results in a new latent state from which the next word is generated. 
Energy minimization is done through a variable number of gradient descent steps, the number of steps is a function of the amount of thinking involved in generating the next word. The parameters of the energy function are specialized to the task of predicting the next word and are estimated using local operations during the learning phase.

The language module thought state gets integrated with that of other sensory modalities, as well as data coming from the episodic memory module, in the central ATL hub, and acts as a conditioning variable during the energy minimization steps.
These operations are repeated in sequence and result in the evolution of the though state as new sensory data comes in and new memories are accessed.

The description of the IM-LEPP model in the [previous paper](https://subirvarma.github.io/GeneralCognitics/2026/08/07/statmech5.html) left out the following two aspects of how the model works: (1) Computation of the energy function $E_W$ and (2) Operation of the episodic memory storage and its interface with the rest of the model. Our objective in this paper is to supply these details, and in the process we make deep connections between IM-LEPP and Transformer models. The IM-LEPP model was inspired by the idea of modeling cognitive processes in terms of energy functions and the process of generation in vision or language as due to the movement of a state variable on energy landscapes. Since Transformers seem to be doing language generation that mimics what humans do, does it fit within this framework? If so what is the nature of the energy function that it is minimizing, and what is the equivalent state variable? We are going to answer these questions during the course of this essay.

Since IM-LEPP is a new type of language model, how does it compare with other such models that have been proposed over the years? The first language models were based on recurrent neural networks or RNNs, and just like IM-LEPP, they were also based on a system state that updated over time in a recurrent fashion. However RNNs suffered from the problem that recurrent state lost information over time, hence it did not have a stable memory. IM-LEPP gets around this problem by integrating with an external memory storage that is used to refresh its state periodically.

Transformers solved the memory decay problem in RNNs by not using a recursive design, hence they don't have an explicit system state that gets recursively updated. In fact they use the entirity of their initial prefix and past generations as their memory, i.e., their memory is effectively their context window. This has worked very well for them, and with context window sizes of several hundred thousand tokens, it has made possible the powerful models that we see today. However this design does come with a cost since the attention operation has quadratic complexity with respect to the context window size, which has led to the high power requirements for these models. Even though large, the context window is finite, and transformers are not able to access data once it fall outside the window.

There are other differences between IM-LEPP and Transformers: Unlike Transformers, IM-LEPP features a system latent state that flows across successive word predictions and is recurrent in nature. Transformers on the other hand use the discrete generated word as a bridge between successive predictions and instead of using a recurrent state, they use the entire past history for future predictions. The latent state in Transformers is localized to the prediction 'column' that is used to generate the next word, and does not cross column boundaries.
The recurrent state design in IM-LEPP is more biologically plausible, since clearly human's don't keep the entirety of their past word generations in mind when generating the next word.

Prediction in IM-LEPP is based on a multistep minimization of an energy function, in which a context generated by the central ATL  serves as a conditioning variable, which allows integration with other sensory modalities as well as memory. Transformers do prediction using the initial prefix and past word predictions as context, which is acted on by a self-attention operation followed by a feed forward network or FFN, together called a Transformer block, and they carry out multiple passes through this block when predicting the next word. It can be shown that each Transformer block is roughly equivalent to a single gradient descent step in the minimization of some implicit energy function. This energy function is made explicit in IM-LEPP and while the number of blocks in a Transformer column is fixed, IM-LEPP can adjust the number of optimization steps depending upon the difficulty of the prediction.
There are other differences in language generation in the two models that were pointed out in [A Hierarchical Energy-Based Model for Multimodal Cognition](https://subirvarma.github.io/GeneralCognitics/2026/08/07/statmech5.html) that make the IM-LEPP model more biologically plausible. An important difference is whereas the weights in a Transformer are fixed once its is trained, IM-LEPP can change its weights during the course of its operations thus leading to continuous learning.

In the last few years there have been several proposals that have been made to improve upon Transformer models. These proposals can be broadly classified into the following categories:

- Loop Transformers and Universal Transformers: The basic idea in these models is to repeat a single Transformer block multiple times, and has been shown to have similar performance to a full Transformer, while saving on parametric memory. This aspect is directly incorporated in IM-LEPP, since if we regard the $E_W$ energy module as being roughly equivalent to a Transformer block, then multiple invocations of the energy module during the process of energy minimization are equivalent to the multiple invocations of the Loop Transformer block, with the caveat that all invocations in either case use the same set of module parameters.
- Techniques to propagate the latent state: The amount of thinking that a Transformer can do is tied to the number of blocks it has in each column, which is a fixed number. In some sense the thinking process has to re-start in a new prediction column, and ll the information in the latent state from the previous column is lost. There have been some recent proposals to correct this by propagating the final latent state from between successive columns, most notably in the Full Bandwidth Transformer. This is done natively in the IM-LEPP design, since the system latent state is propagated between successive prediction stages.
- Techniques to break up a long context into chunks, and then choose a subset of these chunks during the prediction process: IM-LEPP incorporates this design choosing appropriate chunks from its episodic memory store during the prediction process.

In summary, recent Transformer models have begun to incorporate features that make them closer to the IM-LEPP design. Since IM-LEPP itself was inspired by experimental evidence collected over the years from neuroscience about how the brain operates, this convergence brings the latest Transformer design improvements closer to the biological brain.
There is another class of models that have been proposed recently called reasoning models.
In Transformers reasoning requires multiple invocations of the prediction block within a column, and if the number of blocks is fixed, then it leads limitations in the reasoning process. Some information is propagated to the next column using the predicted token, but most of the information in the final latent state is lost. The IM-LEPP model facilitates reasoning through two mechanisms: 
(1) Through the multistep gradient descent based minimzation of the energy function, in which the number of steps is variable, hence can change depending upon the difficulty of the reasoning problem, 
(2) Since the final latent state is sent to the next prediction module, this avoids the problem that Transformers have of loosing the latent state information. Furthermore the new prediction module utilizes fresh conditioning vectors, which prevent the recurrent state from decaying over time.

The rest of this paper is organized as follows: Section 2 has a high level description of IM-LEPP language generation, where the main modules, their functions and inter-module dependencies are described. 
Since language generation is intimately related to memory mechanisms, we start in Section 3 with a description of what is known about how memory works in humans.
Section 4 compares IM-LEPP with other language models, in particular with the Transformer, along the following axes: (a) Memory mechanisms, (b) Latent State definitions, (c) Prediction techniques. There have been several suggestions for modifications to improve the Transformer design over the years, including, Universal Transformers, Looped Transformers, Full Bandwidth Transformers etc. We will discuss the relationship between these models and IM-LEPP in Section 5.
Recently there has been a resurgence of interest in updated forms of recurrent neural networks or RNNs for language modeling, these are discussed in Section 6 along with the connections to IM-LEPP.
In Section 7, we discuss the recent literature on reasoning models, and how the IM-LEPP model fits within this framework.
In Section 8 we go into details of the specific algorithms used in the IM-LEPP language model for (a) Episodic Memory access, (b) Design of the energy function and its training algorithm, (c) Halting techniques for determining number of steps in energy minimization


## The IM-LEPP Model

![](https://subirvarma.github.io/GeneralCognitics/images/stat170.png) 

Figure 1: The IM-LEPP Model

The IM-LEPP model is shown in figure 1. It proposes a hierarchical spatial integration structure for the vision model, it introduces a hierarchical temporal integration structure for language, and finally it proposes how the two may be integrated together to create a common representation. The IM-LEPP model has the following features:

- There is a central ATL type hub at level 1 that integrates representations coming in from the vision and language hubs. Note that the communication between the central hub and the vision and language hubs is bi-directional, so that not only do the spoke hubs influence the representation in the central hub, but they in turn are influenced by the information coming from the central hub.
- The vision hub itself has a two level structure. The central vision hub at level 2 integrates information coming from several simultaneously active level 3 predictive processing pipelines. There is a level 3 pipeline for each of the objects in the scene, as well an always-on pipeline for the scene itself, and all these get integrated at the level 2 vision hub. The representation of each of these pipelines evolves asynchronously in time and the level 2 hub integrates the latest information from each individual object and sends it up to the central level 1 hub. Note that the per object pipelines come and go depending on which objects are currently in the field of vision, while the scene level pipeline is always active.
- The per-object level 3 predictive processing pipelines operate according to the inference-prediction-generation framework that was used for the LEPP model. The system state that results from the inference module in this pipeline is sent to the level 2 vision hub for integration with the states of all the other objects in the scene. This combined representation in turn gets integrated with representations from other modalities in the multimodal level 1 hub. The integrated level 1 representation in turn is fed back to the prediction module in the level 3 object predictive processing pipelines, and the result is used to generate the next percept. Note that these percepts take all the other objects that are in the scene into account (as well as other modalities), by virtue of this architecture.
- The language sub-system also has a two level hierarchical structure, however the hierarchy is in time rather than in space. At the lower level of the hierarchy at level 3 are predictive processing pipelines that operate at the discrete phoneme level (in the case of spoken language) or at the character level (in the case of reading). This level incorporates an inference-prediction-generation modules whose job is to predict the next phoneme or character. Note that unlike the case for vision, only one of the level 3 pipelines is active at any one time; moreover, within whichever pipeline is active, phonemes or characters necessarily arrive one at a time in sequence rather than simultaneously, unlike the multiple objects that can be concurrently present in a visual scene. Together these account for the temporal, rather than spatial, character of the language hub.
The latent representation from this level is sampled at certain discrete instants that contain representations for whole words, and these are fed as input into a word level predictive processing pipeline at level 2. The next word latent prediction done at this level is influenced by the state of the central ATL hub and thus gets modified by information from the other modalities, and ultimately gets sent to the level 3 hub to generate percepts. If the phoneme hub is active then it generates percepts in the form of sound or if the character hub is active then it generates percepts in the form of written text.

Thus the IM-LEPP model paints a picture in which there are number of distributed, predictive processing pipeline modules in the brain, that are individually responsible for predictions in the modality they are tracking. Hence the prediction operations happens in a distributed manner, while central hubs at level 1 and level 2 are responsible for integrating the lower level representations, and in turn feeding them back to the predictive processing pipelines.
All state changes in this model at the various pipelines and hubs are based on the principle of the energy minimization, and thus provide a plausible model for the brain's operation at Marr's level 2.

The [previous paper](https://subirvarma.github.io/GeneralCognitics/2026/08/07/statmech5.html) left several aspects of this model un-specified, in particular details about the operation of the memory module and its interface with the other modules, as well as details of how the energy function $E_W$ is implemented in the prediction module. We will focus on these aspects of the design in this paper.

![](https://subirvarma.github.io/GeneralCognitics/images/stat198.png) 

Figure 3: The IM-LEPP Language Module

The predictive coding pipeline at the word level uses the latent state $z_n$ from the character pipeline as the ground truth that represents the latent representation for for the $m^{th}$ word. Note that the word level subscript $m$ for the current word  is not the same as the character level subscript $n$ for obvious reasons.
This pipeline creates a higher level latent word representation $zz_m$ by modifying the existing representation $xx_m$ to $q_{\phi}(xx_m,z_n)$.
$zz_m$ is then sent to the level 1 central ATL hub where it gets modified by the vision data to the latent $zzz_m$. For example if the current image is that of an apple, then this is reflected in $zzz_m$.

The latent $zzz_m$ is then fed back to the level 2 word pipeline where it is used to predict the next word by using the
the energy based prediction module $E_W(x;zz_m,zzz_m)$ and this results in the prediction $xx_{m+1}$ for the next word latent (see above figure).
Note that, unlike the vision hub at level 2, which performs integration only, the word-level pipeline includes its own dedicated prediction step. This reflects the fact that phoneme-level prediction serves segmentation, while word-level prediction serves ordinary sentence-level anticipation, a genuinely distinct function operating at a different timescale. This mechanism also illustrates why the IM-LEPP model may be able to learn new words faster, since the predicted word is not only a function of the previous word level context $zz_m$, but is also influenced by the vision modality by means of the latent $zzz_m$. Similarly the emotional related information coming in through the valence system (valence) can influence our choice of the next word.

$xx_{m+1}$ is subsequently used to generate the next word latent $yy_{m+1}=g_{\psi}(xx_{m+1})$, and this value is fed back into the  level 3 character level predictive processing pipeline shown in figure 10, where it influences the prediction of the next character $x_{n+2}$ through the energy function $E_{CH}(x;z_{n+1},yy_{m+1})$. This in turn gets modified by the other characters in the next word being read. When the last character of that word is encountered, then the latent representation at that time $z_{n+k}$ (where $k$ is the number of characters in the word just read) is fed back into the word level model to correct the prediction $yy_{m+1}$, and this closes the word level prediction loop. As pointed out in the introduction, this is also an hierarchical system, but the hierarchy is in time rather than in space, as was the case for the visual system.

For the case when we are doing character generation, i.e., writing, this feedback loop between the character level and word level pipelines is still active. In this case it serves as a verification of whether the word that was generated at level 3 matches the word that the level 2 word level system meant to generate.

Do the latent states $zzz_m$ or $zz_m$ encode 'thought'? 
Levelt’s production model as described in his book [Speaking: From Intention to Articulation (1989)](https://www.mpi.nl/publications/item67053/speaking-intention-articulation) has a first stage, conceptualization, whose output is a pre-verbal message i.e., a language-independent conceptual representation of what to say, prior to and dissociable from any particular verbalization (which is why “the same thought” can be expressed in different words or languages). This is a direct architectural instantiation of exactly the proposed role for $zzz_m$ as a persistent, amodal state that the generative pathway then unrolls into a word sequence, with $zzz_m$ playing the role of the preverbal message and the language pipeline playing Levelt’s formulation stage.

Notes for Figure 2:

- The energy module $E_W$ is invoked a variable number of times using schemes such as in the Du, Li, Tenenbaum, Mordatch paper. I will experiment with either no noise added in each E_W step or a constant amount of noise as in the Gladstone paper.
- Before the first invocation $zz_m(1)$ is sent to the ATL hub, where it is changes to $zzz'_m(1)$ using the predictive coding pipeline. This is then used to invoke items from memory (described in figure 3 below), and this results in a change in $zzz'_m(1)$ to $zzz_m(1)$.
- $zzz_m(1)$ is fed back into the prediction module to condition the minimization of $E_W(x;zz_m(1),zzz_m(1))$, which results in  $zz_{m+1}$.
- $zz_{m+1}$ is then fed back into the ATL hub to undergo another round of memory access etc, which in turn is fed back and results in $zz_{m+2}$ etc. Note that memory access is done once per E_W module invocation, so in cases such as the Martha Washington example, either (1) Multi-step reasoning happens to to repeated access to the parametric memory in E_W, and/or (2) Multi-step reasoning ha[[ends over multiple invocations of the E_W module, each time conditioned by a different episodic memory match.
- Comparison to Transformers: (1) IM-LEPP uses a recursive structure unlike Transformers, (2) Episodic memory in IM-LEPP is selectively chosen depending upon current state, unlike Transformers where the entire past history is used as context, (3) Each invocation of the E_W module is like a Transformer Block in which attention and FFN are invoked a variable number of times while using the same parameters in each invocation.
- Comparison to the TRM model: The (z,y) variables in TRM area analogous to the (zz,zzz) variables in IM-LEPP.
- Question: Can RL be done on the IM-LEPP model? Can't think of a way to do it, it would involve changing the parameters of E_W in response to a reward. On the other hand perhaps humans don't learn using RL, rather they memorize algorithms instead.


![](https://subirvarma.github.io/GeneralCognitics/images/stat193.png) 

Figure 2: Generating $zzz_n(i)$ at the ATL Hub using kNN based search and a predictive processing pipeline

- All memories are of the episodic kind and get stored in the long term memory. The break up into episodes uses the surprisal based mechanism described in the previous paper.
- A certain number, say M of these are retrieved after matching using $zzz'_m(i)$ using kNN perhaps. I will get into more details of this mechanism in the detailed write-up.
- These M episodes are then run through a predictive processing pipeline to generate $zzz_m(i)$. Alternatively an attention based mechanism can be used for this purpose, with $zzz'_m(i)$ serving as the query. The details for this have to be worked out.


![](https://subirvarma.github.io/GeneralCognitics/images/stat199.png) 

Figure 5: Computation of the energy function $E_W(x;zz_m(k),zzz_m(k))$ 

I have used the cross attention mechanism for doing the conditioning. There are two other ways of doing this described in the DiT paper.

![](https://subirvarma.github.io/GeneralCognitics/images/stat195.png) 

Figure 6: A single DiT Block

Figures 5 and 6 show a diffusion Transformer based design for computing the energy function.

