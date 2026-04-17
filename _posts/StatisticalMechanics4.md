---
layout: default
title: "Models in Neuroscience Using EBMs"
---

# Models in Neuroscience Using EBMs

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

Modern artificial neural networks (ANNs) such as transformers are purely mathematical functions, that transform inputs into outputs. Since there is no evidence that anything like it exists in biological brains, my objective in this series of articles is to point out that there are alternative AI models that are based on the princples of physics, more specifically thermodynamics, and these are more plausible models for the brain.
In [Part 3](https://github.com/subirvarma/GeneralCognitics/blob/main/_posts/2026-02-13-statmech3.md) I discussed generative AI models whose operation is driven by their energy function.
I pointed out that traditional ANNs can serve as models for the energy function, and this in turn arises as a result of interactions between nodes, very much like in a spin glass model from physics. However, unlike for spin glasses, we ignored the interconnection topology, and by focusing on the energy function instead, the analysis of the system was simplified.

Can such a system serve as a model for the brain?
The topology of the inter-connections in brains, called the connectome, is too complex to comprehend even using the latest advances. However if the functioning of the brain is determined by its energy function, and furthermore if ANNs such as transformers can serve as good models for the brain's energy function, then it provides an alternative way by which the latest advances in ANNs can be used to build models for the brain.
We started down this path in [Part 3](https://subirvarma.github.io/GeneralCognitics/2026/02/13/statmech3.html) by showing how EBM based models can be used to generate images by a process of energy minimization, and in this article we will use it to create a model for perception in brains.
But brains do much more than perception, they enable us to plan hypothetical scenarios, as well as take actions in the real world. We will see that these capabilities are intimately tied to perception so that EBMs models can be used to do these operations as well.

These theories are based on the fundamental idea that in order to survive, living creatures need to create a model for their environment within themselves. Consider the simplest kind of life, such as a uni-cellular creatures such as bacteria. Their insides are cordoned off from the environment by means of a cell wall (in neuroscience this is referred to as a Markov Blanket) . However in order to survive they need informtion about the outside world in order to feed themselves for example, and this is obtained by means of sensors on their cell walls. The information from these sensors gets converted into a model that the creature uses to move around and get closer to food sources, and this serves as a simple example of a environment model.

Higher animals such as ourselves face the same problem since our brains are enclosed in the darkness of our skulls, and thee need to figure out what is happening in the external world. This they do by building a model for the world with the help of signals that are coming in through the sensory organs and when we open our eyes, it is this model that we see in front of us, it is internally generated. It is connected to the actual world out there, but the specific perception model that we use has been designed to help us survive in the world. Different creatures build their own models, and in general the sophistication increases with larger brain sizes. 
Hence our brains are making a best guess of what the external world looks like by using the sparse signals coming in from the sense organs and combining that information with an internal model of the world.
There are several theories of how this works, and we will consider a few of them:

- Active Inference: This is a based on a mathematical framework that uses Bayes Rule, and it explicitly models the internal states of the brain. From the machine learning point of view, this model is similar to Helmhotz Machine that was proposed in the mid-90s by Hionton and others. A more recent version along the same theoretical lines has resulted in an image generation model called VAE or Variational Auto-Encoder.
- Predictive Processing: This is more of a qualitative framework of how the brain works and its main proposal is that the brain's model is predictive. Hence the brain is not just modeling the state of the world as it exists at any instant, but does prediction, i.e., forecast what the world might look like in the future. How far into the future the prediction is done depends on the animal in question, humans excel at this and can do long term prediction, while most other animals can predict at most a few steps into the future.

Prediction is a fundamental aspect of these models and both Active Inference and Predictive Processing put it at the heart of their theory, by connecting predictions not just to perception, but also to action. 
Broadly speaking, action is defined as the way in which living creatures are able to change their environment in order to facilitate goals.
They do this by proposing that brains predict the perceptual consequence of an action internally, and then the muscles carry out the action to make the prediction come true.

In this article I am going to talk about a machine learning based model for the brain that is also based on the predictive processing framework. However unlike Active Inference, this model traces its roots to the Boltzmann Machine, and its recent generalization to diffusion models that was discused in Part 3. It proposes that the brain's model for the environment is captured in the interconnection strengths between neurons in the brain's perception center. EBMs offer a convenient way in which the information processing within these neurons that leads to image generation can be captured by the principle of minimization of energy.
The Active Inference theory is also based on the minimization of energy, however the energy that it refers to is a probabilistic quantity that is called Variational Free Energy or VFE. The energy in diffusion models on the other hand is directly created due to the interaction netween neurons and hence has a physical basis not just a probabilistic one.

![](https://subirvarma.github.io/GeneralCognitics/images/stat60.png) 

Figure 1: A Model for Perception 

In [Part 3](https://github.com/subirvarma/GeneralCognitics/blob/main/_posts/2026-02-13-statmech3.md)  I presented a model for visual perception (see above figure). One of the inputs into the image generation EBM was labeled 'prediction of next frame', and the percieved image was generated by starting from the predicted image and then conditionining it on the information being received from the senses. But how is the prediction for the next frame being done? This is precisely the topic of this article. We will show that prediction models are another example of conditional generative EBMs, such that the prediction of the next frame is conditioned on the current frame. This creates an auto-regressive structure which can be used in important applications such as video or language generation.
This opens the way to model other aspects of the brain using EBMs. 

The brain can clearly generate video, which is nothing more than a succession of images, for example when we are imagining some scenario in our minds.
Video generation is a very important skill since it is connected to knowledge of how the world works, for example when something is dropped it will fall to the ground, in other words it should be a predictive model. Hence, in order to generate video the model should have a common sense notions of how things evolve in time. This is commonly known as a world model
and video generation is closely tied to the problem of creating a world model. But video generation is not done in a vaccuum, but is closely tied to actions that we can take in the real world. Hence the world model should be able to generate the next image as a function of the current image as well as any action that we take.
Once we have a world model which is able to generate a succession of images conditioned on actions, this opens up the possibility of using it to do planning. For example if we want to accomplish a task then we can try out various scenarios mentally to figure out which sequence of actions would result in a successful outcome. 

What I described in the prior paragraph was the neuro-scientific approach to systems that are able to model the world that enable them to take actions and achieve objectives. There is another way to
approach this problem, and this is by using a branch of AI called reinforcement learning or RL. The objective or RL is to find the optimal set of actions that would result in success for a task, which is defined as maximization of a scalar reward value. RL has been somewhat hobbled in its application to robotics due to the absence of a world model that the robot could use to plan its actions. Using EBM generated world models in robotics is currently at the cutting edge of research. 

## The Predictive Processing Framework in Neuroscience

![](https://subirvarma.github.io/GeneralCognitics/images/stat76.png) 

Figure 2: A model for sensory perception generation in the brain

It has long been hypothesized that a fundamental operation of the brain is prediction (for example see Helmholtz or more recently [the palm pilot guy]). In the last couple of decades this theory has been further refined and a good description can be found in the book ["The Experience Machine: How Our Minds Predict and Shape Reality"](https://www.amazon.com/Experience-Machine-Minds-Predict-Reality/dp/B0B6489ZTB/ref=sr_1_1?adgrpid=183606417542&dib=eyJ2IjoiMSJ9.Fyi9d3PdzMTC53VWX7823DXjmQdLDMFgbQL5bpU2yx77AApTelrS2J7RZW7kevX5c3Iwj8BdMiBCvvIK1s-2aQ.kNY6Xa746RCCEx9tUbrInrqWtuuYDtwDu9jxlEmRXNw&dib_tag=se&hvadid=779664909770&hvdev=c&hvexpln=0&hvlocphy=9031954&hvnetw=g&hvocijid=7989718953734198151--&hvqmt=e&hvrand=7989718953734198151&hvtargid=kwd-2027556117302&hydadcr=22594_13821176_8133&keywords=the+experience+machine+andy+clark&mcid=bd89ac636e0c38d39698b254fe27c1b0&qid=1776120362&sr=8-1) by the neuroscientist and philosopher Andy Clark and our description in this section borrows from his work.

The above figure shows a model for visual perception in the brain. The fundamental hypothesis in this model is that our visual perception of the world is internally generated by our brains. Hence reality is not something that exists 'out there', but instead it is a result of a generative model that the brain runs. There is a good deal of experimental evidence that supports this hypothesis, including the fact that amount of signalling that happens 'top-down' from the interior of the brain towards the periphery where the visual cortex is located is much greater than the signalling that happens "bottom-up" from the sensory organs to the interior. This ability to predict the world is something that we gradually learn from birth onwards. Indeed a good indication that the presence of the sensory signals is not enough for visual perception is the case of people of are born congenitally blind, and then their sight is restored later in life. It has been found that they are not able to 'see' as soon as their eyes begin to function normally, but however if theyr are gradually trained to see, then they acquire this facility. This clearly shows the the bottom up signals from the sensory organs are not sufficient.

The output of $y_{n+1}$ of this generative model at time instant $n+1$  is a function
of two variables:

- The output $y_n$ of the model at the previous time instant $n$.
- The error $\epsilon_n = y_n - c_n$ between the previous output $y_n$ and the sensory signals at time $n, c_n$.

Hence the brain predicts what we are going to preceive at the next instant on the basis of what it had predicted at the previous time instant and the error between its predictions and the signal from the sensory organs. 
If the environment is relatively unchanging then the predictions and the sensory data should be close to each other.
If there is a change in the environment, for example if a new object appears in the field of view, then the brain's prediction and the sensory data are no longer in agreement. In this case the error signal generated by the difference between the two is used  to generate the next prediction, which takes the object's presence into account.
Thus the raw sensory data is never directly experienced. What we do experience is modulated by our prior experiences and our expectations.
The amount of weight that the brain gives to the prior prediction vs the error signal depend upon the individual, for example in certain dis-orders such as autism the the sensory signals are over-weighed.

Hence perception is the process of combining the brain's internal model of world, as captured by the conditional distribution $p(y_{n+1}|y_n)$ of how te world evolves with information $c_n$ that is coming through our senses. But where does the internal model $p(y_{n+1}|y_n$ come from? It is created by a continual process of lesrning that our brains are engaged, from the time we first open our eyes. 
If we see something that is unexpected, then it means that the event was not part of our existing model. But once the initial observation happens, it is incorporated into the model, the probability of the prediction getting stronger if the event happens frequently. Hence the next time the event is encountered, it is no longer a big surprise.

![](https://subirvarma.github.io/GeneralCognitics/images/stat77.png) 

Figure 2: A model for action generation in the brain

The predictive processing frameowrk can be used to describe not just perception but also the generation of actions. In order to survive in the world, organisms are not just predicting the what the environment looks like, but they actively change the environment by taking actions. Hence there are two ways to reduce the error signal between the brain's prediction and the sensory data:

- By Changing the prediction itself so that is conforms to the environment, as described above.
- Or, by changing the environment so that it conforms to the prediction, and this is done by taking actions.

The latter mechanism is illustrated in the above figure. As shown, the new prediction $y_{n+1}$ is determined not just by the prior prediction $y_n$ and the error signal $\epsilon_n$, but also the effects of the action $a_n$ that we are planning to take. Hence $y_{n+1}$ takes into account the result of the action on the environment. But note that the action hasn't been taken yet, as a result the next sensory signal $c_{n+1}$ will not agree with the prediction $y_{n+1}$. In order to remedy this, the error $\epsilon_{n+1} = y_{n+1} - c_{n+1}$ is fed into the brain's motor cortex, which in turn generated the signals required for the muscles to move and bring about the action.
You might ask why isn't the error signal fed back into the visual cortex to change the prediction as was described for visual perception. It is though that the brain suppresses this error signal, as a result of which the only way to bring the perceptions in agreement with the sensory data is by changing the environment through action.
It has been known for a long time that the motor and sensory cortices share a similar structure, and this theory explains why this is the case.

So far we have hypothsized the presence of two important cortical areas, namely those associated with vision and action. In a later section we will introduce another important cortical area associated with the generation of language, and this will connect this model to Large Language Models or LLMs.

Central to the description given so far are probability distributions of the form $p(y_{n+1}|y_n, a_n)$ which captures the evolution of the predictions depending upon the actions that the organism is taking. These is referred to as a World Model, since it serves as the organism's internal model of how the world evolves as it takes various actions. In order to survive and reproduce, all organisms need a world model, and its sophistication varies depending upon the organism. This model generates moment by moment predictions and is constantly working, even when we are sleeping. This requires a lot of energy, and accounts for the fact that the brain accounts for a large portion of the energy expended by the body. Later in this article we will connect this probability distribution to the energy arising from the interconnection between neurons in the model, and then show how the system generates new predictions by a process of minimizing the interaction energy. The minimization is done in a gradual manner as in simulated annealing, by using diffusion models.

This theory explains another mysterious property of of perception: That the world that we see is incredibly rich, with an enormous amount of detail even though the information coming from senses is quite sparse in comparison. How can we reconcile the two facts? Predictive processing theory offers a solution by theorizing that the rich detail that see in front of us is purely internally generated using our world model, with the sensory signal serving as a low bandwidth indicator of changes that have to be incorporated into the predictions from one instance to another. Hence even a very sparse external signal is sufficient to generate our image of the world.

This architecture allows our perceptions to be influenced by not just what is happening in the environment, but also our internal thoughts at the time of perception. Hence when we close our eyes we are still able to 'see' images, but now they are a function of our thoughts at that instant. This is not explicitly shown in the above figure, but we will return to this topic when we discuss planning in the next section. There are of course a number of other influences on our perception, for example a big infuence is emotions. Of course emotions are influenced by perception, but this in turn influences perception. For example if the environment is evolving as we expect, then this induces feelings of calm and happiness. On the other hand if there are un-expected changes happening, then the brain tries to bring its predictions in line with the new sensory data as soon as possible, but this can trigger feelings of anxiety. Hence the objective of a living organism is to be in environments whose evolution matches that of its internal world model, and if its put in an unknown environment then it can result in life threatening situations, like a fish out of water.
At the same time organisms such as ourselves often seek out novel situations which are not familiar to our world model, and doing so seems to give us pleasure. Hence there is a balance between exploration and exploitation. New exploration helps expand the organisms world model and prpares it to handle situations that would be threatening otherwise. Too much novelty though results in mental exhaustion, while too little results in boredom, so there is a fine balance in between wherethe amount of surprise causes feelings of being "in the zone".

Andy Clark points out in book that certain mental health issues can be explained as a consequence of this model. He points out that the predictive model not only governs what we 'see', but also is responsible for predicting inner experiences such as pain, pleasure or sadness. An important factor is the relative weighing that the brain provides to its own prediction vs the sensory signal, which is called "precision" in predictive processing theory. Brains are constantly estimating precision and changing the relative weights assigned to the two factors, as a function of how reliable it deems each to be. Problems in the brains precision estimation is now thought to underlie a wide range of psychiatric disorders.

- Autism spectrum disorders: This can be caused due to over weighing of incoming sensory data. People with autism experience the world in its full sensory splendor, however they are not able to put the sensations within a proper context, i.e., they are not able to spot the forest for the trees. They tend to be overwhelmed by a lot of sensory data such as loud sounds or social situations and tend to avoid them.
- Schizophrenia is though to be a result of the brain assigning too much weight to the error signal, i.e., the mismatch between its predictions and sensory daya. As result is mistakenly gives a lot of weight to data that may be purely co-incidental for example with no deep significance. This gradually changes the brains internal model and leads to false predictions and beliefs.
- Studies have shown that PTSD is extremely well correlated with unusually large increases in the precision weighing of the prediction error signal in response to unexpectedly negative outcomes.
- Depression can be caused due to overweighted expectations and underweghted new information. This results in a semi-permanent lock-in of the existing world model, leading us to continue with depresive behaviors.

## The Bayesian Brain: The Active Inference Theory for the Brain

The name most closely associated with the [Active Interference theory](https://www.amazon.com/Active-Inference-Energy-Principle-Behavior/dp/0262553996)  for the brain is that of the prominent neuroscientist Karl Friston.
This theory models the brain using the theory of Bayesian statistics, and is closely related to the Predictive Processing model. It is also proposes that perception is internally generated using the signals coming in through our sensory organs, but it explicitly seeks to model the hidden states in the brain that generate our perception.

![](https://subirvarma.github.io/GeneralCognitics/images/stat75.png) 

Figure 2: Inferring a Model for the External World Using Bayesian Statistics

Figure 2 shows the mathematical framework used in Active Inference theory. The vextor $x^*$ represents the external world to which the organism does not have direct access. The vector $y$ are the sensory neurons in the organism's cortex to which the organism does have access. Hence the external world has an unknown generative model that produce sensation $y$ in the organism. The organism creates an inference about the causes of sensation $y$, and this is summarized in the vector $x$ on the left and is probabilistically captured by the conditional distribution $p(x|y)$. Assuming an inference $x$, also called the hidden states, the organism internally generates a perception $y$ using this model as this is captured by the conditional distribution $p(y|x)$. If the generated $y$ is different than the original sensation that came in through the senses, then the organism changes its inference $x$ so that the two match. Mathematically this by the accomplished by the minimization of a probabilistic quantity, called the variational free energy or VFE.
Note that the organism does not have direct access to the $x$ either, so it is also a hidden state, however it does have access to the sensations $y$ generates by $x$.

The presence of the hidden state $x$ differentiates the Active Inference and Predictive Processing frameworks. While it is used explicitly in Active Inference, the Predictive Processing framework models the perception neurons $y$ directly without using hidden states. The hidden states in the Active Inference framework represents the state of the (non-perception) neurons in the brain that are responsible for creating the world model that the perception neurons depend upon. The Predictive Processing framework is able to get by without using hidden states, since it models the time evolution of the perception neurons directly by using the distribution $p(y_{n+1}|y_n,c)$, without theorizing what is causing the changes. The difference can be understood in terms of the 2-layer Boltzmann machine that we encountered in [Part 2](https://subirvarma.github.io/GeneralCognitics/2025/11/24/statmech2.html) (see figure 7 in Part 2), which has also explicitly models the hidden states. However it is possible to talk about an EBM with no hidden states, as long as we are willing to accept more complex energy functions than the simple quadratic functions used in the Boltzmann machine. This is precisely what is done in EBMs using Diffusion Models as discussed in [Part 3](https://subirvarma.github.io/GeneralCognitics/2026/02/13/statmech3.html). 
Hinton's reserach group Univ. of Toronto actually proposed a generative model calld the [Helmholtz Machine](https://www.cs.toronto.edu/~hinton/absps/helmholtz.pdf) in 1994, whose design is precisely that of shown in figure 2. The original work was hamstrung by the fact that they limited themslves to using sinple feedforward neural networks to model the probability distributions, This was corrected in 2014 by Welling and Kingma, when they came up the Variational Auto Encoder or VAE architecture. This was basically the Helmholtz machine in which the distributions where now modeled using state of the art convolutional neural networks or CNNs, and this was able to do a much better job of generating realistic images (also changed the training algorithm to SGD from wake-sleep). 
Hence in some sense the difference between the Active Inference model and the Preditive Processing model is the same as the difference between generation based on VAEs and those based on diffusions. 

**Rewrite above paragraph**

Lets now get into the nuts and bolts of the Active Inference framework.
This system can be analyzed using Bayesian statistics as follows: We will refer to the probability $p(x)$ as the prior (or existing) model for the brain. If the organism is subjected to sensations $y$, then this results in a change in its model, and it is now given by the posterior probability $p(x|y)$. The objective of the Bayesian statistics is to compute $p(x|y)$, and this is given by Bayes Rule

$$  p(x|y) = {p(y|x)p(x)\over{p(y)}}   $$

The problem in applying this formula is that $p(y)$ in general is a highly complex distribution and not known in advance. Fortunately there exists a variational approach to solving this problem which works by reducing the problem to that of minimization, and works as follows: 

Assume that we can approximate $p(x|y)$ by the distribution $Q_{\theta}(x|y)$, where $\theta$ are the parameters of a neural network.
Define the Variational Free Energy (VFE) for the system as

$$ VFE(Q,y) = E_{Q_{\theta}(x|y)} \log {Q_{\theta}(x|y)\over{p(x,y)}} $$

This can be written as

$$  VFE(Q,y) = E_{Q_{\theta}(x|y)}\log Q_{\theta}(x|y) - E_{Q_{\theta}(x|y)}\log p(x|y) - E_{Q_{\theta}(x|y)} \log p(y) $$

$$      = E_{Q_{\theta}(x|y)}(\log Q_{\theta}(x|y) - \log p(x|y)) - \log p(y) $$

$$      = D_{KL}(Q_{\theta}(x|y)||p(x|y)) - \log p(y) $$

Here $D_{KL}(Q_{\theta}(x|y)||p(x|y))$ is the Kullback-Liebler divergence between the two distributions, and it functions as measure of far apart they are.
Since $Q_{\theta}(x|y)$ is the organism's approximate model for its environment (given sensory data $y$), while $p(x|y)$ is the exact model. If the organism tries to minimize the VFE, then
this is the same as minimizing the KL divergence and this results in the approximate model being closer to the best possible model. Hence by minimizing its VFE, the organism is inferring a best model for the environment $x^{*}$, while knowing only the sensory data $y$.

The state of the perception neurons $y$ change over time as the state of the hidden state neurons and the perception signals from the environment change. This is captured using the distribution $p(y_{n+1}|y_n,c)$ in the Predictive Processing model, while the Active Inference model uses a two state process in which the internal states $x$ of the brain changes first and this is followed by a new perception $y$.

Karl Friston pointed out that there are two ways to minimize the VFE:

- Assuming that the external environment is fixed, i.e., the sensory data $y$ is also fixed, then the VFE can be reduced by getting hold of a better internal model $Q_{\theta}(x|y)$ of the environment.
- If the external environment is allowed to change, then the organism can reduce its VFE by changing the environment so that $-\log p(y)$ is reduced. The organism does so by taking actions and this is known as **Active Inference**.

In the first case the organism changes its internal model $Q_{\theta}$ to reduce the VFE, while in the second case the organism changes its environment $x^{*}$ (which changes the perception signals $y$) to reduce the VFE. 

The Active Inference framework is based on the minimization of a probabilistic quantity, namely the VFE. On the other hand we will see that the Predictive Processing framework is also based on the minimization of energy, but in this case the energy is an explicit thermodynamic quantity generated by the interaction between neurons.

## Models for Planning

All organisms have a model for the the environment along the lines that was described in the previous section. This enables them to react to changes in the environment, obtain food, reproduce etc. However higher organisms also have have the ability to carry out a sequence of actions in order to accomplish a task. The process by which they arrive at the right action sequence to use such that it results in success, is called planning. 
Solving the planning problem is tied to that of perception, since if the organism can use its world model to internally generate a sequence of actions and infer how the environment will react to them, before actually carrying out the actions.

We will describe two approaches to the problem of planning, namely the reinforcement learning or RL framework and the neuro-scientific theory of planning proposed by Karl Friston.
The RL framework is based on the idea that there is a reward associated with the completion of tasks, and organisms take a sequence of actions required to complete the task so as to maximize the reward. 
Individual actions themselves are solely a function of the state that the organism is in, and an optimal policy is one that chooses this mapping to maximize the reward.

The Friston theory, which is aprt of the Active Inference framework, does not use rewards. Instead it posits that an organism starts with an image of what the completed task looks like, and then decomposes it
into a sequence of images that get it to the desired end point. The actions themselves are determined automatically by the predictive processing framework as described in the previous section.


## The Reinforcement Learning Framework for Planning

![](https://subirvarma.github.io/GeneralCognitics/images/agent1.png) 

Figure 2: The Reinforcement Learning Control Framework: An Agent Acting in the Real World

The RL framework is shown above and it shows an organism operating in an environment. Assuming it takes action $A_n$ at time $n$ based on environmental state $O_n$, and this results in a change in its environment. The new environemntal state $O_{n+1}$ is then perceived by the agent, along with an option reward signal $R_n$. The reward signal tells the agent whether the action resulted in a positive outcome (or not). The agent then takes the next action $A_{n+1}$ and the loop goes through another cycle. RL is focused on choosing the actions sequence $A_1,...,A_n$ so as to maximixe the total reward over the lifetime of the agent.

![](https://subirvarma.github.io/GeneralCognitics/images/agent2.png) 

Figure 3: Model Based Control in Reinforcement Learning: An Agent Planning its Actions Based on an Internal Model

The RL framework shown in figure 2 leaves open the problem of how the agent figures out what action to take for a given state of the environment. But what if the agent posseses a model for the enviroment that allows it to predict the next state (and reward), as a function of the prior state and the action it took. This scenario is shown in figure 2, in which I have replaced the real world, by a model for the real world. This model allows the agent to try out various scenarios and sequences of actions, without actually taking any action in the real world, which is also called planning. Potentially this can enable it to figure out the best action for a given state of the environment and this is more fleshed out in figure 3.

![](https://subirvarma.github.io/GeneralCognitics/images/Agent31.png) 

Figure 4: Integration of Planning and Acting: Agent used its Internal Model to take better actions in the Real World

The above figure is similar to figure 2, except that now the agent has a 'brain' that contains a model for the world. Using this model the agent generates multiple scenarios driven by sequences of actions, and then chooses the scenario that has the best outcome in terms of the total reward received. It then carries out the first action in the sequence, which changes the environment state. The agent then incorporates the new information into its model, and then repeats the process. This model underlies the famous Go playing program AlphaGo from DeepMind from a few years ago. This framework shows how critical the world model is for this system to work.

*So far we I haven't talked about how to build a world model, and the question arises whether it can be built using ANNs, or more specifically an EBM. If the latter can be demonstrated, then this provides a model for how the brain operates, since in all likelihood the brain is an EBM consisting of biological neurons, as described in Part 3.*

*All living organisms, even plants, are thought to possess a model for their environment. These models vary in their level of sophistication depending upon the neural capacity of the organism, but in general contain enough information to enable the organism to carry out its day to day activities. For example single celled bacteria such as *E. Coli* sense their environment through sensors on their cell wall, and can move in the direction of food sources by using their flagellum. Theirs is a pretty rudimentary model of the environment, and doesn't even require neurons, but is sufficient for their purposes. As we move up the evolutionary ladder, the models become more sophisticated, and enable the animal to predict the state of the world several steps into the future. Humans have taken this capability to the extreme, our predictive powers extent all the wy to the death of the sun in a few billion years from now.*

## The Expected Free Enegy Framework for Planning



## A Model for Perception Using Diffusion based EBMs


##  Video Generation



### Video Clip Generation



### Autoregressive Video Generation

## Language Generation

Another activity that our brain does is language generation. LLMs that do this are the first AI models that leapt from the lab to the outside world and are currently more or less driving investment activity in the world economy. 
But can EBMs be used to generate language?
This field is still in its research phase, though there is a company called [Inception labs](https://www.inceptionlabs.ai/) that was recently founded to commercialize EBM based LLMs. 
If successful, EBM LLMs will have several advantages over the traditional autoregressive LLMs. The latter generate one word at a time which limits their speed of generation and also increases energy consumption. 
EBM based LLMs on the other hand are able to generate multiple words or even sentences in each step which can speed up generation and at a lower energy costs. This solves another problem that autoregressive models have, which is that a word generated cannot be erased. 
When we speak we typically don’t generate words one at a time. We have a thought that we then try to express in language and
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




## World Models: Incorporation of Actions into Video Generation Models

## A Systems Architecture for the Brain

The brain architecture described here is based on the work of the neuro-scientists Karl Friston and Andy Clark on predictive models for the brain. This is an EBM based model for the planning based perception-action framework shown in figure 4. Animals can broadly be classified into two categories: Type 1 are those whose actions are purely a function of what they are experiencing or perceiving at the moment, while type 2 are those who have the ability to plan ahead, so that their actions are governed by the task that they are trying accomplish. 

![](https://subirvarma.github.io/GeneralCognitics/images/stat73.png) 

Figure 5: A Model for the Brain for Type 1 animals: Short Term Action Generation 

The model shown in figure 5 is for the brain of type 1 animals and this includes all animals except for mammals and birds which are of type 2. The functions of the blocks shown in the model are as follows:

- World Model: This system takes in the current action $A_n$ and the perception state $X_n$, and generates a prediction for what the next state ${\hat X}_{n+1}$ should be.
- Perception Generator: This system takes the prediction ${\hat X_{n+1}}$ and the signal $c_{n+1}$ coming from the senses, and generates the next perception $X_{n+1}$. The EBM implementation of this module was described in [Part 3](https://github.com/subirvarma/GeneralCognitics/blob/main/_posts/2026-02-13-statmech3.md).
- Actor: This model uses the difference between the prediction ${\hat X_{n+1}}$ and the perception $X_{n+1}$ and uses it to generate the next action $A_{n+1}$. Its function to bring the state of the world to the point where the prediction agrees with reality.

![](https://subirvarma.github.io/GeneralCognitics/images/stat74.png) 

Figure 6: A Model for the Brain for Type 2 animals: Planning based Action Generation

There is a video prediction model in our brains that is contantly predicting the next frame that we are going to see. The actual image is generated by combining this information with the information
in sensory signals coming from the eyes (see figure 1).



Video prediction is also critical to building world models. As the name implies these are internal models of how the world evolves with time, and also how to raects to various events taking place,
and this includes the actions that we are taking. To understand this we will use the reinforcement learning framework shown in figure 2.


