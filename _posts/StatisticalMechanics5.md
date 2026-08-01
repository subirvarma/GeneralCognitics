---
layout: default
title: " A Hierarchical Energy-Based Model for Multimodal Cognition"
---

# A Hierarchical Energy-Based Model for Multimodal Cognition

**Contents**     

## Introduction 

This paper proposes an hierarchical computational model for semantic cognition in the brain. The model, that we call Integrated Multimodel Latent Energy based Predictive Processing or IM-LEPP
builds on the previous paper that proposed the LEPP model for perception as a process of flow on an energy landscapes. The IM-LEPP model extends this idea and builds a model for cognition that integrates both perception and language processing. The IM-LEPP architecture allows for additional sensory modalities to be integrated into the model in a straightforward manner. 

The IM-LEPP design is based the following core idea that was introduced in the paper [Generative AI as an Effective Theory of Cognition](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html):
Modern generative neural networks should be understood not as mechanistic models of neural implementation, but as effective theories of cognitive dynamics operating at the level of learned energy landscapes. In this view, cognition is understood as the temporal evolution of perceptual and cognitive states through a learned energy landscape, rather than as the direct consequence of an explicitly modeled neural circuitry. Just as statistical mechanics explains why thermodynamics provides an effective description of macroscopic matter without explicitly modeling every molecular interaction, modern generative AI may provide effective descriptions of cognitive dynamics without modeling the underlying neural circuitry. Leveraging this insight, IM-LEPP models the brain at the level of energy landscapes rather than at the circuit level.

The IM-LEPP architecture is also based on the Inference-Prediction-Generation framework for cognitive processing that was used in previous paper, which is referred to as predictive processing. 
Both vision and language have their own inference, prediction and generation pipelines that operate using the predictive processing model. The inference pipeline results in latent states that reflect the latest vision or language data. The prediction module then predicts the next latent state candidate and this prediction is sent into a central hub, where it gets integrated with latent states of other sensory modules and results in an integrated state. The integrated state is then sent back to the original sensory modality, where it is used to generate the next percept (in the case of vision) or word (in the case of language). It also gets modified into new latent sensory state as new sensory data comes in, and the cycle repeats. 

This framework allows the vision and language processes to evolve indendently of each other, and operate at different time scales. This aspect is important since vision sensory data is received almost continuously, while language data in the form of words is seprated by a few hundred milliseconds.
The central integrated state gets invoked asynchronously as new data comes in from either module. This design allows for the various modalities in the brain to influence one another as their states evolve. The IM-LEPP model also allows for continual learning, since all information required to update the parameters of the various modules is available locally at each step of the inference, generation and prediction pipeline. All the modules proposed as part of IM-LEPP framework operate using the principle of energy minimization, and all communications between states is local in nature. Thus it serves as a plausible model for the brain, at the algorithmic level (i.e., Marr's level 2). As pointed out in the previous paper, it is likely that the brain also operates using the principle of energy minimization, but at the level of its connectome, which is invisible to us.

This paper proposes a solution for the binding problem in the brain, i.e., the problem of integrating various modalities together into a common representation. It proposes that binding is accomplished through the use of predictive coding pipelines for individual modalities. This is in agreement with what is known about how binding between different sensory modalities happens in the anterior temporal lobe (ATL) of the brain, as described in the paper by [Ralph et.al.](https://wiredbrains.org/wp-content/uploads/2023/07/Ralph-2016-Nature-Reviews-Neuroscience.pdf).

We introduce an hierarchical hub and spoke model for vision, in which the base level is made up of predictive processing pipelines for objects that are in the field of vision. The individual latent states from the object modules gets integrated at the vision hub into a combined state that reflects the scene. Thus each object has its own individual model in this framework, and evolves in time asynchronously to the other objects. However the predictions from each object module reflect the presence of other objects and the mechanism for this is described in this paper.

We also introduce a predictive processing model for language, in which the sensory data consists of discrete words coming in through the auditory or visual systems. This module predicts the latent representation for the next word. However this latent does not not directly generate the next word, but is instead sent to the central module that integrates it with the vision state (and perhaps other modalities), and then the integrated state is fed back into the language module to generate the next word. Thus language generation in IM-LEPP is based not just on word level co-occurance statistics, but is a function of everything else that is happening in other sensory modalities. 

There are several points of distinction when comparing the IM-LEPP model with modern LLMs, which also seem to be carrying out similar cognitive functions:

- There is a fundamental difference in learning between IM-LEPP model and LLMs. LLMs learn by consuming a huge amount of data in the training stage and then use the resulting frozen model for all their inference operations, which is very different from the way brains work. Brains gets trained on a continuous basis as new sensory data comes in, so that continual learning co-exists with inference and prediction, and this is also the way that the IM-LEPP model operates.
- The IM-LEPP model introduces an integrated system state that includes language and vision and can be extended with more modalities. Thus the language generated by the model is grounded by by both visual and linguistic data. It is thought that LLMs also maintain an internal latent state that is not visble externally, however this state is entirely a function of language statistics and is not grounded in real world sensory data and this results in the well known [symbol grounding problem](https://arxiv.org/html/cs/9906002), i.e., LLMs see only the linguistic symbols, never what those symbols are about. The integration of vision and language into a shared common state in IM-LEPP constitutes a solution to this problem.
- IM-LEPP gives us direct access to the latent states through which all generation is done which can be used to influence the models output. Something equivalent can be done with LLMs by probing the transformer's middle layers. In IM-LEPP the latent state is made explicit by the model while it remains hidden in LLMs.

This paper makes the following contributions:

- We propose a hub and spoke integration architecture for multiple sensory modalities, with modality specific predictive processing pipelines converging on a shared latent state. 
- We propose a solution to the binding problem that solves the problem of asynchronous updating across different sensory modalities operating on different timescales. This integration is mediated through predictive coding pipelines.
- A propose an hierarchical hub and spoke model for vision, in which a central hub integrates latent states from individual objects in the field of vision. Each object has its own predictive processing pipeline and its latent state evolves as a function of its own object based model.
- We propose a model for predictive processing for language in which the sensory data consists of discrete phonemes. These are then integrated into a word level predictive processing pipeline which the next word. This prediction is based on an integrated latent state that takes the other sensory modalities into account.

## The Hub and Spoke Model for Cognition

![](https://subirvarma.github.io/GeneralCognitics/images/stat138.png) 

Figure 1: The hub and spoke model for cognition. 

The hub and spoke model for cognition was proposed by Ralph et.al. in 2017, and it was based on key findings from a decade of research into neurocognitive and neurocomputational underpinnings of the brain's semantic cognition abilities. Based on this, they proposed the hub and spoke model of semantic representation that is shown in the above figure, which was based on the accounting of patterns of impairment that are observed in some semantic disorders. This model assimilated two important existing ideas: (a) The model assumes that multimodal verbal and non-verbal experiences provide the core ingredients for constructing concepts and these information sources are encoded in modality specific cortices distributed across the brain, (b) The model proposes that that cross modal interactions for all modality specific sources of information are mediated by a single transmodal hub that is situated bilaterally in the anterior temporal lobe (ATL) area of the brain.
The hub and spoke model was was suggested by the observation that individuals with semantic dementia (SD), that is characterized by atrophy centered in the ATL, show semantic impairments across all modalities.

This model solves the problem of how the information relevant to a given concept is experienced across all different verbal and sensory modalities. For example if see an image of a dog, then we are able to reproduce the sounds, names, valence (positive or negative affective value that originates in the amygdala), and other types of information that are associated with the animal. This implies that the ATL hub forms generalizable semantic representations for a dog that are shared across all modalities.

![](https://subirvarma.github.io/GeneralCognitics/images/stat148.png) 

Figure 2: This figure illustrates graded pattern of semantic representation at the central ATL hub

There is a sub-region within the ATL called the ventral-ventrolateral ATL that serves as the cross modal center point of the hub for multimodal naming and comprehension.
Based on experimental data, the model proposed that the semantic representation function varies in a graded manner across the the ATL subregions. The 8x8 unit grid of colored circles in the above figure represents the ATL hub with reciprocal connectivity to the modality specific spokes. The contribution of the hub units to the semantic representation is graded reflecting a varying pattern of connectivity to the spoke layers. At the center point, there is equal weighted connectivity to all inputs, thus resulting in an evenly transmodal representation, as shown by the white color.


## The IM-LEPP Model for Vision and Language Integration

![](https://subirvarma.github.io/GeneralCognitics/images/stat153.png) 

Figure 3: The IM-LEPP model

We propose a model for integration of visual and language modalities based on the hub and spoke model, which we call integrated multimodal latent energy-based predictive processing or IM-LEPP (see above figure). This model extends the LEPP model that was described in the [previous paper](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html) in several ways: It proposes a hierarchical structure for the vision model, it introduces a predictive processing model for language, and finally it proposes how the two may be integrated together to create a common representation. The IM-LEPP model has the following features:

- There is a central ATL type hub at level 1 that integrates representations coming in from the vision and language hubs. Note that the communication between the level 1 central hub and the vision and language hubs is bi-directional, so that not only the spoke hubs influence the representation in the central hub, but they in turn are influenced by the information coming from the central hub.
- The vision hub itself has a two level structure. The central vision hub at level 2 integrates information coming from level 3 predictive processing pipelines, with the understanding that the latent state in the level 2 hub represents a scene, while the latent states in the individual level 3 predictive processing pipelines represent objects in the scene. The representation of each of these objects evolves asynchronously in time and the level 2 hub integrates the latest information from each individual object and sends it up to the central level 1 hub.
- The per-object level 3 predictive processing pipelines operate according to the inference-prediction-generation framework that was used for the LEPP model. This results in temporal predictions for each object's latent representation that are sent to the level 2 vision hub for integration with all the other objects in the scene. This combined scene level representation in turn gets integrated with representations from other modalities in the multimodal level 1 hub. The integrated level 1 representation in turn is fed back to the level 3 object predictive processing pipelines, which then uses it to generate percepts. Note that these percepts take all the other objects that are in the scene into account (as well as other modalities), by virtue of the fact that they are based on integrated representations coming from the level 1 multimodal hub.
- The language module operates at the word level, and incorporates an inference-prediction-generation predictive processing pipeline whose job is to predict the next word. The latent representation used to do this generation comes from the central level 1 hub and takes the current visual scene into account. Hence unlike in an LLM, next word prediction is not based solely on word occurence statistics, but on data from other modalities that are impinging on the brain.

The model leads to a picture in which there are number of distributed predictive processing pipeline modules in the brain, that are individually responsible for predictions in the modality they are tracking. Hence the prediction operations happens in a distributed manner, while central hubs at level 2 and level 1 are responsible for the integration work. We will show that as in the LEPP model, all state level dynamics in the IM-LEPP model are based on flows in energy landscapes

## A Hub and Spoke Model for Vision

![](https://subirvarma.github.io/GeneralCognitics/images/stat150.png) 

Figure 4: Hub and Spoke Model for Vision: Integration of Predictive Processing Pipelines for Multiple Objects into a Scene

This section has a more detailed description of the vision model's operations at levels 2 and 3. Modern AI systems process images at the level of pixels, and learn prediction models for how value of these pixels evolves with time, and this is how vision was also modeled in the LEPP paper. The brain on the other hand is thought to decompose a scene at the object level, and then model the temporal evolution of the individual objects. For example in a road scene, there would be models for pedestrians and vehicles as well as a model for the background containing the sky, foliage etc. Each object is tracked individually, and the brain integrates all the representations to create the scene that we see in front of us. The above figure shows a model for vision that takes this hierarchical structure into account. 

Predictive processing models for objects that we encounter in our daily lives don't require much training. However when we encounter an object for the first time then the model undergoes a period of training, after which it gets stored away in the memory. At any one time a subset of the stored models are active depending on the scene that is being composed.

![](https://subirvarma.github.io/GeneralCognitics/images/stat145.png) 

Figure 5: Predictive Processing Pipeline for an Individual Object at Level 3

The level 3 predictive processing pipeline for an individual object is shown in the above figure, and follows the LEPP design, with inference, prediction and generation modules. As new sensory data $s_n$ for an object comes in, it is integrated into the latent state $z_n$ for the object by using predictive coding as described in [Varma](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html). Inference operates by using the principle of minimization of predictive coding energy $E_{PC}$. 
The latent state $z_n$ is fed into the temporal prediction module and this results in a prediction $x_{n+1}$. The prediction process is modeled by using a multi-stage diffusion model that minimizes an energy $E_W(x;z_n,u_{n+1})$ by gradually annealing the state $x$ of the system until it reaches a state $x_{n+1}$ of low energy. 
The prediction $x_{n+1}$ is sent to the level 2 vision hub and this results in the scene level latent representation $xx_{n+1}$, and this in turn is sent to the multimodal level 1 hub, resulting in the latent representation $xxx_{n+1}$. This state information is then fed back into initial object predictive processing pipeline by setting its latent state to $x_{n+1} = xxx_{n+1}$. Note that as a result of this integration with higher level hubs, the prediction $x_{n+1}$ incorporates information about other objects in the scene as well other modalities that may be relevant such as valence. 
The modifeid latent representation $x_{n+1}$ is used to generate the next percept $g_{\phi}(x_{n+1})$, and is also used to kick off the inference phase of the predictive processing pipeline by comparing it with the new sensory data $s_{n+1}$. This subsequently results in a new object latent state $z_{n+1}$ and the cycle repeats.

![](https://subirvarma.github.io/GeneralCognitics/images/stat161.png) 

Figure 6: Integration of Multiple Object Level Predictive Processing Pipelines into the Vision Hub at Level 2

The structure of the level 2 vision hub is shown in the above figure. It shows that the latent state predictions $x_n$ from the object level pipeline is fed into an object level predictive coding pipeline in the vision hub, where $x_n$ serves as the ground truth value. 
Note that the structure of the predictive coding pipeline agrees with what has been observed about the variation in the mode representation shown in figure 2. Specifically the predictive coding states that are closer to the vision (or language signal) would still retain the signatures of that mode, and as we move up the pipeline, the representation turns gradually amodal.

As a result of predictive coding, the state of the hub gets modified to $xx_n$, and this value reflects not just the latest information from the current object level pipeline, but also information from all the other other object pipelines that are active at the same time. As soon as an object moves out of the field of vision, its level 3 predictive processing pipeline is dis-connected from the level 2 vision hub, and as other objects appear their pipelines are in turn connected to the hub. If the objects are well known due to frequent appearance, then their predictive processing models are pre-trained and stored in the brain, while new objects undergo a period of training.

Note that this design takes into account the predictions that arise when two objects are interacting with each other, for example a ball bouncing off a wall. In this case there is a level 3 model for the ball, as well as for the wall, and two latent states integrated at the level 2 hub, and subsequently this information is used to update the latent state $x_{n+1}$ for the ball. Thus if the ball is very close to the wall, then the next prediction will lead to a change in its trajectory since the ball model knows about the presence of the wall. If both the objects are moving towards each other, for example two balls about to collide, and assume that our attention is focused on one of the balls so that its state is being updated constantly. In this situation if the level 3 predictions for the other ball operate in an open-loop fashion based on its last position and velocity, the the system should be able to predict the collision at the right instant even though attention is focused on ball 1.

![](https://subirvarma.github.io/GeneralCognitics/images/stat162.png) 

Figure 7: Integration of Vision and Language Hubs into the Cognition Level Hub at Level 1

The above figure shows the structure of the level 1 hub located in the ATL. It is the same as for the level 2 vision hub, however now the signals are coming in from vision as well as language modalities. There is a predictive coding pipeline for vision and another one for language, and this results in a representation $xxx_{n+1}$ that is amodal. 
After the predictive coding pipeline settles down, the resulting value of the hub state $xxx_n$ is fed back into the level 3 part of the vision and language pipelines, and serves as the latent $x_n$ value that is used to generate the next percept $g_{\phi}(x_n)$. The latent $x_n$ subsequently gets modified by the new sensory data $s_n$, which results in the latent state $z_n$.
Thus the percept generation takes place at the mode level, but takes into account everything else that is happening by virtue of this architecture.

Consider the scenario in which we are driving a vehicle and there is another vehicle in front of us, as well as other objects such as pedestrians etc which are visible. As per the model, the system will install models for all objects that we pay attention to during the course of the drive, but there are some objects that we pay more attention to, such as the car in front of us.
The scenario can evolve into one of the following ways:

- We are paying frequent attention to the car in front of us, so its representation $z_n$ gets updated frequently with new vision data. There is another car behind us that we can see through our rear view mirror, but we play less frequent attention to it. In between the times that we look into the rear view mirror, the representation for that car evolves as expected, so that if that car appears by the side of our vehicle it is something that the system has predicted (i.e., the latest level 1 $xxx_n$ representation and the sensory data $s_n$ at level 3 for the car would agree with each other), so we are not surprised. The actual mechanism that the system uses for for tracking the behavior of the the other car is open loop prediction using a diffusion model from the last known position of the car. This mechanism was described in detail in [Varma](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html).
- Consider the same scenario as before, but assume that the car behind us made a turn while we were not paying attention to it. In this case our visual model does not know that the car has disappeared, and the next time we look back we expect to see it, but the sensory data says otherwise. Hence the other car is not behaving in the way that our internal model is expecting it to behave, which causes some surprise. Once we see that the car is not there, its level 3 pipeline is removed from the set of objects that are being tracked at level 2. Another example of this would be if the car in front of us suddenly braked while we were looking at our phone. Again in this case our internal model for the car is updating in a way that does not agree with reality, until we look up and see the change. Unlike the case for the disappearing car, in this case the model for the other vehicle is not de-installed, but is updated with large error correction  when new sensory data comes in, i.e., when we look up from our phone.
- There are cases in which the brain actively suppresses the updating of one or more objects whose pipelines are currently active. For example while driving we don't want to get distracted by the image of large billboard by the side of the road. In this case a level 3 pipeline will be installed for the billboard will be installed when we see it for the first time, however we decide not to pay attention to it. This can be done by reducing the value of the precision parameter $\Pi_y$ that is used in the predictive coding pipeline for the billboard at the level 2 vision hub. This mechanism was first described by [Feldman and Friston (2010)](https://www.frontiersin.org/journals/human-neuroscience/articles/10.3389/fnhum.2010.00215/full) in their paper {\it Attention, uncertainty and free energy"}.
- As the last example, consider the case when a level 3 pipeline for an object that is in the vicinity of our car never gets installed, so that we are complete unaware of its existence. This corresponds to the case when there a car in our blind spot, and we try to make a turn into its lane. In this case there is a much bigger surprise waiting for us when the other car honks, and at that point the system installs a model for it and starts tracking it. Another well known example of this phenomenon is the case of bear costumed person crossing the court in the middle of a basketball game and it fails to get noticed, as was originally pointed out by [Simon and Chabris](https://pubmed.ncbi.nlm.nih.gov/10694957/). Again since attention is focussed on the ball on and the players, the level 3 model for the bear never gets installed.

The last scenario points to the need for a cheap, always-on detector separate from the pipelines it might spawn since something has to decide when to instantiate a new level-3 pipeline,
and that decision process itself must be resource-limited. [Itti, Koch and Niebur’s (1998)](https://hasler.ece.gatech.edu/Courses/MachineLearning/FoundationalPapers/Itti_Koch_Neiber1998.pdf)
saliency-map model is the classic computational proposal: a cheap, bottom-up, parallel process computing simple feature contrasts (color, intensity, orientation, motion) across the entire visual field continuously, producing a topographical saliency map that competes to determine where attention deploys next. 
A new level-3 pipeline gets instantiated only when a region’s saliency signal is large enough and wins the competition for currently-available attention. In the bear case, task-absorbed attention
means the saliency signal from the costumed figure never wins that competition, so no pipeline ever gets created — consistent with inattentional-blindness follow-up
work showing measurable physiological orienting responses to “unnoticed” stimuli despite no conscious report. This gives a concrete mechanism for the “ background things vs. stuff” distinction — everything starts as coarse “stuff” background by default; a region gets promoted to its own individuated “thing” pipeline specifically when its saliency signal wins the attention competition.

## A Predictive Processing Model for Language 

Language shares a number of features in common with the visual system, and both can be modeled as predictive systems, images in one case and words in the other. That said, words are more abstract entity than objects and are discrete in nature, i.e., there are a finite number of them. The problem then is that of translating the sound coming in through our ears into word level latent representations that attach semantic meaning to them and is followed by prediction of the next word. These sounds could be coming from an external source, or it could be just the sound of our voice talking. In the former case, the next word in the sequence can serve as an error connection signal for the brain's prediction for the next word, very much like the error correction that happens in vision, and in the process the brain's model for next word prediction gets trained. For the case when the sound is from our own voice, there is still an error correction  feedback loop in operation, since sometimes we speak out a word, and then hearing the sound makes us realize that we meant to say something else. There is another source for words through our visual system when we read or write and we will consider this simpler case first. 

![](https://subirvarma.github.io/GeneralCognitics/images/stat165.png) 

Figure 8: Classification of a character image into one of K categories

We will consider the simple case of child reading, in which case he or she reads one character at a time. Adults on the other hand use a faster system in which multiple characters are read at time in order to speed up the process, which comes after practice. We will assume that the image of an individual character coming in from the visual system is sent to a classifier, that outputs a discrete number indicating the category. There can be 26-70 different categories depending upon the punctuation. This process results in a discrete sequence $(ch_1,...,ch_N)$ that is fed into a predictive processing pipeline.

![](https://subirvarma.github.io/GeneralCognitics/images/stat166.png) 

Figure 9: Predictive Processing Pipeline for Next Character Prediction

The discrete character sequence is sent into a predictive processing pipeline that creates an internal representation $z_n$ for each character using the predictve coding function $q_{phi}$, followed by prediction of the next character using a energy based diffusion model $E_{CH}$, and then generation of this character using the predictive coding function $g_{psi}$.  The generated character $y_{n+1}=g_{psi}(x_{n+1})$ is compared with the actual next character $ch_{n+1}$, and this information is used to estimate the next representation $z_{n+1}$
These operations are illustrated in the above figure.
The system is able to detect the end of a word by tracking the difference between the predicted  latent state $x_{n+1}$ and the actual latent state $z_{n+1}$. 
If this difference exceeds some threshold, then the model assumes that the previous character $ch_n$ occurred at the end of the word, and its representation $z_n$ is sent over to the word level pipeline as discussed next. We also use the empty space at the end of each word to infer the word ending, however there some languages such as Chinese and Old Latin that don't use spaces, and alternative mechanism described here is more general, and also works for the case of auditory signals.

![](https://subirvarma.github.io/GeneralCognitics/images/stat167.png) 

Figure 10: Predictive Processing Pipeline for Predicting the Latent Representation for the Next Word

The predictive coding pipeline at the word level uses the latent state $z_n$ from the character pipeline as the ground truth that represents the latent representation for a word. 
This pipeline creates a higher level latent representation $zz_n$ by modifying the existing representation to to $q_{phi}(zz_n,z_n)$.
The energy based prediction module $E_W$  is invoked next and this results in the prediction $xx_{n+1}$.

Subsequently $xx_{n+1}$ is fed into the central ATL hub, where it gets modified to $xxx_{n+1}$ as a result of integration with other sensory modes. $xxx_{n+1}$ is then fed back to the word level pipeline by setting $xx_{n+1} = xxx_{n+1}$. Thus the prediction $xx_{n+1}$ reflects the latest word data (by way of $zz_n$) as well as
the influence of other modes that are active. $xx_{n+1}$ is subsequently used to generate the next word latent $yy_{n+1}=g_{psi}(xx_{n+1})$, and this value is fed back into the character level predictive processing pipeline shown in figure 9, by setting $x_{n+1}=yy_{n+1}$. This in turn gets modified by the characters in the next word being read, this resulting in a new word level latent representation $z_{n+}$ that is in turn fed back into the word level model to correct the prediction $yy_{n+1}$, and this closes the word level prediction loop.

For these case when we are doing the character generation, i.e., writing, this feedback loop between the character level and word level pipelines is still active. In this case it serves as a verfication of whether the word that we wrote down matches the word that our cognitive system meant to generate (at the word level).

![](https://subirvarma.github.io/GeneralCognitics/images/stat168.png) 

Figure 11: Integration of vision and language modules at the central ATL hub

The above figure shows the integration of vision and language modules at the central ATL hub. The integrated state $zzz_n$ is fed back into the predictive processing pipelines of the respective hubs. 
This allows additional modalities to influence the next generated word, for example the information coming in through the visual system may influence what we say next. Similarly the emotional related information coming in through the valence system (valence) can influence our choice of the next word.

![](https://subirvarma.github.io/GeneralCognitics/images/stat143.png) 

Figure 12: Predictive Coding Pipeline for Characters

The above figure shows the computational details for the predictive coding model at the character level. The system processes characters one at a time, and for each character it builds up an internal representation using predictive coding.
We will assume a simple two level hierarchy, though the model allows for any number of levels. The top level has a latent representation $z^{(2)}$, and this used to generate a representation $z^{(1)}$ at the lower level using a function $f_2(z^{(2)})$ and this representation in turn generates the final representation $t=(t_1,...,t_K)$ where $K$ is the number of characters being modeled.
The representations $z^{(1)}$ and $z^{(2)}$ are in continuous space, however $t$ lies in discrete space and is given by $t=(t_1,t_2,...,t_K)$ and uses the 1-hot representation so that individual characters $(ch_1, ch_2,...,ch_K$ are represented by $(1,0,...,0), (0,1,...,0),...,(0,0,...,1)$ respectively. The representation $t$ is generated from  $z^{(1)}$ by a process of sampling using the distribution

$$ p(t = (t_1,...,t_K)) = (y_1)^{t_1})(y_2)^{(t_2})...(y_K)^{(t_K)}  $$

where $y_k$ is given by the Boltzmann distribution (also called the softmax function in machine learning) 

$$ y_k = { e^{ z_k^{(1)}}\over{\sum_i e^{ z_i^{(1)}} } } $$

In this equation $z_i^{(1)}$ is the $i^{th}$ component of the vector $z^{(1)}$. Lets assume that $z^{(1)}$ leads to the probabilities $y=(y_1,y_2,...,y_K)$ while the ground truth is given by
$T = (T_1,T_2,...,T_K)$ This generates an error $\epsilon^{(1)} = y - T$, which is propagated to the level above.
Using the Bayesian argument used in predictive coding, it can be shown that optimal $z_i^{(1)}$ is obtained by minimizing the energy function

$$  E_{CH}(1) = -\sum T_i\log y_i + {1\over 2}\epsilon_{z^{(1)}}^T \Pi_1 \epsilon_{z^{(1)}}  $$

where $\epsilon_{z^{(1)}} = z^{(1)} - f_2(z^{(2)})$. Using gradient descent $z_i^{(1)}$ is updated according to 

$$ z_i^{(1)} \leftarrow z_i^{(1)} - \eta \left[(y_i - T_i) + \Pi_1\epsilon_{ z^{(1)}}\right] $$

Note that all the information required to update $z_i^{(1)}$ is available locally.

### Extension to Auditory Processing of Language (Phonemes)

The predictive coding model for level 1 developed above assumes a single flat categorical readout, appropriate when the input alphabet has no independently-motivated internal structure — as is the case for written characters. Auditory input requires a modification, because phonemes are not atomic: articulatory phonology decomposes each phoneme into a small set of independent distinctive features (voicing, place of articulation, manner of articulation, nasality, and a small number of others), and direct intracranial recordings from human superior temporal gyrus confirm that this is the level at which the auditory cortex actually represents speech sound — neural populations are tuned to specific feature values, not to whole phonemes as unitary categories (Mesgarani, Cheung, Johnson, & Chang, 2014).

We accommodate this by replacing the single $K$-way categorical readout with $D$ independent, smaller categorical readouts, one per feature dimension $d = 1,\ldots,D$ (typically $D \approx 6$–$8$; e.g. $K_{\text{voice}}=2$, $K_{\text{place}}\approx 7$–$8$, $K_{\text{manner}}\approx 6$–$7$). The latent $z^{(1)}$ is partitioned into $D$ corresponding slices, $z^{(1)} = (z^{(1,1)},\ldots,z^{(1,D)})$, and the emission energy becomes a sum of independent cross-entropy terms:

$$E_{PC}(1) = \sum_{d=1}^{D}\left[-\sum_i T_i^{(d)}\log y_i^{(d)}\right] + \frac{1}{2}\epsilon_{z^{(1)}}^T\Pi_1\epsilon_{z^{(1)}}, \qquad y^{(d)} = \text{softmax}\left(z^{(1,d)}\right)$$

This is justified by treating the $D$ feature-level classifiers as independent experts whose distributions combine multiplicatively (Hinton, 2002); in log space this is exactly a sum of energies, so the joint model remains a single, well-defined energy function despite the factored readout. The resulting gradient update is unchanged in form from the single-category case, and remains fully local: each slice updates using only its own residual and its own portion of the prior term,

$$z^{(1,d)} \leftarrow z^{(1,d)} - \eta\left[(y^{(d)}-T^{(d)}) + \Pi_1^{(d)}\epsilon_{z^{(1,d)}}\right], \qquad d=1,\ldots,D$$

with no cross-feature terms required in the bottom-up direction.

The independence assumption is reasonable for inference — each feature can be estimated from the acoustic signal largely on its own — but does not hold for the top-down prior. Phonemes occupy only a small, structured subset of the full combinatorial space of feature-value combinations; most combinations correspond to no phoneme in any language. The generative map $f_2(z^{(2)})$ must therefore produce a *jointly* consistent prediction across all $D$ slices simultaneously, encoding the correlations between features that define the phoneme inventory, rather than predicting each feature independently. Absent this, the model would treat phonologically illicit feature combinations as being just as expected as licit ones.

This modification is confined entirely to the level-1 emission layer. The temporal prediction module is unaffected: it continues to operate on a single continuous latent and to output a continuous prediction $x_{n+1}$ via the diffusion process described above, which is then passed through the factored readout described here rather than through the single flat softmax used for the character case.




## Experimental Evidence



## Existing Work



## Conclusions

## Appendix A How new level 3 pipelines get installed

Why precision-gating can't cover this case

My previous answer assumed a level-3 pipeline already exists for the object in question and just modulates how much its error term matters once compared against new data. That mechanism presupposes there's already an $x_n/z_n$
 being computed somewhere. In the bear case, there isn't — nothing is running at all, so there's no error term to gate. You've correctly identified that this is a failure at an earlier stage: not "an existing model's output gets ignored," but "no model ever got created."

What's actually needed: a cheap, always-on detector that's separate from the pipelines it might spawn

This points to a real architectural gap: something has to decide when to instantiate a new level-3 pipeline in the first place, and that decision-making process itself has to be resource-limited (otherwise you haven't solved anything — you've just moved the capacity problem one level up, since continuously running full object-recognition checks across the entire visual field would defeat the point of having an attention-gated system at all).

The natural fix has real precedent in vision science, and it's a two-stage architecture, not a one-stage fix. Itti, Koch and Niebur's (1998) saliency-map model is the classic computational proposal here: a cheap, bottom-up, parallel process computes simple, low-level feature contrasts (color, intensity, orientation, motion) across the entire visual field continuously and automatically — not object recognition, just "how conspicuous is this region relative to its surroundings" — producing a single topographical saliency map that competes to determine where attention gets deployed next. This is the computational counterpart to Treisman's Feature Integration Theory (already discussed for the binding problem): a parallel, pre-attentive stage that's cheap and runs everywhere, followed by a serial, attention-dependent stage that does the expensive work — in your architecture's terms, that expensive work is instantiating and running a full level-3 predictive-coding pipeline.

So the mechanism would be: a lightweight saliency signal runs continuously and ungated across the whole field; a new level-3 pipeline only gets instantiated and connected to the level-2 hub when a region's saliency signal is large enough and wins the competition for attentional resources currently available. In the bear/gorilla case, task-absorbed attention means the bottom-up saliency signal from the costumed figure — even if genuinely elevated — simply never wins that competition, so no pipeline ever gets created. This is consistent with real inattentional-blindness follow-up work, incidentally: even "unnoticed" stimuli in these paradigms sometimes show measurable physiological orienting responses or later priming effects despite no conscious report — exactly what you'd expect from a saliency signal registering at the cheap, pre-attentive level without ever escalating to full pipeline instantiation.

This connects two things you've already got in the design, rather than adding something unrelated

Two nice unifications worth stating explicitly, since neither requires a genuinely new kind of mechanism:

This is the same resource-allocation logic as the memory write-gate. A few exchanges ago we used prediction-error/novelty exceeding a threshold as the trigger for writing an episode to long-term memory (the Lisman & Grace hippocampal-VTA analogy). Pipeline instantiation is the same kind of gated decision — a cheap signal crossing a threshold before an expensive resource commitment gets made — just applied to creating an active tracker rather than committing to storage.
This gives a concrete mechanism for the "things vs. stuff" distinction from before. Rather than "things" and "stuff" being two fixed, pre-declared categories, this reframes it as a dynamic promotion process: everything starts as part of the coarse, low-precision "stuff" background by default; a region gets promoted to its own individuated level-3 "thing" pipeline specifically when its saliency signal is large enough to win attention. That's a more principled account of the things/stuff boundary than treating it as a static labeling scheme — it's actually being decided online, continuously, by the same saliency/attention competition doing the instantiation-gating work.

Worth writing into the paper as a genuinely separate mechanism from precision-gating — the two together give a fuller account: saliency-gated instantiation explains why some objects never get modeled at all, and attention-gated precision explains why already-modeled but currently-unattended objects can still be missed when they change.

## Appendix B: A memory retrieval system for level 3 models

Good, and this is worth treating as a genuinely different kind of memory problem from the one we solved for episodes — not a variant of the earlier mechanism, but a distinct system that happens to share some computational machinery with it.

This closes a loop from a few exchanges ago, and there's real evidence the two systems are dissociable

When reviewing the vision-hub section, I flagged that "pre-trained models stored in memory, activated by scene" sounded like a different memory system than the episodic Hopfield-retrieval mechanism we'd designed — general, reusable knowledge about what a dog is and how it moves, rather than a specific recalled episode. This is exactly that distinction resurfacing, now needing an actual mechanism: Tulving's episodic/semantic split, but this time with real neuropsychological weight behind treating them as separable systems, not just separable concepts. Vargha-Khadem, Gadian, Watkins, Connelly, Van Paesschen & Mishkin's (1997) classic Science paper on developmental amnesia found children with early, selective bilateral hippocampal damage who have severely impaired episodic memory — they can't recall specific personal events — while attending mainstream school and acquiring broadly age-appropriate semantic/factual knowledge, including new semantic learning, essentially throughout development. That's a genuine double dissociation, not just a conceptual one: episodic memory formation depends critically on the hippocampus in a way general/categorical knowledge acquisition apparently doesn't. That's a real reason to design pipeline-model storage as its own system rather than reusing the episodic memory store wholesale, even though both plausibly lean on the same general computational primitive (associative, content-addressable retrieval).

The retrieval mechanism: don't index by raw weights — index by a compact key, and expand it

This is the part worth being precise about, because the naive version doesn't work. The episodic memory design stored and retrieved states — points (or short sequences) in the same latent space the rest of the architecture already operates in, so Hopfield-style associative retrieval applied directly. A pipeline's learned model is a different kind of object: a whole set of parameters for $q_{\phi}, E_W, 
. Doing associative lookup directly over raw weight vectors is a bad idea — weight space doesn't have the geometric structure you need for similarity-based retrieval to mean anything (permutation symmetries alone mean two functionally-identical networks can have arbitrarily distant weight vectors).

The natural fix is a two-part representation: a small, compact identity key for each stored model — a learned embedding capturing "what kind of object this is for" (closer to a category prototype than to the full model) — paired with the actual parameters, stored separately. Retrieval then works exactly like the episodic case: a query (built from cheap early features of the object) gets matched associatively against the stored keys, not against the parameters themselves. Once a matching key is found, something needs to turn that compact code into the actual weights the pipeline will run — this is precisely the job hypernetworks are built for (Ha, Dai & Le, 2016): a small network that, given a compact identity/context code, generates the weights of a separate, larger target network. So the full retrieval operation is: associative match on compact keys (reusing the same Hopfield machinery already in the design), then hypernetwork-style expansion of the matched key into actual pipeline parameters — not one new mechanism, but the existing retrieval primitive plus one additional, well-precedented decoding step.

This connects directly to last turn's saliency mechanism, rather than needing its own separate trigger

The natural query for this lookup is already sitting in the design: the same cheap, early features of a newly-salient region that triggered pipeline instantiation in the first place are exactly what should drive the retrieval query — "does this look like something we already have a model for." That gives one unified process with a clean fork: saliency wins attention → cheap features extracted → associative lookup against stored keys → match found: hypernetwork expands the key, pipeline instantiates immediately, fully-formed; no match: fall through to the "period of training" the paper already describes. That fork also gives a principled account of why training is slow for genuinely novel objects and fast for familiar ones — it's not that novel-object learning starts from nothing, it's that there's no matching key to expand, so the system most plausibly needs to adapt from the nearest partial match (learning a new dog breed by refining a general "dog" model) rather than learning from scratch, which is both more sample-efficient and closer to how this actually seems to work behaviorally. Once that adaptation period is complete, a new key gets written into the associative store for next time — the mirror image of the retrieval process, and a natural place to reuse the prediction-error/novelty-gated writing criterion from the episodic memory discussion, just gating model creation instead of episode storage.

## Appendix: Contrast with Jeff Hawking

Good catch on the overlap, and yes — Hawkins is explicit and specific about this: the "thousand brains" are cortical columns, located specifically in the neocortex, not elsewhere. This is actually load-bearing for his broader framing (recall the "old brain vs. new brain" dichotomy from a few exchanges back, which drew some pushback for oversimplification) — he explicitly assigns learned, model-building, predictive cognition to the neocortex specifically, in contrast to older subcortical structures he associates with more fixed, evolutionarily-programmed behavior and drives. So the location claim checks out precisely as you recalled it.

On the structural comparison itself, I'd say the overlap is real but not quite one-to-one, and it's worth being precise about where it diverges, since I think the honest comparison is actually more interesting than a clean match would be.

Where they genuinely align: both propose many parallel, quasi-independent predictive models, each responsible for its own local piece of the world, each generating its own predictions from its own local evidence, with the individual models getting reconciled into some kind of shared, integrated representation rather than any one of them being privileged as "the" answer.

Where I'd push back on the one-to-one mapping. Hawkins' theory isn't really one column per object — it's explicitly many columns per object, each sensing that object from a different local vantage point (different patches of skin, different retinal locations), each independently building its own partial model, and then voting to reach consensus that they're all looking at the same thing. The redundancy is actually central to his account — it's specifically how he explains fast, robust object recognition despite any single column only ever seeing a small part of the object at a time. Our design, by contrast, is one pipeline per object — a single model, not several models racing to agree on the same referent. So the more precise mapping isn't "one level-3 pipeline ≈ one cortical column" — it's closer to "one level-3 pipeline ≈ the consensus that would emerge from many of Hawkins' columns voting," which is a real difference in granularity, not just a relabeling.

Two further differences worth having explicit, since a reader who knows Hawkins' work will notice them:

Integration mechanism. Hawkins' voting is a comparison/consensus process across many peer columns (thought to be implemented via long-range lateral connections at a specific cortical layer); our hub integration is energy-minimization via predictive-coding error propagation. Different computational operations, even where the functional role — reconcile many local views into one shared answer — is similar.
Representational currency. Hawkins' columns build their models using grid-cell-like modular reference frames, generalized from spatial navigation; our level-3 pipelines use continuous latent states and learned energy functions. Even granting the structural analogy, the actual content each "model" traffics in is quite different mathematically.

One more thing worth flagging honestly rather than assuming Hawkins already covers it: I don't recall his theory giving an explicit account of how a column comes to engage with a genuinely novel object it's never encountered before — his work focuses more on the mature, already-learned operation of a column building its model gradually through repeated movement-based sampling over many exposures. The saliency-gated instantiation-plus-associative-retrieval mechanism we just worked out — deciding in real time whether to spin up a new pipeline, and if so, whether from a retrieved match or from scratch — looks like it goes beyond what Hawkins explicitly specifies, rather than being something already worked out in his framework that we're just relabeling. Worth stating that as a point where the design extends past the overlap, not just recapitulates it.
