---
layout: default
title: " A Hierarchical Energy-Based Model for Multimodal Cognition"
---

# A Hierarchical Energy-Based Model for Multimodal Cognition

**Contents**     

## Introduction

This paper proposes a computational model for semantic cognition in the brain based on the controlled semantic cognition (CSC) framework originally developed by [Ralph et.al.](https://wiredbrains.org/wp-content/uploads/2023/07/Ralph-2016-Nature-Reviews-Neuroscience.pdf). The model, that we call Integrated Multimodel Latent Energy based Predictive Processing or IM-LEPP
builds on the previous paper that proposed the LEPP model for perception as a process of flow on an energy landscapes. The IM-LEPP model extends this idea and builds a model for cognition that integrates both perception and language processing. The IM-LEPP architecture allows for additional sensory modalities to be integrated into the model in a straightforward manner. 

The IM-LEPP design is based the following core idea that was introduced in the paper [Generative AI as an Effective Theory of Cognition](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html):
Modern generative neural networks should be understood not as mechanistic models of neural implementation, but as effective theories of cognitive dynamics operating at the level of learned energy landscapes. In this view, cognition is understood as the temporal evolution of perceptual and cognitive states through a learned energy landscape, rather than as the direct consequence of an explicitly modeled neural circuitry. Just as statistical mechanics explains why thermodynamics provides an effective description of macroscopic matter without explicitly modeling every molecular interaction, modern generative AI may provide effective descriptions of cognitive dynamics without modeling the underlying neural circuitry. Leveraging this insight, IM-LEPP models the brain at the level of energy landscapes rather than at the circuit level.

The IM-LEPP architecture is also based on the Inference-Prediction-Generation framework for cognitive processing that was also used in previous paper. 
Both vision and langauge have their own inference and generation pipelines that operate using the predictive coding model. The inference pipeline results in latent states that reflect the latest vision or language data, and these latent states are in turn integrated into a central temporal prediction hub, once again using predictive coding pipelines. The central thought state constitutes the prediction part of the system and is based on an energy based diffusion model. This provides a rich multi-modal landscape from which successive thought states can be sampled from. 
The thought state is in turn is fed back into the individual perception or language modules, to generate the next percept or word. It also gets modified into new latent sensory state as new data comes in, and the cycle repeats. 

This framework allows the vision and language processes to evolve indendently of each other, and operate at different time scales. This aspect is important since vision sensory data is received almost continuously, while language data in the form of words is seprated by a few hundred milliseconds.
The central thought state gets invoked asynchronuosly as new data comes in from either module. This design allows for the various modalities in the brain to influence one another as their states evolve. The IM-LEPP model also allows for continual learning, since all information required to update the parameters of the various modules is available locally at each step of the inference, generation and prediction modules. All the modules proposed as part of IM-LEPP work using the principle of energy minimization, and all communications between states is local in nature. 

The inference and generation modules for perception was proposed earlier as part of the [LEPP framework](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html) and follows the predictive coding structure as proposed by [Rao and Ballard]. In this paper we propose corresponding modules for language. The input sensory data for this module corresponds to words from a language, which unlike vision, happen to be discrete in nature. We take this into account by extending the predictive coding framework to discrete data, and show that the resulting model is also biologically plausible.

IM-LEPP is proposed as a model for cognitive functions in the brain, and there are several points of distinction when comparing it with LLMs, which also seem to be carrying out similar cognitive functions:

- There is a fundamental difference in learning between IM-LEPP model and LLMs. LLMs learn by consuming a huge amount of data in the training stage and then use the resulting frozen model for all their inference operations, which is very different from the way brains work. Brains gets trained on a continuous basis in parallel throughout their lives so that continual training is co-mingled with inference, and this is also the way that the IM-LEPP model operates.
- The internal thought state in the IM-LEPP model and its temporal evolution (called the world model) is influenced by both language and vision, and as a result the language generated by the model is grounded by by both visual and linguistic data, and this is just how the brain operates. It is thought that LLMs also maintain an internal world model that is not visble externally, however this model is built entirely based on langauge statistics and is not grounded in real world sensory data and this results in the well known [symbol grounding problem](https://arxiv.org/html/cs/9906002), i.e., they see only the linguistic symbols, never what those symbols are about. The integration of vision and language into a shared common state in IM-LEPP constitutes a solution to this problem.
- IM-LEPP allows us to directly access the internal thought states through which all generation is done which can be used to get additional insight into the models thought process. Something equivalent can be done with LLMs by probing the transformer's middle layers. In IM-LEPP the relevant state is much easier to locate which increases the reliability of operations such as safety on the model.
LLMs on the other hand operate at the level of words without exposing their internal workings, similar to the DEPP style model discussed in the previous paper. Current safety work focuses on probing for equivalent thought states in the LLM by looking at the middle layers of the transformer.
- The implicit prediction or world model in LLMs is trained using successive word correlations, which seems to work, but only after consuming huge amounts of data. In IM-LEPP on the other hand the equivalent prediction module is trained using a combination of words, images and other modalities that may be available. This implies that the language generation in IM-LEPP benefits not just from words correlations, but also gets grounded using other modalities of data and all these modalities feed into a common thought state. Thus the thought state model can be trained faster if it able to take advantage of all the modality streams.
- The prediction part of IM-LEPP operates on the basis of flows on energy landscapes driven by the process of energy minimization. This brings us one step closer to modeling the brain, since it is thought the brain also operates using a similar mechanism, but driven bit its connectome. In addition IM-LEPP is based on the CSC framework for the brain's architecture that was proposed by Ralph et.al. These aspects make IM-LEPP more biologically plausible compared to LLMs.

This paper makes the following contributions:

- We propose a hob and spoke integration architecture for multiple sensory modalities, with modality specific predictive coding pipelines converging on a shared thought state. The sharing between modalities is also mediated through predictive coding.
- We propose an extension of predictive coding to discrete categorical data needed to model language, and
- The proposed architecture also takes care of asynchronous multi-rate updating across sensory modalities operating on different timescales.

## The Hub and Spoke Model for Cognition

![](https://subirvarma.github.io/GeneralCognitics/images/stat138.png) 

Figure 1: The hub and spoke model for cognition



![](https://subirvarma.github.io/GeneralCognitics/images/stat139.png) 

Figure 2: (a) The inference prediction generation pipeline for each modality (b) Structure of the central hub that integrates all modalities

## The IM-LEPP Model for Cognition

![](https://subirvarma.github.io/GeneralCognitics/images/stat140.png) 

Figure 2: The IM-LEPP model



## Model for the ATL Hub



## A Predictive Coding model for Language 

![](https://subirvarma.github.io/GeneralCognitics/images/stat143.png) 

Figure 3: Predictive Coding based language module

The above figure shows a proposed predictive coding model for words. The system processes language one word at a time, and for each word it builds up an internal representation using predictive coding 
We will assume a simple two level hierarchy, though the model allows for any number of levels. The top level has a latent representation $z^{(2)}$, and this used to generate a representation $z^{(1)}$ at the lower level using a function $f_2(z^{(2)})$ and this representation in turn generates the final representation $t=(t_1,...,t_K)$ where $K$ is the number of words in the library.
The representations $z^{(1)}$ and $z^{(2)}$ are in continuous space, however $t$ lies in discrete space and is given by $t=(t_1,t_2,...,t_K)$ and uses the 1-hot representation so that individual words $(w_1, w_2,...,w_K$ are represented by $(1,0,...,0), (0,1,...,0),...,(0,0,...,1)$ respectively. The representation $t$ is generated from  $z^{(1)}$ by a process of sampling using the distribution

$$ p(t = (t_1,...,t_K)) = (y_1)^{t_1})(y_2)^{(t_2})...(y_K)^{(t_K)}  $$

where $y_k$ is given by the Boltzmann distribution (also called the softmax function in machine learning) 

$$ y_k = { e^{ z_k^{(1)}}\over{\sum_i e^{ z_i^{(1)}} } } $$

In this equation $z_i^{(1)}$ is the $i^{th}$ component of the vector $z^{(1)}$. Lets assume that $z^{(1)}$ leads to the probabilities $y=(y_1,y_2,...,y_K)$ while the ground truth is given by
$T = (T_1,T_2,...,T_K)$ This generates an error $\epsilon^{(1)} = y - T$, which is propagated to the level above.
Using the Bayesian argument used in predictive coding, it can be shown that optimal $z_i^{(1)}$ is obtained by minimizing the energy function

$$  E_{PC}(1) = -\sum T_i\log y_i + {1\over 2}\epsilon_{z^{(1)}}^T \Pi_1 \epsilon_{z^{(1)}}  $$

where $\epsilon_{z^{(1)}} = z^{(1)} - f_2(z^{(2)})$. Using gradient descent $z_i^{(1)}$ is updated according to 

$$ z_i^{(1)} \leftarrow z_i^{(1)} - \eta \left[(y_i - T_i) + \left(\frac{\partial f}{\partial {z^{(1)}} }\right)^T\Pi_1\epsilon_{ z^{(1)}}\right] $$

Note that all the information required to update $z_i^{(1)}$ is available locally.

### Computation of $y$ and $T$






## Inter-Operation between the Vision and Language Modules

Convergence in the hub module PC pipeline if the central z state is simukltaneously being changed by the other modality.



## Experimental Evidence



## Existing Work



## Conclusions


