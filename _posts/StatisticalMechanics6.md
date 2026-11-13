---
layout: default
title: " # An Energy based Model for Language and Thinking"
---

# An Energy based Model for Language and Thinking

## Introduction

Large language models are remarkably capable, yet their design departs from the brain in ways that account for several of their limitations. They spend a fixed amount of computation on every token regardless of difficulty. They carry their past in a context window whose cost grows quadratically with length, and retrieval from very long contexts is unreliable. They pass little of their internal state from one token to the next, since most of the final latent state is discarded once a token is emitted. And they cannot lay down new long-term memories during use (Summerfield and Stachenfeld, 2026). The brain, in contrast, maintains a recurrent latent state, stores experience as discrete episodes that are recalled selectively, and spends more effort on hard problems than on easy ones. This paper proposes an architecture, called IM-LEPP2, that builds these properties into a language and cognition model.

This is the third in a series of papers on models of cognition based on the energy minimization principle. The first, *Generative AI as an Effective Theory of Cognition*, proposed the Latent Energy-based Predictive Processing (LEPP) model, in which sensory signals are translated into latent representations by a predictive coding pipeline, and the latents evolve in time through a prediction module that minimizes an energy function. LEPP models a neo-cortical column. Columns connected to sensory modules predict what we see and hear, and these predictions become our perceptions. Columns can also be stacked, so that higher levels predict the latents of lower ones, giving a hierarchy of predictions that underlies thinking. The second paper, *A Hierarchical Energy-Based Model for Multimodal Cognition*, introduced the Integrated Multimodal LEPP (IM-LEPP). It adds a central hub, modeled on the anterior temporal lobe (ATL), that integrates signals from vision, language and memory into an amodal latent state, which is fed back to the prediction modules of each modality.

IM-LEPP2 extends this model in three ways. In the second paper, memory was a source of conditioning information whose organization was left open. Here it is a worked-out component, the energy function used by the prediction modules was only sketched, and the language hierarchy was described at a high level. The contributions of this paper are:

1. **A model of working and episodic memory** based on Baddeley's working memory framework and Event Segmentation Theory (EST; Zacks et al., 2007). The stream of working-memory states is segmented into episodes when prediction error is high, episodes are stored in a hippocampus-like store, and they are recalled by associative (kNN) match under the control of an executive controller. We use these theories as inspiration rather than implementing them in full.
2. **An explicit model of the energy function and its inference.** Prediction is performed by gradient descent on a learned energy function $E_W$, with a variable number of steps determined by a halting rule, and we describe its training.
3. **A temporal hierarchy for language**, in which a character or phoneme pipeline feeds a word-level pipeline, whose predictions in turn condition the lower level, together with an interface from the word level to episodic memory through the ATL hub.
4. **A mapping to the Transformer and its recent variants.** We show where IM-LEPP2 and Transformers share the same two operations, non-parametric memory access followed by parametric prediction, and where they differ.

IM-LEPP2 combines elements that appear separately in the literature. Like a recurrent network, it carries a latent state forward in time. Like a Transformer, it has access to its history through a non-parametric store, but it reads from selected episodes rather than the entire past, in the spirit of recent episodic-memory language models (Fountas et al., 2025) and retrieval-augmented generation. Its prediction module is an explicit energy minimizer, related to Energy-Based Transformers (Gladstone et al., 2025) and iterative energy-based reasoning (Du et al., 2022), while its recurrent reasoning in latent space relates to HRM, TRM, Geiping et al. (2025) and GRAM (Baek et al., 2026). What distinguishes IM-LEPP2 is the combination: a recurrent latent state, a surprisal-segmented episodic store, an explicit energy function with variable-step inference, and multimodal grounding through a central hub.

The correspondence with Transformers is close enough to be instructive. A Transformer block uses multi-head self-attention (MHSA) to read from its history and a feed-forward network (FFN) that acts as a key-value parametric memory (Geva et al., 2021). In IM-LEPP2 the cross-attention over working or recalled memory plays the role of MHSA, and the minimization of $E_W$ plays the role of the FFN, with each gradient step roughly corresponding to one Transformer block. Several results show that Transformer blocks can implement gradient descent steps on an implicit energy in in-context regression settings (von Oswald et al., 2023; Yang et al., 2023). IM-LEPP2 makes this energy explicit, so that the number of steps can adapt to the difficulty of the prediction and the energy value itself can signal how close the prediction is to a minimum.

Finally, we note the status of this work. This paper presents the architecture and algorithms of IM-LEPP2. [Empirical evaluation is left for future work.] The design makes several testable predictions: (a) accuracy on tasks that require variable amounts of reasoning should improve as the number of inference steps grows, (b) the converged energy should correlate with prediction correctness, and (c) surprisal-based episode boundaries should support better recall than fixed-length chunking. Consolidation of episodes from the hippocampal store into the cortical parameters is also outside the scope of this paper.

The rest of this paper is organized as follows. Section 2 summarizes what is known about the organization of memory in the brain. Section 3 describes the IM-LEPP2 model, its modules, and their interactions. Section 4 compares IM-LEPP2 with Transformers, and with Looped, Universal and Full-Bandwidth Transformers, along three axes: memory mechanisms, latent state definitions, and prediction techniques. Section 5 relates it to recent recurrent language models, and Section 6 to reasoning models. Section 7 gives the algorithms for episodic memory access, the design and training of the energy function, and halting.

*Terminology.* Working memory denotes the multimodal contents of the ATL hub at the current moment. Episodic memory (long-term memory in Baddeley's framework) denotes the store of past episodes, where an episode is a segmented sequence of working-memory states.


## Organization of Memory in the Brain

Memory is integral to cognitive functions in the brain, and in this section we will survey a framework that has been proposed on how it is organized, both functionally as well as biologically in the various parts in the brain. 
The description is based on the book [Memory](https://dn760107.eu.archive.org/0/items/MemoryUltimate/Mnemonics/Alan%20Baddeley%20-%20Memory%20(2017).pdf) by Baddeley, Eysenck and Anderson. 
In the following sections we will connect this framework with the way memory is implemented memory in IM-LEPP2 and Transformer based LLMs.

Human memory can be classified into the following types:

- **Short Term Memory or STM:** This involves simple retention of small amounts of information, tested either immediately or after a short delay. When tested using a sequence of digits, it has been shown that STM capacity is limited to about 6 to 7 digits in most people. Later it was suggested that memory capacity is limited not by the number of items to be recalled, but the number of chunks, where a chunk is defined as a sub-sequence within the larger digit sequence.

  Verbal STM has been modeled using the concept of a phonological loop, which has two sub-components: a short term store and an articulatory rehearsal process. The store is assumed to be limited in capacity and decays within a few seconds, however sound traces can be refreshed by sub-vocal rehearsal (saying the items to yourself). The 6 or 7 limit in STM arises due to the fact that we can say a few digits in sequence before the first digit fades away. Thus this theory posits that STM is based solely on sound, and not on the meaning of the objects being memorized. Long Term Memory or LTM on the other hand is based on semantic content or meaning of the objects being memorized. STM for visual items can also utilize the phonological loop as long as they are nameable.

  STM also exists for visual objects, and has two components, one concerned with spatial memory (where?) and the other concerned with memory for the objects themselves (what?). Spatial location memory shows forgetting over a period of seconds, while object memory is highly accurate to about 4 items, and does not decline. However if we try to remember more than 4 objects, then performance does begin to decline.
Experiments done on patients with brain related impairments have shown that STM and LTM are supported by different regions of the brain, since there have been people in whom one type of memory is impaired while leaving the other type intact.

![](https://subirvarma.github.io/GeneralCognitics/images/stat206.png) 

Figure 1: The Baddeley Working Memory Framework
 
- **Working Memory or WM:** The working memory system not only temporarily stores information, but is also able to manipulate it, thus allowing people to perform complex cognitive functions such as reasoning, learning and comprehension. An example in which working memory would be utilized is when we are adding two multi-digit numbers. This requires us to hold the results of addition of the earlier digits in phonological STM while continuing to add the subsequent digits, with the numbers themselves occupying short term visual memory.

  In order to explain WM, Baddeley proposed the framework shown in figure 1. It has several components, starting with the **phonological loop** that holds sequences of acoustic or speech based patterns and is the same as the verbal STM. The **visuo-spatial sketchpad**  performs a similar function for for visually and/or spatially encoded items and arrays. 
  The whole system is controlled by a **Central Executive**, whose job is to focus attention on a limited number of items or tasks at any one time and serves as a controller for the whole system. In the addition example for instance, the two numbers to be added would be in visual-spatial sketchpad, while the results of the addition would end up in the phonological loop, while the Central Executive decides which two digits to focus on and also does the actual addition.
  
  Under the control of the Central Executive, we are able to mentally manipulate objects that are in the visuo-spatial sketchpad, for example mentally rotate an object. As in the addition example, the phonological loop and the visuo-spatial sketchpad often work together to enhance performance. Since the Central Executive can only focus on a few items at a time, sometimes the information coming through the senses can interfere with the information in the phonological loop and the visuo-spatial sketchpad and vice-versa.
  
  Baddeley also added Long Term Memory or LTM to the WM framework (we will also refer to it as Episodic Memory in this paper). The LTM was added to take into account the fact that sometimes our attention is focussed on objects or sounds that are not located in the phonological loop or the visuo-spatial sketchpad, and hence must have been retrieved from LTM. In order to interface the LTM with the Central Executive, he introduced the  the **Episodic Buffer** or EB, which he assumed is a storage system that can hold about four to six chunks of information in amodal code. As a result of the multi-modality, he hypothesized that the EB also holds information from the phonological loop and the visuo-spatial sketchpad, and thus acts as a link between the various sub-systems as shown in figure 1. According to the model, information is retrieved from the episodic buffer through conscious awareness, thus linking the working memory model with [Baar's theory of consciousness](https://ccrg.cs.memphis.edu/assets/papers/1988/Baars-A%20Cognitive%20Theory%20of%20Consciousness.pdf) (a shorter description can be found [here](https://tilde.ini.uzh.ch/~kiper/Baars_1.pdf)). Thus working memory in the Baddeley framework is identical to the Global Workspace proposed by Baar as a model for consciousness since in both cases conscious awareness serves the function of pulling together separate streams of information from various senses (and memory) and binding them into perceived objects and scenes.
Recent evidence suggests that the Episodic Buffer functions as "display" system for infomation coming in from the various sources, however active manipulation of the objects in the Episodic Buffer is done elsewhere, in the blocks labeled as semantics in figure 1.

  The amodal contents of the EB gets periodically gets aggregated into larger chunks or episodes and stored into the LTM, and these constitute our memory. The process of chunking has been clarified in recent years and is described below. During the process of memory recall, one or more episodes from the LTM are chosen and these are fed into the audio-visual generation systems and then to the visuo-spatial sketchpad (and the phonological loop) to generate our 'inner eye', i.e., our ability to imagine events and sounds from our past. Note that the process of recall is under the control of the Central Executive, so that we are not constantly reminiscing about the past. Ultimately the recalled memory makes its way into the EB, so that at any one time, the EB has information about what is happening currently in real time, as well as a few representations for information that has been recalled from the LTM.
 
- **Episodic Memory:** The concept of episodic memory was introduced by [Endel Tulving](https://turing.iimas.unam.mx/~luis/cursos/MARE2025-2/lecturas/Tulving.pdf) in 1972 to emphasize the difference between the recollection of specific events stamped by time and location, vs semantic memory which is generalized knowledge of the world. Episodic memory enables "mental time travel", allowing us to relive past episodes as well "travel forward" and anticipate future events. It is thought that episodic memory is accumulated and consolidated to form the basis for semantic memory, so that disruption to the episodic memory system also leads to inability to form semantic memory. Episodic memory is also called fast memory since it requires just a single episode to store information, while semantic memory storage happens over a longer time scale. Encoding and retrieval of episodic memory is easier if the material is meaningful and well organized, i.e., episodic memory is encoded at a higher semantic level compared to sound or vision traces that we encountered for STM. When trying to store a word in episodic memory, it helps if there is an image associated with the word, so that the word can be recalled both visually and verbally.

  There is a special category of episodic memory called autobiographical memory, and this refers to memories that we hold regarding ourselves and our relations to the world around us. Some aspects of autobiographical memory are semantic in nature, such as facts about ourselves (our phone number for example). Autobiographical memory has been investigated using diary studies, and it has been found that the recall level decreases as time passes, but this also depends on the nature of recall cues provided, with who, what and where cues providing better recall then when cues. Also in general more frequent recall helps to retain the item in memory. Within this category, the concept of flashbulb memory has been proposed to capture the case when some event is recalled with almost photographic detail provided extreme emotion coincided with its actual occurrence.

- **Semantic Memory:** This is defined as general knowledge of the world and is not tied down to a specific time or place. The pre-frontal cortex or PFC has been shown to be involved in semantic memory, while episodic memory is associated with the hippocampus. Semantic memory is organized in the brain on the basis of semantic relatedness or semantic distance, i.e., how closely related pairs of words are. In machine learning terms, this implies that the brain stores latent representations.
  
  The different properties of an object are stored in different areas in the brain. For example when we recall a seagull for example, the visual area gets activated with an image of the bird while the sound areas are activated with its call.
Semantic memory for objects that can be visualized is stored differently and in a different part of the neo-cortex  according to the sensory-functional theory. This says that information about objects in semantic memory is organized in terms of distinction between sensory properties (visual, auditory, taste, tactile) and functional properties or non-perceptual properties (what an object does or what is used for). Using a process which has not been explained yet by traditional neuroscience, the brain manages to integrate all the different types of information associated with an object rapidly and automatically when we think about any given concept (with the IM-LEPP2 model we present a theory for how this can be done).

  In addition to object level information, semantic memory is also thought to store knowledge of schemas and one such type of sechema is called a script. For example the sequence of events that happens when we go out to eat at a restaurant (entering, giving reservation name, ordering drinks, discussing the menu etc) form a schema. Schemas help us in forming expectation, and if they are violated then we take action.

  Patients suffering from semantic dementia have severe problems accessing the meaning of words but often retain access to script knowledge, which implies that semantic and script information is stored in different parts of the brain, with the former being associated with the anterior temporal region of the brain and the latter with the prefrontal cortex.

- **Memory Recall:** Memories are recalled by means of cues or queries. In the case of episodic memory, these can be in the form of time or place for the event, as well as various retrieval cues that were associated with the event at the time of occurrence (also called keys in machine learning terms). Sometimes the memory is present but we are not able to access it due to lack of appropriate cues to activate it. In general, the more cues associated with a memory, the easier it is to recall it. Any aspect of of the content of memory can serve as a reminder that could access the experience, this is known as content addressability. The power of a cue depends upon the attention given to it during the retrieval process.

  Memories have activation levels, which determines how accessible an episode is in memory.  An episode's activation level increases when we perceive something associated with it, or when we think of it directly. The activation persists for some time even after the attention has been removed. If there are multiple cues present, then the activation levels for particular episodes additively increases in proportion to the individual cues. For a cue to be useful, it needs to be present at the encoding, and encoded with the desired episode. Memories with higher activation are easier to recall.

  We are not constantly bombarded by memories, we have to be in the right frame of mind to recollect the past and this is mediated by the Executive Controller. We are aware of episodic memories while they are being recalled. However there is also the case that memories can influence us without an associated recall, so that we are unaware of the connection, this is called implicit memory. In terms of the framework in figure 1, this implies a direct connection between the LTM module and the EB, thus bypassing the sensory pipelines all together.

- **Segmentation of Event Sequences into Episodes** Even though the information coming in through the senses happens in a continuous stream, our memory is organized in the form of distinct episodes which are chunks of subjective experience that have a beginning and an end. The brain uses the episode that is currently happening as the principal context while events from the recent past are rapidly forgotten which unburdens the mind  from potentially obsolete working memory representations. Context shifts from an episode to the next can be caused by changes in narrative (while reading or listening), spatial (usually caused due to motion, for example when we step into a new room) or other perceptual shifts. If there are items that appear on both sides of an episode boundary, their sequential binding is reduced, thus leading to the phenomenon of people forgetting what they came for when they step into a new room.

  [Zacks et.al, 2007](https://bpb-us-e2.wpmucdn.com/sites.wustl.edu/dist/e/952/files/2017/09/zackspsychbull07-sbm4za.pdf) proposed a theory for segmentation which they called Event Segmentation Theory or EST (episodes are called events in their paper). It states that episode boundaries are created when the sensory pipelines prediction differs significantly from the ground truth evidence coming the sensory inputs. They also proposed the idea of an **Event Model** whose output is used to guide the prediction module at the sensory level. This output stays constant during a single episode, thus guiding all the sensory predictions with a stable baseline. The change in the event model output at the episode boundary clears the old context, thus leading to the effect that was mentioned earlier of abrupt change in our cognition when moving to a new room. They also proposed that the predictions of the event model are governed by a still higher level predictive model
which they called a **event schemata** in their paper. Event schemata contain previously learned information about the sequential structure of the event model.
At the times when the sensory level predictions differ significantly from the input data, a new episode is initiated and at the same time the event model gets updated.
In general there can be several levels in this hierarchy, with the output of the event schemata controlled by its own model operating at higher level, which in turn gets updated with the information coming in through the event sequence. The latent sequence at all these levels can be segmented into episodes with the segmentation becomes progressively finer as we proceed from higher levels to lower levels.
Zacks et.al. also proposed that the perceptual information from event boundaries is preferentially accessible in LTM, thus making them an attractive target for the associative recall process.

### Episodic Memory in the Hippocampus 

**How the brain stores episodes.** The hippocampus is the main site of fast, one-shot learning in the brain: a single experience is enough to lay down a trace. A long-standing account, the hippocampal indexing theory (Teyler and DiScenna, 1986), holds that the hippocampus does not store the content of an experience itself. It stores an index, a pattern that binds together the distributed neocortical patterns that represent the content (the sights, sounds and meanings), so that reactivating part of the index can reactivate the rest. Summerfield and Stachenfeld (2026) express the same idea in machine-learning terms: the hippocampus holds the keys and the neocortex the values of an associative memory. Retrieval is content-addressable. A partial cue reinstates the full episode by pattern completion, and the more cues that match, the more likely recall succeeds. To keep similar episodes from interfering, the input to the hippocampus is thought to be sparsified, a process known as pattern separation [verify: Yassa and Stark, 2011].

The hippocampus does not work alone, and it does not learn structure from scratch each time. The entorhinal cortex supplies grid-like codes that act as a positional scaffold for memories, and the Tolman-Eichenbaum machine (Whittington et al., 2020) shows how such a structural code can be learned separately from sensory content and then bound to it, so that the same structure generalizes across new situations. Broader schematic knowledge, the learned regularities of how events usually unfold, is held in neocortex (Zacks et al., 2007, call these event schemata and place them in semantic memory, implemented by permanent synaptic changes). Prior schemas speed up the learning of consistent new information [verify: Tse et al., 2007; van Kesteren et al., 2012]. Over time, and especially during sleep, episodes are replayed and gradually consolidated into the neocortex, with replay prioritizing memories that are novel, salient or weakly encoded (Summerfield and Stachenfeld, 2026). Finally, the hippocampus attaches a time and place stamp to each episode, which allows recall to be cued by when and where an event happened (Tulving, 1972).

## The IM-LEPP2 Model

The IM-LEPP2 model adopts Baddeley's memory framework described in the previous section, with its division into working memory, episodic memory and semantic memory, as well as the event segmentation theory due to Zack et.al. It has several sub-components: (1) A module for visual processing, (2) A module for language processing (3) A module for integration of visual/sensory and language signals in the central ATL hub, (4) A  module for episodic memory, (5) A module for higher level cognitive processing, at the episode and higher levels (6) The Executive Controller module. Broadly speaking, the model's functions are divided among the following areas:

- Modules that implement the predictive processing algorithm, involving the inference, prediction and generation functions: In the brain these are thought to reside in the neo-cortical columns of the cortex. These modules have the responsibility of building predictive models for their inputs, which can be sensory data, as for the case of vision, hearing, smell, taste, touch etc. But they can also be arranged in an hierarchical fashion, so that higher levels in the hierarchy models the outputs of the levels below them. We saw one example of this in [paper 2](https://subirvarma.github.io/GeneralCognitics/2026/08/07/statmech5.html) where language was modeled as a word level predictive processing pipeline operating on top of a phoneme level pevel predictive processing pipeline. This idea is extended in this paper to model predictions at even higher levels, resulting in models at the schema level which have been hypothesized by cognitive scientists. The parameters in the predictive processing pipelines serve as the equivalent of semantic memory in Baddeley's framework.
- Modules that implement multi-sensory integration functions: In the brain these functions are thought to reside in the temporal regions. They receive inputs from multiple sensory and language pipelines and integrate them, resulting in amodal representations that is the counterpart of the working memory in Baddeley's model. This representation is fed back into the sensory and language modules to serve as an influence on their predictions, as well as periodically aggregated into episodes and stored into episodic memory. These episodes are periodically recalled and stored resulting in the equivalent of Baddeley's episodic buffers.
- Episodic Memory sub-system: Episodic memory constitutes the non-parametric part of the brain's memory architecture, and is capable of quickly storing sequences of working memory representations even after a single exposure to them. In the brain  episodic memory is thought to be implemented using a combination of the hippocampus and the cortex, with the hippocampus storing the keys to episodic sequences and the cortex storing the actual content.

![](https://subirvarma.github.io/GeneralCognitics/images/stat212.png) 

Figure 2: The IM-LEPP2 Model
 
The IM-LEPP2 model as shown in figure 2, functions as follows:

- There is a central ATL type hub at level 1 that integrates signal coming in from the vision and language hubs into an amodal working memory representation (these are the two connections labeled 1) in the figure). These two connections are is bi-directional, so that not only do the spoke hubs influence the representation in the central hub, but they in turn are influenced by the information coming from the central hub. The reverse connection enables the language hub state to be influenced by the vision hub state (and vice versa).
- The representation in the central hub gets split into episodes, which are sequences of amodal latent representations, using surprisal information from the prediction modules in the vision and language hubs. These episodes are stored in episodic memory using the connection labeled 4) in the figure.
- The episode or schema level module receives input from the central hub (through the connection marked 2)), and is responsible for building predictive processing pipelines that operate at the episode or higher levels, and thus represents the part of vision or language evolution that stays stable during the course of a single episode. The output of this module serves as an additional conditioning variable that influences the prediction modules in the vision and language hubs (through the two connections marked 3)).
- Memory recall from episodic memory is cued by the state of the central hub, using a kNN type retrieval, and results in the transfer of one or more episodes from episodic memory into the vision module using the connection labeled 5), where they get transformed into visual representations. These representations are then routed to the central hub where they occupy one of the episodic buffers. There are upto six episodic buffers in the central hub, one of which contains the current unfinished episode, while the others contain episodes recalled from memory. The language module uses the contents of one or more of these episodic buffers to condition its next word prediction module.
- The executive controller provides overall supervision of the system. Among other tasks it decides where to focus attention at any one time, for example it can focus attention on an object in the visual field, or on the generation of the next word, or on sequences recalled from episodic memory. It has other functions that have to do with planning etc that are not modeled here.

More detailed descriptions of the various modules follow.+

### The Language Module

![](https://subirvarma.github.io/GeneralCognitics/images/stat213.png) 

Figure 4: Predictive Processing Pipeline for Next Character Prediction

The IM-LEPP2 language model consists of a lower level phoneme or character level model and a higher word level model. In the following we first describe the predictive processing pipeline for characters, followed by that for words.

The discrete character sequence is sent into a predictive processing pipeline shown in the above figure, that creates an latent representation $z_n$ for each character using the predictive coding function $q_{\phi}$, followed by prediction of the next latent representation $x_{n+1}$ using a energy based model $E_{CH}(x;z_n,u_{n+1}=yy_m)$. 
Note that this prediction is conditioned on not just the previous character level latent $z_n$, but also on a latent representation $yy_m$ for the $m^{th}$ word (whose characters are being generated), which comes from the level 2 word pipeline. The computation of $yy_m$ is explained below when we discuss the word level pipeline.
Next $x_{n+1}$ is converted into a character using the predictive coding function $g_{\psi}$. The generated character $y_{n+1}=g_{\psi}(x_{n+1})$ is compared with the actual next character $ch_{n+1}$, and the error generated by this information is used to estimate the next representation $z_{n+1}$. These operations are illustrated in the above figure.

The system is able to detect the end of a word by tracking the difference between the predicted  latent state $x_{n+1}$ and the actual latent state $z_{n+1}$. 
If this difference exceeds some threshold, then the model assumes that the previous character $ch_n$ occurred at the end of a word (saw the $m^{th}$ word $w_m$), and the representation $z_n$ is sent over to the word level pipeline as discussed next. 

![](https://subirvarma.github.io/GeneralCognitics/images/stat214.png) 

Figure 5: Predictive Processing Pipeline for Next Word Prediction

The predictive coding pipeline at the word level uses the latent state $z_n$ from the character pipeline as the ground truth that represents the latent representation for for the $m^{th}$ word. Note that the word level subscript $m$ for the current word  is not the same as the character level subscript $n$ for obvious reasons.
This pipeline creates a higher level latent word representation $zz_m$ by modifying the existing representation $xx_m$ to $zz_m = q_{\phi}(xx_m,z_n)$.
$zz_m$ is then sent to the level 1 central ATL hub where it gets modified by the vision data to the latent $zzz_m$. For example if the current image is that of an apple, then this is reflected in $zzz_m$. 

The next word latent prediction done at the word level can be influenced by the following factors (which act as conditioning variables used during prediction): 

1. The current state $zz_m$ of the word pipeline: This captures the recurrent thought state.
2. The current state $zzz_t$ of the central hub: This takes vision and other modalities into account and is short term in nature, corresponding to the working memory in Baddeley's model..
3. The contents $zzz_t,...,zzz_{t+q}$ of one or more of the episodic buffers from the central hub: The episodic memory information coming to the language module is mediated through the vision pipeline as described above, and this corresponds to conscious memory recall. The prediction module focuses its attention of specific parts of this sequence when computing the energy function value.
Access to the episode sequence allows the prediction module in the word pipeline to focus on parts of the sequence that are relevant to next word prediction.
There can also be non-conscious memory recall which can be modeled by routing the content of the episodic memory directly to the language module. 
4. The output $yy^{EV}_p$ of the event level predictive processing pipeline: This variable captures long term regularities in the currently ongoing episode, as captured by the episode level pipeline.

The Executive Controller decides whether the current state, the current episode or one of the recalled episodes, or a combination of these, should be used as context in the language module. In the case of memory recall, the model assumes that the executive controller is able to pause the generation of the next word until contents of the episodic memory are played in the vision pipeline (which happens at a faster rate compared to when the episode was recorded).

The context information is fed into 
the energy based prediction module $E_W(x;context)$ and this results in the prediction $xx_{m+1}$ for the next word latent (see above figure).
$xx_{m+1}$ is subsequently used to generate the next word latent $yy_{m+1}=g_{\psi}(xx_{m+1})$, and this value is fed back into the  level 3 character level predictive processing pipeline shown in figure 4, where it influences the prediction of the next character $x_{n+2}$ through the energy function $E_{CH}(x;z_{n+1},yy_{m+1})$. This in turn gets modified by the other characters in the next word being read. When the last character of that word is encountered, then the latent representation at that time $z_{n+k}$ (where $k$ is the number of characters in the word just read) is fed back into the word level model to correct the prediction $yy_{m+1}$, and this closes the word level prediction loop. As pointed out in the introduction, this is also an hierarchical system, but the hierarchy is in time rather than in space, as was the case for the visual system.

For the case when we are doing character generation, i.e., writing, this feedback loop between the character level and word level pipelines is still active. In this case it serves as a verification of whether the word that was generated at level 3 matches the word that the level 2 word level system meant to generate.

The proposed system models the process of thinking or reasoning in the language module at two levels: (1) Through the multistage process by which the energy $E_W$ settles to a minimum value in the prediction module, and (2) Through multiple invocations of the prediction module, each time with a new context vector. This process happens entirely in latent space, in which the representation $zz_m$ serves as a hidden latent state that changes recursively over time in response to new sensory data and episodic memory recalls. 

This model does not look like the Transformer model at first glance, but as explained in the following sections, both are based on the following two operations:

1. Non-parametric memory access to create a context: IM-LEPP2 does this using its working memory or recalled episodes from episodic memory, while Transformers use the entirety of their past generations as memory. Using only specific episodes from memory reduces the amount of processing involved, thus avoiding the quadratic complexity in the Transformer self attention operation.
2. Predictions using parametric memory: IM-LEPP2 uses an energy based prediction module, while Transformers use a feed-forward network or FFN. The energy based prediction uses gradient optimization to minimize the energy function, and the number of gradient steps can be adjusted depending upon the difficulty of the prediction. The scalar energy also serves as an indication of how close the prediction is to the optimal value.

### The Vision Module

![](https://subirvarma.github.io/GeneralCognitics/images/stat218.png) 

Figure 4: The vision hub with the addition of a pipeline for memory recall

The vision module largely retains the structure described in the [previous paper](https://subirvarma.github.io/GeneralCognitics/2026/08/07/statmech5.html)
and is organized around a vision hub as shown in the above figure. 
The vision module has a two level structure: The central vision hub at level 2 integrates information coming from several simultaneously active level 3 predictive processing vision pipelines. There is a level 3 pipeline for each of the objects in the scene, as well an always-on pipeline for the scene itself, and all these get integrated at the level 2 vision hub. The representation of each of these pipelines evolves asynchronously in time and the level 2 hub integrates the latest information from each individual object and sends it up to the central level 1 hub.  We have added a new pipeline to handle input coming from episodic memory recall, which gets activated when the executive controller decides to focus on memory. In normal operation the executive controller focuses on one of the objects in the scene, or on the scene itself, which results in the chosen pipeline receiving sensory data.
Note that the scene level pipeline is always active, while the number of object level and memory pipelines come and go depending upon the objects currently in the field of vision.

![](https://subirvarma.github.io/GeneralCognitics/images/stat215.png) 

Figure 4: Vision Pipeline for Object and Scene Inputs

The per-object level 3 predictive processing vision pipelines operate according to the inference-prediction-generation framework that was used for the LEPP model in [paper 1](https://subirvarma.github.io/GeneralCognitics/2026/07/15/statmech4.html). The system state that results from the inference module in this pipeline is sent to the level 2 vision hub for integration with the other pipelines. This combined representation in turn gets integrated with representations from other sensory modalities and language in the multimodal level 1 hub. The integrated level 1 representation in turn is fed back to the prediction module in the level 3 pipelines, and the result is used to generate the next percept. By virtue of this architecture, these percepts take all the other objects that are in the scene into account as well as memory recall and other modalities.

We have added a new conditioning latent vector $yy^{EV}_p$, called the episodic vector, to the scene level pipeline. This represents the predictions coming from the episode level predictive processing pipeline (described below). The state of this variable remains fixed for the duration of an episode, and can be considered to be an implementation of the event level model as proposed by Zacks et.al. When the sequence of episodes follow a certain pattern (for example the sequences of things that we expect to happen when we go to a restaurant for example), then this is captured by the predictions from the episode level pipeline.

![](https://subirvarma.github.io/GeneralCognitics/images/stat216.png) 

Figure 4: Vision Pipeline for Episodic Memory Input

We have added a new pipeline to handle the output sequence $zzz_t$ coming from episodic memory recall, where it is used to condition the prediction module. The output of the prediction module is fed into the generation pipeline and this results in the phenomenon of playing back an event from our memory. Note that since there is no sensory data to compare with, there is no inference pipeline and the predicted output $x_n$ is routed directly to the level 2 vision hub and from there to the central hub, where it combines with data from other modules and then gets stored in one of the episodic buffers. This model for episodic memory recall captures the fact that the process of memory recall changes the contents of the recalled memory. 
The Executive Controller decides whether to focus attention on the memory recall pipeline, or one of the other pipelines. During memory replay, sensory data is no longer being sent to the other pipelines, which accounts for the fact that when we are reminiscing, we often loose track of what is happening in our vicinity.

### Episodic Memory

The episodic memory is a store of sequences coming from the ATL hub. and works as follows:

- The event sequence is split into episodes based on the surprisal value in the predictive processing pipelines in the vision module. The hippocampus attaches a time and place stamp to the stored sequences which is not modeled here.
- Episodes are recalled from memory by means of an kNN associative match between the current state of the ATL hub and the events in the stored episode. The recalled episode is sent to the 
vision module as described above, where it generates a visual sequence, and this gets sent to the central hub where it gets stored in one of the episodic buffers. The contents of these buffers is used to condition the generation of the next word.
- Note that once an episodic memory is recalled, its representation changes as a result of its journey through the vision and central hubs, thus accounting for the observation that memories change as a result of recall.

The executive controller is one of the new elements in the design, and has the following functions:

- The executive controller decides when to recall items from episodic memory, and these episodes are recalled one at at a time under its control.
- The executive controller is able to control the generation of the next word, by delaying the prediction module until the episodic memory information for the entire episode is available from the ATL hub.
- For the vision sub-system, the executive controller decides which object to focus on at at any one time (so that it receives sensory updates), while the model tracks up to 5-6 objects concurrently.

### Episode Level Model

![](https://subirvarma.github.io/GeneralCognitics/images/stat217.png) 

Figure 4: Episode Level Predictive Model


## Energy Minimization

![](https://subirvarma.github.io/GeneralCognitics/images/stat209.png) 

Figure 4: Energy minimization steps in the prediction module

We will adopt the methodology of directly minimizing the energy function $E_W(x;zz_m,{zzz_m}) through multiple gradient descent steps, which results in an iterative computation with a natural termination criteria. The output of this algorithm $xx_{m+1}$ is obtained by solving the optimization problem

$$ xx_{m+1} = arg\ min_{x}\ E_W(x; zz_m,{zzz_m}) $$

using a variable number of individual gradient descent steps

$$  x^t = x^{t-1} - \lambda\nabla_x E_W(x; zz_m,{zzz_m})  $$

where $\lambda$ is the step size. This iterative computation is repeated until $x^t$ is at a local minima of the energy landscape. Thus finding a local minima provides a natural mechanism to halt the iterative computation. 

**Estimating Model Parameters**

Given $$xx^N_{m+1}$$ which is the result of the gradient descent after $N$ steps, and and the corresponding ground truth value $$zz_{m+1}$, 
the parameters $W$ of the energy landscape can be learnt by solving the minimization problem (The parameter $N$ is kept fixed during training, while during inference it varies depending on the difficulty of the prediction).

$$  L_{MSE}(W) = ||xx^N_{m+1} - zz_{m+1}||^2 $$

Strictly speaking this requires a differentiation through the underlying optimization procedure (see [Finn et.al.](https://arxiv.org/abs/1703.03400)), which involves the computation of second order gradients across optimization steps. However it has been found (see [Du et.al.](https://arxiv.org/abs/2206.15448)) truncating the back-propagation to the last optimization step maintains good performance at faster training speed.

An alternative probabilistic algorithm for doing EBMs is by using several stages of noise annealing, with Langevin diffusion steps at each stage. This algorithm requires us to use a preset number of annealing stages, since the noise series has to follow a pre-defined schedule. This works well for image prediction systems, however in the case of language and reasoning models, the number of stages is a function of the level of difficulty of the problem being solved and hence cannot be set in advance. Working directly with the energy function avoids this problem since we can vary the number of stages as a function of a stopping rule. The direct energy based approach has the following additional benefits:


![](https://subirvarma.github.io/GeneralCognitics/images/stat210.png) 

Figure 5: A Model for the Energy Function

Figure 5 shows a model for computing the energy function $E(x;zz_m;{zzz_m})$. Following the encoder Transformer architecture, it consists of two stages: The first stage uses cross attention between the current state $x$ and the retrieved information, either from working memory or episodic memory (One can also have a design in which the two are concatenated together, for now we will assume that one or the other is chosen under the direction of the Executive Controller). The cross attention operation retrieves the parts of the memory that are most relevant to the state of the pipeline. It is followed by a feed forward network or FFN. I have chosen to feed $zz_m$ directly into the FFN rather than through the cross attention, with the reasoning being that cross attention is a mechanism for choosing the relevant part of a sequence while $zz_m$ is current state of the pipeline and serves as a type of short term memory.

Note 1: In the Transformer architecture the FFN follows a three layer design and plays the role of a key-value parametric memory and has a particular design with non-linearity in the middle layer, but not in the other two layers. 
It is not clear whether we should follow the same design. For example the energy function in  [Du et.al.](https://arxiv.org/abs/2206.15448) (see Table 01) uses the ReLu activation all layers. Strictly speaking the FFN is not acting as a key-value memory in IM-LEPP2, since the parametric memory is captured in the minima of the energy landscape $E_W$.

Note 2: We can presumably add a positional encoder to the recalled memory sequences. Do you have any opinion for the best way to do this? Please see [Fountas et.al](https://arxiv.org/abs/2407.09450) for a Transformer architecture which has modified to use episodic memory. They use a fixed positional embedding as in [Raffel et.al](https://arxiv.org/abs/1910.10683). In general I am wondering whether the design can learn anything from design of scaffoldings in the hippocampus (as in the TEM machine).
If you take a look at [Zacks et al](https://pmc.ncbi.nlm.nih.gov/articles/PMC2852534/) they talk about event models that provide a stable representation of the current event to guide perceptual processing and event schemata that contain previously learned information about sequential structure of activity. I am assuming these have o do with how information is organized in the hippocampus, with positional embeddings being one way to do this. I haven't read the TEM paper in detail, but does it show a way in which these structures can be learnt from data? If so how can we incorporate the ideas from there into IM-LEPP2?

## Episodic Memory in the Hippocampus and in IM-LEPP2

**How the brain stores episodes.** The hippocampus is the main site of fast, one-shot learning in the brain: a single experience is enough to lay down a trace. A long-standing account, the hippocampal indexing theory (Teyler and DiScenna, 1986), holds that the hippocampus does not store the content of an experience itself. It stores an index, a pattern that binds together the distributed neocortical patterns that represent the content (the sights, sounds and meanings), so that reactivating part of the index can reactivate the rest. Summerfield and Stachenfeld (2026) express the same idea in machine-learning terms: the hippocampus holds the keys and the neocortex the values of an associative memory. Retrieval is content-addressable. A partial cue reinstates the full episode by pattern completion, and the more cues that match, the more likely recall succeeds. To keep similar episodes from interfering, the input to the hippocampus is thought to be sparsified, a process known as pattern separation [verify: Yassa and Stark, 2011].

The hippocampus does not work alone, and it does not learn structure from scratch each time. The entorhinal cortex supplies grid-like codes that act as a positional scaffold for memories, and the Tolman-Eichenbaum machine (Whittington et al., 2020) shows how such a structural code can be learned separately from sensory content and then bound to it, so that the same structure generalizes across new situations. Broader schematic knowledge, the learned regularities of how events usually unfold, is held in neocortex (Zacks et al., 2007, call these event schemata and place them in semantic memory, implemented by permanent synaptic changes). Prior schemas speed up the learning of consistent new information [verify: Tse et al., 2007; van Kesteren et al., 2012]. Over time, and especially during sleep, episodes are replayed and gradually consolidated into the neocortex, with replay prioritizing memories that are novel, salient or weakly encoded (Summerfield and Stachenfeld, 2026). Finally, the hippocampus attaches a time and place stamp to each episode, which allows recall to be cued by when and where an event happened (Tulving, 1972).

**Correspondence with IM-LEPP2.** Table 1 summarizes how these elements map onto the model. The episodic store is a non-parametric memory of segmented sequences. Each episode is the sequence of ATL states $zzz_t$ between two event boundaries, where boundaries are detected by surprisal in the pipelines, following Event Segmentation Theory (Zacks et al., 2007). Writing to the store requires no gradient step, which models one-shot learning.

Each episode is stored with one or more keys. The key is derived from the event-level states of the pipelines above the word level, which are updated at the boundary and so summarize the event. When there are several event levels, each level contributes a key, so that an episode can be retrieved by a coarse cue (the gist) or a fine one. The keys are learned by training the key encoder on partial episodes, so that a mid-episode state, which is what the query will be at recall time, falls near the key of the complete episode. Retrieval is by nearest-neighbor match, which implements pattern completion from a partial cue.

The structural scaffold has no counterpart in the model beyond a positional code applied within each episode. We use relative (rotary) position encodings as a stand-in, and leave learned recurrent position codes of the TEM type as an extension. Schemas correspond to the learned parameters of the prediction modules, in particular the energy function at the event level, which learns the typical sequence of events. They are not stored in the episodic memory. The hippocampal store thus holds specific episodes and their keys, while structural and schematic knowledge resides in the weights.

Recall follows the two routes described in Section 3. The stored sequence either conditions the energy function directly (an implicit route, with no regeneration), or is replayed through the sensory pipelines and integrated in the ATL before being used (an explicit route). The regenerated sequence may differ from the stored one, which reproduces the reconstructive character of human recall. To avoid drift, a modified recall is stored as a copy, not written over the original.

Consolidation is modeled as offline training of the energy function and the pipelines on replayed episodes. The target at each position is the next stored element, with that element and everything after it hidden from the model's conditioning, and the replayed episode excluded from retrieval. Otherwise the model could simply copy the target from memory and nothing would be learned in the weights. Episodes are replayed in priority order of surprisal, interleaved with older material to limit interference.

**Simplifications.** We do not model the time and place stamp, so recall is cued only by content. We do not model pattern separation explicitly. We also do not model the entorhinal scaffold, except through the positional code, and the anatomical division of labor between hippocampal subfields is outside the scope of this paper.

| Brain | IM-LEPP2 |
|---|---|
| Hippocampal index (one-shot binding) | Non-parametric store of episodes with keys; write needs no gradient step |
| Neocortical content (values) | Stored $zzz_t$ sequence (and words, for language) |
| Pattern completion from a partial cue | kNN retrieval, with keys trained on partial episodes |
| Entorhinal positional scaffold | Within-episode positional code (rotary); learned recurrent code as extension |
| Event schemata (neocortex) | Parameters of the energy functions, in particular at the event level |
| Event boundaries (EST) | Surprisal thresholds at each pipeline level |
| Reconsolidation | Recall stored as a modified copy |
| Sleep replay and consolidation | Offline training on replayed episodes with the target masked |
| Time and place stamp | Not modeled |

*Table 1: Correspondence between the brain's episodic memory system and IM-LEPP2.*

**References for this section**

- Teyler, T. J., and DiScenna, P. (1986). The hippocampal memory indexing theory. *Behavioral Neuroscience*.
- Whittington, J. C. R., et al. (2020). The Tolman-Eichenbaum machine. *Cell*.
- Zacks, J. M., et al. (2007). Event perception: a mind/brain perspective. *Psychological Bulletin* 133(2).
- Summerfield, C., and Stachenfeld, K. (2026). The recipe for intelligence in natural and artificial systems. *Neuron* 114.
- Tulving, E. (1972). Episodic and semantic memory.
- [verify] Yassa, M., and Stark, C. (2011), *Trends in Neurosciences*; Tse, D., et al. (2007), *Science*; van Kesteren, M., et al. (2012), *Trends in Neurosciences*.



## Transformer Models

In the last few years there have been several proposals that have been made to improve upon Transformer models. These proposals can be broadly classified into the following categories:

- Loop Transformers and Universal Transformers: The basic idea in these models is to repeat a single Transformer block multiple times (with shared parameters), and has been shown to have similar performance to a full Transformer, while saving on parametric memory. This aspect is directly incorporated in IM-LEPP2, since if we regard each step of $E_W$ minimization as being roughly equivalent to a Transformer block, then multiple invocations of the gradient descent during the process of energy minimization are equivalent to the multiple invocations of the Loop Transformer block.

- Techniques to propagate the latent state: The amount of thinking that a Transformer can do is tied to the number of blocks it has in each column, which is a fixed number. In some sense the thinking process has to re-start in a new prediction column, and the information in the latent state from the previous column is lost. There have been some recent proposals to correct this by propagating the final latent state from between successive columns, most notably in the Full Bandwidth Transformer. This is done natively in the IM-LEPP design, since the system latent state is propagated between successive prediction stages.
- Techniques to break up a long context into chunks, and then choose a subset of these chunks during the prediction process (as in [Raffel et.al](https://arxiv.org/abs/1910.10683)): IM-LEPP2 incorporates this design choosing appropriate chunks from its episodic memory store during the prediction process.

Note: There remains one different between the two: Transformers do multiple independent 'episodic' memory accesses during the course of a single prediction, while IM-LEPP2 uses the same recalled episode. How important is it to do multiple memory accesses? I have been reluctant to add this to the design, since every memory access changes the context, and thus the energy landscape, which might mess up the energy minimization process (this goes back to a discussion we had). On the other hand emitting intermediate tokens is probably fine and forms part of the CoT process.

In summary, recent Transformer models have begun to incorporate features that make them closer to the IM-LEPP2 design. Since IM-LEPP2 itself was inspired by experimental evidence collected over the years from neuroscience about how the brain operates, this convergence brings the latest Transformer design improvements closer to the biological brain.
There was a nice survey of the correspondences between the Transformer and brains that was published recently (see [Summerfield et.al.](https://www.cell.com/neuron/fulltext/S0896-6273(26)00643-4).
I am curious to get your reading on this paper and how its lessons apply to IM-LEPP2.

There is another class of models that have been proposed recently called reasoning models.
In Transformers reasoning requires multiple invocations of the prediction block within a column, and if the number of blocks is fixed, then it leads limitations in the reasoning process. Some information is propagated to the next column using the predicted token, but most of the information in the final latent state is lost. The IM-LEPP2 model facilitates reasoning through two mechanisms: 
(1) Through the multistep gradient descent based minimzation of the energy function, in which the number of steps is variable, hence can change depending upon the difficulty of the reasoning problem, 
(2) Since the final latent state is sent to the next prediction module, this avoids the problem that Transformers have of loosing the latent state information. Furthermore the new prediction module utilizes fresh conditioning vectors, which prevent the recurrent state from decaying over time.



