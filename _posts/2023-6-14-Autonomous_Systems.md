---
layout: default
title: "The Evolution of Agents: From Reinforcement Learning to LLM Agents"
---

# LLM Based Autonomous Agents

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

LLMs are trained using using Self Supervised Learning on huge corpora of text, by using the next word prediction method. As a result, an LLM in the inference phase works by sucecssively predicting the next word, after it has been give a few words to start off with (called the context). The prediction is done in a probabilistic fashion, with the LLM generating a probability distribution over all the words in the vocabulary, from which a particular word is chosen based on some criteria, such as the word with the highest probability. When LLMs were first invented, over ten years ago, it was thought that the word generation process is purely probabilistic and words are generated on the basis of how frequently the same word occurs in a similar context in the training dadaset. However LLMs were first implemented using less powerful Neural Networks such as RNNs or LSTMs and they were not able to scale up to very large sizes. With the invention of Transformers, it became possible to scale up LLMs to hundreds of billions of parameters, and at the same time train them on massive text datasets. The resulting LLMs, such the GPT3 or the GPT4 seem to have new emergent properties that were not seen in smaller models, and one of these properties may be the existence of a World Model. The evidence that is indeed the case has been accumulating, but is not yet universally accepted. For example Yann LeCun has maintained LLMs are incapable of forming World Models, and he has made the suggestion that visual prediction is necessary for this to happen, which is apparantly the way the human brain forms models.

In this section we review the evidence for World Models in LLMs. The first two examples are from the space of Board Games, with Transformers trained not on language, but on sequences of game moves. World Models for Board Games are much simpler than those in the real world, but they are also more tractable due to their simplicity. However they are still complicated enough to enable us to investigate their properties. In the following two Sections we first look at the game of Chess followed by Othello. It is shown that even though the model is trained to predict just the next move, it actually learns to compute the full board state at each move, i.e. the World Model. Hence rather than predicting the next move based on statistical correlations about the distribution of moves, the LLM actually learns to model the underlying process that generated that data.

## LLM based World Models in Chess

![](https://subirvarma.github.io/GeneralCognitics/images/agent13.png)

Figure 7

Traditional LLMs are built using large Transformer models traned of billions of language tokens. Progress is being made in extracting evidence that they indeed incorporate World Models, however another line of research is to look for World Models in simpler systems, susch as those encountered in games. Board games for example have world models that corresponding to the configuration of the board itself and knowledge of legal moves that can be made. It is much easier to look for evidence of world models within their simpler confines, as opposed to a full scale language model. We review the work by [Toshniwal et. al](https://arxiv.org/abs/2102.13249) in the context of the game of chess. Transformers can be trained on chess moves instead of word tokens, but otherwise the resulting systems are quite similar.

Tohniwal et.al point out that even though chess represents a controlled domain, predicting the next move is not a trivial proposition. Consider the board shown on the LHS of Fig. 1(b), where it is white's turn to move: 
In order to generate a valid move, the model needs to do the following: (1) Infer that it is white's turn, (2) Represent the locations all the pieces on the board, (3) Select one of the white pieces which can be legally moved, and (4) Make a legal move of the selected piece. Thus the Transformer model has to learn to track the board state, learn to generate moves according to the rules of chess and also learn chess strategies to predict the actual move.

In order to program the chess based LLM, Toshniwal labeled all the positions on the board using a 2D co-ordinate system and then converted chess moves into a linear sequence which the called the Universal Chess Notation (UCI). FOr example the move shown in Figure 1(b) is represented as **f1b5** in UCI, where **f1** is the starting position and **b5** is the ending position. They concerted chess games into a sequence of these kind of moves (for example **e2, e4, e7, e5, g1, f3**), such that each position corresponds to a single token. They also used a slightly modified version of this system for representing sequences in which only the chess piece to be moved is specified, as opposed to its location.

These tokens were then fed into the usual autoregressive language model, using the standard maximum likelihood objective. The training dataset consisted of 200K games, while the validation and test datasets consisted of 15K games each. Another 50K games were set aside for probing the LLM to detect the presence or absence of a world model. The actual Transformer model used was the GPT2-Small architecture from OpenAI.

The probing of the trained LLM was carried out in two ways:

**Ending Square Probing Tasks**: The model is given a game prefix and prompted with the starting square of the next move (**fe** in the sample in Fig. 1(b)). The model's next token prediction represents its prediction for the ending square of this move. This probe tests the model's ability to track the board state (thus deducing the type of piece that is being moved) and follow the rules of chess for that piece, as well as ability to follow strategy.

**Starting Square Probing Tasks**: In these probes, once again the model is given a game prefix, but prompted with just the piece type for the next move, such as **B** for bishop. The model's next token prediction tests its ability to predict where the prompted piece type is located on the board, and thus its ability to track pieces.

Toshniwal et.al. showed that the probes are indeed able to predict the the starting squares and the ending squared with a good accuracies (see Tables 5 and 6 in their paper). They also showed that in order to so, the entire game history had to be fed into the model, the performance decreased when only the most recent 50 tokens were fed into the model. 

We can conclude from this work that the LLM is able to create an internal model of the game state, so that it knows the precise locations of each piece on the board in addition to the allowed legal moves for each of these pieces. It acquires this knowledge entirely from the linear sequence of game moves were fed into it during the training process. It then uses this information to figure out the identity and position of the piece involved in the next move, as well as the ending position of a piece (given its starting position). This paper makes the case that the LLM is able to do these things by making use of its internal world model, as opposed to auto regressive statistical prediction of the next move from sequence data being fed into it.

## LLM based World Models for the Game of Othello

Inspired by Toshniwal et.al.'s work, [Kenneth Li et.al.](https://arxiv.org/abs/2210.13382) observed that the LLMs modeled using chess moves showed the presence of a world model, however the probes used by Toshniwal et.al. did not precisely locate how or where this world model was located within the LLM. Li et.al's work was undertaken with the objective of addressing this issue, and they did it in the context of the board game called Othello. Othello is actually a simpler game than chess, but still complex enough so that its moves cannot be predicted by memorization.

![](https://subirvarma.github.io/GeneralCognitics/images/agent10.png) 

Figure 8

The rules of Othello are quite simple and summarized in Fig. 8. There are 64 positions on the board, where the 4 positions in the middle are always occupied to start of the game, so that there 60 possible positions that are occupied during the course of the game. 
Li et.al. trained an 8-layer GPT model with an 8-head attention mechanism and a 512 dimensional hidden space, in an autoregressive fashion, which they called OthelloGPT. This is fed with a word embedding consisting of 60 vectors, one for each possible board position to get the sequence $(X_1,...,X_{T-1})$,
where T is the length of the sequence fed so far. The intermediate features for the $t^{th}$ token after the $l^{th}$ layer is given by $X_t^l$. Note that $X_t^8$ goes into a linear classifier to predict the logits for the next move.

Li et.al. showed that OthelloGPT was very good at predicting the next legal move, conditioned on the partial games before the move, and this could not be attributed to memorization. Assuming that the model had built in internal representation of the game board, they used a standard tool called a "probe" (see [Tenney et.al.](https://arxiv.org/abs/1905.05950)), to look for it. A probe is a classifier or regressor whose input consists of internal activations of a network, and out is the feature of interest. If the probe is indeed able to do prediction accurately, then this implies that a representation of the feature is encoded in the network's activations. For OthelloGPT, the input to the probe was the features $X_t^l$ for different layers $l$. The output $p_\theta(X_t^l)$ of the probe is a 3-way categorical probability distribution, where the classification is into the states Empty, Black or White. They trained a total of 60 different probes, one for each of the 60 positions on the board. They discovered that linear probes did not work very well, however probes with a single hidden layer were able to predict the board state with approximately 98.3% accuracy. The accuracy was highest for the seventh layer $X_t^7$ and decreased to about 95.4% for $X_t^8$. This implies that the model expends its energy in estimating an accurate picture of the board state in the initial 7 layers, and then uses this information in the final layers to do the next move prediction.

![](https://subirvarma.github.io/GeneralCognitics/images/agent12.png) 

Figure 9

So far we have seen that the board state is captured in the activations $X_t^l$ of OthelloGPT. But how can we show that the model is in fact using the information in the board states to actually make its next move. One way of doing this is by changing the value of $X_t^l$ so that it corresponds to a **different** board state, and then observing the effect of this change on the next move prediction. This procedure was actually carried out by Li et.al., and the results on one of the board configurations is shown in Fig. 9. The bottom left figure shows the board state before the intervention, while the bottom right shows the board state after the intervention, the E7 position has been flipped from black to white. The top left figure has the predicted probabilities before the intervention while the top right shows the probabilities after the intervention. As can be seen, the model modifies its predictions to take the post intervention board position into account, which shows a causal connection between OthelloGPT's board state and its move predictions. The intervention itself is carried out by running the classifier for the position being modified in the backwards direction, and using the error gradients to modify the input $X_t^l$ rather than the classifier parameters.

The examples of World Models that we have presented so far are from the world of games, with the LLM tarined on the linear sequence of board positions. The next few examples involve LLMs trained on language. These presumably learn a much more complex World Model, and it is interesting to find out their capabilities in this area.

## Map Building from Text Prompts

![](https://subirvarma.github.io/GeneralCognitics/images/agent14.png)

Figure 10

We humans build up a mental image of the environment we are in by means of our visual sense. Since the current generation of LLMs don't have the vision capability, it would be an interesting experiment to find out if an LLM can build a 'mental map' of its environment by text prompts alone. Such a map would correspond to a World Model, and can be used by the LLM to do planning. This experiment was carried out by [Bubeck et.al.](https://arxiv.org/abs/2303.12712) at Microsoft Research, who used text based games to interact with the LLM GPT4. One such experiment is summarized in Fig. 10, in which the LLM is given an objective to navigate through an environment get to a Goal. The environment consists of a set of interconnected rooms with doors between them, as shown in the map in the bottom left of the figure.
The experiment consists of two parts: In the first part the LLM is prompted with its objective and this followed by a dialogue in which the LLM issues commands to move left, right, up or down and the human responds with a short description of the effect of the carrying out the command (as shown in the upper RHS of Fig. 10). This continues until the LLM reaches it goal room.
In the second part of the experiment the experimenters test the ability of the LLM to form a model of all the rooms, by prompting it to describe their locations. GPT4's response is shown in the RHS of Fig. 10, and is also diagrammed on the bottom RHS of the figure. As we can see the LLM's map of the rooms corresponds to the true map, and the LLM is able to paint an accurate picture of the rooms that it has been in. The response also includes descriptions of the rooms based on what LLM 'imagines' them to be, based on their names.

This paper shows that LLMs build an internal map of the world based on the information that is being fed into them. They presumably use this internal map or World Model to formulate their output, as opposed to purely statistical next word prediction. This allows them to handle the 'covariate shift' problem i.e., be able to give effective responses to inputs that are not part of their training data. This example of World Model building differs from the prior two, since by using GPT4 we are starting with an LLM that has already been trained. Based on this training, the GPT4 has presumably formed a model for the world, which is why it is able to understand concepts such as 'left', 'right' or 'up', and 'down'. During the course of the chat session which takes place in the inference mode, GPT4 forms a more specialized World Model that is specific to the information it is being fed during the chat.


## Isomorphism between the LLM World Models and the Real World

The World Model that LLMs build is obviously of a different nature, than the one that exists in our brains. The latter is based on our sense of vision, sound, touch etc and is grounded in the real world. The World Model in LLMs on the other hand is built entirely on the basis of text sequences, and since LLMs are not embodied and have no sense organs, it is not grounded in the real world. If so, what is the relationship between the LLM's World Model, and the real world? This question was explored by [Patel and Pavlick](https://openreview.net/forum?id=gJcEM8sxHK), who showed that in certain cases the LLM's World Model is isomorphic to a grounded World Model built by interacting with the real world. This means that the structure of relations between concepts that is learnt by the LLM in text form, is identical to what a grounded model would learn. They carried out their investigation in the areas of Spatial Terms (for example left and right), Cardinal Directions (for example East and West) and RGB Colors. 

![](https://subirvarma.github.io/GeneralCognitics/images/agent15.png)

Figure 11

Figure 11 shows examples of how the concepts for Sptial Terms, Cardinal Directions and RGB Colors are grounded. In each case the LHS figure shows the grounded concepts, while the RHS has textual representations of the groundings that can serve as prompts for LLMs. In the first two cases the groundings are done using grid world representations, while in the last case it uses 3 dimensional RGB codes associated with the various colors.

![](https://subirvarma.github.io/GeneralCognitics/images/agent16.png)

Figure 12

Figure 12 shows an example of the grounding process for the Spatial Terms case. As shown in the box on the LHS, a prompt uses the Few-Shot technique and consists of sequence of twenty in-context examples of a grid in which the location of the '1' corresponds to the grounding, followed by the text instantiation of the concept. The last element in the prompt is the question to the model and the two boxes on the right are examples of responses. The top box is for a smaller model called GPT2 with 124M parameters, while the bottom box is for GPT3 with 175B parameters.  As we can the larger model correctly predicts the spatial orientation as 'left', while the smaller model is not able to do so. This shows that the model's ability to form a World Model from its training data is an Emergent Property, i.e., it forms only after the model size exceeds a threshold. This example also shows that the GPT3 model is able to generalize the concept of 'left' to "unseen worlds'. For example the grid in the final question prompt is different from all the other 20 grids used for in-context learning.

![](https://subirvarma.github.io/GeneralCognitics/images/agent17.png)

Figure 13

Patel and Pavlick also showed the following:

-    *Generalization to Rotated Worlds*: Patel and Pavlick also showed that the concepts of Spatial Orientation and Cardinal Directions also continue to hold in Rotated Worlds. In other words the GPT3 model understands that these are relative concepts, and if the grounding prompt shows a rotated 'left' for example, then the 'right' is also rotated by the same amount. This also shows that the models are not simply memorizing these concepts.
-    *Generalization to Unseen Concepts*: Instead of grounding the entire conceptual structure to a grounded world, what if we ground only a small subset of points in the domain. Will the model still be able to ground the entire conceptual domain? Patel and Pavlick tested this hypothesis for the Cardinal Directions case, and showed that even if the model was grounded with a subspace consisting of the directions *north* and *east* for example, it was still able to identify the directions *south* and *west*, even though they didn't occur in the in-context training examples. They repeated this experiment for the case of Color Grounding as shown in Fig. 13. The grounding was done by using 60 in-context examples of colors which are mostly shades of red, with only a single example of a shade of blue. Inspite of this, the GPT3 model was able to correctly  identify the shade of blue that it was tested with.

These examples suggest that the GPT3 model has built an internal World Model based on its training examples, so that even if it is grounded on a subset of the world, it is able to use its world model to map to the entire space. In other words it already the concepts of Spatial Orientations, Cardinal Directions and Colors and has mapped them to an internal representation that it has built. Once a subset of these concepts are mapped in the Grounded World, the other points in the space also get automatically mapped. In other words the model's internal World Model is Isomorpic to the Grounded World Model (i.e., they have one-to-one correspondence with each other).


## Planning Using LLMs

Forming a World Model is only one aspect of how an Intelligent Agent works. The other critical function is to be able to formulate an Action plan or a Policy, which ultimately result in successful completion of the task assigned to the Agent. Using LLMs to formulate a Policy is fast evolving area, with new discoveries and proposals coming almost on a daily basis. In this section we will attempt to survey the current work in this exciting area.

Planning proposals come in two flavors:

-	**Decision making with no interaction with the outside world**: In this case the planning happens entirely within the ‘mind’ of the LLM. This can be further divided into single step planning and multistep planning.

    (1)   **Single Step Planners**: Algorithms such as [Chain of Thought (CoT)](https://arxiv.org/abs/2201.11903) and [Self Consistency COT (SC-CoT)](https://arxiv.org/abs/2203.11171) fall into the category of **Single Step Planners**. These algorithms typically propose a sequence of Actions, without any mechanism to check whether these Actions are in fact useful in accomplishing the goal. Algorithms that are specialized for solving Math problems such as the GSM8K Solver and the MATH solver from OpenAI also fall in this class.
SC-COT proposes and evaluates multiples chains of Actions, and then uses a simple majority vote to decide which answer is correct. The [GSM8K solver](https://arxiv.org/abs/2110.14168) uses a separate LLM fine tuned on the detecting the correct solution, to propose a score, and then uses the solution with the highest score. The more powerful [MATH solver](https://arxiv.org/abs/2305.20050) on the other hand also uses a separate LLM, but now this LLM is used to propose a score for the correctness of each individual step in the solution.

    (2)  **Multistep Planners**: Algorithms such as [Tree of Thought (ToT)](https://arxiv.org/abs/2305.10601) and [Reasoning vis Planning (RAP)](https://arxiv.org/abs/2305.14992) are in the category of **Multistep Planners**. These algorithms propose multiple Actions at each step, and then use a mechanism for deciding which of these Actions is the best. This decision can be made by using the LLM (with a different prompt). If the algorithm ends up in a ‘dead’ spot, then it can also backtrack to a previous state.

-	**Systems in which Decision Making and Outside World Interaction are Interleaved**:  The outside world interaction in these systems can come in a number of forms: For example, Consulting a Website or the Wikipedia, robotic manipulation, using a calculator or Mathematica  etc. Some of the early work in this area, such as the [Zero Shot Planner](https://arxiv.org/abs/2201.07207), was of the Single Step type, in the sense that the LLM was used to propose a sequence of Actions which were then implemented by a Robot. However, all recent work uses Multistep planning in which feedback from the outside world is used to inform the next Action. Examples of this include the successor to the Zero Shot Planner called the [Inner Monologue system](https://arxiv.org/abs/2207.05608) as well the [ReAct algorithm](https://arxiv.org/abs/2210.03629).


The Decision Tree diagram shown in Figure 3 is a useful reference to keep in mind, since we will see that most planning techniques fit within this framework. 

## Chain of Thought (CoT) Prompting and Self Consistency with CoT

LLMs were originally prompted by asking them to respond or solve a problem by posing a question as a prompt, with the expectation being that the LLM will complete the prompt with the appropriate answer. This technique worked well for simpler problems, but researchers dicovered that if the solution to the problem involved multistep reasoning, then simple prompting did not work very well. [Wei et.al.](https://arxiv.org/abs/2201.11903) showed that the results could be considerably improved if the LLM was prompted using a prompting technique that they called 'Chain of Thought' or CoT prompting. 

![](https://subirvarma.github.io/GeneralCognitics/images/agent18.png)

Figure 14

Examples of CoT prompts are shown in Figure 14 with the CoT in colored highlight, using the format <input, chain of thought, output>, for arithemetic, commonsense and symbolic reasoning benchmarks. As can be seen, the CoT prompt is essentially decomposing the solution to the problem into multiple steps. For example, the CoT for the arithmetic problem in the top left can be decomposed into:

-  Initial state $S_0$: Roger has 5 tennis balls
-  Action 1: He buys 2 more cans of tennis balls, with 3 balls per can.
-  State $S_1$: Since 2 cans hold 6 balls, Roger now has 11 tennis balls.

This decomposition into multiple actions is more explicit in the SayCan robot example in the lower left. Going back to the decision tree shown in Fig. 3, the CoT prompt can be considered to be an example of a succesful traversal of the tree, starting from some initial state. By giving the LLM one or more examples of successful traversals, it is able to better replicate the multistep reasoning process involved. Wei et.al. also discovered that the CoT prompting method only works well for the larger models with at least 100B parameters, hence it an emergent property of LLMs.

![](https://subirvarma.github.io/GeneralCognitics/images/agent27.png)

Figure 15

The CoT prompting technique can be considered to be a 'greedy' method in the sense that it takes a single path through the decision tree to get to its goal, as shown in part (a) of Fig. 15. [Wang et.al](https://arxiv.org/pdf/2203.11171.pdf) came up with another prompting technique, which they called CoT with Self Consistency or SC-CoT. The main idea behind this is illustrated in the Decision Tree shown in Part (b) of Fig. 15. Wang et.al. pointed out there are often multiple reasoning paths through the Decision Tree that lead to the same final answer, and one way to make sure that the answer is correct, is by choosing one the one that is predicted the majority of times.

![](https://subirvarma.github.io/GeneralCognitics/images/agent24.png)

Figure 16

Figure 16 illustrates the SC-CoT technique. As shown, the prompt is similar to what one would use for CoT prompting. The CoT greedy decoding is shown on the top part of the figure, which results in a wrong answer in this case. The SC-CoT method on the other hand samples multiple times from the LLM, resulting in a different reasoning path each time. Since the $18 occurs as the final answer on a couple of those paths, it is chosen as the correct result by SC-CoT. Wang et.al. showed that SC-CoT results in a significant improvement in the correctness for complex reasoning tasks compares to CoT, and furthermore has the advantage that it is simple to implement.

Both the CoT and the SC-CoT techniques are dependent on humans generating good example prompts that can lead to correct reasoning steps by the LLM. [Xu et.al.](https://arxiv.org/abs/2305.09993) proposed a technique by which the LLM itself can be use to generate the CoT prompt, which they called Reprompting. This requires the use of two LLMs, such that LLM1 is used to generate the example CoT prompts, while LLM2 is used to solve the actual problem. The method works in two steps:

- In Step 1 a number of example CoT prompts are generated by LLM1 by using simple K-shot prompting (this can be done by prompting the LLM to think 'step-by-step').
- In Step 2, these prompts are in turn fed back into LLM1 as CoT prompts to further refine them. This results in the final set of CoT prompts that are then used in LLM2 to solve the actual problem (which may be un-related)


## Tree of Thought Prompting

Tree of Thought or ToT prompting methods are a further generalization of CoT and SC-CoT such that they are closer approximation to human decision making. As was mentioned earlier, human decision making is a mixture of mental planning followed by actual actions, and during the planning process various alternatives are evaluated on how to solve the problem. A technique that closely resembles this process is an algorithm from Reinforcement Learning called Monte Carlo Tree Search or MCTS. We start by delving deeper into MCTS, and then examine how it can be applied to LLM based decision making.

![](https://subirvarma.github.io/GeneralCognitics/images/agent29.png)

Figure 17

MCTS is a way in which the decision tree of possibilities for solving a problem can be built out, along with some information about which path through the tree is the best. MCTS proceeds in four steps, as shown in Fig. 17, which are as follows:

- **Selection**: Assume that the MCTS tree has already been built up to the extent shown on the LHS figure. As before the white circles correspond to States while the black circles represent Actions (at the start of the tree building, only the Root State at the top exists). The tree consists of two kinds of states: (1) States in which all Actions have been explored, for example the Root State and the child state to the left after the Root State, (2) States in which some or all of the Actions still need to be explored. The Agent plots a course through this partially built tree, until it comes to a state in which not all Actions have been evaluated, as shown the blue arrows. At each of these States, an Action is chosen based on the following criteria:

$$A^* = arg\max_{A\in A(S)} [Q(S,A) + w\sqrt{{\ln N(S)}\over{N(c(S,A))}}]$$
  
-  **Expansion**: The Selection step ends when the Agent comes to a State with partially explored Actions. At this point, the Agent expands the tree by adding (one or more) States to the tree, as shown in the figure. The new State in turn will have one or more unexplored Actions of its own. The Agent chooses ones of these States and then goes to the Simulation step.
-  **Simulation**: This step of the MCTS algorithm consists of building out the rest of the tree starting from the State that was chosen in the Expansion step. The build consists of taking successive Actions, until the system enters a Terminal State. The Actions are chosen using a **Rollout** Policy, which is usually a simple rule such as chose an Action at random (since none of these Actions have been evaluated yet).
-  **Back-Propagation**: The Backpropagation step consists of updating the $Q(S,A)$ values of all the State-Action pairs that were encountered in the path from the Root State all the way down to the Terminal State. These updates proceed backwards, starting from the Terminal State, using the following update equation:
-  $$Q(S,A) \leftarrow Q(S,A) + \alpha(R + \gamma Q(S',A') - Q(S,A))$$

Typically the MCTS tree building continues until a pre-determined number of iterations is reached. Once this threshold is reached, the final trace through the tree is constructed. This can be done using one of several methods, such as:

-  Choose the Action with the highest Q value
-  Choose the path that yields the highest reward, or
-  Choose the leaf node that has been visited the most

MCTS can be considered to be a more sophistictaed version of SC-CoT. It is similar to SC-CoT since it involves multiple traversals of the decision tree starting from the Root State. However unlike SC-CoT, the decision making is more sophisticated with the tree being allowed to branch from any state in MCTS. Moreover the optimum path through the decision tree in MCTS is governed by rewards (rather than a simple majority vote on the outcomes). 

![](https://subirvarma.github.io/GeneralCognitics/images/agent25.png)

Figure 18

[Hao et.al.](https://arxiv.org/abs/2305.14992) adapted MCTS to work with LLMs and came up with an algorithm they called Reasoning via Planning (RAP). A high level view of RAP is shown in Fig. 18. As shown, it adopts the usual Reinforcement Learning framework for decision making, with the caveat that LLMs are used to propose appropriate Actions, as well as for keeping track of the current State. This framework adopts two LLMs for its functioning, with LLM1 used to propose Actions while LLM2 is used to keep track of the current State. This is a point of differentiation from CoT or SC-CoT, since in those systems a single LLM keeps track of both the Action and State.

The graph shown on the RHS of the figure is referred to as a Markov Decision Process or MDP in Reinforcement Learning nomenclature. It consistes of the tuple $(S_t, A_t, R_t, p), t = 0, 1, ..., T$, such that the Action $A_t$ at time step $t$ is distributed according to $A_t ~ p(A|A_t,c)$ where $c$ is a prompt used to steer the LLM for Action generation, the state $S_{t+1}$ is distributed according to $S_{t+1} ~ p(s|S_t, A_t, c')$ where $c'$ is another prompt used to guide the LLM to generate the next state. The Markov in the name refers to the fact that both the Action $A_t$ and State $S_{t+1}$ are entirely determined by the prior State $S_t$, and are independent of what happened before.

![](https://subirvarma.github.io/GeneralCognitics/images/agent28.png)

Figure 19

Fig. 19 has two examples of how Reinforcement Learning State and Actions can be chosen to solve problams using LLMs. The example on the left consists of a set of colored blocks arranged in a starting configuration, with the Goal of the problem being to re-arrange the blocks in a particular fashion. In this case th system State corresponds to the current block configuration, while an Action is Picking up and Placing blocks. The example on the right shows how RAP can be used to solve Math problems. In this case the State corresponds to the current state of the calculation, while Actions correspond to Questions posed by the LLM to move the solution along. Note that in both these examples the Decision Tree is generated without interacting with the real world, i.e. it corresponds to a human contemplating how to do a task. There are two ways in which the Decison Tree can be translated to actual actions:

- Generate the entire Decision Tree and then carry out the Actions prescribed. This is appropriate for tasks that of the cerebral kind such as solving a Math problem.
- Use the Decision Tree to decide on the next Action, and then go ahead and take this Action in the real world. Use the new State of the World to create a new Decision Tree, which then is used to decide on the next Action etc. This corresponds to the AlphaGo algorithm, and is appropriate for applications such as robotics in which the feedback from the real world is needed before deciding on the next action.

For the Block World example, the State, Actions and Rewards were generated as follows:

-   How to generate and update the World Models used to generate the state of the MDP.
-   How to generate the Actions for the Agent, and also how to assign probabilities for the Actions
-   How to assign Rewards for States and Actions
-   

The assignment of rewards for the MDP in the RAP algorithm is an important design decision. [Hao et.al] made the following proposals for reward assignment:

- 

![](https://subirvarma.github.io/GeneralCognitics/images/agent26.png)











![](https://subirvarma.github.io/GeneralCognitics/images/agent22.png)

![](https://subirvarma.github.io/GeneralCognitics/images/agent23.png)

[Yao et.al.](https://arxiv.org/abs/2305.10601)

![](https://subirvarma.github.io/GeneralCognitics/images/agent21.png)

[Long](https://arxiv.org/abs/2305.08291)




## Inner Monologue in Embodied Agents

![](https://subirvarma.github.io/GeneralCognitics/images/agent19.png)

[Huang, Xia et.al](https://arxiv.org/abs/2207.05608)

![](https://subirvarma.github.io/GeneralCognitics/images/agent20.png)

[Huang, Abbeel et.al.](https://arxiv.org/abs/2201.07207)





## Human Feedback to Improve Multi-Step Reasoning

[Lightman et.al.](https://arxiv.org/abs/2305.20050)

A point of weakness with the SC-CoT method is that there is no gaurantee that the final result that occurs in the majority of cases is in fact the correct response. For the special case of Math problems, it is possible to train a model to predict whether the anser is correct, by fine tuning it on the Math dataset. Hence instead of relying on a simple majority rule, the model can be used to figure out which of the responses have the highest probability of being correct.

## Generative Agents with Memory and Planning Abilities

![](https://subirvarma.github.io/GeneralCognitics/images/agent7.png) 

![](https://subirvarma.github.io/GeneralCognitics/images/agent8.png) 


### BabyAGI



## AutoGPT


## The Langchain Framework


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

In general System 2 operation in Agents seems to connected to the idea of running Neural Networks multiple times during a computation, so that later stages are able to make use of results of the prior stages. In the context of an LLM, from this we can surmise that more powerful Agents can be created by increasing the context length of the data that is fed into it. This enables the LLM to make use of more results from the intermediate steps of
