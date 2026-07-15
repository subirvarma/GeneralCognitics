---
layout: default
title: " Generative AI as an Effective Theory of Cognitive Dynamics"
---

# Generative AI as an Effective Theory of Cognitive Dynamics

**Contents**     

- Introduction
- The Predictive Processing Framework in Computational Neuroscience
- Energy based Temporal Predictive Coding (ETPC)
  - Implementing the Inference and Generation Modules: Predictive Coding
  - Implementing the Prediction Module using EBM/Diffusions
  - Training the Diffusion Model
  - Biological Plausibility
- Are Letent States Necessary? An Alternative Model (DEPP)
- Planning 
  - The Reinforcement Learning Framework for Planning
- Micro-architecture of Energy based Models

## Introduction

Recent advances in generative artificial intelligence have led to remarkable progress in modeling human perception, language, and reasoning. Models such as transformers and diffusion models exhibit behaviors that, while not equivalent to human cognition, increasingly resemble aspects of human thought. This success has naturally prompted attempts to relate these architectures to biological neural circuits. In particular, researchers have sought neural correlates of attention mechanisms, transformer architectures, and diffusion processes within the cortex.

This paper argues that such comparisons may be taking place at the wrong level of description. We hypothesize that modern generative neural networks should be understood not as mechanistic models of neural implementation, but as **effective theories of cognitive dynamics operating at the level of learned energy landscapes**. In this view, cognition is understood as the temporal evolution of perceptual and cognitive states through a learned energy landscape, rather than as the direct consequence of an explicitly modeled neural circuitry.

The history of physics provides a useful analogy. Thermodynamics provides an effective description of macroscopic matter without explicitly modeling every molecular interaction. Statistical mechanics explains why such effective descriptions are possible: the collective effects of microscopic molecular interactions can be summarized by a free-energy function that governs the macroscopic dynamics of the system. Thermodynamics is therefore not a model of molecular structure, but an effective theory of its observable behavior. This distinction between mechanistic and effective theories is common throughout physics but has received comparatively little attention in computational neuroscience, where advances in AI are often interpreted in terms of architectural similarities to biological neural circuits.

![](https://subirvarma.github.io/GeneralCognitics/images/stat134.png)

**Figure 1:** Proposed analogy between statistical mechanics and generative AI. Just as statistical mechanics explains why thermodynamics provides an effective description of macroscopic matter without explicitly modeling every molecular interaction, modern generative neural networks may provide effective descriptions of cognitive dynamics without modeling the underlying neural circuitry.

Throughout this paper we distinguish three levels of scientific description. At the microscopic level lies the brain's connectome and neuronal circuitry. At an intermediate level lie the hidden cognitive dynamics responsible for perception and thought. At the macroscopic level lie observable behaviors such as perception, language, and action. The central thesis of this paper is that modern generative AI operates primarily at this highest level, learning effective dynamical laws governing observable cognitive behavior without explicitly modeling the lower levels.

We propose that modern generative neural networks should be interpreted in this spirit. Rather than viewing transformers or diffusion models as candidate models of the brain's circuitry, we suggest viewing them as *effective theories of cognitive dynamics*. Their parameters should not be expected to correspond directly to neurons, synapses, or cortical microcircuits. Instead, they may be regarded as learning an effective energy landscape governing the evolution of perceptual and cognitive states. The underlying biological implementation—encoded in the brain's connectome and cellular physiology—remains hidden, just as microscopic molecular interactions remain hidden within thermodynamic descriptions.

This perspective has several consequences. First, it suggests that searching for direct anatomical counterparts of transformer blocks or diffusion networks may be misguided. Different microscopic implementations can generate remarkably similar macroscopic dynamics, a phenomenon familiar throughout statistical physics. Second, it provides a natural explanation for the success of modern generative AI. These models need not recover the brain's internal circuitry in order to reproduce important aspects of cognitive behavior; they need only learn the effective dynamical laws governing its observable outputs.

Building upon the predictive processing framework of Clark and the predictive coding formulations of Rao, Ballard, and Friston, we develop an alternative interpretation of perception based on energy-based dynamics. Rather than treating latent causes as indispensable components of a computational theory, we explore the possibility that perceptual and cognitive states themselves evolve according to a learned energy landscape. Diffusion models provide a natural mathematical framework for describing such dynamics, allowing effective energy functions to be learned directly from observable behavior without requiring an explicit model of the underlying neuronal interactions.

The aim of this paper is not to argue that the brain literally implements a diffusion model or a transformer architecture. Rather, we argue that modern generative neural networks constitute a new class of effective theories for cognition, analogous to the role played by thermodynamics in physics. Viewed from this perspective, recent developments in generative AI suggest a shift in emphasis for computational neuroscience—from searching for detailed mechanistic replicas of neural circuitry toward identifying the effective dynamical principles governing cognition.

Predictive processing provides the natural computational framework within which this proposal can be formulated. In this view, perception is not a passive reconstruction of sensory input. The brain continuously generates expectations about the state of the world and revises them in response to incoming sensory evidence. Perception therefore reflects an interaction between internally generated predictions and signals produced by the environment.

An important feature of this framework is its temporal character. The organism must not only estimate the present state of its environment, but also anticipate how that state is likely to evolve. Such predictions can guide perception, action, and—when extended over longer horizons—planning. The central question considered here is whether these predictive dynamics can be modeled directly as motion through a learned energy landscape, without requiring an explicit model of the neuronal circuitry that implements them.

To explore this question we develop two complementary energy-based formulations of predictive processing. The first, **Latent Energy-Based Predictive Processing (LEPP)**, retains the latent-state representation of classical predictive processing while reformulating both inference and temporal prediction as processes of energy minimization. The second, **Direct Energy-Based Predictive Processing (DEPP)**, dispenses with an explicitly specified latent-state architecture and instead models the evolution of perceptual states directly through a learned energy function. The comparison between these models allows us to distinguish between mechanistic and effective theories of cognition and to ask whether explicit latent representations are essential components of an effective computational theory.

Recent work by Yann LeCun and colleagues on Joint Embedding Predictive Architectures (JEPAs) and world models similarly emphasizes predictive latent representations and energy-based learning as foundations for intelligent systems. The present work adopts a complementary perspective by asking what such architectures imply for computational theories of cognition.

The next section summarizes the predictive-processing framework and clarifies the distinctions among perceptual inference, temporal prediction, action, and planning that will be used throughout the article.

## The Predictive Processing Framework in Computational Neuroscience

Predictive processing has emerged as one of the leading theoretical frameworks in contemporary computational neuroscience. Although its roots can be traced to Helmholtz's theory of unconscious inference, modern formulations by [Rao and Ballard](https://homes.cs.washington.edu/~rao/predcoding2011.pdf), [Friston](https://direct.mit.edu/books/oa-monograph/5299/Active-InferenceThe-Free-Energy-Principle-in-Mind), [Clark](https://www.amazon.com/Experience-Machine-Minds-Predict-Reality/dp/B0B6489ZTB/ref=sr_1_1?adgrpid=183606417542&dib=eyJ2IjoiMSJ9.Fyi9d3PdzMTC53VWX7823DXjmQdLDMFgbQL5bpU2yx77AApTelrS2J7RZW7kevX5c3Iwj8BdMiBCvvIK1s-2aQ.kNY6Xa746RCCEx9tUbrInrqWtuuYDtwDu9jxlEmRXNw&dib_tag=se&hvadid=779664909770&hvdev=c&hvexpln=0&hvlocphy=9031954&hvnetw=g&hvocijid=7989718953734198151--&hvqmt=e&hvrand=7989718953734198151&hvtargid=kwd-2027556117302&hydadcr=22594_13821176_8133&keywords=the+experience+machine+andy+clark&mcid=bd89ac636e0c38d39698b254fe27c1b0&qid=1776120362&sr=8-1), and others have developed it into a quantitative framework for understanding perception, action, and learning.
It proposes that perception is fundamentally an active process of prediction rather than a passive registration of sensory signals.

The central insight is that an organism has direct access only to sensory signals generated at its sensory surfaces. These signals are noisy, incomplete, and inherently ambiguous. The computational problem facing the brain is therefore to construct a coherent estimate of the external world from this limited information. Predictive processing proposes that this is achieved by continuously combining internally generated predictions with incoming sensory evidence. Perception is therefore not a direct copy of the sensory input, but the result of an ongoing interaction between expectation and observation.

One consequence of this view is that the predictive model itself must be learned. Evidence for this comes from individuals whose vision is restored after congenital blindness or prolonged congenital cataracts. Although the retina and optic nerve may function normally following treatment, visual perception is initially severely impaired. Object recognition, depth perception, and scene understanding improve only gradually through experience. These observations suggest that retinal input alone is insufficient for mature visual perception. The brain must also acquire an internal model capable of interpreting sensory signals.

A second consequence is that perception becomes fundamentally temporal. Rather than merely estimating the current state of the world, the brain continuously predicts how the sensory environment will evolve over time. Incoming sensory information is compared with these predictions, and discrepancies are used to update the brain's internal model. When the environment changes only slowly, prediction errors remain small. Unexpected events generate larger prediction errors, forcing the internal model to adapt.

Figure 2 illustrates a simplified computational model of this process. The organism maintains an internal state that summarizes its current estimate of the world. This state is updated using incoming sensory information, used to predict its future evolution, and finally transformed into the conscious percept experienced by the organism. The prediction generated by this process is continuously compared with new sensory observations, producing an error signal that modifies the internal state and closes the perception loop.

![](https://subirvarma.github.io/GeneralCognitics/images/stat131.png) 

Figure 2: A model for sensory perception generation in the brain

An important implication of predictive processing is that much of what we perceive is generated internally rather than directly specified by sensory input. Sensory signals primarily indicate where the current prediction should be modified, while the detailed percept is constructed from the organism's learned internal model. This offers a natural explanation for the richness and continuity of conscious perception despite the relatively sparse and noisy information available from the sensory organs.

Predictive processing has also been extended beyond perception. The same internal model that predicts future sensory states can be used to evaluate the consequences of potential actions. During planning, the model is effectively run "open loop," allowing future scenarios to be simulated without requiring new sensory input. More generally, actions themselves can be viewed as another mechanism for reducing prediction error, either by changing the organism's internal model or by changing the external world so that it conforms more closely to the organism's predictions.

Although predictive processing has proved remarkably successful as a computational framework, an important modeling question remains. Most existing formulations assume that perception proceeds by inferring latent variables representing the hidden causes responsible for sensory observations. These latent states are updated from sensory evidence, evolved forward in time, and subsequently transformed into perceptual experience.

The motivation for introducing latent variables is clear. Sensory observations are incomplete, noisy, and inherently ambiguous. Many different external situations can produce similar sensory signals, and the brain therefore benefits from constructing an internal representation that captures the hidden causes responsible for those observations. Classical predictive processing formulates perception as inference over these latent states.

The present work asks whether this latent representation is indispensable for an effective computational theory of perception. Rather than questioning the existence or usefulness of latent cognitive states, we ask a different question: **must they be represented explicitly within the computational model itself?** Modern energy-based generative models suggest that, in many cases, the observable dynamics of a system can be learned directly without explicitly modeling every intermediate variable responsible for those dynamics.

This distinction is best understood as a hierarchy of effective theories rather than as a contrast between mechanistic and effective descriptions. Both approaches developed in this paper operate at the level of effective energy landscapes rather than at the level of neuronal circuitry. The difference lies in the choice of state variables over which those energy landscapes are defined.

The first formulation, **Latent Energy-Based Predictive Processing (LEPP)**, retains the latent-state representation of classical predictive processing. It learns an effective energy landscape governing the temporal evolution of latent cognitive states while leaving the underlying neuronal implementation implicit.

The second formulation, **Direct Energy-Based Predictive Processing (DEPP)**, performs one further level of abstraction. Instead of explicitly representing latent cognitive states, it models the evolution of observable perceptual states directly through a learned energy landscape. The latent dynamics are not denied; rather, they become implicit within the learned effective dynamics.

Viewed in this way, LEPP and DEPP should not be regarded as competing theories of perception. Instead, they represent two complementary levels of effective description. LEPP models the evolution of latent cognitive dynamics, whereas DEPP models the observable dynamics emerging from them. Both remain effective descriptions that abstract away from the microscopic neuronal mechanisms responsible for implementing cognition.

The remainder of this paper develops these two complementary formulations. We first construct LEPP by reformulating classical predictive processing entirely within an energy-based framework. We then show how DEPP emerges as a further abstraction, raising the broader question of whether effective theories of cognition can themselves be organized into a hierarchy of increasing levels of abstraction.

## Latent Energy-Based Predictive Processing (LEPP)

The previous sections argued that modern generative AI should be viewed not as a mechanistic model of neural circuitry, but as an effective theory of cognitive dynamics. The next question is how such an effective theory might be formulated within the predictive-processing framework.

The **Latent Energy-Based Predictive Processing (LEPP)** architecture proposed here provides one possible answer. Its purpose is not to replace the classical predictive-processing framework, but to demonstrate that predictive processing can be reformulated entirely within an energy-based computational paradigm. LEPP retains the central assumption that perception proceeds through the inference of latent causes from sensory observations while expressing every stage of the computation as a process of stochastic energy minimization.

Within the hierarchy of effective theories proposed in this paper, LEPP occupies the first level above mechanistic descriptions of neural circuitry. Rather than modeling neurons, synapses, or cortical circuits directly, LEPP models the evolution of **latent cognitive states** through learned energy landscapes. The microscopic biological implementation remains implicit, while the latent cognitive dynamics are represented explicitly.

![](https://subirvarma.github.io/GeneralCognitics/images/stat133.png)

**Figure 3:** The Latent Energy-Based Predictive Processing (LEPP) architecture.

A central idea underlying LEPP is that predictive processing naturally decomposes into **three interacting computational processes**, each solving a different inference problem.

1. **Latent-state inference:** Estimate the latent state that best explains the current sensory observations.

2. **Temporal prediction:** Predict how that latent state is expected to evolve over time.

3. **Percept generation:** Transform the predicted latent state into the organism's perceptual experience.

Although these processes solve different computational problems, they all operate according to the same underlying principle: **stochastic minimization of learned energy functions**. The inference and generation processes are implemented using predictive coding, while temporal prediction is implemented using a diffusion-based energy model. Consequently, the entire predictive-processing cycle becomes a sequence of coupled energy-minimization processes rather than a system trained through global error backpropagation.

An important distinction should be noted. The word *prediction* is used in two different senses within the predictive-processing literature. In **predictive coding**, prediction refers to estimating the latent causes responsible for the current sensory observations. In **predictive processing**, prediction refers to forecasting how the organism's internal state is expected to evolve over time. LEPP separates these two computations explicitly. Predictive coding performs inference over the current latent state, while the temporal prediction module models its future evolution.

The operation of LEPP is illustrated in Figure 3.

At time step $n$, a stream of sensory observations $s_n$ is processed by the predictive-coding inference module, producing the latent representation $z_n$. This latent state represents the organism's current estimate of the hidden causes responsible for the incoming sensory data.

The inferred latent state is then supplied to the temporal prediction module. Unlike the inference module, whose task is to explain the current sensory observations, the prediction module estimates how the latent representation is expected to evolve before the next sensory observation arrives. Rather than computing a deterministic prediction, the module performs stochastic sampling over a learned energy function

$$E_W(x;z_n,u_{n+1}),$$

where $u_{n+1}$ denotes contextual variables such as intended actions or other factors influencing the future evolution of the environment. The sampling process converges toward a low-energy region of the learned landscape, yielding the predicted latent state $x_{n+1}$.

The predicted latent state is subsequently transformed into the organism's percept through the generative model

$$y_{n+1}=p_\psi(x_{n+1}),$$

where $y_{n+1}$ denotes the predicted percept at the next instant.

When the next sensory observations $s_{n+1}$ become available, the predicted latent state $x_{n+1}$ serves as the initial estimate for the next inference cycle. Predictive coding recursively updates this estimate until it converges to the refined latent state

$$z_{n+1}=q_\phi(x_{n+1},s_{n+1}),$$

which then becomes the input to the temporal prediction module for the following prediction cycle.

The complete computational flow may therefore be summarized as

$$s_n \rightarrow z_n \rightarrow x_{n+1} \rightarrow y_{n+1}.$$

Each stage performs a distinct computational operation.

| Transformation | Computational Task | Computational Module |
|---------------|--------------------|----------------------|
| $s_n \rightarrow z_n$ | Infer the current latent state | Predictive Coding |
| $z_n \rightarrow x_{n+1}$ | Predict the future latent state | Diffusion-based Energy Model |
| $x_{n+1} \rightarrow y_{n+1}$ | Generate the predicted percept | Generative Model |

Notice, however, that all three transformations are unified by a common computational principle. The inference module minimizes an energy defined over latent states that best explain the current sensory observations. The temporal prediction module minimizes an energy governing the future evolution of those latent states. The generative model transforms the resulting low-energy latent state into perceptual experience. LEPP therefore reformulates the entire predictive-processing loop as a sequence of interacting energy-minimization processes.

Classical presentations of predictive processing often emphasize the overall perception–action loop. LEPP instead decomposes this loop into three computational processes, allowing each to be formulated using the mathematical framework most naturally suited to the task while preserving a common energy-based interpretation.

The model assumes that temporal prediction converges within the interval separating successive sensory observations. Consequently, inference, temporal prediction, perception, and learning proceed continuously and in parallel, producing a continually updated estimate of the organism's environment.

An attractive feature of LEPP is that perception and learning occur simultaneously. Each prediction cycle not only generates the organism's current percept but also provides training signals for all three computational modules. The inference model $q_\phi$, the temporal energy model $E_W$, and the generative model $p_\psi$ are therefore continuously refined as new sensory observations arrive. In this respect LEPP more closely resembles the continual online learning performed by biological nervous systems than the separate training and inference phases characteristic of most artificial neural networks.

The remainder of the LEPP framework develops these three computational processes in turn. We first revisit predictive coding as an energy-based implementation of inference and generation before introducing a diffusion-based energy model for temporal prediction. Together these modules provide a complete energy-based realization of predictive processing while retaining the explicit latent-state representation characteristic of classical predictive processing.

## Implementing the Inference and Generation Modules: Predictive Coding

As discussed in the previous section, the LEPP architecture reformulates predictive processing as **three coupled energy-minimization processes**: latent-state inference, temporal prediction, and percept generation. In this section we consider the first and third of these processes. We show that they can be naturally implemented using **predictive coding**, originally proposed by Rao and Ballard (1999). Viewed from this perspective, predictive coding becomes the inference component of a larger energy-based theory of cognition.

Predictive coding provides a biologically plausible mechanism for inferring latent causes from sensory observations using only local neural computations. It can itself be viewed as an energy-based model whose objective is to minimize a predictive-coding energy function, which we shall denote by $E_{PC}$.

![](https://subirvarma.github.io/GeneralCognitics/images/stat99.png)

**Figure 4:** Predictive coding architecture. Higher cortical areas generate top-down predictions of activity in lower areas, while lower areas return bottom-up prediction errors. Perception emerges through iterative reduction of these prediction errors (from [Rao and Ballard](https://www.cs.utexas.edu/~dana/Rao.pdf)).

Predictive coding assumes that the cortex is organized hierarchically. Each cortical level attempts to predict the activity of the level immediately below. The lower level compares this prediction with its actual activity and sends only the resulting prediction error back upward. Consequently, information flows in two directions through the hierarchy: predictions propagate downward, while prediction errors propagate upward. Through repeated interactions the hierarchy converges to a mutually consistent interpretation of the sensory input.

For a two-level hierarchy, the generative model can be written as

$$ z^{(2)} \rightarrow z^{(1)} \rightarrow y. $$

Here $y$ denotes the sensory activity (for example retinal or LGN responses), $z^{(1)}$ represents lower-level cortical features such as V1-like responses, and $z^{(2)}$ represents higher-level latent causes corresponding to more abstract visual structure. Throughout this section the inference process is assumed to occur within a single sensory interval, so the temporal index has been omitted for clarity. The highest-level representation $z^{(2)}$ corresponds to the latent state $z_n$ introduced in the LEPP architecture.

Suppose that level $l$ predicts the activity of the level immediately below according to

$$ \hat z^{(l-1)} = f_l(z^{(l)}). $$

The corresponding prediction error is

$$ \epsilon_{l-1} = z^{(l-1)} - f_l(z^{(l)}), $$

while the sensory prediction error is

$$ \epsilon_0 = s - f_1(z^{(1)}), $$

where $s$ denotes the sensory input.

The objective of predictive coding is to adjust the latent representations so that these prediction errors are minimized throughout the hierarchy. Each latent representation therefore evolves under the influence of two competing constraints: it must explain the activity of the level below while remaining consistent with the prediction supplied by the level above. Perception corresponds to the equilibrium reached when these competing influences balance.

---

### Bayesian Interpretation

Predictive coding can be derived directly from Bayesian inference.

For simplicity, consider a single latent representation $z$ generating a sensory observation $y$. Bayes' rule gives

$$ p(z|y)=\frac{p(y|z)p(z)}{p(y)}. $$

Since $p(y)$ is constant with respect to $z$,

$$ z^*=\arg\max_z\left[\log p(y|z)+\log p(z)\right], $$

which is the familiar Maximum A Posteriori (MAP) estimate.

Assume the sensory observation is generated according to

$$ y=f(z)+\epsilon, $$

where

$$ \epsilon\sim\mathcal N(0,\Sigma_y). $$

Then

$$ -\log p(y|z)=\frac12(y-f(z))^T\Sigma_y^{-1}(y-f(z)). $$

Defining the sensory prediction error

$$ \epsilon_y=y-f(z), $$

the likelihood term becomes

$$ \frac12\epsilon_y^T\Pi_y\epsilon_y, $$

where

$$ \Pi_y=\Sigma_y^{-1} $$

is the sensory precision matrix.

Similarly, assuming

$$ z\sim\mathcal N(\mu_z,\Sigma_z), $$

the prior contributes

$$ \frac12\epsilon_z^T\Pi_z\epsilon_z, $$

where

$$ \epsilon_z=z-\mu_z. $$

The negative log posterior is therefore

$$ E_{PC}(z)=\frac12\epsilon_y^T\Pi_y\epsilon_y+\frac12\epsilon_z^T\Pi_z\epsilon_z. $$

This expression has a natural interpretation as an **energy function**. Bayesian inference therefore becomes mathematically equivalent to minimizing the predictive-coding energy $E_{PC}$. Bayesian inference and energy minimization are thus not competing computational principles but two complementary descriptions of the same optimization problem.

---

### Local Energy Minimization

The latent representation is updated according to

$$ z\leftarrow z-\eta\frac{\partial E_{PC}}{\partial z}, $$

giving

$$ -\frac{\partial E_{PC}}{\partial z}=\left(\frac{\partial f}{\partial z}\right)^T\Pi_y\epsilon_y+\Pi_z\epsilon_z. $$

The first term is driven by bottom-up sensory prediction error and encourages the latent state to better explain the observations. The second term is driven by top-down expectations encoded by the prior.

Although this resembles ordinary gradient descent, an important feature of predictive coding is that the required information is entirely local. Each cortical area requires only its own activity together with the prediction arriving from the level above and the prediction error arriving from the level below. The global optimization therefore decomposes into a collection of local computations that can plausibly be implemented by recurrent cortical circuitry.

This locality is one of the principal reasons predictive coding has been regarded as biologically plausible. The cortex need not implement global error backpropagation; instead each cortical area performs a local energy-minimization computation using only information available from neighboring levels of the hierarchy.

For the linear model originally considered by Rao and Ballard,

$$ y=Wz+\epsilon, $$

the update simplifies to

$$ -\frac{\partial E_{PC}}{\partial z}=W^T\Pi_y\epsilon_y+\Pi_z\epsilon_z. $$

---

### Extension to Hierarchical Representations

The same derivation extends naturally to multiple cortical levels

$$ z^{(L)}\rightarrow\cdots\rightarrow z^{(2)}\rightarrow z^{(1)}\rightarrow y. $$

Each level predicts the activity below according to

$$ z^{(l-1)}=f_l(z^{(l)})+\epsilon_l, $$

and the complete predictive-coding energy becomes

$$ E_{PC}=\sum_l\frac12\epsilon_{l-1}^T\Pi_{l-1}\epsilon_{l-1}. $$

Every latent representation participates in two prediction relationships: it is predicted by the level above while simultaneously predicting the level below. Consequently, each latent state is updated using both top-down and bottom-up prediction errors until the hierarchy converges to a consistent explanation of the sensory input.

---

### Learning the Generative Model

Predictive coding naturally unifies inference and learning within the same dynamical system.

The latent representations correspond to neuronal activity, while the parameters of the generative mappings are encoded in synaptic strengths. During perception the latent representations rapidly change to minimize prediction error, while synaptic weights evolve more slowly according to local Hebbian-style learning rules. For the linear model the weight update is

$$ -\frac{\partial E_{PC}}{\partial W_l}=\Pi\left(z^{(l-1)}-W_lz^{(l)}\right)z^{(l)T}. $$

The change in each synapse depends only on locally available quantities: presynaptic activity and postsynaptic prediction error. Consequently, inference and learning occur simultaneously during normal operation of the network rather than as separate training and inference phases.

---

### Role within LEPP

Predictive coding therefore provides a biologically plausible implementation of the inference and percept-generation components of the LEPP architecture. Within the hierarchy of effective theories developed in this paper, predictive coding supplies the inference engine that enables LEPP to represent latent cognitive dynamics explicitly.

An important limitation, however, is that predictive coding fundamentally addresses only **one of the three computational processes** identified in Figure 3. It explains how the brain infers the latent state responsible for the current sensory observations, but it says relatively little about how those latent states evolve through time. LEPP completes the predictive-processing framework by introducing a separate temporal energy model governing the dynamics of those latent states. It is to this second energy-minimization process that we now turn.

## Temporal Prediction as Energy Minimization

The previous section showed that latent-state inference can be formulated as the minimization of a predictive-coding energy function, $E_{PC}$. We now turn to the second computational process in the LEPP architecture: **temporal prediction**. The central question is whether the evolution of latent cognitive states can likewise be formulated as stochastic minimization of a learned energy function.

Unlike predictive coding, this is fundamentally a problem of **dynamical modeling** rather than state estimation. Given the current latent state $z_n$, together with contextual variables $u_{n+1}$ such as intended actions, the prediction module seeks to model the conditional distribution

$$ p(x_{n+1}|z_n,u_{n+1}). $$

Rather than predicting a single deterministic future, LEPP represents this conditional distribution using an **Energy-Based Model (EBM)**,

$$ p_W(x|z,u)=\frac{\exp[-E_W(x;z,u)]}{Z_W}, $$

where $E_W(x;z,u)$ is a learned energy function parameterized by $W$, and

$$ Z_W=\int e^{-E_W(x;z,u)}\,dx $$

is the partition function.

The energy function defines an effective energy landscape over future latent states. Regions of low energy correspond to highly probable future trajectories, while regions of high energy correspond to unlikely futures. Rather than committing to a single prediction, the model therefore represents an entire probability distribution over possible future latent states.

In this sense, the learned energy landscape serves as the **effective dynamical law** governing latent-state evolution.

Like predictive coding, the temporal prediction module operates entirely at the level of an effective energy landscape. It does not attempt to model the microscopic neuronal interactions responsible for prediction. Instead, it learns the large-scale dynamical laws governing the evolution of latent cognitive states directly from experience.

![](https://subirvarma.github.io/GeneralCognitics/images/stat83.png)

**Figure 5:** Learning an effective energy landscape governing the temporal evolution of latent cognitive states.

A sufficiently expressive function approximator, such as a Transformer or Diffusion Transformer (DiT), can be trained to approximate the unknown energy function directly from observed latent-state trajectories. In this way, the microscopic details of the underlying neural circuitry are replaced by an effective dynamical description of latent-state evolution.

This is precisely the effective-theory viewpoint introduced in the Introduction. Statistical mechanics replaces microscopic molecular interactions with an effective free-energy landscape governing macroscopic behavior. The diffusion prediction module performs an analogous abstraction, replacing unknown neuronal interactions with a learned energy landscape governing latent cognitive dynamics.

---

## Sampling Future Latent States Using Diffusion Models

Once the energy function has been learned, the remaining problem is to generate samples from the conditional distribution

$$ p_W(x|z,u). $$

This is itself an optimization problem. Beginning from an initial state, the system evolves toward progressively lower-energy regions until a probable future latent state is reached.

In biological nervous systems this optimization may emerge through the interactions of large populations of neurons. In machine learning, an efficient approximation is provided by **diffusion models**, which implement stochastic energy minimization using Langevin dynamics.

![](https://subirvarma.github.io/GeneralCognitics/images/stat122.png)

**Figure 6:** Temporal prediction by stochastic energy minimization. Starting from a noisy initial condition, Langevin dynamics gradually moves the system toward lower-energy regions of the learned landscape.

The sampling procedure begins from a high-noise initial state and gradually reduces the noise level over a sequence of diffusion stages. At each stage several Langevin updates are performed,

$$ x(t,k+1)=x(t,k)-\eta\nabla_xE_W(x(t,k),t,z_n,u_{n+1})+\sqrt{2\eta}\,\epsilon, $$

where

$$ \epsilon\sim\mathcal N(0,I). $$

The injected noise prevents the dynamics from becoming trapped in poor local minima while allowing exploration of multiple possible futures. As the diffusion process proceeds, the noise level is gradually reduced, causing the latent state to settle into progressively lower-energy regions of the learned energy landscape.

![](https://subirvarma.github.io/GeneralCognitics/images/stat123.png)

**Figure 7:** One Langevin update within a diffusion stage.

Although diffusion models are usually introduced as denoising algorithms, their deeper interpretation is that of **stochastic gradient flows on learned energy landscapes**. This interpretation is particularly natural here because it places diffusion models and predictive coding within the same mathematical framework.

Notice the close symmetry between the two principal computational processes within LEPP.

| Computational Process | Energy Function | Equilibrium Represents |
|----------------------|-----------------|------------------------|
| **Latent-state inference** | $E_{PC}$ | Best explanation of the current sensory observations |
| **Temporal prediction** | $E_W$ | Most probable future latent state |

Predictive coding minimizes the energy function

$$ E_{PC}, $$

whose equilibrium estimates the latent state responsible for the current sensory observations.

The diffusion prediction module minimizes the energy function

$$ E_W, $$

whose equilibrium predicts the latent state expected at the next instant.

LEPP therefore unifies state inference and temporal prediction within a common computational language. Both are equilibrium-seeking dynamical systems that differ only in the energy function they minimize and the computational problem they solve.

---

### Learning the Prediction Energy

Learning the prediction module consists of estimating the parameters of the conditional energy function

$$ E_W(x;z,u). $$

Unlike predictive coding, which receives current sensory observations directly, the prediction module learns by comparing its predicted latent state with the latent state inferred after the next sensory observation becomes available.

Suppose that after predicting $x_{n+1}$, the inference module computes the corrected latent state $z_{n+1}$. The tuple

$$ (z_n,u_{n+1},x_{n+1},z_{n+1}) $$

then provides a supervised training example describing the true temporal evolution of the latent space.

The parameters $W$ are learned by maximizing the conditional log-likelihood

$$ L(W)=E_{p(x|z,u)}[\log p_W(x|z,u)]. $$

Using the Boltzmann representation, the corresponding gradient becomes

$$ \nabla_WL(W)=-E_{\text{data}}[\nabla_WE_W]+E_{\text{model}}[\nabla_WE_W]. $$

The first expectation is evaluated using latent-state transitions inferred from subsequent sensory experience, while the second is evaluated using samples generated by the prediction model itself. The prediction module therefore learns by continually comparing its own imagined futures with the futures subsequently experienced, gradually refining its energy landscape over time.

This learning rule is directly analogous to that used in classical Boltzmann machines. If the underlying neuronal interactions were explicitly known, Hebbian learning would emerge as a special case. Since the brain's connectome is unknown, however, the energy function is instead approximated by a neural network function approximator, while modern diffusion-learning algorithms such as [Diffusion Recovery Likelihood (DRL)](https://arxiv.org/abs/2012.08125) provide efficient procedures for estimating its parameters.

Viewed in this way, the diffusion prediction module occupies the same role within LEPP that predictive coding occupies for inference. Both replace detailed neuronal mechanisms with effective energy-minimization dynamics, differing only in the computational problem they solve. Together they provide a unified energy-based realization of predictive processing.

## Biological Interpretation of LEPP

An important question is whether the computations required by the LEPP architecture admit biologically plausible implementations. The answer depends critically on the level of scientific description at which the model is interpreted. LEPP is not intended as a literal reconstruction of the brain's neuronal circuitry. Rather, it should be viewed as an **effective computational theory** of the dynamical processes underlying perception.

Within the hierarchy of effective theories developed in this paper, LEPP occupies the first level above mechanistic descriptions of the brain. Rather than modeling neurons, synapses, or cortical microcircuits directly, it models the evolution of **latent cognitive states** through learned energy landscapes. The microscopic biological implementation remains implicit, while the latent cognitive dynamics are represented explicitly.

The LEPP architecture consists of two principal computational components: the latent-state inference module and the temporal prediction module. Both are formulated as stochastic energy-minimization processes, but they solve complementary computational problems. Predictive coding infers the organism's current latent state, while the diffusion-based prediction module estimates how that latent state is expected to evolve over time.

### Biological Plausibility of Predictive Coding

There is considerable evidence supporting the biological plausibility of the predictive-coding component of LEPP. Indeed, predictive coding was originally proposed by Rao and Ballard as a computational model of cortical processing. As shown in the previous section, both inference and learning can be formulated as local energy-minimization processes. Each cortical area communicates only with neighboring levels in the hierarchy through top-down predictions and bottom-up prediction errors, while synaptic plasticity depends only on locally available neuronal activity and prediction errors. Consequently, neither inference nor learning requires global error backpropagation, making predictive coding considerably more compatible with known cortical circuitry than conventional deep-learning algorithms.

### Biological Interpretation of the Prediction Module

The temporal prediction module proposed in LEPP is based on an energy-based model whose predictions are generated through stochastic sampling. This should not be interpreted as a claim that the brain literally implements a diffusion model or Langevin dynamics. Rather, the diffusion model provides an effective computational description of a more general physical process.

The brain contains a vast network of recurrently connected neurons whose detailed connectivity remains largely unknown. As new sensory information arrives, neuronal activity is perturbed away from its previous equilibrium state and gradually relaxes toward a new stable configuration corresponding to the organism's updated latent representation of the world.

The diffusion model provides one computational mechanism for approximating this relaxation process. Starting from the current latent state, stochastic dynamics evolve over a learned energy landscape until a new low-energy equilibrium is reached. Although the computational mechanism differs from neuronal signaling, both systems solve the same abstract computational problem: finding stable states of an underlying energy landscape.

The two systems therefore differ in their microscopic implementation while sharing a common macroscopic objective. The diffusion model achieves this through stochastic sampling over a learned energy function, whereas the brain presumably achieves it through the collective interactions of large populations of neurons. LEPP makes no claim that these microscopic mechanisms are identical. Rather, it proposes that they represent different implementations of the same effective dynamical process.

Learning in the prediction module admits a similar interpretation. When the underlying interaction graph is explicitly known, maximum-likelihood learning reduces to local update rules closely related to Hebbian plasticity. Since the detailed architecture of the brain's connectome is unknown, however, the energy function is instead represented using a neural-network function approximator. The resulting model should therefore be regarded as an effective description of cortical dynamics rather than a mechanistic reconstruction of neuronal circuitry.

### LEPP as an Effective Theory

The principal lesson of LEPP is methodological rather than architectural. The objective is not to reproduce the detailed structure of the brain's connectome, but to identify the effective dynamical principles governing latent cognitive evolution.

This viewpoint is closely analogous to the role of statistical mechanics in physics. Statistical mechanics does not explicitly model every microscopic molecular interaction. Instead, it captures their collective effects through effective energy functions governing the dynamics of macroscopic variables. Likewise, LEPP replaces the unknown neuronal interactions of the brain with an effective energy landscape governing the evolution of latent cognitive states.

Viewed in this way, LEPP occupies an intermediate level of scientific description. It abstracts away from the microscopic organization of the brain while retaining an explicit representation of latent cognitive dynamics. The model therefore preserves the central insight of classical predictive processing—that perception proceeds through latent-state inference—while reformulating the entire computation in terms of coupled energy-minimization processes.

This naturally raises a further question. If the essential computational object is the learned energy landscape rather than the underlying neuronal circuitry, is the explicit latent-state representation itself indispensable?

The next section explores this possibility by proposing a second effective theory of perception—**Direct Energy-Based Predictive Processing (DEPP)**. Whereas LEPP models the evolution of latent cognitive states, DEPP performs one further level of abstraction, dispensing with an explicitly modeled latent-state architecture and instead describing the observable evolution of perceptual states directly through a learned energy landscape.

## Direct Energy-Based Predictive Processing (DEPP)

The LEPP architecture developed in the previous sections demonstrates that classical predictive processing can be reformulated entirely within an energy-based computational framework while preserving its central assumption that perception proceeds through the inference of latent causes.

This naturally raises a more fundamental question.

If the objective is to construct an **effective theory of cognition** rather than a mechanistic reconstruction of neural circuitry, is the explicit latent-state representation itself necessary?

The **Direct Energy-Based Predictive Processing (DEPP)** architecture explores this possibility. Rather than explicitly modeling latent-state inference, temporal prediction, and percept generation as separate computational processes, DEPP models the observable dynamics of perceptual states directly through a learned energy landscape.

It is important to emphasize what DEPP does **not** claim. DEPP does not argue that latent causes do not exist, nor that the brain lacks internal representations. Rather, it asks a more modest question: **must an effective computational theory represent those latent variables explicitly, or can their collective influence be absorbed into a learned energy landscape defined directly over perceptual states?**

![](https://subirvarma.github.io/GeneralCognitics/images/stat127.png)

**Figure 8:** Direct Energy-Based Predictive Processing (DEPP).

The DEPP architecture predicts the next perceptual state directly from the current perceptual state, previous sensory observations, and contextual variables such as intended actions. Instead of operating in latent space, prediction occurs directly within perceptual state space.

The conditional distribution over future perceptual states is represented by

$$
p_W(y_{n+1}|y_n,s_n,u_{n+1}) = \frac{\exp[-E_W(y_{n+1};y_n,s_n,u_{n+1})]}{Z_W}. $$

Prediction proceeds through stochastic sampling over this learned energy landscape using the same diffusion-based optimization procedure introduced for LEPP.

Unlike LEPP, the energy function must now capture the complete observable dynamics of perception. The latent-state computations have not disappeared; rather, they have become implicit within the learned energy landscape itself. In this sense, latent variables become properties of the effective dynamics rather than explicit components of the computational architecture.

---

## Perceptual Dynamics as Motion on an Energy Landscape

The operation of DEPP may be understood by considering how the effective energy landscape evolves through time.

Suppose that at time step $n+1$ the perceptual state is

$$
y_{n+1}=y'.
$$

This corresponds to a local minimum of the energy landscape

$$
E_W(y;y_n,u_{n+1},s_n).
$$

When new sensory observations $s_{n+1}$ arrive and the organism selects a new action $u_{n+2}$, the conditioning variables change, producing a new energy landscape

$$
E_W(y;y',u_{n+2},s_{n+1}).
$$

The previous perceptual state $y'$ is generally no longer an equilibrium of this new landscape. The system therefore evolves through stochastic energy minimization until it reaches a new low-energy state,

$$
y_{n+2}=y'',
$$

which becomes the organism's next percept.

![](https://subirvarma.github.io/GeneralCognitics/images/stat125.png)

**Figure 8:** Evolution of the effective energy landscape as sensory observations and planned actions change through time.

Every new sensory observation and intended action therefore reshapes the energy landscape governing perception. The current percept becomes energetically unstable, initiating a stochastic relaxation process toward a new equilibrium. DEPP interprets perception itself as this continual motion through an evolving energy landscape.

---

## Learning the Effective Dynamics

Learning proceeds in essentially the same manner as in the temporal prediction module of LEPP.

Each observed perceptual transition

$$
(y_n,s_n,u_{n+1},y_{n+1})
$$

provides a supervised training example from which the parameters of the energy function are refined through maximum-likelihood estimation.

If the underlying neuronal interaction graph were explicitly known, the resulting learning rule would reduce to local Hebbian-style updates. Since the brain's connectome remains largely unknown, however, the energy landscape is instead represented by a neural-network function approximator trained using modern energy-based learning algorithms such as Diffusion Recovery Likelihood (DRL).

Once again, the emphasis is not on reproducing the microscopic implementation of the brain, but on learning an effective dynamical law governing its observable behavior.

---

## Hierarchy of Effective Theories

The principal conceptual distinction between LEPP and DEPP is **not** that one is mechanistic while the other is effective. Both are effective energy-based theories of cognition. Neither attempts to model the brain's connectome or neuronal circuitry directly.

The difference lies instead in the choice of state variables over which the effective energy landscape is defined.

LEPP defines its energy landscape over **latent cognitive states**. It therefore retains an explicit internal representation of the organism's inferred model of the world while abstracting away from the underlying neuronal implementation.

DEPP performs one additional level of abstraction. Rather than explicitly representing latent cognitive states, it defines its energy landscape directly over **observable perceptual states**. The latent dynamics have not disappeared; rather, their collective effects have been absorbed into the learned energy landscape itself.

The relationship between the two models may therefore be summarized as follows.

| Aspect | LEPP | DEPP |
|---------|------|------|
| State variables | Latent cognitive states | Observable perceptual states |
| Energy landscape | Defined over latent states | Defined over perceptual states |
| Latent variables | Explicit | Implicit |
| Inference module | Explicit predictive coding | Absorbed into the energy landscape |
| Temporal prediction | Latent dynamics | Perceptual dynamics |
| Level of abstraction | Intermediate effective theory | Higher-level effective theory |

LEPP and DEPP should therefore not be regarded as competing theories of perception. Rather, they represent successive levels within a hierarchy of effective descriptions. Both replace the unknown microscopic neuronal interactions of the brain with learned energy landscapes. They differ only in the variables chosen to describe the resulting dynamics.

LEPP asks:

> *How do latent cognitive states evolve over time?*

DEPP asks:

> *What effective dynamical law governs the observable evolution of perception?*

Viewed in this way, DEPP is not a rejection of latent-state theories but a further abstraction of them. It preserves the same underlying principle of stochastic energy minimization while shifting the description to a higher level of effective dynamics.

## Planning as Open-Loop Prediction

The prediction modules developed in the LEPP and DEPP architectures were introduced as mechanisms for predicting the immediate future during perception. Their significance, however, extends well beyond perceptual inference. Once the organism has learned an **effective dynamical model** of its environment, the same model can be used to simulate hypothetical future scenarios without requiring new sensory input. This capability forms the computational basis of planning.

During normal perception the prediction module operates in **closed loop**. Each prediction is immediately compared with incoming sensory observations, and the resulting prediction error is used to refine both the current perceptual state and the parameters of the prediction model. Through continual interaction with the environment, the model gradually learns the effective dynamical laws governing perceptual evolution.

Planning differs only in how this learned model is used. Instead of receiving continual sensory feedback, the prediction module operates **open loop**, repeatedly generating hypothetical future states conditioned on proposed actions. The resulting sequence of predicted perceptual states allows the organism to evaluate possible courses of action before interacting with the external world.

The distinction is therefore operational rather than architectural.

| **Perception** | **Planning** |
|---------------|--------------|
| Closed-loop operation | Open-loop operation |
| Continual sensory feedback | No sensory feedback |
| Prediction errors continually corrected | Hypothetical futures simulated |
| Learns the world model | Uses the world model |

Planning therefore requires no fundamentally new computational machinery. It is simply a different operating mode of the same predictive architecture.

![](https://subirvarma.github.io/GeneralCognitics/images/stat118.png)

**Figure 9:** Planning in the LEPP framework. During perception the prediction module operates in closed loop using continual sensory feedback. During planning the same prediction module is run open loop, generating hypothetical future trajectories conditioned on candidate actions.

Within the LEPP architecture, planning begins from the currently inferred latent state $z_n$. Given a candidate action $u_{n+1}$, the prediction module estimates the next latent state

$$ x_{n+1}\sim p(x_{n+1}|z_n,u_{n+1}). $$

The predicted latent state is subsequently transformed into its corresponding percept through the generative model. This predicted percept then serves as the starting point for the next prediction, allowing the system to generate an entire sequence of hypothetical future experiences without requiring additional sensory observations.

The same principle applies to DEPP.

![](https://subirvarma.github.io/GeneralCognitics/images/stat128.png)

**Figure 10:** Planning in the DEPP framework.

Because DEPP predicts perceptual states directly, the prediction module simultaneously performs prediction and percept generation. Starting from the current perceptual state, successive applications of the learned energy model generate hypothetical future perceptual trajectories conditioned on candidate actions. In this sense, the learned energy landscape functions as an internal **world model**, allowing the organism to mentally simulate possible future interactions with its environment.

Once learned, the prediction module becomes considerably more than a predictor of the next perceptual state. It becomes an internal simulator capable of generating arbitrary hypothetical trajectories through the learned energy landscape.

The principal distinction between perception and planning therefore lies not in the model being used, but in whether its predictions are continually corrected by sensory observations.

---

### Choosing Actions

Predicting future states is only part of planning. The organism must also decide **which** of the many possible futures it should pursue.

One widely studied framework is **Reinforcement Learning (RL)**, in which the objective is to select the sequence of actions that maximizes expected cumulative reward. Within this framework, the learned prediction model serves as a world model that allows the agent to evaluate hypothetical future trajectories before committing to an action. Modern model-based reinforcement learning systems make extensive use of this principle.

An alternative framework is **Active Inference**, developed by Karl Friston. Rather than maximizing reward, Active Inference proposes that organisms choose actions that minimize expected variational free energy. Although the optimization criterion differs from reinforcement learning, the underlying predictive machinery is remarkably similar. Both frameworks require an internal model capable of simulating future trajectories under alternative actions.

From the perspective developed in this paper, the principal distinction between these approaches lies in the **objective function** used to evaluate predicted futures rather than in the mechanism used to generate them. In both cases, the essential computational requirement is the same: a learned model capable of predicting how perceptual states evolve under different actions.

---

### Planning as a Consequence of Predictive Processing

The discussion above suggests that planning is not an independent cognitive process but a natural extension of predictive processing itself.

During perception, the prediction module is continually trained using sensory feedback, gradually learning the effective dynamical laws governing the organism's environment. Once this effective world model has been acquired, the same computational machinery can be run in open loop to simulate hypothetical futures, evaluate alternative actions, and guide behavior.

Viewed in this way, perception and planning become two operating modes of the same predictive architecture. Perception uses the world model to estimate the present while continually incorporating sensory feedback. Planning uses the same world model to imagine possible futures in the absence of sensory input.

This interpretation further reinforces the central theme of this paper. The prediction modules developed in LEPP and DEPP should not be viewed merely as mechanisms for predicting the next perceptual state. They constitute learned **effective theories of environmental dynamics**. The same learned energy landscape that supports perception also supports imagination, counterfactual reasoning, and planning, without requiring an explicit model of the underlying neuronal circuitry.

## Relationship to LeCun's World Model Program

One of the research programs most closely related to the present work is Yann LeCun's proposal for autonomous machine intelligence. LeCun argues that intelligent systems require predictive world models operating in learned latent representation spaces. His Joint Embedding Predictive Architectures (JEPAs) learn abstract representations of sensory inputs and predict their future evolution, providing the basis for planning and reasoning. Energy-based formulations play a central role in this program.

The LEPP architecture proposed in this paper is closely aligned with this viewpoint. Like JEPA, it separates inference from temporal prediction, performs prediction in latent space, and treats planning as repeated prediction using a learned world model.

The principal difference lies in the interpretation.

Where LeCun's work is primarily concerned with constructing intelligent systems, the present work interprets these architectures as effective theories of cognition. Rather than asking whether a particular architecture reproduces the brain's circuitry, we ask whether it captures the effective dynamical laws governing cognition.

This viewpoint naturally leads to the DEPP architecture, which explores whether latent representations must appear explicitly within the effective theory at all. Whereas JEPA and LEPP formulate prediction over latent cognitive states, DEPP proposes that observable perceptual dynamics may themselves constitute a valid effective level of description. From this perspective, LEPP and DEPP become complementary effective theories defined over different cognitive state spaces.

## Autoregressive Models as Effective Theories of Cognition

The discussion so far has focused on diffusion models because they provide a natural mechanism for stochastic optimization over learned energy landscapes. Modern generative AI, however, is dominated by a second family of models based on **autoregressive generation**, most notably transformers and Large Language Models (LLMs). Although these systems are usually formulated probabilistically rather than energetically, recent theoretical work has shown that the two viewpoints are much more closely related than previously appreciated.

Autoregressive models are based on the chain rule of probability,

$$ p_W(y^1,\ldots,y^N|x,u,s)=\prod_{k=1}^{N}p_W(y^k|y^1,\ldots,y^{k-1},x,u,s). $$

Rather than modeling the complete joint distribution directly, the model predicts one output token at a time by estimating the conditional probability of the next token given all previous ones. Generation therefore proceeds sequentially,

$$ y^1 \rightarrow y^2 \rightarrow \cdots \rightarrow y^N, $$

until the complete sequence has been produced.

Although autoregressive models are usually expressed in terms of probabilities, every probability distribution defines an equivalent energy through

$$ E_W(y^k)=-\log p_W(y^k|y^1,\ldots,y^{k-1},x,u,s)+\text{constant}. $$

Consequently,

$$ p_W(y^k|y^1,\ldots,y^{k-1},x,u,s)=\frac{\exp[-E_W(y^k)]}{Z_W}, $$

where $Z_W$ is the corresponding partition function.

Autoregressive generation may therefore be interpreted as a sequence of local energy-minimization decisions. At each step the model selects a token lying in a relatively low-energy region conditioned on the previously generated sequence.

Unlike diffusion models, which optimize all variables simultaneously through stochastic relaxation, autoregressive models perform this optimization sequentially, one variable at a time. At first sight these approaches appear fundamentally different. Diffusion models optimize an entire state simultaneously, whereas autoregressive models appear to make irrevocable local decisions.

### Sequential Optimization and Global Coherence

A natural question therefore arises.

How can a model that commits to one token at a time nevertheless generate globally coherent sequences extending over hundreds or even thousands of tokens?

Recent theoretical work (see [Blondel et.al.](https://arxiv.org/pdf/2512.15605)) has shown that this apparent contradiction is largely illusory. Under appropriate assumptions, autoregressive models and energy-based models constitute mathematically equivalent representations of the same conditional probability distributions. Moreover, the conditional probabilities used for next-token prediction satisfy a recursion closely related to the **soft Bellman equation** from maximum-entropy reinforcement learning.

This provides an important conceptual insight. Each next-token prediction is not merely a locally optimal decision. Rather, the conditional probability of the next token already incorporates the model's expectations about all possible future continuations of the sequence. The autoregressive model therefore performs a form of implicit dynamic programming, where each local decision reflects the expected quality of future completions.

From this viewpoint, diffusion models and autoregressive models should be regarded as two different computational strategies for sampling from learned energy landscapes. Diffusion models perform stochastic optimization over an entire state simultaneously, whereas autoregressive models decompose the same optimization into a sequence of locally conditioned decisions whose probabilities implicitly encode future consequences.

This perspective helps explain why autoregressive language models exhibit remarkably coherent long-range behavior despite generating one token at a time.

---

## Implications for Computational Neuroscience

The interpretation developed throughout this paper suggests a different way of understanding the remarkable success of transformer-based language models.

We have argued that **LEPP** and **DEPP** represent two effective descriptions of cognition operating over different state spaces. LEPP models latent cognitive states explicitly, whereas DEPP models the observable evolution of perceptual states directly, absorbing the latent computations into its learned energy landscape.

Autoregressive language models occupy a position closely analogous to DEPP.

Rather than explicitly representing latent cognitive states, transformers learn the observable dynamics of **language states** directly. The hidden cognitive processes responsible for producing language are never modeled explicitly. Instead, their collective influence is absorbed into the learned probability—or equivalently, energy—landscape governing linguistic sequences.

The relationship between these models may therefore be summarized as follows.

| Model | Explicit State Variables | Hidden Dynamics Absorbed into the Model |
|---------|-------------------------|-----------------------------------------|
| **LEPP** | Latent cognitive states | Connectome |
| **DEPP** | Perceptual states | Latent cognition + connectome |
| **LLMs** | Language states | Thought dynamics + perception + connectome |

The important observation is that DEPP and transformer language models occupy **parallel positions** within the hierarchy of effective theories. Both abandon explicit latent-state representations in favor of directly modeling observable dynamics. They differ primarily in the modality over which those dynamics are defined: DEPP models perception, whereas LLMs model language.

Consequently, the success of transformer language models need not imply that transformer architectures resemble cortical circuits or that attention mechanisms correspond directly to biological computations. Their success may instead arise because they learn effective dynamical laws governing the evolution of language, just as DEPP learns effective dynamical laws governing the evolution of perceptual states.

This viewpoint is closely aligned with the effective-theory perspective developed throughout this paper. Statistical mechanics replaces microscopic molecular interactions with effective energy functions governing progressively more macroscopic variables. Likewise, LEPP, DEPP, and transformer language models replace increasingly detailed cognitive mechanisms with learned dynamical laws defined over different cognitive state spaces.

---

## Recovering Hidden Structure from Observable Behavior

If language is viewed as an observable projection of an underlying cognitive process, then training a language model becomes an inverse problem. The model never observes internal thought directly. Instead, it observes an enormous collection of linguistic projections generated by those hidden cognitive states.

Learning therefore consists of constructing an effective dynamical model capable of reproducing the observable evolution of language without explicitly reconstructing the hidden cognitive variables that generated it.

This perspective offers one possible explanation for the surprising capabilities of modern Large Language Models. Although they have no direct access to human thoughts or perceptual representations, they are exposed to an enormous number of observable consequences of those hidden cognitive processes. Given sufficiently diverse data and sufficiently expressive function approximators, much of the large-scale structure governing human linguistic behavior can be recovered indirectly.

The resulting representation should therefore not be interpreted as a mechanistic model of human cognition. Rather, it is an effective theory defined over language states. Just as DEPP absorbs latent perceptual dynamics into an energy landscape defined over perceptual states, transformer language models absorb latent thought dynamics into an effective model defined over linguistic states.

More generally, the success of modern generative AI suggests that complex systems often reveal considerably more information about their internal organization through their observable behavior than might initially be expected.

Many problems in physics involve recovering hidden structure from indirect observations. Tomographic reconstruction, inverse scattering, and system identification all infer unobservable internal properties from measurements made at the system's boundaries. Training a generative model may be viewed as a similar inverse problem. Rather than recovering neuronal connectivity directly, the model recovers an effective dynamical law governing the observable behavior produced by that connectivity.

The relationship proposed throughout this paper may therefore be summarized as follows.

| Biological System | Effective Theory |
|-------------------|------------------|
| Connectome | Microscopic implementation |
| Latent cognition | LEPP |
| Perceptual dynamics | DEPP |
| Language dynamics | Transformer / LLM |

The central lesson of modern generative AI is therefore not necessarily that artificial neural networks have discovered the architecture of the brain. Rather, they demonstrate that remarkably accurate models of highly complex systems can be learned directly from observable behavior without requiring explicit knowledge of the underlying microscopic implementation.

Viewed in this way, diffusion models, transformers, and related architectures should not be regarded as competing models of cortical circuitry. Instead, they represent complementary effective theories operating over different cognitive state spaces. Their significance lies less in their architectural resemblance to the brain than in their ability to recover the large-scale dynamical laws governing perception, language, and thought from observable behavior alone.

## From Effective Energy Functions to Neural Micro-Architecture

The central thesis of this paper is that modern generative AI models should be interpreted as **effective theories of cognition** rather than mechanistic models of neural circuitry. Throughout the paper, the primary scientific objective has been to infer an effective energy landscape from observable cognitive dynamics. This naturally raises a second inverse problem.

> **Given a learned effective energy function, what classes of microscopic neural architectures are capable of realizing it?**

This question differs fundamentally from the traditional goal of reconstructing the brain's connectome. Rather than seeking the unique neuronal circuitry responsible for cognition, it asks which families of neural architectures are consistent with the observed effective dynamics. We shall refer to this as the **realization problem** for cognitive energy landscapes.

At first sight, the answer appears discouraging. One of the central lessons of statistical mechanics is that an effective theory does not uniquely determine its microscopic realization. Many different molecular systems exhibit identical macroscopic behavior despite possessing entirely different microscopic interactions. Water, liquid helium, and liquid nitrogen, for example, differ dramatically in their constituent particles and intermolecular forces, yet their large-scale fluid dynamics are governed by essentially the same effective equations.

However, non-uniqueness does not imply the absence of microscopic information. Throughout physics, effective theories constrain the *class* of microscopic systems capable of realizing them. Different Hamiltonians may belong to the same universality class because they generate identical large-scale behavior. Likewise, many different neuronal architectures may produce equivalent effective energy landscapes despite differing substantially in their detailed connectivity.

The objective therefore shifts from identifying *the* connectome to identifying an **equivalence class of connectomes** that realize the same effective cognitive dynamics.

### Hopfield Networks as an Existence Proof

The existence of multiple microscopic realizations is not merely a theoretical possibility. An instructive example is provided by the development of modern Hopfield networks.

Classical Hopfield networks employed pairwise interactions between neurons, giving rise to relatively simple quadratic energy functions. Their architecture closely resembled spin-glass models from statistical mechanics and was biologically attractive because all interactions occurred between pairs of neurons.

Later work by Hopfield and Krotov demonstrated that considerably richer energy functions could be constructed while retaining biologically plausible pairwise neuronal interactions. Rather than introducing explicit higher-order synaptic interactions, they incorporated hidden variables whose collective dynamics generated a much more expressive effective energy function.

The resulting microscopic architecture differed substantially from the original Hopfield network, yet both implemented the same fundamental principle of energy minimization.

This observation illustrates an important general principle. A complicated effective energy landscape need not imply equally complicated direct interactions among the observable neurons. Much of the apparent complexity may instead be absorbed into hidden neuronal populations whose collective interactions generate the effective energy observed at the macroscopic level.

### Implications for Modern Generative AI

The same principle is likely to apply to the energy functions learned by modern generative AI systems.

Throughout this paper we have argued that diffusion models, transformers, and related architectures should be interpreted as parameterizations of effective energy landscapes rather than literal models of cortical circuitry. From this perspective, a transformer or diffusion model represents one possible realization of an effective dynamical law—not necessarily the realization employed by the brain.

It is therefore entirely plausible that many very different neural architectures—biological or artificial—could realize approximately the same effective energy landscape while possessing radically different microscopic organizations.

![](https://subirvarma.github.io/GeneralCognitics/images/stat96.png)

**Figure 11:** One possible realization of an effective energy landscape through a network of visible and hidden units interacting via biologically plausible pairwise connections. The realization is not unique; many different microscopic architectures may generate the same effective energy landscape.

### The Realization Problem

This viewpoint suggests a new research direction for computational neuroscience.

Rather than asking whether transformer layers, attention mechanisms, or diffusion processes literally exist within cortical circuitry, one may instead ask:

> **Which classes of biologically plausible neural architectures are capable of realizing the effective energy landscapes inferred from behavior?**

This question occupies an intermediate position between inverse statistical mechanics, realization theory in control systems, and computational neuroscience.

The problem is fundamentally one of realization rather than reconstruction. Observable behavior is first used to infer an effective energy landscape. The task then becomes to characterize the family of microscopic neural architectures capable of generating that landscape.

Symbolically, the program may be summarized as

$$
\text{Observable Dynamics}
\;\longrightarrow\;
\text{Effective Energy Landscape}
\;\longrightarrow\;
\text{Equivalence Class of Neural Architectures}.
$$

At present, very little is known about this correspondence. Whether a general theory of realizability exists remains an open question. Nevertheless, the effective-theory perspective developed throughout this paper suggests that this may prove to be a more fruitful direction than searching directly for architectural counterparts of transformers, attention mechanisms, or diffusion processes within the brain.

From this perspective, effective theories do not replace mechanistic neuroscience. Rather, they define the space within which mechanistic explanations should be sought. Their role is to identify the large-scale dynamical laws governing cognition and thereby constrain the family of microscopic neural architectures capable of implementing those laws.

# Conclusions

The central question addressed in this paper is how recent advances in generative artificial intelligence should be interpreted within computational neuroscience. Rather than asking whether transformers, diffusion models, or other neural-network architectures resemble the brain's anatomical circuitry, we have argued that these models are more naturally understood as **effective theories of cognition**. Like statistical mechanics in physics, their significance lies not in reproducing microscopic mechanisms but in discovering effective dynamical laws that govern observable behavior.

From this perspective, the remarkable success of modern generative AI is perhaps less surprising. A sufficiently expressive neural network need not recover the brain's connectome in order to model cognition successfully. Instead, it may learn an effective energy landscape that captures the observable evolution of perception, language, or thought, while leaving the underlying neuronal implementation unspecified.

Within this framework we introduced two complementary formulations of predictive processing.

The first, **Latent Energy-Based Predictive Processing (LEPP)**, reformulates predictive processing entirely within an energy-based computational framework while retaining its traditional latent-state representation. Predictive coding implements latent-state inference through local energy minimization, while temporal prediction is formulated as stochastic optimization over a learned energy landscape using diffusion-based energy models. Both computations are expressed within a common energy-minimization framework, providing a unified computational interpretation of predictive processing that is compatible with biologically plausible local learning.

The second formulation, **Direct Energy-Based Predictive Processing (DEPP)**, asks a different question. Rather than explicitly representing latent cognitive states, it models the observable evolution of perceptual states directly through a learned effective energy landscape. Importantly, DEPP does not deny the existence of latent internal representations. Instead, it explores whether those representations must appear explicitly within an effective computational theory or whether their collective influence can be absorbed into the learned energy landscape itself.

Viewed in this way, LEPP and DEPP should not be regarded as competing theories. Both are effective theories in the statistical-mechanical sense. They differ not in whether they are mechanistic, but in the state variables over which their effective dynamics are defined. LEPP constructs an effective theory over latent cognitive states, whereas DEPP constructs an effective theory over perceptual states. Likewise, transformer-based language models may be interpreted as parallel effective theories operating over language states. Together, these models suggest that cognition may admit multiple complementary effective descriptions, each appropriate for a different observable domain.

The effective-theory viewpoint also provides a different interpretation of the success of modern generative AI. The remarkable capabilities of diffusion models, transformers, and large language models need not imply that these architectures reproduce the organization of the cerebral cortex. Rather, they demonstrate that highly expressive function approximators can recover effective dynamical laws directly from observable behavior. Their learned parameters should therefore be interpreted not as models of neuronal circuitry but as compact representations of the energy landscapes governing the dynamics of perception, language, and cognition.

This perspective naturally suggests a different research program for computational neuroscience. Rather than searching for cortical implementations of transformer layers, attention mechanisms, or diffusion processes, one may first seek the effective dynamical principles governing cognition and then ask what classes of biological mechanisms are capable of realizing those principles. The realization problem introduced in this paper represents one possible formulation of this objective.

This viewpoint closely parallels David Marr's influential distinction between **computational**, **algorithmic**, and **implementation** levels of analysis. Marr argued that understanding a cognitive system requires answering three separate questions: *What computation is being performed? How is that computation carried out? And how is it physically implemented?* Importantly, the computational and algorithmic levels can often be understood without first identifying the underlying biological hardware. The perspective developed here suggests that modern generative AI provides a new family of computational and algorithmic models for cognition, while leaving open the question of their biological realization. Effective energy landscapes provide one possible mathematical language for expressing these higher levels of description.

The ideas developed throughout this paper suggest several open problems for future research.

**1. The Realization Problem**

Given a learned effective energy landscape, what classes of biologically plausible neural architectures are capable of realizing it? Rather than reconstructing the connectome uniquely, the goal is to characterize the equivalence class of neural micro-architectures consistent with the observed cognitive dynamics.

**2. Learning Effective Cognitive Dynamics**

Can effective energy landscapes be learned directly from large-scale neural recordings or behavioral data? Such models could provide a complementary alternative to detailed mechanistic simulations by focusing on the dynamical laws governing cognition rather than the underlying circuitry.

**3. Parallel Effective Theories**

The present work suggests that perception (DEPP) and language (LLMs) may represent parallel effective theories defined over different observable state spaces. An important question is whether similar effective theories can be constructed for motor control, auditory processing, social cognition, and other cognitive domains, and whether these models can ultimately be unified within a common energy-based framework.

**4. Planning, Imagination, and Reasoning**

The planning framework developed here suggests that perception, imagination, planning, dreaming, and counterfactual reasoning may all represent different operating modes of the same predictive world model. Understanding how these apparently distinct cognitive functions emerge from a common predictive architecture remains an important open problem.

**5. Connecting AI and Neuroscience**

Modern AI systems are typically compared according to their architectural components—transformers, diffusion models, recurrent networks, and so forth. The effective-theory viewpoint suggests an alternative comparison based on the energy landscapes these models learn. Two architectures with very different internal organizations may nevertheless implement remarkably similar effective cognitive dynamics.

**6. Experimental Tests**

The framework proposed here also suggests new experimental directions. Rather than searching directly for neural correlates of transformer attention or diffusion processes, one could attempt to infer effective energy landscapes from neural population recordings and compare these with the landscapes learned by modern generative AI systems. Such comparisons may provide a more meaningful bridge between artificial and biological intelligence than architectural similarity alone.

Ultimately, the principal contribution of modern generative AI to neuroscience may be methodological rather than architectural.

For much of its history, computational neuroscience has attempted to understand cognition by beginning with microscopic neural circuitry and working upward toward behavior. The perspective developed here suggests an alternative strategy. One may instead begin by learning the effective dynamical laws governing observable cognition and then ask what classes of neural architectures are capable of realizing those laws.

If this viewpoint proves fruitful, future computational neuroscience may come to resemble statistical mechanics more closely than traditional mechanistic modeling. The primary scientific objective would no longer be the direct reconstruction of the brain's circuitry, but the discovery of the effective dynamical principles that organize cognition across multiple levels of description.

Viewed in this way, the enduring lesson of modern generative artificial intelligence is not that it has discovered the architecture of the brain. Rather, it has demonstrated that highly accurate models of complex cognitive systems can be learned directly from observable behavior. The greatest contribution of generative AI to neuroscience may therefore be not a new model of the brain itself, but a new methodology for understanding cognition.
