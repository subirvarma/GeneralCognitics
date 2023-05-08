# The Evolution of Agents: From Reinforcement Learning to LLM Agents

## Introduction

An Intelligent Agent is defined as a system that is capable of doing tasks that are usually associated with a human worker. These tasks involve taking multiple actions and also be able to react to feedback received during the course of the work. The most obvious example of one would be a robot or a game playing Agent. Industrial Robots have been around for some time, but their behavior is hardwired and they are not capable of showing the adaptibility and flexibility one associated with a human. Agents such as Siri from Apple and the Google Assistant have been around for several years, but have limited capabilities. In recent years, as the discipline of Artificial Intelligence has advanced, we have begun to make progress in designing more intelligent Agents.These advances have come in the following two areas:

-  Intelligent Agents using Deep Reinforcement Learning (DRL) Algorithms: DRL Agents have had their greatest success in building Game Playing systems. They have been used successfully to play video games such as Atari, and more recently to play board games such as Go and Chess at the superhuman level. Progress in using them in robotics is not as advanced, for reasons that will be explained later. DRL based Agents hva shown how Computer Vision, based on Deep Learning systems, can be incorporated in Agent design.
-  Intelligent Agents based on Large Language Models (LLMs): This a new type of Intelligent Agent that has become possible due to the availability of LLMs. Their capabilities are still being explored, but initial work suggests that they may be capable of advancing this technology beyond what was acheivable until now.

Both DRL and LLM based Agents use Artificial Neural Networks (ANN) and the associated Deep Learning Technology. These systems, that are modeled after the brain, had so far excelled in tasks that involved sensory processing, such as vision or speech. The invention of a new Deep Learning system called the Transformer, has now made them very good at language related tasks. An essential aspect that had been missing until now was the problem of equiping Intelligent Agents with the capability to form what is called a "World Model". These are thought to be essential in the way humans operate, and it enables them to do form mental models of the world and thus plan out their actions in advance of performing them. An unexpected benefit of LLMs seems to be that even though they are trained using simple next word prediction, they seem to have formed a World Model. This is an example of an Emergent Ability in LLMs, their ability to acquire new skills simply by scaling up the size of the LLM model.

A few years ago the Nobel Laureate Daniel Kahneman published a book called *Thinking Fast and Slow*. This book was based on research that he had carried out
with his late collaborator Amos Tversky over the course of more than 30 years. These scientists discovered that there is an interesting structure in the way the human
brain works. Our thinking process can be split roughly into two types: 

-  The first type, which they called System 1, is the part of our thinking that takes place outside our field of consciousness and happens automatically and quickly. All instances of perception and memory fall in this category, as does the type of thinking called intuitive. A typical example would be when we meet a person and are able to immediately tell whether it is someone we know. 
-  The second type called System 2 is the part of our thinking that we are conscious of, and requires an appreciable amount of mental effort to carry out. A typical example here would multiplying two numbers together. All System 2 operations require attention, and are disrupted when our attention is drawn away.

Kahneman remarks in his book that System 1 seems to maintain a world model in our brain, which works for most day-to-day functions. However whenever the model is violated, for example we see something out of the ordinary, then System 2 is invoked.

In the last few years, we have begun to build Artificial Neural Networks (ANNs) that mimic certain operations of the human brain. These systems first drew attention due to their ability to classify images, and this was not that long ago, in 2012 to be exact when AlexNET was invented. Later they were coupled with the discipline of Reinforcement Learning to make Deep Reinforcement Learning (DRL) systems that were able to make decisions and play games, even video games like Atari, at the superhuman level. The current wave of excitement is in the area of Large Language Models or LLMs, that have the ability to generate human level text, and a lot more besides. 

DRL and LLM systems share an additional characteristic: They can be used to make **Intelligent Agents**. An Agent is defined as an entity that is capable of interacting with the external world and take actions that may affect its environment. Furthermore, given an objective, it is capable of making intelligent decisions which enable it to achieve its goal. Agents were initially defined in the context of RL and DRL systems, and more recently they have been constructed using LLM systems.

We survey the current State of the Art for both DRL and LLM Agents, and point out an interesting similarity in their operation and Kahneman's ideas regarding System 1 and System 2 in the human brain. In particular:

-   Agents that are implemented using a single prompt of an LLM or a single invocation of Neural Network (in the case of DRL) are analagous to System 1
-   Agents that are implemented using a combination of Neural Networks and logical reasoning, are analogous to System 2. 

In LLM Agents, System 2 operation is connected to the concept of Chain of Though (CoT) reasoning. There are some very interesting similarities between the way CoT works and what we know about System 2 in the human brain. DRL Agents have been built using a combination of Neural Networks and an algorithm called Monte Carlo Tree Search or MCTS. Even though the analogy with System 2 is not perfect for this case, there are some interesting similarities here as well.

In general System 2 operation in Agents seems to connected to the idea of running Neural Networks multiple times during a computation, so that later stages are able to make use of results of the prior stages. In the context of an LLM, from this we can surmise that more powerful Agents can be created by increasing the context length of the data that is fed into it. This enables the LLM to make use of more results from the intermediate steps of the System 2 type operation.


## Deep Reinforcement Learning Agents

![](https://subirvarma.github.io/GeneralCognitics/images/agent1.png) 

The easiest way to understand the discipline of RL is to think about how animals, such as a dog, get trained. Since they don't understand human language, the only way to make them do what we want is by rewarding them if they indeed do it. Usually this messsage does not get to the dog with only a single instance of the reward, but has to be repeated multiple times before the animal gets it. Hence the Agent in this case is the dog, and a more general picture of the framework used in RL is shown in Figure 1. There is an Agent that is capable of taking one or more Actions, and an Action results in some change in the environment the Agent is operating in. The results of the environment change are communicated back to the Agent, in addition to a scalar number called the **Reward**. In order to make the Agent acheive some objective, which usually takes several Actions and thus several traversals though the loop, the Agent is **trained**. During the training, if the Agent's Actions are such that they lead to acheiving the objective, then those Actions result in higher reward, and if not then the reward is witheld. Hence the Agent gets trained by means of the reward signal, and carries out Actions that result in the maximization of the sum of the rewards from each step.

This technique of using the reward signal as means to make the RL Agent do what we want it to do, works as long as the objective is somewhat simple and of limited scope. However to build Agents that are capable to doing more human-like tasks RL runs into problems. For example if we want to design an robot (controlled by a RL Agent) that is capable of doing our dishes, what reward signal should we use? The basic issue is that the RL Agent does not have a mental model of the world we live in, and also cannot understand language. If you ask a human to do something, how does he (or she) go about the job? We can modify Figure 1 slightly to show this, as in Figure 2.

![](https://subirvarma.github.io/GeneralCognitics/images/agent2.png) 

Usually the human takes the time to think through how to acheive the objective as opposed to immediately starting Actions. During this time, the human uses a model of the world, that exists in brains, to figure out the sequence of Actions to take, and result of these actions on the Environment. Once this process is complete, then the task is actually started. The human does not need to be reinforced after each step with a reward, but is able to able to figure out what is required since he understands language also has a model of the world.

Thus lack of a World Model and lack of language are the two critical shortcomings that have held back RL Agents. Until a few years ago these seemed to be unsurmountable problems. Reserachers had little to no understanding of how world models are built in human brains, which is a very complex process that takes place all throughout our childhood and beyond. 


### Agents of Type 1: Neural Network Based

### Agents of Type 2: Algorithmic + Neural Networks

## LLM Based Agents

### The SayCAN Robot System with Inner Monologue

### Generative Agents with Memory and Planning
