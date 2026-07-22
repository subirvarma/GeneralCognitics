---
layout: default
title: " A Model for Semantic Cognition Using Latent Thought States"
---

# A Model for Cognition Using Latent Thought States

**Contents**     

- 

## Introduction

This paper proposes a computational model for semantic cognition in the brain based on the controlled semantic cognition (CSC) framework originally developed by [Ralph et.al.](https://wiredbrains.org/wp-content/uploads/2023/07/Ralph-2016-Nature-Reviews-Neuroscience.pdf). The model, that we call Integrated Predictive Processing Model for Cognition or IPPC,
builds on the previous paper that proposed a model called LEPP (Latent Energy based Predictive Processing) for perception as a process of a flow on an energy landscape. The IPPC model extends this idea and builds a model for cognition that integrates both perception and language processing. The IPPC architecture allows for additional sensory modalities to be integrated in a straightforward manner. 

The architecture is based on the Inference-Prediction-Generation framework that was also used for LEPP. 
The vision and language parts of the model are integrated together using a central temporal prediction hub, and this results in an internal 'thought' state that evolves as a function of both these modalities as new sensory data is received.
Both vision and langauge have their own inference and prediction pipelines that operate using the predictive coding model. They generate latent states that reflect the latest sensory vision or language data, and these latent states are in turn integrated into a central latent though state, once again using predictive coding pipelines. The central thought state itself is modeled using energy based diffusion models that provide a rich multi-modal landscape from which successive states can be sampled from. 
The central thought state is turn is fed back into the individual perception or language state, which in turn gets modified as new sensory data comes in, and the cycle repeats. This framework allows the vision and thought latent states to evolve indendently of each other, and operate at different time scales. The central thought state gets invoked asynchronuosly as new data comes in. This design allows for the various modalities in the brain to influence one another as the states evolve. The IPPC model also allows for continual learning, since all information required to update the various modules is available locally.

The perception module used in the IPPC model was proposed earlier as part of the LEPP model. In this paper we propose a corresponding model for language. For this module the input sensory data corresponds to words from a language which happens to be discrete in nature. In order to do so we extend the predictive coding framework to discrete data, and show that the resulting model is also bilogically plausible.

All the modules proposed as part of the IPPC model work using the principle of energy minimization, and all communications between states is local in nature. The model allows us to directly access the internal though states which can be very useful whether the model is operating in the 'safe' zone. In contrast LLM models

LLM models







## The Hub and Spoke Model for Cognition

Based on the Lambon Ralph paper


## Model for Modality Specific Modules



## Model for the ATL Hub



## Model for the Language Module



## Inter-Operation between the Vision and Language Modules



## Experimental Evidence



## Existing Work



## Conclusions


