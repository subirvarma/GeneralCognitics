# The Evolution of Agents: From Reinforcement Learning to LLM Agents

## Introduction

An Intelligent Agent is defined as a system that is capable of doing tasks that are usually associated with a human worker. These tasks involve taking multiple actions to achieve an objective and in some cases also be able to react to feedback received during the course of the task. The most obvious example of one would be a robot or a game playing Agent. Industrial Robots have also been around for some time, but their behavior is hardwired and they are not capable of showing the adaptibility and flexibility one associated with a human. 
Agents such as Siri from Apple and the Google Assistant have been around for several years, but have limited capabilities. 

In recent years, as the discipline of Artificial Intelligence has advanced, we have begun to make progress in designing more intelligent Agents. These advances have come in the following two areas:

-  Intelligent Agents using Deep Reinforcement Learning (DRL) Algorithms: DRL Agents have had their greatest success in building Game Playing systems. They have been used successfully to play video games such as Atari, and more recently to play board games such as Go and Chess at the superhuman level. Progress in using them in robotics is not as advanced, for reasons that will be explained later. DRL Agents work by using Rewards as a way to motivate the Agent to exhibit the desired behavior.
-  Intelligent Agents based on Large Language Models (LLMs): The current wave of excitement is in the area of Large Language Models or LLMs, that have the ability to generate human level text, which has been their initial application. However more and more evidence is piling up that LLMs are also capable of forming World Models and also do Task Planning, which are the fundamental abilities needed for an Intelligent Agent. As a result, new types of Intelligent Agents have become possible. Their capabilities are still being explored, but initial work suggests that they may be capable of advancing Intelligent Agent technology beyond what was acheivable until now.

Both DRL and LLM based Agents use Artificial Neural Networks (ANN) and the associated Deep Learning Technology. These systems, that are modeled after the brain, had so far excelled in tasks that involved sensory processing, such as vision or speech. The invention of a new Deep Learning system called the Transformer, has now made them very good at language related tasks. 
An essential aspect that had been missing until now was the problem of equiping Intelligent Agents with the capability to understand language and also form what is called a "World Model". 
These are thought to be essential in the way humans operate, since it enables them to form mental models of the world and thus plan out their actions in advance of performing them. An unexpected benefit of the largest LLMs seems to be that even though they are trained using simple next word prediction, they seem to have formed World Models that can be used for Planning. This is an example of an Emergent Ability in LLMs, i.e., their ability to acquire new skills simply by scaling up the size of the LLM model.

The rest of this blog is organized as follows: We start with a discussion of Deep Reinforcement Learning Agents. These can be classified as purely Neural Network based or using a combination of Neural Networks and Algorithmic techniques and both of these are described. The following section is on the emerging field of LLM based Agents. We discuss evidence that LLMs are indeed capable to generating their own World Models as a result of their training. We also discuss various techniques that can be used for Task Planning using LLMs, which is a very active area with new results almost on a daily basis. We point out some interesting similarities in the operation of Intelligent Agents and the Kahneman-Tversky theory of human decision making.

## Deep Reinforcement Learning Agents

![](https://subirvarma.github.io/GeneralCognitics/images/agent1.png) 

Figure 1

The easiest way to understand the discipline of RL is to think about how animals, such as a dog, get trained. Since they don't understand human language, the only way to make them do what we want is by rewarding them when they perform the correct Action. Usually this messsage does not get to the dog with only a single instance of the reward, but has to be repeated multiple times before the animal 'gets it' (hence the word 'reinforcement' in the name). The Agent in this case is the dog, and a more general picture of the framework used in RL is shown in Figure 1. There is an Agent that is capable of taking one or more Actions, and an Action results in some change in the environment the Agent is operating in. The results of the environment change are communicated back to the Agent, in addition to a scalar number called the **Reward**. In order to make the Agent acheive some objective, which usually takes several Actions and thus several traversals though the loop, the Agent is **trained**. During the training, if the Agent's Actions are such that they make progress towards the objective, then those Actions result in higher reward, and if not then the reward is witheld. Hence the Agent gets trained by means of the reward signal, and carries out Actions that result in the maximization of the sum of the rewards it receives over the course of the task.

This technique of using the reward signal as means to make the RL Agent do what we want it to do, works as long as the objective is somewhat simple and of limited scope. However to build Agents that are capable to doing more human-like tasks RL runs into problems. For example if we want to design an robot (controlled by a RL Agent) that is capable of doing our dishes, what reward signal should we use? The basic issue is that the RL Agent does not have a mental model of the world we live in, and also cannot understand language. If you ask a human to do something, how does he (or she) go about the job? We can modify Figure 1 slightly to show this, as in Figure 2.

![](https://subirvarma.github.io/GeneralCognitics/images/agent2.png) 

Figure 2

Usually the human takes the time to think through, or plan, how to acheive the objective as opposed to immediately starting Actions. During this planning stage, the human uses a model of the world, to figure out the sequence of Actions to take, and result of these actions on the Environment. Once the planning is complete, then the task is actually started. The human does not need to be reinforced after each step with a reward, but is able to able to figure out what the sequence of Actions to be performed (called Planning) since he understands language and also has a model of the world. Thus lack of a World Model and lack of language understanding are the two critical shortcomings that have held back RL Agents. Until a few years ago these seemed to be unsurmountable problems. Researchers had little to no understanding of how world models are built in human brains, which is a very complex process that takes place all throughout our childhood and beyond.

![](https://subirvarma.github.io/GeneralCognitics/images/agent9.png) 

Figure 3

The process of human decision making is captured in the graph shown above. The white circles represent the state of the world, while the black circles represent Actions that the Agent may take. Note that there is more than one Action (black circle) associated with each State (white circle), which models the fact that the Agent has a choice of multiple Actions that he can perform in each State, and has to decide on the right Action. Also once an Action is taken, there are multiple possible States that the sysem may transition to. This captures the uncertainity in the World Model: For example if the Agent is playing a video game, then the game may spring an unexpected surprise after the player takes an Action. The Agent starts the decision making from the top of the Graph, and as he performs Actions, he proceeds on a path down the Graph, until the task is complete (this is shown a terminal state marked T). Once such complete path is marked in red in the figure. Some of these paths result in a successful completion of the task, while others result in failure. While planning  how to do the task, the Agent has to choose a sequence of Actions that result in success. This sequence of Actions can either be taken in the real world (such as an Agent playing chess), or they can be taken within the "brains" of the Agent without impacting the external world (such as thinking about what to do before actually doing it). The latter approach is called **Planning** and is integral to the way we human's operate. Given a task, we plan out how to do it using a tree like the one shown in Figure 3, and then proceed to actually carry out the task. A critical factor to do planning is the ability for the Agent to visualize the effects of its Actions on the World. The lack of a such a World Model that could be used for Planning was a critical factor that hobbled Intelligent Agents until now. LLMs remove this constraint, and enable the Agent to plan its Actions just as a human would. 


### Agents of Type 1: Solely Neural Network Based

![](https://subirvarma.github.io/GeneralCognitics/images/agent3.png) 
Figure 4

The Figure above shown an RL Agent that is being trained to play Atari games. The Actions in this case are the movements of the game controller, while the environment or world that the Agent operates in, are the successive screens of the game. Every time the Agent takes an Action, the screen changes and the Agent receives a reward from the game. The Agent, which is a Neural Network, is trained by playing the game hundreds of thousands of times, and observing the effects of its Actions on the reward and the next screen that is displayed (the algorithm used is called DQN which stands for Deep Q-Networks).

![](https://subirvarma.github.io/GeneralCognitics/images/agent4.png) 

Figure 5

Once the Agent is trained, it can be used to play the game, and this is shown above. The last 4 screen shots are fed into the Agent, which then figures out what the next Action should be. This in turn leads to the next screen in the game, which is in turn fed back into the Neural Network, and the cycle continues. 

We are calling this type of RL Agent, that is implemented using a Neural Network, as an Agent of Type 1. These Agents are characterised by:

-   They are Model Free, i.e., they don't incorporate a World Model. Hence the only way to train them is by using Model Free RL, which is a very time consuming process, requiring hundreds and thousands of iterations through the loop shown in Figure 4. This is also means that these Agents are incapable of planning in advance. The only way to train them is by dropping them in the real environment in which they will be operating and proceeding by trial and error.
-   The policy which they use to take their Actions is purely a function of the input state (which in this case is the game screen). This policy is 'hardwired' into the Neural Network, so for example, the same Agent cannot be used to play other games.

Hence training Agents of Type 1 is very much like training a dog, and the trained Neural Network is like the trained dog's brain, which instinctively knows how to perform the task it was trained for, but not any new task (without further training).


### Agents of Type 2:  Planning before Acting 

![](https://subirvarma.github.io/GeneralCognitics/images/agent5.png) 

Figure 6

There is another type of RL Agent, the most famous example of which the Alpha Zero game playing system from Deep Mind. The initial version of these Agents required a model of the game being played, hence its use was limited to board games such as Go or Chess (for these games, a model of the game is the same as the rules of the game). The Alpha Zero system also incorporated a Neural Network, whose input is the last few board configuration and its output is the next move. This is shown in Part (b) of the figure where the model outputs the probabilities *p* that the Agent should make a particular move. However in the addition to the next move, the Neural Network has another output: This is shown as the letter 'V' in the figure, and it stands for the probability that the current board position will in fact lead to a winning game. This is analogous to a human looking at the board and making an intuitive judgement whether it will lead to a winning game. 

The critical difference between the way Alpha Zero plays, vs Type 1 Agents, is shown in Part (a) of the figure. For every move, Alpha Zero runs a quick simulation of the game, starting from the current position known as a Monte Carlo Tree Search or MCTS (this is shown in the tree graph). In order to run this simulation, it uses the rules of the game (or model), and also the Neural Network from Part (b). It builds as much of the tree graph as it can in the finite time allocated between moves, and from that it figures out the best move to make.  Since there is usually not enough time to complete an entire game during the simulation, the winning probability number V used to make an educated guess whether in fact the last board position in the tree is in fact a winning one. Hence the operation of Alpha Zero involves a combination of 'mental' Planning, followed by taking an Action in the real world of the game. During the Planning process, the Agent tries out several potential moves (which is represented by the Tree in Figure 6), and then chooses the best move, which then gets played. This is closer to the way humans act to achieve an objective, which is a combination of mental Planning, followed by Actions.

In our daily life, the majority of our decisions are of Type 1 and take place 'automatically' or 'intuitively' as we go about our day. This corresponds to single pass through our neural network, which has already been pre-trained to do routine tasks through thousands of iterations of training from our childhood onwards. On the other hand, when we perform a task that is not routine, such as planning for a vacation or playing a board game, then it requires planning. This is accomplished by a tree type decision structure shown in Figure 6(a) where various alternatives are fleshed out and weighed for their chances of success. This takes up more of our mental energy, since it requires multiple passes through our neural network. 

## LLM Based Agents

Large Language Models or LLMs appeared in 2017 with the system called GPT1 from OpenAI, this was soon after the invention of Transformers, which is the base technology that they use. Since then, OpenAI has released progressively larger models, and the current model with 175B parameters is called GPT4. OpenAI also released a version of its LLMs called ChatGPT in 2022, which combined LLM technology with two other techniques: (1) Fine tuning of the LLM using Supervised Learning with human teachers (called Supervised Fine Tuning or SFT), (2) Training of the LLM to avoid toxic and dangerous content as well as hallicunations using a technique called Reinforcement Learning based on Human Feedback (RLHF). The resulting model was released by OpenAI as a service (and also incorporated into the Microsoft Bing search engine), and quickly racked up more than 100 million subscribers within a month of release, faster than any previous technology. This model seems to exhibit an understanding of the world, which it uses to answer questions in a human like manner, and its capabilities far exceed any other LLM that has been released. An especially exciting find is that the model has what are known as Emergent Properties. These are capabilities that have not been explicitly programmed or trained into the model, but the model nevertheless acquires these skills when its size exceeds certain thresholds. Trying to explain how this happens is an active area of research. Important Emergent Properties include:

-   Ability to synthesize Code
-   Chain of Thought Prompting or CoT: This is the ability of the LLM to better solve Arithmetic or Symbolic Reasoning tasks by adding an example of solution of a similar problem, but with an explanantion provided, as part of the prompt.

Shortly after the appearance of ChatGPT, researchers began to embed it within the framework of a larger system which they called Autonomous Agents. The motivation behind this was to design more powerful systems that take advantage of the capabilities of the LLM, and also give it additional skills that ChatGPT lacks. These include skills such as: Surfing the Web, using tools such as calculators and WolframAlpha, invoking other Neural Networks for Image Processing or Auditory Processing tasks, synthesis of Python code (which is then executed) etc. Another important addition was that of a memory module, to store the results of intermediate computations.

The common feature of these systems is use of the LLM not so much for generating text, but as a planner. Given a task, the LLM is able to decompose the work into a series of simpler tasks that it then farms out to itself or to other tools available to it. In order to do this, the LLM needs an understanding of the world in which the task is to be performed, i.e., it needs a World Model. Evidence has piled in the last year or two that LLMs do indeed form World Models as a result of their training, and this is reviewed in the next section.

## LLMs and World Models

- Chess
- Othello
- Color and Spatial Semantics
- Language Semantics

LLMs are trained using using Self Supervised Learning on huge corpora of text, by using the next word prediction method. As a result, an LLM in the inference phase works by sucecssively predicting the next word, after it has been give a few words to start off with (called the context). The prediction is done in a probabilistic fashion, with the LLM generating a probability distribution over all the words in the vocabulary, from which a particular word is chosen based on some criteria, such as the word with the highest probability. When LLMs were first invented, over ten years ago, it was thought that the word generation process is purely probabilistic and words are generated on the basis of how frequently the same word occurs in a similar context in the training dadaset. However LLMs were first implemented using less powerful Neural Networks such as RNNs or LSTMs and they were not able to scale up to very large sizes. With the invention of Transformers, it became possible to scale up LLMs to hundreds of billions of parameters, and at the same time train them on massive text datasets. The resulting LLMs, such the GPT 3 or the GPT 4 seem to have new emergent properties that were not seen in smaller models, and one of these properties may be the existence of a World Model based on the input data. The evidence that is indeed the case has been accumulating, but is not yet universally accepted. For example Yann LeCun has maintained LLMs are incapable of forming World Models, and he has made the suggestion that visual prediction is necessary for this to happen, which is apparantly the way the human brain forms models.

In this section we review the evidence for World Models in LLMs. The first two examples are from the space of Board Games, with Transformers trained not on language, but on sequences of game moves. World Models for Board Games are much simpler than those in the real world, but they are also more tractable due to their simplicity. However they are still complicated enough to enable us to investigate their properties. In the following two Sections we first look at the game of Othello followed by Chess.


**Transformer based World Models for the Game of Othello**

![](https://subirvarma.github.io/GeneralCognitics/images/agent10.png) 


![](https://subirvarma.github.io/GeneralCognitics/images/agent12.png) 


![](https://subirvarma.github.io/GeneralCognitics/images/agent11.png) 



**Transformer based World Models in Chess**



**LLM based World Models**



## Planning Using LLMs





### BabyAGI



### AutoGPT





### The SayCAN Robot System with Inner Monologue

![](https://subirvarma.github.io/GeneralCognitics/images/agent6.png) 


### Generative Agents with Memory and Planning Abilities

![](https://subirvarma.github.io/GeneralCognitics/images/agent7.png) 

![](https://subirvarma.github.io/GeneralCognitics/images/agent8.png) 


## Connections with Kahnemann-Tversky Theory of Human Decision Making

A few years ago the Nobel Laureate Daniel Kahneman published a book called *Thinking Fast and Slow*. This book was based on research that he had carried out
with his late collaborator Amos Tversky over the course of more than 30 years. These scientists discovered that there is an interesting structure in the way the human
brain works. Our thinking process can be split roughly into two types: 

-  The first type, which they called System 1, is the part of our thinking that takes place outside our field of consciousness and happens automatically and quickly. All instances of perception and memory fall in this category, as does the type of thinking called intuitive. A typical example would be when we meet a person and are able to immediately tell whether it is someone we know. 
-  The second type called System 2 is the part of our thinking that we are conscious of, and requires an appreciable amount of mental effort to carry out. A typical example here would multiplying two numbers together. All System 2 operations require attention, and are disrupted when our attention is drawn away.

Kahneman remarks in his book that System 1 seems to maintain a world model in our brain, which works for most day-to-day functions. However whenever the model is violated, for example we see something out of the ordinary, then System 2 is invoked.

We survey the current State of the Art for both DRL and LLM Agents, and point out an interesting similarity in their operation and Kahneman's ideas regarding System 1 and System 2 in the human brain. In particular:

-   Agents that are implemented using a single prompt of an LLM or a single invocation of Neural Network (in the case of DRL) are analagous to System 1
-   Agents that are implemented using a combination of Neural Networks and logical reasoning, are analogous to System 2. 

In LLM Agents, System 2 operation is connected to the concept of Chain of Though (CoT) reasoning. There are some very interesting similarities between the way CoT works and what we know about System 2 in the human brain. DRL Agents have been built using a combination of Neural Networks and an algorithm called Monte Carlo Tree Search or MCTS. Even though the analogy with System 2 is not perfect for this case, there are some interesting similarities here as well.

In general System 2 operation in Agents seems to connected to the idea of running Neural Networks multiple times during a computation, so that later stages are able to make use of results of the prior stages. In the context of an LLM, from this we can surmise that more powerful Agents can be created by increasing the context length of the data that is fed into it. This enables the LLM to make use of more results from the intermediate steps of the System 2 type operation.
