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

In Part 3 we saw how EBMs can be used to generate images, in this article we will extend this to the generation of video. But since video is nothing else then a succession of images
this ties this problem of prediction: How to predict frame n+1 given frame n and perhaps other frames in the past. But why are video predictions model important?
We will ret to answer this question from the point of view of biological systems

![](https://subirvarma.github.io/GeneralCognitics/images/stat60.png) 

Figure 1: A Model for Biological Brains 

There is a video prediction model in our brains that is contantly predicting the next frame that we are going to see. The actual image is gneertaed by combining this information with the information
in sensory signals coming from eyes (see figure 1).

![](https://subirvarma.github.io/GeneralCognitics/images/Agent31.png) 

Figure 2: A Decision Making system

Video prediction is also critical to building world models. As the name implies these are internal models of how the world evolves with time, and also how to raects to various events taking place,
and this includes the actions that we are taking. To understand this


