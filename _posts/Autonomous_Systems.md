# The Evolution of Agents: From Reinforcement Learning to LLM Agents

## Introduction

An Intelligent Agent is defined as a system that is capable of doing tasks that are usually associated with a human worker. These tasks involve taking multiple actions to achieve an objective and also be able to react to feedback received during the course of the work. The most obvious example of one would be a robot or a game playing Agent. Industrial Robots have also been around for some time, but their behavior is hardwired and they are not capable of showing the adaptibility and flexibility one associated with a human. Agents such as Siri from Apple and the Google Assistant have been around for several years, but have limited capabilities. In recent years, as the discipline of Artificial Intelligence has advanced, we have begun to make progress in designing more intelligent Agents. These advances have come in the following two areas:

-  Intelligent Agents using Deep Reinforcement Learning (DRL) Algorithms: DRL Agents have had their greatest success in building Game Playing systems. They have been used successfully to play video games such as Atari, and more recently to play board games such as Go and Chess at the superhuman level. Progress in using them in robotics is not as advanced, for reasons that will be explained later. DRL based Agents have shown how Computer Vision, based on Deep Learning systems, can be incorporated in Agent design.
-  Intelligent Agents based on Large Language Models (LLMs): The current wave of excitement is in the area of Large Language Models or LLMs, that have the ability to generate human level text, and a lot more besides. A new type of Intelligent Agent that has become possible due to the availability of LLMs. Their capabilities are still being explored, but initial work suggests that they may be capable of advancing Intelligent Agent technology beyond what was acheivable until now.

Both DRL and LLM based Agents use Artificial Neural Networks (ANN) and the associated Deep Learning Technology. These systems, that are modeled after the brain, had so far excelled in tasks that involved sensory processing, such as vision or speech. The invention of a new Deep Learning system called the Transformer, has now made them very good at language related tasks. 
An essential aspect that had been missing until now was the problem of equiping Intelligent Agents with the capability to understand language and also form what is called a "World Model". 
These are thought to be essential in the way humans operate, since it enables them to form mental models of the world and thus plan out their actions in advance of performing them. An unexpected benefit of LLMs seems to be that even though they are trained using simple next word prediction, they seem to have formed a World Model that can be used for Planning. This is an example of an Emergent Ability in LLMs, i.e., their ability to acquire new skills simply by scaling up the size of the LLM model.

The rest of this blog is organized as follows: We start with a discussion of DRL Agents. These can be classified as purely Neural Network based or using a combination of Neural Networks and Algorithmic techniques and both these are described. The following section is on the emerging field of LLM Agents. We survey two research papers in this area, one of them from the field of Robotics and the other from human behavior simulation. The following section points out some interesting similarities in the operation of Intelligent Agents and the Kahneman-Tversky theory of human decision making.

## Deep Reinforcement Learning Agents

![](https://subirvarma.github.io/GeneralCognitics/images/agent1.png) 

The easiest way to understand the discipline of RL is to think about how animals, such as a dog, get trained. Since they don't understand human language, the only way to make them do what we want is by rewarding them. Usually this messsage does not get to the dog with only a single instance of the reward, but has to be repeated multiple times before the animal gets it (hence the 'reinforcement' in the name). The Agent in this case is the dog, and a more general picture of the framework used in RL is shown in Figure 1. There is an Agent that is capable of taking one or more Actions, and an Action results in some change in the environment the Agent is operating in. The results of the environment change are communicated back to the Agent, in addition to a scalar number called the **Reward**. In order to make the Agent acheive some objective, which usually takes several Actions and thus several traversals though the loop, the Agent is **trained**. During the training, if the Agent's Actions are such that they make progress towards the objective, then those Actions result in higher reward, and if not then the reward is witheld. Hence the Agent gets trained by means of the reward signal, and carries out Actions that result in the maximization of the sum of the rewards it receives over the course of the task.

This technique of using the reward signal as means to make the RL Agent do what we want it to do, works as long as the objective is somewhat simple and of limited scope. However to build Agents that are capable to doing more human-like tasks RL runs into problems. For example if we want to design an robot (controlled by a RL Agent) that is capable of doing our dishes, what reward signal should we use? The basic issue is that the RL Agent does not have a mental model of the world we live in, and also cannot understand language. If you ask a human to do something, how does he (or she) go about the job? We can modify Figure 1 slightly to show this, as in Figure 2.

![](https://subirvarma.github.io/GeneralCognitics/images/agent2.png) 

Usually the human takes the time to think through, or plan, how to acheive the objective as opposed to immediately starting Actions. During this time, the human uses a model of the world, to figure out the sequence of Actions to take, and result of these actions on the Environment. Once the planning is complete, then the task is actually started. The human does not need to be reinforced after each step with a reward, but is able to able to figure out what is required since he understands language and also has a model of the world. Thus lack of a World Model and lack of language understanding are the two critical shortcomings that have held back RL Agents. Until a few years ago these seemed to be unsurmountable problems. Reserachers had little to no understanding of how world models are built in human brains, which is a very complex process that takes place all throughout our childhood and beyond.

![](https://subirvarma.github.io/GeneralCognitics/images/agent9.png) 

The process of decision making is captured in the graph shown above. The white circles represent the state of the world, while the black circles represent Actions that the Agent may take. Note that there is more than one Action (black circle) associated with each State (white circle), which models the fact that the Agent has a choice of multiple Actions that he can perform in each State, and has to decide on the right Action. Also once an Action is taken, there are multiple possible States that the sysem may transition to. This captures the uncertainity in the World Model: For example if the Agent is playing a video game, then the game may spring an unexpected surprise after the player takes an Action. The Agent starts the decision making from the top of the Graph, and as he performs Actions, he proceeds on a path down the Graph, until the task is complete (this is shown a terminal state marked T). Once such path is marked in red in the figure. Some of these paths result in a successful completion of the task, while others result in failure. While planning  how to do the task, the decision maker has to choose a sequence of Actions that result in success. A critical factor in order to do this is the ability for the Agent to visualize the effects of its Actions on the World. The lack of a such a World Model that could do this was a critical factor that hobbled Intelligent Agents until now. LLMs remove this constraint, and enable the Agent to plan its Actions just as human would. 


### Agents of Type 1: Neural Network Based

![](https://subirvarma.github.io/GeneralCognitics/images/agent3.png) 

The Figure above shown a RL Agent that is being trained to play Atari games. The Actions in this case are the movements of the game controller, while the environment or world that the Agent operates in, are the successive screens of the game. every time the Agent takes an Action, the screen changes and the Agent receives a reward from the game. The Agent, which is a Neural Network, is trained by playing the game hundreds of thousands of times, and observing the effects of its Actions on the reward and the next screen (the algorithm used is called DQN which stands for Deep Q-Networks).

![](https://subirvarma.github.io/GeneralCognitics/images/agent4.png) 

Once the Agent is trained, it can be used to play the game, and this is shown above. The last 4 screen shots are fed into the Agent, which then figures out what the next Action should be. This in turn leads to the next screen in the game, which is in turn fed into the Agent, and the cycle continues. 

We are calling this type of RL Agent, that is implemented using a Neural Network, as an Agent of Type 1. These Agents are characterised by:

-   They are Model Free, i.e., they don't incorporate a World Model. Hence the only way to train them is by using Model Free RL, which is a very time consuming process, requiring hundreds and thousands of iterations. This is also means that these Agents are incapable of planning in advance. The only way to train them is by dropping them in the environment and proceeding by trial and error.
-   The policy which they use to take their Actions is purely a function of the input state (which in this case is the game screen). This policy is 'hardwired' into the Neural Network, so for example, the same Agent cannot be used to play other games.

Hence training Agents of Type 1 is very much like training a dog, and the trained Neural Network is like the trained dog's brain, which instinctively knows how to perform the task it was trained for, but not any new task (without further training).


### Agents of Type 2: Algorithmic + Neural Networks

![](https://subirvarma.github.io/GeneralCognitics/images/agent5.png) 

There is another type of RL Agent, the most famous example of which the Alpha Zero game plating system from Deep Mind. The initial version of these Agents required a model of the game being played, hence its use was limited to board games such as Go or Chess (for these games, a model of the game is the same as the rules of the game). The Alha Zero system also incorporated a Neural Network, whose input is the current board configuration and its output is the next move, this is shown in Part (b) of the figure. However in the addition to the next move, the Neural Network has another output: This is shown as the letter 'V' in the figure, and it stands for the probability that the current board position will in fact lead to a winning game.

The critical difference between the way Alpha Zero plays, vs Type 1 Agents, is shown in Part (a) of the figure. For every move, Alpha Zero runs a quick simulation of the game, starting from the current position (shown in the tree graph), known as a Monte Carlo Tree Search or MCTS. In order to run this simulation, it uses the rules of the game (or model), and also the Neural Network from Part (b). It builds as much of the tree graph as it in the finite allocated between moves, and from that it figures out the best move to make.  Since there is usually not enough time to complete an entire game during the simulation, the winning probability number V used to make an educated guess whether in fact the last board position in the tree is in fact a winning one. 




## LLM Based Agents

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
