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

Figure 1: The controlled semantic cognition (CSC) for cognition. 

The controlled semantic cognition (CSC) framework was proposed by Lambon Ralph et.al. in 2017, and it was based on key findings from a decade of research into neurocognitive and neurocomputational underpinnings in the brain's semantic cognition abilities. Based on this, they proposed the 'hub and spoke' theory of semantic representation that is shown in the above figure, which was based on accounting os patterns of impairment that are observed in some semantic disorders. This theory assimilated two important existing ideas: (a) The model assumes that multimodal verbal and non-verbal experiences provide the core ingredients for constructing concepts and these information sources are encoded in modality sepcific cortices distributed across the brain, (b) The model proposes that that cross modal interactions for all modality sepcific sources of information are mediated by a single transmodal hub that is situated bilaterally in the anterior temporal lobe (ATL) area of the brain.
The hub and spoke model was was suggested by the observation that individuals with semantic dementia (SD) show semantic impairments across all modalities, and SD is characterized by atrophy centered in the ATL.

This model solves the problem of how the information relevant to a given concept is experienced across all different verbal and sensory modalities. For example if see an image of a dog, then we are able to reproduce the sounds, names valence and other types of information that are associated with the animal. This implies that the ATL hub forms generalizable semantic representations for a dog that are shared across all modalities.

![](https://subirvarma.github.io/GeneralCognitics/images/stat148.png) 

Figure 2:

There is a sub-region within the ATL called the ventral-ventrolateral ATL that serves as the cross modal center point of the hub for multimodal naming and comprehension.
Based on experimental data, the model also proposed that the semantic representation function varies in a graded manner across the the ATL subregions. The 8x8 unit grid of colored circles in the above figure represents the ATL hub with reciprocal connectivity to the modality specific spokes. The contribution of the hub units to the semantic representation is graded reflecting a varying pattern of connectivity to the spoke layers. At the center point, there is equal weighted connectivity to all inputs, thus resulting in an evenly transmodal representation, as shown by the white color.


## The IM-LEPP Model for Vision and Language Integration

![](https://subirvarma.github.io/GeneralCognitics/images/stat149.png) 

Figure 3: The IM-LEPP model

We propose a model for integration of visual and language modalites based on the hub and spoke model, which we call integrated multimodal latent energy-based predictive processing or IM-LEPP (see above figure). This model extends the LEPP model that was described in the [previous paper](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html) in two ways: It extends the vision model to a hierarchical structure, and it introduces a LEPP style model for language, and finally proposes how the two may be integrated together to create a common representation. The IM-LEPP model has the following features:

- There is a central ATL type hub at level 1 that integrates representations coming in from the vision and language hubs. Note that the communication between the level 1 central hub and the vision and language hubs is bi-directional, so that not only the spoke hubs influence the representation in the central hub, but they in turn are influenced by the information coming from the central hub.
- The vision hub itself has a two level structure. There is a central vision hub at level 2 thats integrates information coming from level 3 hubs, with the understanding that the level 2 represents a scene, while there is an idividual level 3 hub to represent each object in the scene. The representation of each of these objects changes asynchronously while the level 2 hub integrates the latest information and sends it up to the central level 1 hub.
- The object based level 3 vision hubs operate according to the inference-prediction-generation framework that was used for the LEPP model. This results in temporal predictions for the object representation that are sent to the level 2 visionhub for integration with all the other objects in the scene. This representation in turn gets integrated with representations from other modalities in the multimodal level 1 hub. The level 1 representation in turn is fed back to level 3 vision hubs, which then uses it to generate percepts. Note that these percepts take all the other objects that are in the scene into account (as well as other modalities), by virtue of the fact that they are based on representations coming from the level 1 multimodal hub.
- The language module operates at the word level, and incorporates an inference-prediction-generation pipeline whose job is to predict the next word. The latent representation used to do this generation comes from the central level 1 hub and takes the current visual scene into account. Hence unlike in an LLM, next word prediction is not based solely on word occurence statistics, but on other data that are impinging on the brain.

The model leads to a picture in which there are number of distributed level 3 hubs in the brain, that are individually responsible for predictions in the modality they are tracking. Hence the prediction operations happens in several places in the brain, while central hubs at level 2 and level 1 are responsible for the integration work. We will show that as in the LEPP model, all state level dynamics in the IM-LEPP model are based on flows in energy landscapes


## Hub and Spoke Model for Vision

![](https://subirvarma.github.io/GeneralCognitics/images/stat150.png) 

Figure 4: Hub and Spoke Model for Vision: Integration of Objects into a Scene

This section has a more detailed description of the vision models operating at levels 2 and 3. Modern AI systems process images at the level of pixels, and learn prediction models for how value of these pixels evolves with time, and this is how vision was also modeled in the LEPP paper. The brain on the other hand is thought to decompose a scene at the object level, and then model the evolution of the individual objects with time. For example in a road scene, there would be models for the pedestrians, the trees, the cars as well as a model for the background containing the sky, background landscape etc. Each object is tracked individually, but the brain also integrates the representations of all them to create the scene that we see in front of us. This is the kind of system that we propose to model as shown in the above figure. 

Predictive level 3 models for objects that we encounter in our daily lives don't require much training. HOwever when we encounter an object for the first time then the predictive model undergoes a period of training, after which it gets stored away. At any one time a subset of trhe models are required depending on the scene that is being composed.

![](https://subirvarma.github.io/GeneralCognitics/images/stat145.png) 

Figure 5: Predictive Processing Pipeline for an Individual Object at Level 3

The level 3 predictive processing model for an individual object is shown in the above figure, and follows the LEPP design, with inference, prediction and generation modules. As new sensory data $s_n$ for an object comes in, it is integrated into the latent state $z_n$ for the object by using the predictive coding pipeline by using the principle of minimization of the predictive coding energy $E_{PC}$. 
Subsequently the prediction module is invoked and this results in a prediction $x_{n+1}$. The prediction process is modeled by using a multi-stage diffusion process that gradually anneals the state of the system until it reaches a state of lower energy. The state $x_{n+1}$ is sent to the level 2 visioon hub and this results in the state $zz_{n+1}$, and this in turn is sent to the multimodal level 1 hub, resulting in the state $zzz_{n+1}$. This state information is then fed back into the level 3 object level pipeline by settting $x_{n+1} = zzz_{n+1}$. Note that as a result of this integration with higher level hubs, the state $x_{n+1}$ incorporates information about other objects in the scene as well other modalities that may be relevant such as sound. The representation $x_{n+1}$ is used to generate the next percept $g_{\phi}(x_{n+1})$, and is also used to kick off the next phase of the predictive coding pipeline by comparing it with the new sensory data $s_{n+1}$. This subsequently results in a new state $z_{n+2}$ and the cycle repeats.


![](https://subirvarma.github.io/GeneralCognitics/images/stat146.png) 

Figure 4: Integration of Multiple Object Level Pipelines into the Vision Hub at Level 2





![](https://subirvarma.github.io/GeneralCognitics/images/stat151.png) 

Figure 5:Integration of Vision and Language Hubs into the Cognition Level Hub at Level 3





## A Predictive Coding model for Language 

![](https://subirvarma.github.io/GeneralCognitics/images/stat143.png) 

Figure 6: Predictive Coding based language module

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


