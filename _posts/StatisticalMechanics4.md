---
layout: default
title: "Energy Based Models Part 4: World Models and LLMs Using EBMs"
---

# Energy Based Models Part 4: World Models and LLMs Using EBMs

**Contents**     

- Introduction       
  -  Reinforcement Learning and agentic models
  -  Why World Models are important
  -  Building World Models using EBMs
    - Video models
    - Auto-regressive video models
    - WAM: World Action Models - Generates next image on the basis of prior image and action.
    - VLA: Vision Language Action Models - Generates action sequence on the basis of image and text inputs.
  -  Achieving task objectives using World Models and agentic actions
- LLMs using EBMs

## Introduction

A common motif that we pursued in [Part 3](https://github.com/subirvarma/GeneralCognitics/blob/main/_posts/2026-02-13-statmech3.md) was to come up with EBM models that serve as as biologically plausible models for the brain.
In part 3 we looked at EBMs that can be used to generate images, and connected these to our visual perception.
But what about other aspects of the brain? The brain can also generate video, for example when we are imagining some scenario in our minds. Can EBMs also serve as video generators? We will show that this is indeed the case. 
Video generation is a very important skill since it is connected to knowledge of how the world works, for example when something is dropped it will fall to the ground. In order to generate video the model should have a knowledge of the physics as well as common sense notions of how everything evolves in time. This is commonly known as a world model.
Hence video generation is closely tied to the problem of creating a world model. 

Once we have a world model which is able to generate video scenarios, this opens up the possibility of using it to do planning. For example if we wan’t to accomplish a task then we can try out various scenarios mentally to figure out which sequence of actions would result in a successful outcome. 
This leads us to the science of reinforcement learning, whose objective is to find the optimal set of actions that would result in success for a task. RL has been somewhat hobbled in its application to robotics due to the absence of a world model that the robot could use to plan its actions. 
Using EBM generated world models in robotics is currently at the cutting edge of research.

Another activity that our brain does is language generation. LLMs that do this are the first AI models that leapt from the lab to the outside world and are currently more or less driving investment activity in the world economy. 
But can EBMs be used to generate language?
This field is still in its research phase, though there is a company called [Inception labs](https://www.inceptionlabs.ai/) that was recently founded to commercialize EBM based LLMs. Founded by Stefani Ermon. 
If successful EBM LLMs will have several advantages over the traditional autoregressive LLMs. The latter generate one word at a time which limits their speed of generation and also increases energy consumption costs. 
EBM based LLMs on the other hand are able to generate multiple words or even sentences in each step. This can speed up generation and at a lower energy cost. Also solves the problem that AR models have, which is I’ve a word is generated it an it be erased. 
When we speak we typically don’t generate words one at a time. We have a thought that we then try to express in language. 
EBM based LLMs are closer to this way of operating. This shifts the focus to thinking of EBM based LLMs as thought generators, with language only serving as a way those thoughts are communicated to the outside rites. This also gets around the critique that is leveled at auto regressive EBMs that are like stochastic parrots since they only think one word at a time. 

Hence we can regard thoughts as the fundamental unit just as images are a fundamental unit. Just as a succession of images results in a video scenario, a succession of thoughts results in an argument. This leads the way to models that are able to generate thoughts in an auto regressive manner, with one thought following the other. 
We will see that the EBM framework that we developed for generating video can also be used to generate a succession of thoughts auto regressively. 
We can choose the thoughts to lead to some objective and this is the basis of human endeavors such as math, science or even writing or debating  in general. 
Once again RL can be applied to find the optimal series of thoughts and this is indeed how the latest generation of AR LLMs have achieved their level of intelligence at tasks such as math, game playing and code generation.

But AR LLMs do generation one word at a time, not a thought at a time. How are they equivalent to EBMs which generate at the level of thoughts. 
We will try to resolve this conundrum by examining the energy landscape of thought EBMs. The bottom of the valleys in this landscape corresponds to coherent thoughts, just as the bottom of the valleys of image EBMs corresponds to coherent images. 
When we generate language using thought EBMs we are sampling the system until it settles to a valley bottom and that is the output thought. AR LLMs can also be regarded as seeking a configuration that is at the bottom of the valley, but they assume that we are already at a valley bottom, and then generate words that correspond to the thought at that bottom.

They are guided to which particular thought to turn into words by several factors: 1) The prefix that we use. This serves as a conditional probability that shapes the landscape. Moreover in LLMs that do reasoning, the prefix is augmented with already generated words, which changes the energy landscape while the generation is going on. 2) post training based on RL which guides the particular energy bottom that the LLM settles into. Since in general, given a prefix, there are several minima that can be chosen. Schemes such as RLHF guide the generation to a minima that satisfies properties that humans find more acceptable.
The image EBM and the thought EBM are connected. For instance we can generate an image that corresponds to a description expressed as a thought. When we read a book or listen to someone speak, the stream of thoughts can lead to a succession of images in our head. Conversely we can generate a thought that corresponds to an image, or to a succession of images, which is something that we humans do all the time when we describe a scene in words. We will see how EBMs can be used to replicate these skills. 
Thoughts can exist independent of language. Hence people who haven’t learn a language, or infants who haven’t learnt how to speak, can still have thoughts that they can use to go about their lives. Presumably this is true for animals too. 
The fundamental phenomenon that generates both images and thoughts is the neural configuration. In the case of vision, Our consciousness translates this configuration into images that we see, while in the case of language, our consciousness translates the configuration into words. 


In Part 3 we saw how EBMs can be used to generate images, in this article we will extend this to the generation of video. But since video is nothing else then a succession of images
this ties this problem of prediction: How to predict frame n+1 given frame n and perhaps other frames in the past. But why are video predictions model important?
We will ret to answer this question from the point of view of biological systems.

![](https://subirvarma.github.io/GeneralCognitics/images/stat60.png) 

Figure 1: A Model for Biological Brains 

There is a video prediction model in our brains that is contantly predicting the next frame that we are going to see. The actual image is generated by combining this information with the information
in sensory signals coming from the eyes (see figure 1).

![](https://subirvarma.github.io/GeneralCognitics/images/agent1.png) 

Figure 2: The Reinforcement Learning Control Framework

![](https://subirvarma.github.io/GeneralCognitics/images/agent2.png) 

Figure 3: Model Based Control in Reinforcement Learning

![](https://subirvarma.github.io/GeneralCognitics/images/Agent31.png) 

Figure 4: A Decision Making system

Video prediction is also critical to building world models. As the name implies these are internal models of how the world evolves with time, and also how to raects to various events taking place,
and this includes the actions that we are taking. To understand this we will use the reinforcement learning framework shown in figure 2.


