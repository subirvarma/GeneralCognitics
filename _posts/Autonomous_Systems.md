# The Evolution of Agents: From Reinforcement Learning to LLM Agents

## Introduction

A few years ago the Nobel Laureate Daniel Kahneman published a book called *Thinking Fast and Slow*. This book was based on research that he had carried out
with his late collaborator Amos Tversky over the course of more than 30 years. These scientists discovered that there is an interesting structure in the way the human
brain works. Our thinking process can be neatly split into two types: 

-  The first type, which they called System 1, is the part of our thinking that takes place outside our field of consciousness and happens automatically and quickly. All instances of perception and memory fall in this category, as does the type of thinking called intuitive. A typical example would be when we meet a person and are able to immediately tell whether it is someone we know. 
-  The second type called System 2 is the part of our thinking that we are conscious of, and requires an appreciable amount of mental effort to carry out. A typical example here would multiplying two numbers together. All System 2 operations require or attention, and are disrupted when our attention is drawn away.

Kahneman remarks in his book that System 1 seems to maintain a world model in our brain, which works for most day-to-day functions. However whenever the model is violated, for example we see something out of the ordinary, then System 2 is invoked.

In the last few years, we have begun to build Artificial Neural Networks (ANNs) that mimic certain operations of the human brain. These systems first drew attention due to their ability to classify images, and this was not that long ago, in 2012 to be exact when AlexNET was invented. Later they were coupled with the discipline of Reinforcement Learning to make Deep Reinforcement Learning (DRL) systems that were able to make decisions and play games, even video games like Atari, at the superhuman level. The current wave of excitement is in the area of Large Language Models or LLMs, that have the ability to generate human level text, and a lot more besides. 

DRL and LLM systems share an additional characteristic: They can be used to make **Intelligent Agents**. An Agent is defined as an entity that is capable of interacting with the external world and take actions that may affect its environment. Furthermore, given an objective, it is capable of making intelligent decisions which enable it to achieve its goal. Agents were initially defined in the context of RL and DRL systems, and more recently they have been constructed using LLM systems.

We survey the current State of the Art for both DRL and LLM Agents, and point out an interesting similarity in their operation and Kahneman's ideas regarding System 1 and System 2 in the human brain. In particular:

-   Agents that are implemented using Neural Networks are analagous to System 1
-   In LLM Agents, System 2 operation is connected to the concept of Chain of Though (CoT) reasoning. There are some very interesting similarities between the way CoT works and what we know about System 2 in the human brain.
-   DRL Agents have been built using a combination of Neural Networks and an algorithm called Monte Carlo Tree Search or MCTS. Even though the analogy with System 2 is not perfect for this case, there are some interesting similarities here as well.


## Deep Reinforcement Learning Agents

- Training a dog

### Agents of Type 1: Neural Network Based

### Agents of Type 2: Algorithmic + Neural Networks

## LLM Based Agents

### The SayCAN Robot System with Inner Monologue

### Generative Agents with Memory and Planning
