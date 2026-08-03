---
layout: default
title: " A Hierarchical Energy-Based Model for Multimodal Cognition"
---

# A Hierarchical Energy-Based Model for Multimodal Cognition

**Contents**     

## Introduction 

This paper proposes an hierarchical computational model for semantic cognition in the brain. The model, that we call Integrated Multimodel Latent Energy based Predictive Processing or IM-LEPP
builds on the previous paper that proposed the LEPP model for perception as a process of flow on energy landscapes. The IM-LEPP model extends this idea and builds a model for cognition that integrates both perception and language processing. The IM-LEPP architecture allows for additional sensory modalities to be integrated into the model in a straightforward manner. 

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
- The IM-LEPP model introduces an integrated system state that includes language and vision and can be extended with more modalities. Thus the language generated by the model is grounded by by both visual and linguistic data. It is thought that LLMs also maintain an internal latent state that is not visible externally, however this state is entirely a function of language statistics and is not grounded in real world sensory data and this results in the well known [symbol grounding problem](https://arxiv.org/html/cs/9906002), i.e., LLMs see only the linguistic symbols, never what those symbols are about. The integration of vision and language into a shared common state in IM-LEPP constitutes a solution to this problem.
- IM-LEPP gives us direct access to the latent states through which all generation is done which can be used to influence the models output. Something equivalent can be done with LLMs by probing the transformer's middle layers. In IM-LEPP the latent state is made explicit by the model while it remains hidden in LLMs.

This paper makes the following contributions:

- We propose a hub-and-spoke integration architecture for multiple sensory modalities, with modality-specific predictive processing pipelines converging on a shared latent state via predictive coding, solving both the binding problem and asynchronous multi-rate updating across modalities operating on different timescales.
- We propose an hierarchical hub and spoke model for vision, in which a central hub integrates latent states from individual objects in the field of vision. Each object has its own predictive processing pipeline and its latent state evolves as a function of its own object based model. The model includes mechanisms for attentional suppression (through precision reduction), saliency-gated instantiation of new object pipelines, and open-loop prediction for objects outside current attentional focus. Together these aspects of the model give a mechanistic account of phenomena including in-attentional blindness and change blindness.
- We propose a predictive processing model for language with parallel phoneme-based and character-based input channels, each feeding a two-level (character/phoneme at the lower level and words at the higher level) hierarchy, including an extension of predictive coding to discrete/categorical data and a proposed biologically plausible implementation of the categorical readout via divisive normalization. The next word prediction in this model is based on an integrated semantic level latent state that takes the other sensory modalities into account.
- We demonstrate that the model's own mathematical structure recovers or motivates several independently established findings in psycholinguistics and neurolinguistics, including surprisal theory, the N400 and P600 components, and garden-path reanalysis. We also discuss a specific, falsifiable point of contrast with transformer-based language models regarding trajectory-sensitivity in next-word prediction (via comparison with [Barenholtz, 2026)](https://arxiv.org/pdf/2606.05346).
- We propose a model for the memory subsystem that distinguishes semantic (object-model) and episodic memory, with associative (Hopfield-style) retrieval, a proposed novelty and valence-gated storage criterion linking hippocampal and amygdalar mechanisms, and integration into the central ATL hub.

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

![](https://subirvarma.github.io/GeneralCognitics/images/stat169.png) 

Figure 3: The IM-LEPP model

We propose a model for integration of visual and language modalities based on the hub and spoke model, which we call integrated multimodal latent energy-based predictive processing or IM-LEPP (see above figure). This model extends the LEPP model that was described in the [previous paper](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html) in several ways: It proposes a hierarchical spatial integration structure for the vision model, it introduces a hierarchical temporal integration structure for language, and finally it proposes how the two may be integrated together to create a common representation. The IM-LEPP model has the following features:

- There is a central ATL type hub at level 1 that integrates representations coming in from the vision and language hubs. Note that the communication between the central hub and the vision and language hubs is bi-directional, so that not only do the spoke hubs influence the representation in the central hub, but they in turn are influenced by the information coming from the central hub.
- The vision hub itself has a two level structure. The central vision hub at level 2 integrates information coming from level 3 predictive processing pipelines, with the understanding that the latent state in the level 2 hub represents a scene, while the latent states in the individual level 3 predictive processing pipelines represent objects in the scene. The representation of each of these objects evolves asynchronously in time and the level 2 hub integrates the latest information from each individual object and sends it up to the central level 1 hub.
- The per-object level 3 predictive processing pipelines operate according to the inference-prediction-generation framework that was used for the LEPP model. This results in temporal predictions for each object's latent representation that are sent to the level 2 vision hub for integration with all the other objects in the scene. This combined scene level representation in turn gets integrated with representations from other modalities in the multimodal level 1 hub. The integrated level 1 representation in turn is fed back to the object predictive processing pipelines, which then use it to generate percepts. Note that these percepts take all the other objects that are in the scene into account (as well as other modalities), by virtue of the fact that they are based on integrated representations coming from the level 1 multimodal hub.
- The language sub-system also has a two level hierarchical structure, however the hierarchy is in time rather than in space. At the lower level of the hierarchy is a predictive processing pipeline that operates at the discrete phoneme level (in the case of spoken language) or at the character level (in the case of reading). This level incorporates an inference-prediction-generation modules whose job is to predict the next phoneme or character. The latent representation from this level is sampled at certain discrete instants that contain representations for whole words, and these are fed as input into a word level predictive processing pipeline at level 2. The next word prediction done at this level is in turn sent to the cenntral ATL hub where it gets modified by information from the other modalities, and then it is sent back to the word level hub, and ultimately to the phoneme level hub to generate percepts in the form of sound.
Note that unlike in an LLM, next word generation is not based solely on word occurrence statistics, but utilizes a shared central latent representation that is influenced by all the other modalities in the brain.

Thus the the IM-LEPP model paints a picture in which there are number of distributed, predictive processing pipeline modules in the brain, that are individually responsible for predictions in the modality they are tracking. Hence the prediction operations happens in a distributed manner, while central hubs at level 1 and level 2 are responsible for integrating the lower level representations, and in turn feeding them back to the predictive processing pipelines.
All state changes in this model at the various pipelines and hubs are based on the principle of the energy minimization, and thus provide a plausible model for the brain's operation at Marr's level 2. 

## A Hub and Spoke Model for Vision

![](https://subirvarma.github.io/GeneralCognitics/images/stat150.png) 

Figure 4: Hub and Spoke Model for Vision: Integration of Predictive Processing Pipelines for Multiple Objects into a Scene

This section has a more detailed description of the vision model's operations at levels 2 and 3. Modern generative AI systems process images at the level of pixels, and learn prediction models for how  these pixels evolves with time. The brain on the other hand is thought to decompose a scene at the object level, and then model the temporal evolution of the individual objects. For example in a road scene, there are models for pedestrians and vehicles as well as a model for the background containing the sky, foliage etc. The brain tracks each object individually, and then integrates all the representations to create the scene that we see in front of us. The above figure shows the IM-LEPP model for vision that uses a similar hierarchical structure. 

The IM-LEPP model proposes that the brain stores models for most of the objects that we encounter in our lives in memory, and a subset of these models is invoked and attached to the vision hub depending on the objects that are in the field of vision. If a new object is encountered, then its model is not trained from scratch, but instead it builds on an existing model that is similar to it. This allows the model to learn using much fewer training examples compared to AI systems which solely depend on using pixel level correlations.

![](https://subirvarma.github.io/GeneralCognitics/images/stat171.png) 

Figure 5: Predictive Processing Pipeline for an Individual Object at Level 3

The level 3 predictive processing pipeline for an individual object is shown in the above figure, and follows the LEPP design, with inference, prediction and generation modules. As new sensory data $s_n$ comes in, it is integrated into the latent state $z_n$ for the object by using predictive coding as described in [Varma](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html). Inference and generation operate by using the principle of minimization of predictive coding energy $E_{PC}$ given by

$$ E_{PC} = {1\over 2}\epsilon_y^T\Pi_y\epsilon_y + {1\over 2}\epsilon_z^T\Pi_z\epsilon_z  $$

Thus the latent state is estimated so as to reduce the error $\epsilon_y$ between the generated value and the sensory data, plus the error $\epsilon_z$ that tracks how far latent state strays from its prior predicted value. The predictive coding based inference results in a latent state $z_n$ that is fed into the temporal prediction module and this results in a prediction $x_{n+1}$. 

The prediction process is modeled by using a multi-stage diffusion model that minimizes an energy $E_W(x;z_n,u_{n+1})$ by gradually annealing the state $x$ of the system until it reaches a state $x_{n+1}$ of low energy. Hence the energy landscape reflects the latest sensory data $s_n$ through the state $z_n$, and thus as new sensory data arrives the energy landscape changes over time thus changing the energy minimas. This is illustrated in figure 8 in [Varma](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html).

The prediction $x_{n+1}$ is sent to the level 2 vision hub and this results in the scene level latent representation $xx_{n+1}$ that takes the presence of other objects into account. This in turn is sent to the multimodal level 1 hub, resulting in the latent representation $xxx_{n+1}$ which takes the other modalities into account.
This state information is then fed back into initial object predictive processing pipeline by setting its latent state to $x_{n+1} = xxx_{n+1}$. Note that as a result of this integration with higher level hubs, the prediction $x_{n+1}$ incorporates information about other objects in the scene as well other modalities that may be relevant such as valence. 
The modified latent representation $x_{n+1}$ is used to generate the next percept $g_{\phi}(x_{n+1})$, and is also used to kick off the inference phase of the predictive processing pipeline by comparing it with the new sensory data $s_{n+1}$. This subsequently results in a new object latent state $z_{n+1}$ and the cycle repeats.

![](https://subirvarma.github.io/GeneralCognitics/images/stat161.png) 

Figure 6: Integration of Multiple Object Level Predictive Processing Pipelines into the Vision Hub at Level 2

The structure of the level 2 vision hub is shown in the above figure. It shows that the latent state predictions $x_n$ from the object level pipeline is fed into an object level predictive coding pipeline in the vision hub, where $x_n$ serves as the ground truth value. As a result of this architecture the hub latent state $xx_n$ gets modified, and the new value reflects the value of the latent state $x_n$ at the object level.
The presence of other predictive coding pipelines at the hub ensures that the hub state $xx_n$ reflects not just the latest information from the current object level pipeline, but also information from all the other other object pipelines that are active at the same time. Thus $xx_n$ serves as a scene level representation for the vision system.
As soon as an object moves out of the field of vision, its level 3 predictive processing pipeline is dis-connected from the level 2 vision hub, and as other objects appear their pipelines are in turn connected to the hub. If the objects are well known due to frequent appearance, then their predictive processing models are pre-trained and stored in memory, while new objects undergo a period of training.

Note that the structure of the predictive coding pipeline agrees with what has been observed about the variation in the mode representation in the biological ATL hub as shown in figure 2. Specifically the predictive coding states that are closer to the vision (or language signal) mode still retain the signatures of that mode, and as we move up the pipeline, the representation turns gradually amodal.

Note that this design takes into account the predictions that arise when two objects are interacting with each other, for example a ball bouncing off a wall. In this case there is a level 3 model for the ball, as well as for the wall, and two latent states integrated at the level 2 hub, and subsequently this information is used to update the latent state $x_{n+1}$ for the ball. Thus if the ball is very close to the wall, then the next prediction will lead to a change in its trajectory since the ball model knows about the presence of the wall.

If both the objects are moving towards each other, for example two balls about to collide, and assume that our attention is focused on ball 1 so that its state is being updated constantly. 
In this situation the model's level 3 predictions for ball 2 operate in an open-loop fashion based on its last position and velocity, and continue to get integrated with ball 1's predictions at the level 2 hub. 
Thus the system should be able to predict the collision at the right instant even though attention is focused on ball 1.

![](https://subirvarma.github.io/GeneralCognitics/images/stat162.png) 

Figure 7: Integration of Vision and Language Hubs into the Cognition Level Hub at Level 1

The above figure shows the structure of the level 1 hub located in the ATL. It is the same as for the level 2 vision hub, however now the signals are coming in from vision as well as language modalities. There is a predictive coding pipeline for vision and another one for language, and this results in a representation $xxx_{n+1}$ that is amodal and is influenced by both.
After the predictive coding pipeline settles down, the resulting value of the hub state $xxx_n$ is fed back into the level 3 part of the vision and language pipelines, and serves as the latent $x_n$ value that is used to generate the next percept $g_{\phi}(x_n)$. The latent $x_n$ subsequently gets modified by the new sensory data $s_n$, which results in the latent state $z_n$.
Thus the percept generation takes place at the mode level, but takes into account everything else that is happening by virtue of this architecture.

Note that the vision updates happen almost continuously, while the language updates in the form of words happen every hundreds of milliseconds. The problem of integrating two streams running on different time scales is called the *multirate sensor fusion problem* in robotics. 
The proposed solution to this problem as shown in the above figure has empirical support in psycholinguistics. the Visual World Paradigm literature
[Tanenhaus, Spivey-Knowlton, Eberhard, & Sedivy, 1995](https://sites.socsci.uci.edu/~rfutrell/teaching/lsci159-f2020/readings/tanenhaus1995integration.pdf) showed via eye tracking that visual context influences spoken word recognition and syntactic parsing during the earliest moments of processing.
We will assume that the update to the shared state $xxx_n$ on the arrival of a new word happens much faster than the interval between successive vision updates, in other words the system does not run into the problem that the target for the word update is continuously changing as a result of the faster vision updates.

Consider the scenario in which we are driving a vehicle and there is another vehicle in front of us, as well as other objects such as pedestrians etc which are visible. As per the model, the system will install level 3 predictive processing for all objects that we pay attention to during the course of the drive, but there are some objects that we pay more attention to, such as the car in front of us.
The scenario can evolve into one of the following ways:

- We are paying frequent attention to the car in front of us, so its representation $z_n$ gets updated frequently with new vision data. There is another car behind us that we can see through our rear view mirror, but we play less frequent attention to it. In between the times that we look into the rear view mirror, the representation for that car evolves as expected, so that if that car appears by the side of our vehicle it is something that the system has predicted (i.e., the latest level 1 $xxx_n$ representation and the sensory data $s_n$ at level 3 for the car would agree with each other), so we are not surprised. The actual mechanism that the system uses for for tracking the behavior of the the other car is open loop prediction using a diffusion model from the last known position of the car. This mechanism was described in detail in [Varma](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html).
- Consider the same scenario as before, but assume that the car behind us made a turn while we were not paying attention to it. In this case our visual model does not know that the car has disappeared, and the next time we look back we expect to see it, but the sensory data says otherwise. Hence the other car is not behaving in the way that our internal model is expecting it to behave, which causes some surprise. Once we see that the car is not there, its level 3 pipeline is removed from the set of objects that are being tracked at level 2. Another example of this would be if the car in front of us suddenly braked while we were looking at our phone. Again in this case our internal model for the car is updating in a way that does not agree with reality, until we look up and see the change. Unlike the case for the disappearing car, in this case the model for the other vehicle is not de-installed, but is updated with a large error correction when new sensory data comes in, i.e., when we look up from our phone.
- There are cases in which the brain actively suppresses the updating of one or more objects whose pipelines are currently active. For example while driving we don't want to get distracted by the image of large billboard by the side of the road. In this case a level 3 pipeline will be installed for the billboard when we see it for the first time, however we decide not to pay attention to it. This can be done by reducing the value of the precision parameter $\Pi_y$ that is used in the predictive coding pipeline for the billboard at the level 2 vision hub. This mechanism was first described by [Feldman and Friston (2010)](https://www.frontiersin.org/journals/human-neuroscience/articles/10.3389/fnhum.2010.00215/full) in their paper {\it Attention, uncertainty and free energy"}.
- As the last example, consider the case when a level 3 pipeline for an object that is in the vicinity of our car never gets installed, so that we are complete unaware of its existence. This corresponds to the case when there is a car in our blind spot, and we try to make a turn into its lane. In this case there is a much bigger surprise waiting for us when the other car honks, and at that point the system installs a model for it and starts tracking it. Another well known example of this phenomenon is the case of bear costumed person crossing the court in the middle of a basketball game and it fails to get noticed, as was originally pointed out by [Simon and Chabris](https://pubmed.ncbi.nlm.nih.gov/10694957/). Again since attention is focussed on the ball and the players, the level 3 model for the bear never gets installed.

The last scenario points to the need for a cheap, always-on detector separate from the pipelines it might spawn since something has to decide when to instantiate a new level-3 pipeline,
and that decision process itself must be resource limited. [Itti, Koch and Niebur’s (1998)](https://hasler.ece.gatech.edu/Courses/MachineLearning/FoundationalPapers/Itti_Koch_Neiber1998.pdf)
saliency-map model is the classic computational proposal: a cheap, bottom-up, parallel process computing simple feature contrasts (color, intensity, orientation, motion) across the entire visual field continuously, producing a topographical saliency map that competes to determine where attention deploys next. 
A new level 3 pipeline gets instantiated only when a region’s saliency signal is large enough and wins the competition for currently available attention. In the bear case, task absorbed attention
means the saliency signal from the costumed figure never wins that competition, so no pipeline ever gets created. This is consistent with inattentional-blindness follow-up
work showing measurable physiological orienting responses to “unnoticed” stimuli despite no conscious report. This gives a concrete mechanism for the “ background things vs. stuff” distinction, everything starts as coarse “stuff” background by default and a region gets promoted to its own individuated “thing” pipeline specifically when its saliency signal wins the attention competition.

## A Predictive Processing Model for Language 

Language comprehension and generation is a relatively late addition to our cognitive system, it happened in the last 50,000 years. By then the brain had already built a rich, grounded, pre-linguistic continuous conceptual state (the $zzz_n$ in the IM-LEPP model), and language was added comparatively effortful, serial auto-regressive-like process that reads from and writes to that substrate rather than buikding another one from scratch. Hence the brain's $zzz_n$ equivalent is grounded in perception, sound, social experience etc and language is another channel feeding into this already existing representation. This points out to a fundamental difference between the brain (and the IM-LEPP model) and modern LLMs, since the latter are not grounded and base their latent representations purely from word co-occurrance statistics and nothing else. There have been some recent efforts to build a predictive processing model for language, for example see the [LD4LG](https://arxiv.org/abs/2212.09462) model. However this and similar models run into the problem of designing a good auto-encoder for language, which hasn't been solved yet. The reason for this is that their latent representations are not grounded with other sensory data, and no amount of auto-encoder engineering can fix lack of grounding.

Language shares a number of features in common with the visual system, and both can be modeled as predictive systems, images in one case and words in the other. That said, words are a more abstract entity than objects and are discrete in nature, i.e., there are a finite number of them. The problem then is that of translating the sound coming in through our ears into word level latent representations that attach semantic meaning to them and is followed by prediction of the next word. These sounds could be coming from an external source, or it could be just the sound of our voice talking. In the former case, the next word in the sequence can serve as an error connection signal for the brain's prediction for the next word, very much like the error correction that happens in vision, and in the process the brain's model for next word prediction gets trained. For the case when the sound is from our own voice, there is still an error correction  feedback loop in operation, since sometimes we speak out a word, and then hearing the sound makes us realize that we meant to say something else. 

There has been a good amount of evidence that has been collected over the years that unlike for vision, the brain uses discrete representations when processing language.
The paper on categorical perception by [Liberman, Harris, Hoffman & Griffith, 1957](https://philpapers.org/rec/LIBTDO-2) is a classic in this area. They showed that a continuously-varying acoustic parameter is perceived and discriminated categorically, with a sharp identification boundary. Direct neurophysiological confirmation was established by [Chang et al. (2010)](https://www.nature.com/articles/nn.2641) who found categorical speech representations in human superior temporal gyrus (STG).
[Mesgarani, Cheung, Johnson & Chang (2014)](https://linguistics.berkeley.edu/~kjohnson/papers/Mesgarani_et_al_2014_Science.pdf), using intracranial recordings, found STG populations
tuned to discrete phonetic features, not raw continuous acoustics. 

So the brain does discretize but not at the level of the word vocabulary size, which easily exceeds 10,000 words for most people.
Instead  a hierarchical cascade of much smaller categorical decisions are made at the phoneme level on a twenty dimensional acoustic feature vector that was identified by Mesgarani et.al, and then several phoneme representations are strung together to compose into a word representation. Hence while phoneme level feature encoding is well established (see [Leonard et. al. (2024)](https://www.nature.com/articles/s41586-023-06839-2)), exactly how these compose into whole-word representations is still an open question. In this paper we propose a hierarchical two level mechanism by which this can be accomplished.

There is another source for words through our visual system when we read or write and we will consider this simpler case first. 

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

The hierarchical system composed of a discrete character (or phoneme) level pipeline at level 1 with a continuous word level pipeline at level 2 constitutes a possible solution to the whole word representation problem posed in [Leonard](https://www.nature.com/articles/s41586-023-06839-2).

![](https://subirvarma.github.io/GeneralCognitics/images/stat168.png) 

Figure 11: Integration of vision and language modules at the central ATL hub

The above figure shows the integration of vision and language modules at the central ATL hub. The integrated state $zzz_n$ is fed back into the predictive processing pipelines of the respective hubs. 
This allows additional modalities to influence the next generated word, for example the information coming in through the visual system may influence what we say next. Similarly the emotional related information coming in through the valence system (valence) can influence our choice of the next word.

In order to see the see multi-modal language model in operation, consider the following scenario: The model is initially shown a video, which results in the invocation of the vision model. Lets assume that the ATL hub state at the end of the video is $ZZZ_1$. Then the user asks a written question that has to do with the video, and this information comes in through the language model, and at the end of the question the ATL hub state is at $ZZZ_2$. Note that this hub state is now a summary of all that the model has seen and read so far, and is now primeed to provide an answer. This it does by feeding $ZZZ_2$ back into the level 2 next word model, which results in the production of characters at the level 3. These characters are then fed back into the level 2 word model (i.e. the model self reads to make sure that the characters are consistent with the predicted word), and this results in the prediction of the next word, and an update to the word model state $zz_n$. The updated state is then fed into the ATL hub, so that it gets updated with any new information that has come in through any of the other modalities, and then gets fed back to the word model to generate the next word. This cycle continues until the model has generated the answer to the question.

Modern multimodal LLMs can also be used for the scenario described above, but there is an important distinction between the way the model operates compared with the LLM. The LLM presumably has the equivalent of an internal latent representation $z$ that summarizes everything that model has seen, read and generated so far. However this latent state is not directly observable, experiments done by probing the middle layers of the transformer have been shown to have similar characteristics. The latent state in the IM-LEPP model is explicitly made available, at all levels of operation. This allows us to directly probe the 'mind' of the model, and also influence it through the ATL hub modalities. For example one can imagine creating an emotion state for the model by tracking how well its latent state predictions match with sensory data thus simulating the amygdala. The state of the artificial amygdala can in turn be fed back into the ATL hub to influence the model's central latent state, and thus its furure word or image generation. Note that this type of pperation cannot be done with LLMs due to lack to access to its latent state.

There is another point of distinction between the IM-LEPP model and LLMs and this has to do with how the models go about doing the next word generation.

### The Predictive Coding Pipeline for Discrete Senesory Data

![](https://subirvarma.github.io/GeneralCognitics/images/stat143.png) 

Figure 12: Predictive Coding Pipeline for Characters

The traditional predictive coding pipeline was designed for analog sensory data, but it can be extended to the case when the data happens to be discrete, as for the case of characters or phonemes in the level 3 part of the language model (see [Whittington and Bogacz](https://www.bndu.ox.ac.uk/sites/default/files/pdf_files/Whittington%20Bogacz%202017_Neural%20Comput.pdf)).
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

### Approximating the Softmax Function in Brain Circuitry

The computations in the predictive coding pipeline described above require the computation of $y_i$ using the softmax function. How can this be accomplished in the brain?

A substantial body of work by Carandini and Heeger identifies **divisive normalization** as what they term a canonical neural computation, i.e., as a a single computational motif recurring, with only minor variation, across an unusually wide range of brain systems and species ([Carandini & Heeger, 2012](https://redwood.berkeley.edu/wp-content/uploads/2018/08/carandini-heeger.pdf)). In its general form, the response of an individual neuron is divided by a term reflecting the pooled, summed activity of a local population of neighboring neurons:

$$ response_i = {R_i^n\over{ \sigma^n + \sum_j R_j^n} }  $$

where $R_i^n$ is neuron $i$'s driven input, $n$ is an exponent emppirically estimated in the range of roughly 2–4, and $\sigma$ is a semi-saturation constant preventing division by zero at low input levels. Since this discovery, this circuit has been found in several other areas in the brain other than vision.

This is directly relevant to the biological plausibility of categorical, competitive readouts of the kind used in this paper's discrete phoneme and character-level predictive coding pipelines. Heeger's own theoretical treatment of cortical function makes the connection explicit, noting that "max pooling (also called softmax) can be approximated by normalization" ([Heeger, 2017](https://www.pnas.org/doi/10.1073/pnas.1619788114)).
This means that the same divisive circuit already documented for contrast and motion processing is, in principle, capable of implementing the kind of competitive, winner-take-all-like selection among discrete alternatives that a softmax output layer performs in an artificial network. 
One point worth noting here is that the biologically-supported nonlinearity in this circuit is a power law (i.e, response raised to exponent $n$), not the base $e$
exponential used in the standard machine-learning softmax function. The two forms are qualitatively similar since both produce graded, saturating competition among a pool of candidates, sharpening toward winner-take-all behavior as the exponent or gain increases, but they are not mathematically identical, and the power-law form is the one with direct physiological support, while literal exponentiation appears in the literature mainly as a convenient link function in statistical (point-process GLM) fits to spike data rather than as an established biophysical mechanism.

### Extension to Auditory Processing of Language (Phonemes)

The predictive coding model for level 1 developed above assumes a single flat categorical readout, appropriate when the input alphabet has no independently-motivated internal structure — as is the case for written characters. Auditory input requires a modification, because phonemes are not atomic: articulatory phonology decomposes each phoneme into a small set of independent distinctive features (voicing, place of articulation, manner of articulation, nasality, and a small number of others), and direct intracranial recordings from human superior temporal gyrus confirm that this is the level at which the auditory cortex actually represents speech sound — neural populations are tuned to specific feature values, not to whole phonemes as unitary categories [Mesgarani, Cheung, Johnson, & Chang, 2014](https://linguistics.berkeley.edu/~kjohnson/papers/Mesgarani_et_al_2014_Science.pdf).

We accommodate this by replacing the single $K$-way categorical readout with $D$ independent, smaller categorical readouts, one per feature dimension $d = 1,\ldots,D$ (typically $D \approx $6$–$8$; e.g. $K_{\text{voice}}=2$, $K_{\text{place}}\approx 7$–$8$, $K_{\text{manner}}\approx $6$–$7$). The latent $z^{(1)}$ is partitioned into $D$ corresponding slices, $z^{(1)} = (z^{(1,1)},\ldots,z^{(1,D)})$, and the emission energy becomes a sum of independent cross-entropy terms:

$$E_{PC}(1) = \sum_{d=1}^{D}\left[-\sum_i T_i^{(d)}\log y_i^{(d)}\right] + \frac{1}{2}\epsilon_{z^{(1)}}^T\Pi_1\epsilon_{z^{(1)}}, \qquad y^{(d)} = \text{softmax}\left(z^{(1,d)}\right)$$

This is justified by treating the $D$ feature-level classifiers as independent experts whose distributions combine multiplicatively (Hinton, 2002); in log space this is exactly a sum of energies, so the joint model remains a single, well-defined energy function despite the factored readout. The resulting gradient update is unchanged in form from the single-category case, and remains fully local: each slice updates using only its own residual and its own portion of the prior term,

$$z^{(1,d)} \leftarrow z^{(1,d)} - \eta\left[(y^{(d)}-T^{(d)}) + \Pi_1^{(d)}\epsilon_{z^{(1,d)}}\right], \qquad d=1,\ldots,D$$

with no cross-feature terms required in the bottom-up direction.

The independence assumption is reasonable for inference — each feature can be estimated from the acoustic signal largely on its own — but does not hold for the top-down prior. Phonemes occupy only a small, structured subset of the full combinatorial space of feature-value combinations; most combinations correspond to no phoneme in any language. The generative map $f_2(z^{(2)})$ must therefore produce a *jointly* consistent prediction across all $D$ slices simultaneously, encoding the correlations between features that define the phoneme inventory, rather than predicting each feature independently. Absent this, the model would treat phonologically illicit feature combinations as being just as expected as licit ones.

This modification is confined entirely to the level-1 emission layer. The temporal prediction module is unaffected: it continues to operate on a single continuous latent and to output a continuous prediction $x_{n+1}$ via the diffusion process described above, which is then passed through the factored readout described here rather than through the single flat softmax used for the character case.

The three level model for language that has been presented here is backed up by some experimental data that has been collected over the years.
The paper on categorical perception by [Liberman, Harris, Hoffman & Griffith, 1957)](https://philpapers.org/rec/LIBTDO-2) is a classic in this area, they showed that a continuously-varying acoustic parameter (voice onset time) is perceived and discriminated categorically, with a sharp identification boundary. 
[Chang et.al. (2010)](https://www.nature.com/articles/nn.2641) provided direct neurophysiological confirmation by finding categorical speech representations in superior temporal gyrus (STG) area of the brain; [Mesgarani, Cheung, Johnson & Chang (2014, Science)](https://linguistics.berkeley.edu/~kjohnson/papers/Mesgarani_et_al_2014_Science.pdf), using intracranial recordings, found STG populations
tuned to discrete phonetic features, not raw continuous acoustics.
[Hickok and Poeppel’s (2007)](https://www.nature.com/articles/nrn2113) dual-stream model locates early phonological processing in STG/STS of the brain with a lexical-interface stage in posterior middle temporal gyrus (pMTG) — mapping cleanly onto the three stages of the model presented here: STG/STS for phonetic features, pMTG for word-level $zz$ representation, and, continuing upward, Lambon Ralph’s ATL hub for integration with other modalities.

Do the latent states $zzz_n$ or $zz_n$ encode 'thought'? 
Levelt’s production model as described in his book [Speaking: From Intention to Articulation (1989)](https://www.mpi.nl/publications/item67053/speaking-intention-articulation) has a first stage, conceptualization, whose output is a preverbal message — a language-independent conceptual representation of what to say, prior to and dissociable from any particular verbalization (which is why “the same thought” can be expressed in different words or languages). This is a direct architectural instantiation of exactly the proposed role for 𝑧:̄ a persistent, amodal state that the generative pathway then unrolls into a word sequence, with 𝑧 ̄ playing the role of the preverbal message and the language pipeline playing Levelt’s formulation stage.

### Connection to Surprisal Theory, the N400 Effect and Garden Path Re-analysis

Over the years neuroscientists have discovered a number of patterns in the way the brain goes about processing language, and the three phenomena references in the header are the among the most well known among the. In the following we will investigate the relation between these and predictions from the IM-LEPP model.

**Surprisal Theory**

[Hale (2001)](https://dl.acm.org/doi/10.3115/1073336.1073357) and more influentially [Levy (2008)](https://www.mit.edu/~rplevy/papers/levy-2008-cognition.pdf) proposed that the processing difficulty of a word during real-time comprehension is proportional to its surprisal, which was defined as the negative log probability of that word given its pretceding context:

$$  surprisal(w_i) = -\log p(w_i|w_{\lt i}) $$

This equation says that predictable words (low surprisal) are read quickly while unexpected words (high surprisal) cause measurable slowdowns in reading time and eye-tracking measures. This has been extensively validated, including with surprisal estimates from modern LLMs The IM-LEPP model provides a direct mathematical reason that explains the extra comprehension effort as explained next.
The IM-LEPP model uses a decomposition of a word $w$ into a sequence of characters $(ch_1,...,ch_k)$, so by applying the cahin rule of probability, the surprisal definition becomes

$$ surprisal(w) = -\log p(w_i|yy) = \sum_{j=1}^k [-\log P(c_j|c_1,...,c_{j-1},yy)]  $$

where the $yy$ is the latent representation of the word as predicted by the level 2 word level pipeline. Hence the generation of the word corresponding to $yy$ is decomposed into a serial generation of the characters for that word. Assuming that the ground truth for the $i^{th}$ character is given in 1-hot form by $t=(t_1,...,t_K)$, the previous section showed that the predictive coding pipeline for the $i^{th}$ character is driven by the minimization of the energy term $-\sum_k t_k\log y_k$ which reduces to the definition of surprisal $-\log y_{true\ character}$. If there is a big difference between the ground truth character $t$ and the predicted character, then the predictive coding energy pipeline will take longer to settle down for each character, and thus for the entire word, which maps naturally onto longer reading times, which is the surprisal effect.

Note that there is an additional error correction happening at level 2, where the  level1 generated ground truth latent representation of the word that actually arrived is compared with the predicted latent $yy$.
This happens in continuous latent space, not over word identity, so it isn't measuring "how likely was this word" the way the summed level-1 terms do. It's closer to measuring "how well did the higher-level semantic/contextual expectation $yy$ fit what arrived," independent of how surprising the word's bare identity was, which brings us to the N400 effect.

**N400**

[Kutas and Hillyard (1980)](http://kutaslab.ucsd.edu/people/kutas/pdfs/1980.S.203.pdf) found a negative EEG deflection peaking around 400ms after a word was read, and this was larger for semantically unexpected words in the context. Their original example, "He spread the warm bread with socks," showed a large N400 for the anomalous final word.
There's an active, unresolved debate in the ERP literature about what N400 actually indexes. Some accounts treat it as reflecting ease of lexical access/retrieval (a facilitation account), others as reflecting the difficulty of integrating a word's meaning into the evolving sentence/discourse representation (an integration account). 

This maps remarkably well onto a distinction already built into IM-LEPP's two level structure for language:
The summed level-1 cross-entropy terms are the natural computational candidate for the lexical-access side of the N400 debate (word-identity predictability, classical surprisal), while level 2's continuous prior-mismatch term is the natural candidate for the integration side (how well the word's meaning fits the evolving discourse representation). These are two terms that correspond to two different, independently-motivated quantities in the psycholinguistic literature, occurring at two different, architecturally-distinct levels.
There's contemporary work pursuing exactly this kind of decomposition (a recent paper titled ["Decomposition of surprisal: Unified computational model of ERP components in language processing,"](https://arxiv.org/abs/2409.06803) and [Kuperberg, Brothers & Wlotko's](https://www.biorxiv.org/content/10.1101/404780v2) work proposing distinct neural signatures for violated predictions at different levels of representation), so IM-LEPP's energy decomposition is relevant to a current research conversation rather than restating settled science.

[Osterhout and Holcomb (1992)](https://faculty.washington.edu/losterho/Osterhout%26Holcomb1992.pdf) identified a distinct ERP component P600 corresponding to a positive deflection around 600ms which was specifically elicited by syntactic anomaly and distinct from N400's semantic profile. It's since been found to respond to a broader range of syntactic ambiguities and reanalysis demands, not just outright grammatical violations, which brings us to the next topic.

**Garden Path Re-Analysis**

A garden-path sentence is one that's temporarily structurally ambiguous in a way that leads readers to commit to an incorrect initial parse, requiring revision once disambiguating material arrives. The canonical example, from [Bever (1970)](https://dingo.sbs.arizona.edu/~tgb/pdfs/beverpdf_11.pdf): "The horse raced past the barn fell". Readers initially parse "raced" as the main verb, then hit "fell" and must reanalyze "raced past the barn" as a reduced relative clause. [Frazier and Rayner (1982)](https://www.sciencedirect.com/science/article/abs/pii/0010028582900081) established the empirical signature via eye-tracking, which was increased reading times and regressive eye movements specifically at the disambiguating word.

Garden-path reanalysis can be explained using IM-LEPP as follows: On the first reading of the sentence, the diffusion based optimization causes the system latent state $xx_n$ 
at the output of the prediction module at level 2, to settle into a locally low-energy but incorrect interpretation after the word 'raced' is read, which propagates into a large error several words later when the word 'fell' is read. At this point the attention tracks back to the point of dis-ambiguation 'raced' which is read again and this results in an escape from $xx$ to a new prediction $xx'$ that has a lower prediction error when the word 'fell' is read gain. The large prediction error encountered on the first reading of 'fell' changes the energy landscape and this facilitates the escape using the mechanism that explained in figure 8 in [Varma](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html). 

The initial mis-interpretation of 'raced' connects to [Ghio et al.'s (2023)](https://arxiv.org/abs/2308.14085) finding that diffusion-based sampling can get trapped by an emergent competing local maximum along the annealing path, and this maps directly onto "the parser gets trapped in the wrong garden-path interpretation," with P600 as the plausible neural signature of the resulting escape-and-resettle process.
"Garden-Path Model" is actually the name of a specific theory (Frazier's), proposing the parser commits serially to one analysis at a time. There's a rival, well-established account called the constraint-based/parallel tradition ([MacDonald, Pearlmutter & Seidenberg, 1994](https://psycnet.apa.org/record/1995-08264-001)) which proposes that multiple candidate parses are entertained simultaneously with graded activation, more like a genuine probability distribution than a single serial commitment. IM-LEPP's own architecture, representing a distribution over candidate states via diffusion sampling before settling, is arguably a better structural match to the constraint-based account than to Frazier's original serial model, despite sharing the "garden path" name with the phenomenon both theories are trying to explain.


### Comparison of Next Word Prediction Strategies in Transformers vs IM-LEPP

In lieu of doing experiments on the human brain, [Barenholtz (2026)](https://arxiv.org/abs/2606.05346) probed the internal dynamics of a transformer based LLM to understand how it generates language.
He introduced a quantity called trajectory extrapolation error (TEE) which is defined as follows: At each word, fit a linear trajectory to the preceding 3 hidden states of a transformer
(GPT-2/Pythia), extrapolate one step forward, and measure how far the actual next hidden state lands from that extrapolated point. His key finding is that TEE is nearly orthogonal
to surprisal (which is defined as the difference between the predicted word and the ground truth word)  with $𝑟 = .044$ and independently predicts reading times, replicating across GPT-2 sizes,
on both garden-path sentences and thousands of naturalistic word positions (Natural Stories). The displacement control is the sharpest result: raw magnitude of representational
change (i.e. surprisal) and TEE predict reading time in opposite directions — a large change that continues the established direction is facilitative, while a small change that breaks direction is costly.

Critically, the GPT2 model itself doesn’t use this trajectory structure in its own processing — direction preservation collapses to near-chance one step ahead at the intermediate layer, so each forward pass that results in the next word prediction is essentially a fresh computation, not a running extrapolation. Trajectory structure in GPT2 is a passive residual of training on human-produced text (which itself has local planning momentum), not an active computational strategy that the transformer exploits.

The core dissociation — word-level prediction error vs. representational reorientation cost — maps onto the predictive-coding energy in the IM-LEPP model

$$ E_{PC} = {1\over 2}\epsilon_y^T\Pi_y\epsilon_y + {1\over 2}\epsilon_z^T\Pi_z\epsilon_z  $$

Surprisal is the natural analogue of $\epsilon_y$ (bottom-up word-level error); TEE looks like an empirical proxy for $𝜖\epsilon_z$ (top-down: how badly did the state land where its own momentum/prior predicted it should). Barrenholtz found that these two are independent, additive, and non-interacting is a nontrivial piece of evidence for keeping $\epsilon_y$ and $\epsilon_z$ as separate energy terms in the IM-LEPP model.

The paper explicitly finds that plain autoregressive transformers don’t do what the design assumes — they don’t carry forward a persistent state with real momentum that gets used prospectively; they recompute fresh from context every step, and trajectory structure in their hidden states is an accidental byproduct of training data, not an active mechanism. 
Barrenholtz himself flags this as the open question: Is trajectory-sensitivity in humans just a passive correlate of prediction, or is comprehension “fundamentally a dynamical process in which the evolving representational state carries local trajectory continuity that is actively maintained and exploited”? His data is consistent with either. 

The IM-LEPP model is a specific, falsifiable bet on the second hypothesis — stronger than anything this paper establishes, but a natural sharpening
of the exact question the paper leaves open. If anything, the paper’s finding that an ordinary transformer’s own dynamics don’t do active momentum-tracking is a
reason to think an ordinary transformer is the wrong underlying mechanism for what the human data show.
A concrete follow-up test this suggests: replace the paper’s linear extrapolation for the latent state (deliberately
the crudest possible transition model) with an actual trained, ideally multimodal, next-$𝑧$ predictor, and check whether its residual explains reading times even
better. That would be direct evidence favoring something like a diffusion-based transition module over simple momentum model.

To summarize: The discussion of the Barrenholtz paper lays bare the fundamantal difference betweeen how LLMs and the IM-LEPP model does language generation:

- LLMs sample from the distribution $p(w_{n}|w_{\lt n})$ at each step of the generation. Thus they are able to access all the data in their prefix, as well as everything that they have generates so far, which may run into hundreds of thousands of words for the latest transformer models.
- The IM-LEPP model generates its next state $zz_n$ by sampling using an energy funciion $E_W$, it does not maintain all the previously data in its memory but instead summarizes its 'gist' in the form of the latent state.

It is quite likely that the brain operates like the IM-LEPP, we don't keep the entirety of what we have read or heard while deciding what word to generate next. This also is a reflection of the difference between RNNs and transformers, since RNNs are a more primitive version of the IM-LEPP model (without the diffusion based prediction step, RNNs have a simpler linear model for doing so). The full attention mechanism in transformers gives every past state a direct, undiluted, distance independent access, but it does come with some drawbacks: [Liu et. al.](https://arxiv.org/abs/2307.03172) "Lost in the Middle' result shows that large context models don't use context evenly, they have U-shaped retrieval curve which is worse for information buried mid-context. In addition the self attention costs in transformers grows quadratically with context length.
Strictly speaking the brain uses another source of information which we haven't put into the IM-LEPP model yet, and this memory. It is thought that some of the prior experiences that the berain has undergone gets stored as a sequence of latent states in the hippocampus, and gets recalled when the brain's language module is deciding on what word to generate next. The specific sequence of states that is recalled depends on the IM-LEPPs current state $zzz_n$ and is done using an associative memory mechanism such as the modern Hopfield network, this topic is further discussed in the next section.
It should be added here that the full attention

## Inclusion of Memory

There are several places in the paper where we pointed out the need for a memory sub-system for the IM-LEPP model which differs from the full attention mechanism used in transformers.
The need for a memory sub-system is also motivated by [Lewis and Vashisth's](https://tallinzen.net/media/readings/lewis_vasishth_2005.pdf) activation and cue based retrieval model explains long distance dependency resolution in the brain not via continuous attention over everything, but via content addressable retrieval from a declarative memory, cued by partial feature matches. modulated by decay and similarity based interference. Memory based designs have also been proposed to make transformers more efficient, for example see [Borgeaud et.al.](https://arxiv.org/abs/2112.04426)).

There are two kinds of memory sub-systems that have been alluded to in this paper:

- Object Model semantic memory: The level 2 vision hub interfaces with predictive processing modules that are instantiated on a per-object basis, depending on the objects that are present in our field of vision, and which we are consciously tracking. Clearly it is not efficient to build up the predictive model for each object (involving the parameters for the energy models $q_{\phi}, g_{\psi}$ and $E_W$) from scratch every time the object appears, and hence points to a system in which the brain stores away object models for later use, perhaps in the brain's cortical columns. These models are recalled and put into the level 2 vision hub when the time arises, and as a result their parameters evolve while they are active, and once they are no longer needed, they are once again stored away with the modified parameters. Hence, as has been pointed out by others, recalling a memory is an active process, in which the contents of the memory changes as a result of the recall.
This memory is probably organized in an hierarchical fashion, for example there could be model for the generic category of dogs, while under it there could be specific models for various breeds of gods, and at a lower level, a model for my pet dog.
- Episodic Memory: Each stored element in this system consists of a sequence of latent states $zzz_1,...,zzz_N$ sampled from the central ATL hub. Sampling states from the ATL ensures that these states are multimodal, so that they can be turned into a sequence of images or they can be turned into sound, language or other modalities.
[Tulving](https://alicekim.ca/12.EpSem72.pdf) in a classic work from 1972 proposed that episodic memory is inherently events extended in time. There is a fair amount of evidence that the seat for episodic memory in the brain lies in the hippocampus. There is direct physiological evidence that hippocampal place cells replay compressed, ordered sequences (see [Wilson and MacNoughton (1994)](https://www.weizmann.ac.il/brain-sciences/labs/ulanovsky/sites/neurobiology.labs.ulanovsky/files/uploads/wilson_mcnaughton_reactivationofhippocampalensembleactivity_science_1994.pdf)).

[Vargha-Khadem, Gadian, Watkins, Connelly, Van Paesschen & Mishkin’s (1997)](https://pubmed.ncbi.nlm.nih.gov/9219696/) classic study of developmental amnesia in which they studied children with early, selective bilateral hippocampal damage, found severely impaired episodic memory alongside broadly age-appropriate semantic/factual knowledge acquisition throughout development. This shows a genuine double dissociation, supporting the need for both object level semantic storage as well as as episodic memory.

There are several questions that needs to be answered in the design of a memory sub-system:

- What is the nature of the memory to be used? In all likelihood an associative memory of the modern Hopfield network type is an appropriate choice.
- What is the storage criteria? Obviously not all episodes that we come across with need be stored, nor do we need to store models for objects that we almost will never comes across a second time, such as strangers on the street. Some possible storage criteria ideas include: Store episodes whose state prediction $x_n$ differs a lot from the state $z_n$ that results from new ground truth data.
This corresponds to a state of surprise in human terms, and should result in the storage of $z_n$ and the subsequent states in to episodic memory. This criteria applies equally well to vision or to language data. In the case of language it results in the storage of thoughts that are of significance. The length of the sequence to be stored is governed by when the next surprise state occurs, at which point it is terminated. This is reminiscent of the design used for splitting up a sequence of characters into words in the language model, in this case we are splitting up a sequence of words into thoughts, with the caveat that not all thoughts are stored, only those whose surprise value exceeds some threshold. This matches a real biological mechanism that was proposed by [Lisman and Grace (2005)](https://www.cell.com/action/showPdf?pii=S0896-6273%2805%2900397-1). They proposed a hippocampal VTA loop for detection of newly arrived information not already stored, by triggering a novelty signal and dopamine release, which is like prediction error gated writing in our model.
Another storage criteria can be developed based on the valence signal coming from the amygdala. It is possible that the amygdala gets activated as a result of the surprise value alluded to earlier, and it generates the valence signal for the ATL hub that leads to the storage of the episode. In this sense the amygdala's signal will not be a separate mechanism but a way in the surprise mechanism is implemented by the system at the ATL hub.
- Since it is an associative memory, what are query and key values to be used? What are the rules to be used for memory decay and over writing?
- How many episodes or objects can be active simultaneously at any one time? Empirical data from human tests shows that the capacity id about 3-4 chunks (see [Cowan (2001)](https://www.cambridge.org/core/services/aop-cambridge-core/content/view/44023F1147D4A1D44BDC0AD226838496/S0140525X01003922a.pdf/div-class-title-the-magical-number-4-in-short-term-memory-a-reconsideration-of-mental-storage-capacity-div.pdf))
- What is the mechanism for feeding episodic memory states into the system? The most natural point of entry is the central ATL hub. The ATL itself is connected to the hippocampus through a rich set of connections. A study using intracranial recordings during a word-list learning task found that hippocampal sharp-wave ripples coordinate with cortical ripples specifically in the ATL-centered semantic network during both encoding and recall. Since sharp-wave ripples are the neural signature of hippocampal replay (see Wilson & McNaughton, 1994), this shows that exact replay machinery interacting, in a temporally precise way, with the ATL hub specifically during real memory formation and retrieval. Hippocampal replay is time compressed at a speed that is 10-20x faster than originally recorded. Thus an entire memory episode can be replayed in the time between successive state updates at the word level.

![](https://subirvarma.github.io/GeneralCognitics/images/stat170.png) 

Figure 13: Incorporation of Episodic Memory into the IM-LEPP system

The above figure shows a proposed design for incorporation of episodic memory into the IM-LEPP model.
It shows connections between the predictive processing modules and the amygdala, for both vision and language. When prediction module in any of these pipelines notices a large gap between the prediction $x_n$ and the sensory data mediated next state $z_n$, then it sends a signal to the amygdala. Subsequently the amygdala communicates with the ATL hub, which initiates the process of storing the hub state $zzz_n$ into the memory. The hub states continue to be stored until the reception of the next signal from the amygdala.
We are working on the details of this model, and will be documented in an upcoming paper.



## Existing Work



## Conclusions



