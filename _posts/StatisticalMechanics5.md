---
layout: default
title: " A Model for Semantic Cognition Using Latent Thought States"
---

# A Model for Cognition Using Latent Thought States

**Contents**     

- 

## Introduction

This paper proposes a computational model for semantic cognition in the brain based on the controlled semantic cognition (CSC) framework originally developed by [Ralph et.al.](https://wiredbrains.org/wp-content/uploads/2023/07/Ralph-2016-Nature-Reviews-Neuroscience.pdf). The model, that we call Integrated Multimodel Latent Energy based Predictive Processing IM-LEPP
builds on the previous paper that proposed the LEPP for perception as a process of a flow on an energy landscape. The IM-LEPP model extends this idea and builds a model for cognition that integrates both perception and language processing. The IM-LEPP architecture allows for additional sensory modalities to be integrated into the model in a straightforward manner. 

The IM-LEPP architecture is based on the Inference-Prediction-Generation framework for cognitive processing that was also used in LEPP. 
The vision and language parts of the model are integrated together using a central temporal prediction hub, and this results in an internal 'thought' state that evolves as a function of both these modalities as new sensory data is received.
Both vision and langauge have their own inference and prediction pipelines that operate using the predictive coding model. They generate latent states that reflect the latest sensory vision or language data, and these latent states are in turn integrated into a central latent thought state, once again using predictive coding pipelines. The central thought state constitues the prediction part of the model and is based on an energy based diffusion model. This provides a rich multi-modal landscape from which successive states can be sampled from. 
The central thought state is in turn is fed back into the individual perception or language state, which get modified as new sensory data comes in, and the cycle repeats. This framework allows the vision and language latent states to evolve indendently of each other, and operate at different time scales. The central thought state gets invoked asynchronuosly as new data comes in from either module. This design allows for the various modalities in the brain to influence one another as the states evolve. The IPPC model also allows for continual learning, since all information required to update the parameters of the various modules is available locally.

The perception module used in the IPPC model was proposed earlier as part of the LEPP model. In this paper we propose a corresponding model for language. For this module the input sensory data corresponds to words from a language which happens to be discrete in nature. In order to do so we extend the predictive coding framework to discrete data, and show that the resulting model is also biologically plausible.

All the modules proposed as part of the IPPC model work using the principle of energy minimization, and all communications between states is local in nature. 

There are several advantages that the IM-LEPP model has when compared to the current generation of LLM models:

- There is a fundamental difference between the IM-LEPP model and modern LLMs. LLMs learn by consuming a huge amount of data in the training stage, which is very different from the way our brains work. The child's brain gets trained on a continuous basis in parallel to its inference operation, and this is also the way that the IM-LEPP model learns. The internal thought state in the IM-LEPP model is grounded by the perceptual data coming in through sensory modules, and this is just like how the brain operates. The equivalent though state in the LLM is solely based on word associations from which the model tries to infer the underlying grounding.
- Unlike LLM models, the IM-LEPP model allows us to directly access the internal though states which can be very useful to find out whether the model is operating in the 'safe' zone. LLM models on the other hand model the evolution of words directly, similar to the DEPP model discussed in the previous paper. In all likelihood they also possess internal thought like states, but they are not directly accessible. 
- The implicit prediction or world model in LLMs is trained using successive word correlations, which seems to work, but only after consuming huge amounts of data. Im IM-LEPP on the other hand the equivalent prediction module is trained using a combination of words, images and other modalities that may be available. This implies that the language generation in IM-LEPP benefits not just from words correlations, but also gets grounded using other modalities of data and all these modalities feed into a common thought state. Thus the thought state model can be trained faster if it able to take advantage of all the modality streams.
- Unlike LLM models, IM-LEPP models allow for continual learning and update of parameters as new data comes in.
- There is stong biological plausibility for the IM-LEPP model, both in terms of its operation using the idea of state evolution based on energy flows, and evidence of a hub and spoke model for cognition in the brain, as described in the CSC paper.
- There is strong recent experimental evidence that language processing in the brain is more like the language part of the IM-LEPP model, rather than LLM models (Barenholtz).
- LLM models work by starting from an initial prefix, which can incorporate both images and words, and then it generates outputs, which are also a combination of words and images. However the architecture does not allow for new input data to be incorporated into the model while it is 'thinking' or in the moddle of generation. The IM-LEPP model on the other hand does allow this since its internal thought state can be accessed.


LLM models







## The Hub and Spoke Model for Cognition

Based on the Lambon Ralph paper




## Model for the ATL Hub



## Model for the Language Module



## Inter-Operation between the Vision and Language Modules

Convergence in the hub module PC pipeline if the central z state is simukltaneously being changed by the other modality.



## Experimental Evidence



## Existing Work



## Conclusions


