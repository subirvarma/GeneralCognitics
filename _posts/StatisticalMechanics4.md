---
layout: default
title: " Generative AI as an Effective Theory of Cognition"
---

# Generative AI as an Effective Theory of Cognition

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

This paper argues that such comparisons may be taking place at the wrong level of description. We hypothesize that modern generative neural networks should be understood not as mechanistic models of neural implementation, but as effective theories of cognitive dynamics.

The history of physics provides a useful analogy. 
Thermodynamics provides an effective description of macroscopic matter without explicitly modeling every molecular interaction. 
Statistical mechanics explains why such effective descriptions are possible: the collective effects of microscopic molecular interactions can be summarized by a free-energy function that governs the macroscopic dynamics of the system.
Thermodynamics is therefore not a model of molecular structure, but an effective theory of its observable behavior.
This distinction between mechanistic and effective models is common throughout physics but has received comparatively little attention in computational neuroscience, where advances in AI are often interpreted in terms of architectural similarities to biological neural circuits.

![](https://subirvarma.github.io/GeneralCognitics/images/stat130.png) 

Figure 1: Proposed analogy between statistical mechanics and generative AI. Just as statistical mechanics provides an effective description of macroscopic matter without explicitly modeling every molecular interaction, modern generative neural networks may provide effective descriptions of cognitive dynamics without modeling the underlying neural circuitry.

We propose that modern generative neural networks should be interpreted in a similar manner. Rather than viewing transformers or diffusion models as candidate models of the brain's circuitry, we suggest viewing them as *effective theories of cognitive dynamics*. Their parameters should not be expected to correspond directly to neurons, synapses, or cortical microcircuits. Instead, they may be regarded as learning an effective energy landscape that captures the observable evolution of perception and thought. The underlying biological implementation—encoded in the brain's connectome and cellular physiology—remains hidden, just as microscopic molecular interactions remain hidden within thermodynamic descriptions.

This perspective has several consequences. First, it suggests that searching for direct anatomical counterparts of transformer blocks or diffusion networks may be misguided. Different microscopic implementations can generate remarkably similar macroscopic dynamics, a phenomenon familiar throughout statistical physics. Second, it provides a natural explanation for the success of modern generative AI. These models need not recover the brain's internal circuitry in order to reproduce important aspects of cognitive behavior; they need only learn the effective dynamical laws governing its observable outputs.

Building upon the predictive processing framework of Clark and the predictive coding formulations of Rao, Ballard, and Friston, we develop an alternative interpretation of perception based on energy-based dynamics. Rather than treating latent causes as the fundamental objects of inference, we explore the possibility that perceptual and cognitive states themselves evolve according to a learned energy landscape. Diffusion models provide a natural mathematical framework for describing such dynamics, allowing effective energy functions to be learned directly from observable behavior without requiring an explicit model of the underlying neuronal interactions.

The aim of this paper is not to argue that the brain literally implements a diffusion model or a transformer architecture. Rather, we argue that modern generative neural networks offer a new class of effective theories for cognition, analogous to the role played by statistical mechanics in physics. Viewed from this perspective, recent developments in generative AI suggest a shift in emphasis for computational neuroscience—from searching for detailed mechanistic replicas of neural circuitry toward identifying the effective dynamical principles that govern cognition.

Predictive processing provides the natural computational framework within which this proposal can be formulated. On this view, perception is not a passive reconstruction of sensory input. The brain continuously generates expectations about the state of the world and revises them in response to incoming sensory evidence. Perception therefore reflects an interaction between internally generated predictions and signals produced by the environment.

An important feature of this framework is its temporal character. The organism must not only estimate the present state of its environment, but also anticipate how that state is likely to evolve. Such predictions can guide perception, action, and—when extended over longer horizons—planning. The central question considered here is whether these predictive dynamics can be modeled directly as motion through a learned energy landscape, without requiring a detailed model of the neuronal circuitry that implements them.

We develop two energy-based formulations of this idea. The first, Latent Energy-Based Predictive Processing (LEPP), separates perception into three operations: inference of a latent state from sensory evidence, prediction of its subsequent state, and generation of a percept from that prediction. The second, Direct Energy-Based Predictive Processing (DEPP), dispenses with an explicitly specified latent-cause architecture and instead models the evolution of perceptual states directly through a learned energy function. The comparison between these models allows us to ask whether latent causes are necessary components of a computational theory or merely one possible factorization of a more general effective dynamics.

The next section summarizes the predictive-processing framework and clarifies the distinctions among perceptual inference, temporal prediction, action, and planning that will be used throughout the article.

## The Predictive Processing Framework in Computational Neuroscience

Predictive processing has emerged as one of the leading theoretical frameworks in contemporary computational neuroscience. Although its roots can be traced to Helmholtz's theory of unconscious inference, modern formulations by Rao and Ballard, Friston, Clark, and others have developed it into a quantitative framework for understanding perception, action, and learning.
It proposes that perception is fundamentally an active process of prediction rather than a passive registration of sensory signals.

The central insight is that an organism has direct access only to sensory signals generated at its sensory surfaces. These signals are noisy, incomplete, and inherently ambiguous. The computational problem facing the brain is therefore to construct a coherent estimate of the external world from this limited information. Predictive processing proposes that this is achieved by continuously combining internally generated predictions with incoming sensory evidence. Perception is therefore not a direct copy of the sensory input, but the result of an ongoing interaction between expectation and observation.

One consequence of this view is that the predictive model itself must be learned. Evidence for this comes from individuals whose vision is restored after congenital blindness or prolonged congenital cataracts. Although the retina and optic nerve may function normally following treatment, visual perception is initially severely impaired. Object recognition, depth perception, and scene understanding improve only gradually through experience. These observations suggest that retinal input alone is insufficient for mature visual perception. The brain must also acquire an internal model capable of interpreting sensory signals.

A second consequence is that perception becomes fundamentally temporal. Rather than merely estimating the current state of the world, the brain continuously predicts how the sensory environment will evolve over time. Incoming sensory information is compared with these predictions, and discrepancies are used to update the brain's internal model. When the environment changes only slowly, prediction errors remain small. Unexpected events generate larger prediction errors, forcing the internal model to adapt.

Figure 2 illustrates a simplified computational model of this process. The organism maintains an internal state that summarizes its current estimate of the world. This state is updated using incoming sensory information, used to predict its future evolution, and finally transformed into the conscious percept experienced by the organism. The prediction generated by this process is continuously compared with new sensory observations, producing an error signal that modifies the internal state and closes the perception loop.

![](https://subirvarma.github.io/GeneralCognitics/images/stat131.png) 

Figure 2: A model for sensory perception generation in the brain

An important implication of predictive processing is that much of what we perceive is generated internally rather than directly specified by sensory input. Sensory signals primarily indicate where the current prediction should be modified, while the detailed percept is constructed from the organism's learned internal model. This offers a natural explanation for the richness and continuity of conscious perception despite the relatively sparse and noisy information available from the sensory organs.

Predictive processing has also been extended beyond perception. The same internal model that predicts future sensory states can be used to evaluate the consequences of potential actions. During planning, the model is effectively run "open loop," allowing future scenarios to be simulated without requiring new sensory input. More generally, actions themselves can be viewed as another mechanism for reducing prediction error, either by changing the organism's internal model or by changing the external world so that it conforms more closely to the organism's predictions.

Although predictive processing has proved remarkably successful as a computational framework, an important modeling question remains. Most current formulations assume that the brain maintains latent internal variables representing the hidden causes responsible for sensory input. These latent variables are inferred from sensory evidence, evolved forward in time, and finally transformed into perceptual experience.

The motivation for introducing latent causes is that sensory input is both incomplete and ambiguous. Many different external situations can produce similar sensory signals, and the brain therefore seeks a representation that captures the underlying causes responsible for those observations. Latent variables provide one mathematical framework for representing these hidden causes. Classical predictive processing therefore formulates perception as inference over latent states rather than directly over sensory observations.

The present work asks whether this intermediate representation is fundamentally necessary. Instead of explicitly modeling latent causes, we investigate whether the observable dynamics of perception can be described directly by a learned energy landscape. From the perspective developed in the Introduction, these two alternatives correspond to different effective theories of cognition. The first retains the latent-state representation of classical predictive processing, while the second models perceptual dynamics directly. 
This distinction can be viewed as analogous to the distinction between microscopic and macroscopic descriptions in statistical physics. Classical predictive processing seeks to model the hidden causes underlying perception. The approach developed in this paper instead asks whether the observable evolution of perceptual states themselves admits an effective dynamical description, analogous to the role played by thermodynamics in physics.

The remainder of this paper explores two alternative energy-based formulations of this computational framework.

## Latent Energy-Based Predictive Processing (LEPP)

The previous section described predictive processing as a computational framework in which perception arises through the continual interaction between prediction and sensory evidence. The next question is how such a system might be implemented.

The **Latent Energy-Based Predictive Processing (LEPP)** architecture proposed here provides one possible computational realization of predictive processing. Its purpose is not to replace the classical predictive-processing framework, but to demonstrate that it can be reformulated entirely within an energy-based computational paradigm. LEPP retains the central assumption that perception proceeds through the inference of latent causes from sensory observations, while expressing every stage of the computation as an energy-minimization process.

![](https://subirvarma.github.io/GeneralCognitics/images/stat133.png)

**Figure 3:** The Latent Energy-Based Predictive Processing (LEPP) architecture.

A central idea of LEPP is that predictive processing naturally decomposes into **three distinct computational problems**, each requiring a different form of computation.

1. **Latent-state inference:** Estimate the latent state that best explains the current sensory observations.

2. **Temporal prediction:** Predict how that latent state is expected to evolve over time.

3. **Percept generation:** Convert the predicted latent state into the organism's conscious percept.

Although these three computations solve different problems, they all operate through the common principle of energy minimization. The inference and generation modules are implemented using predictive coding, while temporal prediction is implemented using a diffusion-based energy model. Consequently, the entire predictive-processing cycle can be viewed as a sequence of interacting energy-minimization processes rather than as a system trained through global error backpropagation.

An important distinction should be noted. The word *prediction* is used in two different senses within the predictive-processing literature. In **predictive coding**, prediction refers to estimating the latent causes responsible for the current sensory observations. In **predictive processing**, prediction refers to forecasting how the internal state of the organism will evolve over time. LEPP separates these two computations explicitly. Predictive coding performs inference over the current latent state, while the temporal prediction module models its future evolution.

The operation of LEPP is illustrated in Figure 3.

At time step $n$, a stream of sensory observations $s_n$ is processed by the inference module, producing the latent representation $z_n$. This latent state represents the organism's current estimate of the hidden causes responsible for the incoming sensory data.

The inferred latent state is then supplied to the temporal prediction module. Unlike the inference module, whose task is to explain the current sensory observations, the prediction module estimates how the latent representation is expected to evolve before the next sensory observation arrives. Rather than computing a deterministic prediction, the module performs stochastic sampling over a learned energy function

$$ E_W(x;z_n,u_{n+1}), $$

where $u_{n+1}$ denotes contextual variables such as intended actions or other factors influencing future environmental dynamics. The sampling process converges to a predicted latent state $x_{n+1}$ corresponding to a low-energy region of the learned energy landscape.

The predicted latent state is subsequently transformed into the organism's percept through the generative model

$$ y_{n+1}=p_\psi(x_{n+1}), $$

where $y_{n+1}$ denotes the predicted percept at the next instant.

When the next sensory observations $s_{n+1}$ become available, the predicted latent state $x_{n+1}$ serves as the initial estimate for the next inference cycle. Predictive coding then recursively updates this estimate until it converges to the refined latent state

$$ z_{n+1}=q_\phi(x_{n+1},s_{n+1}), $$

which becomes the input to the temporal prediction module for the following prediction cycle.

The complete computational flow may therefore be summarized as

$$ s_n \rightarrow z_n \rightarrow x_{n+1} \rightarrow y_{n+1}. $$

Each stage solves a distinct computational problem:

| Transformation | Computational task | Module |
|---------------|--------------------|--------|
| $s_n \rightarrow z_n$ | Infer the current latent state | Predictive Coding |
| $z_n \rightarrow x_{n+1}$ | Predict the future latent state | Diffusion-based Energy Model |
| $x_{n+1} \rightarrow y_{n+1}$ | Generate the predicted percept | Generative Model |

This decomposition is one of the principal features of LEPP. Classical predictive processing often treats perception as a single predictive process. LEPP instead separates **state estimation**, **state evolution**, and **percept generation** into distinct computational modules, allowing each problem to be implemented using the mathematical framework most naturally suited to it.

The model assumes that temporal prediction converges within the interval separating successive sensory observations. Consequently, inference, temporal prediction, perception, and learning proceed continuously and in parallel, producing a continually updated estimate of the organism's environment.

An attractive feature of LEPP is that perception and learning occur simultaneously. Each prediction cycle not only generates the organism's current percept but also provides training signals for all three computational modules. The inference model $q_\phi$, the temporal energy model $E_W$, and the generative model $p_\psi$ are therefore continuously refined as new sensory observations arrive. In this respect LEPP more closely resembles the continual online learning performed by biological nervous systems than the separate training and inference phases characteristic of most artificial neural networks.

The following sections develop these three modules in turn. We begin by showing how predictive coding provides a biologically plausible implementation of the inference and generation modules before turning to the diffusion-based energy model used for temporal prediction.

## Implementing the Inference and Generation Modules: Predictive Coding

The LEPP architecture introduced in the previous section consists of three computational modules: **latent-state inference**, **temporal prediction**, and **percept generation**. In this section we consider the first and third of these modules. We show that they can be naturally implemented using **predictive coding**, originally proposed by Rao and Ballard (1999). Predictive coding provides a biologically plausible mechanism for inferring latent causes from sensory observations using only local neural computations, making it a natural realization of the latent-state inference process assumed by LEPP.

![](https://subirvarma.github.io/GeneralCognitics/images/stat99.png)

Figure 4: Predictive coding architecture. Higher cortical areas generate top-down predictions of activity in lower areas, while lower areas return bottom-up prediction errors. Perception emerges through iterative reduction of these prediction errors.

Predictive coding assumes that the cortex is organized hierarchically. Each cortical level attempts to predict the activity of the level immediately below it. The lower level compares this prediction with its actual activity and sends only the resulting prediction error back upward. Consequently, information flows in two directions through the hierarchy: predictions propagate downward, while prediction errors propagate upward. Through repeated interactions the hierarchy converges to a mutually consistent interpretation of the sensory input.

For a two-level hierarchy, the generative model can be written as

$$ z^{(2)} \rightarrow z^{(1)}\rightarrow y. $$

Here $y$ denotes the sensory activity (for example retinal or LGN responses), $z^{(1)}$ represents lower-level cortical features such as V1-like responses, and $z^{(2)}$ represents higher-level latent causes corresponding to more abstract visual structure. Throughout this section the inference process is assumed to occur within a single sensory interval, so the temporal index has been omitted for clarity. The highest-level representation $z^{(2)}$ corresponds to the latent state $z_n$ introduced in the LEPP architecture.

Suppose that level $l$ predicts the activity of the level immediately below according to

$$ \hat z^{(l-1)} = f_l(z^{(l)}), $$

where $f_l(\cdot)$ is the learned generative mapping. The prediction error at the lower level is therefore

$$ \epsilon_{l-1} = z^{(l-1)} - f_l(z^{(l)}), $$

while the sensory prediction error is

$$ \epsilon_0 = s - f_1(z^{(1)}), $$

where $s$ denotes the sensory input.

The objective of predictive coding is to adjust the latent representations so that these prediction errors are minimized throughout the hierarchy. Each latent representation therefore evolves under the influence of two competing constraints: it must explain the activity of the level below while remaining consistent with the prediction supplied by the level above. Perception corresponds to the equilibrium reached when these competing influences balance.

### Bayesian Interpretation

Predictive coding can be derived directly from Bayesian inference.

For simplicity, consider a single latent representation $z$ generating a sensory observation $y$. Bayes' rule gives

$$ p(z|y) = \frac{p(y|z)p(z)}{p(y)}. $$

Since $p(y)$ is constant with respect to $z$,

$$
z^* = \arg\max_z \left[\log p(y|z)+\log p(z)\right],  $$

which is the familiar Maximum A Posteriori (MAP) estimate.

Assume the sensory observation is generated according to

$$ y = f(z) + \epsilon, $$

where

$$ \epsilon \sim \mathcal N(0,\Sigma_y). $$

Then

$$ -\log p(y|z) = {1\over 2} (y-f(z))^T \Sigma_y^{-1} (y-f(z)). $$

Defining the sensory prediction error

$$ \epsilon_y = y-f(z), $$

the likelihood term becomes

$$ {1\over 2}\epsilon_y^T\Pi_y\epsilon_y, $$

where

$$ \Pi_y = \Sigma_y^{-1} $$

is the sensory precision matrix.

Similarly, assuming a Gaussian prior

$$
z \sim\mathcal N(\mu_z,\Sigma_z), $$

the prior contributes

$$ {1\over 2}\epsilon_z^T\Pi_z\epsilon_z,$$

where

$$ \epsilon_z = z-\mu_z. $$

The negative log posterior is therefore

$$ E_{PC}(z) = {1\over 2}\epsilon_y^T\Pi_y\epsilon_y + {1\over 2}\epsilon_z^T\Pi_z\epsilon_z. $$

This expression has a natural interpretation as an **energy function**. Inferring the latent representation is therefore equivalent to minimizing this energy.

### Local Energy Minimization

The latent representation is updated according to

$$ z \leftarrow z - \eta\frac{\partial E_{PC}}{\partial z}, $$

giving

$$ - \frac{\partial E_{PC}}{\partial z} = \left(\frac{\partial f}{\partial z}\right)^T\Pi_y\epsilon_y + \Pi_z\epsilon_z.  $$

The first term is driven by bottom-up sensory prediction error and encourages the latent state to better explain the observations. The second term is driven by top-down expectations encoded by the prior.

Although this resembles ordinary gradient descent, an important feature of predictive coding is that the required information is entirely local. Each cortical area requires only its own activity, the prediction arriving from the level above, and the prediction error arriving from the level below. The global optimization therefore decomposes into a collection of local computations that can plausibly be implemented by recurrent cortical circuitry.

For the linear model originally considered by Rao and Ballard,

$$ y = Wz + \epsilon, $$

the update simplifies to

$$ - \frac{\partial E_{PC}}{\partial z} = W^T\Pi_y\epsilon_y + \Pi_z\epsilon_z. $$

### Extension to Hierarchical Representations

The same derivation extends naturally to multiple cortical levels

$$ z^{(L)} \rightarrow\cdots\rightarrow z^{(2)}\rightarrow z^{(1)}\rightarrow y. $$

Each level predicts the activity below according to

$$ z^{(l-1)} = f_l(z^{(l)}) + \epsilon_l, $$

and the complete energy becomes

$$
E_{PC} = \sum_l {1\over 2}\epsilon_{l-1}^T\Pi_{l-1}\epsilon_{l-1}. $$

Every latent representation participates in two prediction relationships: it is predicted by the level above while simultaneously predicting the level below. Consequently, each latent state is updated using both top-down and bottom-up prediction errors until the hierarchy converges to a consistent explanation of the sensory input.

### Learning the Generative Model

Predictive coding performs not only inference but also continual learning.

The latent representations correspond to neuronal activity, while the parameters of the generative mappings are encoded in synaptic strengths. During perception the latent representations rapidly change to minimize prediction error. At the same time, synaptic weights evolve more slowly according to local Hebbian-style learning rules. For the linear model the weight update is

$$ -\frac{\partial E_{PC}}{\partial W_l} = \Pi\left(z^{(l-1)} - W_lz^{(l)}\right)z^{(l)T}.$$

The change in each synapse depends only on locally available quantities: presynaptic activity and postsynaptic prediction error. Consequently, inference and learning occur simultaneously during normal operation of the network rather than as separate phases.

### Role within LEPP

Predictive coding therefore provides a biologically plausible implementation of the inference and percept-generation components of the LEPP architecture. Bayesian inference is reformulated as the minimization of a local energy function, allowing latent representations to emerge through recurrent interactions within the cortical hierarchy.

An important limitation, however, is that predictive coding is fundamentally a model of **state inference**. It explains how the brain estimates the latent state responsible for current sensory observations, but it does not specify how those latent states evolve over time. Within the LEPP architecture this second problem is solved by the temporal prediction module, which we develop in the next section using diffusion-based energy models.

## Temporal Prediction as Energy Minimization

The previous section described how predictive coding can be used to infer the latent state $z_n$ responsible for the current sensory observations. The remaining component of the LEPP architecture is the **temporal prediction module**, whose task is to estimate the latent state expected at the next instant.

Unlike predictive coding, this is fundamentally a problem of **dynamical modeling** rather than state estimation. Given the current latent state $z_n$, together with contextual variables $u_{n+1}$ such as intended actions, the prediction module must learn the conditional probability distribution

$$ p(x_{n+1}|z_n,u_{n+1}). $$

Rather than predicting a single deterministic future state, we propose to represent this conditional distribution using an **Energy-Based Model (EBM)**,

$$ p_W(x|z,u)=\frac{\exp[-E_W(x;z,u)]}{Z_W}, $$

where $E_W(x;z,u)$ is a learned energy function parameterized by $W$, and

$$ Z_W=\int e^{-E_W(x;z,u)}dx $$

is the partition function.

The energy function defines an effective energy landscape over future latent states. States of low energy correspond to highly probable future predictions, while states of high energy correspond to unlikely futures. Rather than predicting one future explicitly, the model therefore represents an entire probability distribution over possible futures.

This formulation is closely related to the effective-theory viewpoint introduced in the Introduction. The prediction module does not attempt to model the microscopic interactions between neurons. Instead, it learns an effective energy landscape whose minima capture the observable evolution of the brain's latent representations.

![](https://subirvarma.github.io/GeneralCognitics/images/stat83.png)

**Figure 5:** Learning an effective energy landscape for temporal prediction using a neural network function approximator.

A sufficiently expressive function approximator, such as a Transformer or Diffusion Transformer (DiT), can be trained to approximate the unknown energy function directly from observed latent-state trajectories. In this way, the microscopic details of the underlying neural circuitry are replaced by an effective dynamical description of latent-state evolution.

This viewpoint closely parallels statistical mechanics. Statistical mechanics does not simulate every molecular interaction individually, but instead models the macroscopic behavior of matter through an effective free-energy landscape. Similarly, the prediction module bypasses the intractable problem of modeling the brain's connectome by directly learning an effective energy function governing latent-state dynamics.

---

## Sampling Future Latent States Using Diffusion Models

Once the energy function has been learned, the remaining problem is to generate samples from the conditional distribution

$$ p_W(x|z,u). $$

This is itself an optimization problem. Beginning from an initial state, the system must evolve toward regions of lower energy until a probable future latent state is reached.

In biological systems such optimization may occur through the direct interactions of large populations of neurons. In machine learning, an efficient approximation is provided by **diffusion models**, which implement stochastic energy minimization through Langevin dynamics.

![](https://subirvarma.github.io/GeneralCognitics/images/stat122.png)

**Figure 6:** Temporal prediction using stochastic energy minimization. Starting from a noisy initial state, Langevin dynamics progressively moves the system toward lower-energy latent states.

The sampling procedure begins from a high-noise initial condition and gradually reduces the noise level over a sequence of diffusion stages. At each stage several Langevin updates are performed,

$$ x(t,k+1)=x(t,k)-\eta\nabla_xE_W(x(t,k),t,z_n,u_{n+1})+\sqrt{2\eta}\,\epsilon, $$

where

$$ \epsilon\sim\mathcal N(0,I). $$

The injected noise prevents the dynamics from becoming trapped in poor local minima while allowing the system to explore multiple possible futures. As the diffusion process proceeds, the noise level is gradually reduced, causing the latent state to settle into progressively lower-energy regions of the learned energy landscape.

![](https://subirvarma.github.io/GeneralCognitics/images/stat123.png)

**Figure 7:** One Langevin update within a diffusion stage.

Although diffusion models are often described as denoising algorithms, they may equally be interpreted as stochastic optimization algorithms operating on an energy landscape. Throughout this paper we adopt the latter viewpoint because it connects naturally with predictive coding, where inference likewise proceeds by minimizing an energy function.

Notice the close analogy between the two modules of LEPP.

Predictive coding minimizes an energy function

$$ E_{PC}, $$

whose equilibrium estimates the current latent state responsible for the sensory observations.

The diffusion prediction module minimizes a different energy function

$$ E_W, $$

whose equilibrium predicts the latent state expected at the next instant.

The LEPP architecture therefore decomposes predictive processing into two complementary energy-minimization problems:

- **State inference:** estimating the current latent state using predictive coding.
- **State prediction:** estimating the future latent state using diffusion-based stochastic optimization.

Both modules operate through local energy minimization while solving fundamentally different computational problems.

### Learning the Prediction Energy

Learning the prediction module consists of estimating the parameters of the conditional energy function

$$ E_W(x;z,u). $$

Unlike predictive coding, which receives the current sensory observations directly, the prediction module learns by comparing its predicted latent state with the latent state inferred after the next sensory observation arrives.

Suppose that after predicting $x_{n+1}$, the inference module computes the corrected latent state $z_{n+1}$. The pair

$$ (z_n,u_{n+1},z_{n+1}) $$

then provides a supervised training example describing the true temporal dynamics of the latent space.

The parameters $W$ are learned by maximizing the conditional log-likelihood

$$ L(W)=E_{p(x|z,u)}[\log p_W(x|z,u)]. $$

Using the Boltzmann representation, the resulting gradient becomes

$$ \nabla_WL(W)=-E_{\text{data}}[\nabla_WE_W]+E_{\text{model}}[\nabla_WE_W]. $$

The first expectation is evaluated using latent-state transitions inferred from sensory experience, while the second is evaluated using samples generated by the prediction model itself. Consequently, the prediction module continuously compares its own imagined futures with the futures subsequently observed, gradually refining its energy landscape through experience.

This learning rule is directly analogous to the learning rules used for classical Boltzmann machines. If the microscopic neural interactions were explicitly known, Hebbian learning would emerge as a special case. Since the brain's connectome is unknown, however, the energy function is instead approximated using a neural network function approximator, while modern diffusion-learning algorithms such as Diffusion Recovery Likelihood (DRL) provide efficient procedures for estimating its parameters.

## Biological Interpretation of LEPP

An important question is whether the computations required by the LEPP architecture admit biologically plausible implementations. The answer depends on the level of description at which the model is interpreted. LEPP is not intended as a literal reconstruction of the brain's neuronal circuitry. Rather, it should be viewed as an effective computational model of the dynamical processes underlying perception.

The LEPP architecture consists of two principal computational components: the latent-state inference module and the temporal prediction module. Both are formulated as energy-minimization processes, but they operate on different aspects of the perceptual computation.

### Biological Plausibility of Predictive Coding

There is considerable evidence supporting the biological plausibility of the predictive-coding component of LEPP. Indeed, predictive coding was originally proposed by Rao and Ballard as a computational model of cortical processing. As shown in the previous section, both inference and learning can be formulated as local energy-minimization processes. Each cortical area communicates only with neighboring levels in the hierarchy through top-down predictions and bottom-up prediction errors, while synaptic plasticity depends only on locally available neuronal activity and prediction errors. Consequently, neither inference nor learning requires global error backpropagation, making predictive coding considerably more compatible with known cortical circuitry than conventional deep-learning algorithms.

### Biological Interpretation of the Prediction Module

The temporal prediction module proposed in LEPP is based on an energy-based model whose predictions are generated through stochastic sampling. This should not be interpreted as a claim that the brain literally implements a diffusion model or Langevin dynamics. Rather, the diffusion model provides an effective computational description of a more general physical process.

The brain contains a vast network of recurrently connected neurons whose detailed connectivity remains largely unknown. As sensory information arrives, neuronal activity moves away from its previous equilibrium state and gradually relaxes toward a new stable configuration corresponding to the updated perceptual state. The diffusion model performs an analogous computation by allowing stochastic dynamics to evolve over a learned energy landscape until a low-energy state is reached.

The two systems therefore differ in their microscopic implementation while sharing a common macroscopic objective: both evolve toward equilibrium states determined by an underlying energy function. The diffusion model achieves this through stochastic sampling over a learned energy landscape, whereas the brain presumably achieves it through the collective interactions of large populations of neurons. LEPP makes no claim that these microscopic mechanisms are identical. Rather, it proposes that they may represent different implementations of the same effective dynamical process.

Learning in the prediction module admits a similar interpretation. When the underlying interaction graph is explicitly known, maximum-likelihood learning reduces to local update rules closely related to Hebbian plasticity. Since the detailed architecture of the brain's connectome is unknown, however, the energy function is instead represented using a neural-network function approximator. The resulting model should therefore be regarded as an effective description of cortical dynamics rather than a mechanistic reconstruction of neuronal circuitry.

### LEPP as an Effective Theory

The principal lesson of LEPP is methodological rather than architectural. The objective is not to reproduce the detailed structure of the brain's connectome, but to identify the effective dynamical principles governing perceptual evolution. This distinction is familiar throughout physics. Thermodynamics successfully predicts the behavior of macroscopic systems without explicitly modeling every molecular interaction. Likewise, LEPP models the effective energy landscape governing latent perceptual dynamics without requiring an explicit model of the underlying neuronal circuitry.

Viewed in this way, LEPP demonstrates that predictive processing can be reformulated entirely within an energy-based computational framework while preserving its central latent-state representation. This naturally raises a further question. If the objective is to model the effective dynamics of perception rather than its microscopic implementation, is the explicit latent-state representation itself a necessary component of the theory?

The next section explores this possibility by proposing a second effective model of perception—**Direct Energy-Based Predictive Processing (DEPP)**—which dispenses with an explicitly modeled latent-state architecture and instead describes the observable evolution of perceptual states directly through a learned energy landscape.

## Direct Energy-Based Predictive Processing (DEPP)

The LEPP architecture developed in the previous sections demonstrates that classical predictive processing can be reformulated entirely within an energy-based computational framework while preserving its central assumption that perception proceeds through the inference of latent causes.

This naturally raises a more fundamental question.

If the objective is to construct an **effective theory of cognition** rather than a mechanistic reconstruction of neural circuitry, is the explicit latent-state representation itself necessary?

The **Direct Energy-Based Predictive Processing (DEPP)** model explores this possibility. Rather than explicitly modeling latent-state inference, temporal prediction, and percept generation as separate computational processes, DEPP models the observable dynamics of perceptual states directly through a learned energy landscape.

It is important to emphasize what DEPP does **not** claim. DEPP does not argue that latent causes do not exist, nor that the brain lacks internal representations. Instead, it asks whether an effective theory of perceptual dynamics must explicitly represent those latent variables, or whether their collective effects can be absorbed into a single learned energy function defined directly over perceptual states.

![](https://subirvarma.github.io/GeneralCognitics/images/stat127.png)

**Figure 8:** Direct Energy-Based Predictive Processing (DEPP).

The DEPP architecture predicts the next perceptual state directly from the current perceptual state, previous sensory observations, and contextual variables such as intended actions. Instead of operating in latent space, prediction occurs directly within perceptual state space.

The model represents the conditional distribution of future perceptual states using the energy function

$$ p_W(y_{n+1}|y_n,s_n,u_{n+1})=\frac{\exp[-E_W(y_{n+1};y_n,s_n,u_{n+1})]}{Z_W}. $$

Prediction proceeds by stochastic sampling over this learned energy landscape using the same diffusion-based optimization procedure introduced for the temporal prediction module in LEPP.

Unlike LEPP, the energy function is now required to capture the complete dynamics of perception. The complexity of latent-state inference has not disappeared. Rather, it has been absorbed into the learned energy landscape itself. Latent variables therefore become an implicit property of the energy function rather than an explicit component of the computational architecture.

### Perceptual Dynamics as Motion on an Energy Landscape

The operation of DEPP may be understood by considering how the effective energy landscape evolves through time.

Suppose that at time step $n+1$ the perceptual state is given by

$$ y_{n+1}=y'. $$

This state corresponds to a local minimum of the energy landscape

$$ E_W(y;y_n,u_{n+1},s_n). $$

When new sensory observations $s_{n+1}$ arrive and the organism selects its next action $u_{n+2}$, the effective energy landscape changes to

$$ E_W(y;y',u_{n+2},s_{n+1}). $$

The previous perceptual state $y'$ is no longer, in general, an equilibrium of the new landscape. The system therefore evolves through stochastic energy minimization until it reaches a new low-energy state,

$$ y_{n+2}=y'', $$

which becomes the organism's next percept.

![](https://subirvarma.github.io/GeneralCognitics/images/stat125.png)

**Figure 9:** Evolution of the effective energy landscape as sensory observations and planned actions change through time.

Each new sensory observation and planned action therefore modifies the energy landscape governing perception. The current perceptual state becomes energetically unstable, triggering interactions that drive the system toward a new equilibrium. In DEPP, perception is interpreted as this continual process of stochastic relaxation over a changing energy landscape.

### DEPP as an Effective Theory

The principal conceptual difference between LEPP and DEPP is not the learning algorithm but the level of scientific description.

LEPP explicitly factorizes perception into three computational stages:

- inference of latent causes,
- temporal prediction of latent states,
- generation of perceptual experience.

DEPP instead absorbs this entire factorization into a single effective energy function defined directly over perceptual states.

| **LEPP** | **DEPP** |
|-----------|----------|
| Explicit latent-state representation | No explicit latent-state representation |
| Separate inference and prediction modules | Unified energy landscape |
| Two energy functions ($E_{PC}$ and $E_W$) | Single effective energy function |
| Decoder required | Decoder unnecessary |
| Latent causes represented explicitly | Latent causes implicit within the learned energy landscape |

This does not imply that latent causes are absent. Rather, DEPP proposes that they need not appear explicitly in the effective theory. Their influence is incorporated into the learned energy landscape, which captures the observable dynamics of perception directly.

Learning proceeds in essentially the same manner as in the LEPP prediction module. After each prediction, the observed perceptual transition

$$ (y_n,s_n,u_{n+1},y_{n+1}) $$

provides a training example for refining the energy function through maximum-likelihood estimation. If the microscopic interaction graph were explicitly known, this learning process would reduce to local Hebbian-style update rules. Since the connectome remains largely unknown, however, the energy landscape is instead approximated using a neural-network function approximator trained using modern energy-based learning algorithms such as Diffusion Recovery Likelihood (DRL).

### Levels of Scientific Description

The distinction between LEPP and DEPP closely parallels the distinction between statistical mechanics and thermodynamics.

LEPP seeks to explain perceptual dynamics by explicitly modeling latent internal variables whose interactions give rise to perception.

DEPP instead models the observable evolution of perceptual states themselves through an effective energy landscape.

Neither description necessarily invalidates the other. Rather, they address different scientific questions.

LEPP asks:

> *How are latent causes inferred and propagated through time?*

DEPP asks:

> *What effective dynamical law governs the evolution of perceptual states?*

This distinction reflects the central theme developed throughout the paper. Just as thermodynamics successfully predicts macroscopic physical behavior without explicitly modeling every molecular interaction, DEPP proposes that the observable dynamics of perception may admit an effective description that does not require an explicit model of either the brain's connectome or its latent-state representations.

From this perspective, latent-state models and direct energy-based models should not necessarily be viewed as competing theories. Rather, they represent complementary descriptions of cognition at different levels of abstraction.

## Planning as Open-Loop Prediction

The prediction modules developed in the LEPP and DEPP architectures were introduced as mechanisms for predicting the immediate future during perception. Their significance, however, extends far beyond perceptual inference. Once a predictive model of the world has been learned, exactly the same model can be used to simulate hypothetical future scenarios without requiring new sensory input. This process constitutes the basis of planning.

During normal perception the prediction module operates in **closed loop**. Each prediction is immediately compared with incoming sensory observations, and the resulting prediction error is used to refine both the current perceptual state and the parameters of the prediction model. Through continual interaction with the environment, the model gradually learns the dynamical laws governing perceptual evolution.

Planning differs only in how this learned model is used. Instead of receiving continual sensory feedback, the prediction module operates **open loop**, repeatedly generating hypothetical future states conditioned on proposed actions. The resulting sequence of predicted perceptual states allows the organism to evaluate possible courses of action before interacting with the external world.

![](https://subirvarma.github.io/GeneralCognitics/images/stat118.png)

**Figure 10:** Planning in the LEPP framework. During perception the prediction module operates in closed loop using continual sensory feedback. During planning the same prediction module is run open loop, generating hypothetical future trajectories conditioned on candidate actions.

Within the LEPP architecture, planning begins from the currently inferred latent state $z_n$. Given a candidate action $u_{n+1}$, the prediction module estimates the next latent state

$$ x_{n+1}\sim p(x_{n+1}|z_n,u_{n+1}). $$

The predicted latent state is then converted into the corresponding percept through the generative model. This predicted percept becomes the starting point for the next prediction, allowing the system to simulate an entire sequence of hypothetical future experiences without requiring additional sensory observations.

The same principle applies to DEPP.

![](https://subirvarma.github.io/GeneralCognitics/images/stat128.png)

**Figure 11:** Planning in the DEPP framework.

Because DEPP predicts perceptual states directly, the prediction module simultaneously performs both prediction and percept generation. Starting from the current perceptual state, successive applications of the learned energy model generate hypothetical future perceptual trajectories conditioned on candidate actions. In this sense, the learned energy landscape functions as a **world model**, allowing the organism to mentally simulate future interactions with its environment.

The principal difference between perception and planning is therefore not architectural but operational. Both rely on exactly the same learned predictive model. During perception the model continually incorporates sensory observations, while during planning it evolves autonomously to explore possible future trajectories.

### Choosing Actions

Planning requires more than predicting future states; it also requires selecting actions.

One widely studied approach is **Reinforcement Learning (RL)**, in which the objective is to choose the sequence of actions that maximizes expected cumulative reward. Within this framework, the learned prediction model serves as a world model that allows the agent to evaluate hypothetical future trajectories before committing to an action. Modern model-based reinforcement learning systems make extensive use of this principle.

An alternative formulation is provided by **Active Inference**, developed by Karl Friston. Rather than maximizing reward, Active Inference proposes that organisms choose actions that minimize expected variational free energy. Although the optimization objective differs from reinforcement learning, both frameworks rely on the existence of an internal predictive model capable of simulating future trajectories.

From the perspective developed in this paper, these approaches differ primarily in the objective used to evaluate predicted futures rather than in the mechanism used to generate them. In both cases the essential computational requirement is the same: a learned model capable of predicting how perceptual states evolve under different actions.

### Planning as a Consequence of Predictive Processing

The discussion above suggests that planning is not an independent cognitive process but a natural extension of predictive processing itself.

During perception, the prediction module is continually trained using sensory feedback, gradually learning the effective dynamical laws governing the organism's environment. Once this model has been acquired, it can be run in open loop to simulate hypothetical futures, evaluate alternative actions, and guide behavior.

Viewed in this way, perception and planning become two modes of operation of the same underlying predictive architecture. Perception uses the world model to estimate the present in the presence of continual sensory feedback. Planning uses the same world model to explore possible futures in the absence of sensory input.

This interpretation further reinforces the central theme of the paper. The prediction modules developed in LEPP and DEPP should not be viewed merely as mechanisms for predicting the next perceptual state. They constitute learned **effective models of environmental dynamics**, capable of supporting both perception and planning without requiring an explicit model of the underlying neuronal circuitry.

## Autoregressive Models as Effective Theories of Cognition

The discussion so far has focused on diffusion models because they provide a natural mechanism for stochastic optimization over learned energy landscapes. Modern generative AI, however, is dominated by a second family of models based on **autoregressive generation**, most notably transformers and Large Language Models (LLMs). Although these systems are usually formulated probabilistically rather than energetically, they admit a closely related interpretation.

Autoregressive models are based on the chain rule of probability,

$$ p_W(y^1,\ldots,y^N|x,u,s)=\prod_{k=1}^{N}p_W(y^k|y^1,\ldots,y^{k-1},x,u,s). $$

Rather than modeling the complete joint distribution directly, the model predicts one output token at a time by estimating the conditional probability of the next token given all previous ones. Generation therefore proceeds sequentially, sampling

$$ y^1 \rightarrow y^2 \rightarrow \cdots \rightarrow y^N $$

until the complete sequence has been produced.

Although autoregressive models are usually expressed in terms of probabilities, every probability distribution defines an equivalent energy through

$$ E_W(y^k)=-\log p_W(y^k|y^1,\ldots,y^{k-1},x,u,s)+\text{constant}. $$

Consequently,

$$ p_W(y^k|y^1,\ldots,y^{k-1},x,u,s)=\frac{\exp[-E_W(y^k)]}{Z_W}, $$

where $Z_W$ is the corresponding partition function.

From this perspective, autoregressive generation may be interpreted as a sequence of local energy-minimization decisions. At each step the model chooses a token that lies in a region of relatively low energy conditioned on the previously generated sequence. Unlike diffusion models, which optimize all variables simultaneously through stochastic relaxation, autoregressive models perform this optimization incrementally, one token at a time.

The two approaches therefore represent different computational strategies for sampling from complex probability distributions rather than fundamentally different probabilistic models.

### Implications for Computational Neuroscience

This interpretation suggests a different way of viewing the remarkable success of transformer-based language models.

Their success need not imply that transformer architectures resemble cortical circuits or that attention mechanisms correspond directly to biological neural computations. Instead, transformers may be regarded as highly expressive parameterizations of effective cognitive dynamics. Their parameters encode statistical regularities governing linguistic behavior rather than explicit models of neuronal connectivity.

This viewpoint is closely aligned with the effective-theory perspective developed throughout this paper. Statistical mechanics successfully predicts the behavior of gases, liquids, and solids without explicitly modeling every molecular interaction. Likewise, autoregressive language models successfully reproduce many statistical regularities of human language without explicitly modeling the brain's connectome.

If language is viewed as one observable projection of an underlying cognitive process, then training a language model becomes an inverse problem. Rather than observing internal cognitive states directly, the model observes a vast collection of linguistic projections generated by those states. By learning the statistical structure of these observable outputs, the model is able to construct an effective representation sufficient to predict future linguistic behavior.

This perspective offers one possible explanation for the surprising capabilities of modern Large Language Models. Although they have no direct access to human thoughts or perceptual representations, they are exposed to an enormous number of observable consequences of those hidden cognitive processes. With sufficiently diverse data and sufficiently expressive function approximators, much of the large-scale structure governing human linguistic behavior can be recovered indirectly.

The resulting representation should therefore not be interpreted as a mechanistic replica of human cognition. Rather, it is an effective theory learned entirely from observable behavior. Like thermodynamics, it does not reveal the microscopic implementation of the system it describes. Instead, it captures those large-scale dynamical regularities that are necessary for accurate prediction.

### Recovering Hidden Structure from Observable Behavior

The success of modern generative AI suggests a broader methodological principle. Complex systems often reveal far more information about their internal organization through their observable behavior than might initially be expected.

Many problems in physics involve recovering hidden structure from indirect observations. Tomographic reconstruction, inverse scattering, and system identification all infer unobservable internal properties from measurements made at the system's boundaries. Training a generative model may be viewed as a similar inverse problem. Rather than recovering neuronal connectivity directly, the model recovers an effective dynamical law governing the observable behavior produced by that connectivity.

From this perspective, the relationship proposed throughout this paper may be summarized as

| **Brain** | **Effective Model** |
|-----------|---------------------|
| Connectome | Unknown microscopic dynamics |
| Cognitive dynamics | Effective energy landscape |
| Speech, text, and behavior | Observable projections |
| Generative AI model | Learned effective theory |

The central lesson of modern generative AI is therefore not necessarily that artificial neural networks have discovered the architecture of the brain. Rather, they demonstrate that remarkably accurate models of highly complex systems can be learned directly from observable behavior, without requiring explicit knowledge of the underlying microscopic implementation.

Viewed in this way, transformers, diffusion models, and related architectures should be regarded not as competing models of cortical circuitry, but as increasingly powerful parameterizations of effective cognitive dynamics. Their significance lies less in their architectural resemblance to the brain than in their ability to recover the large-scale laws governing perception, language, and thought from observable data alone.

Connectome
      │
      ▼
Effective Energy
      │
      ▼
Observable Dynamics

## From Effective Energy Functions to Neural Micro-Architecture

The central thesis of this paper is that modern generative AI models should be interpreted as **effective theories of cognition** rather than mechanistic models of neural circuitry. This naturally raises an interesting question.

If a learned energy function provides an accurate effective description of perceptual or cognitive dynamics, does it contain any information about the microscopic neural architecture that generated those dynamics?

At first sight the answer appears to be negative. One of the central lessons of statistical physics is that many different microscopic systems may exhibit identical macroscopic behavior. Water, liquid helium, and liquid nitrogen possess very different microscopic constituents, yet their large-scale fluid dynamics are described by essentially the same equations. Effective theories therefore do not uniquely determine the microscopic mechanisms that produce them.

Nevertheless, effective theories often constrain the class of microscopic systems capable of realizing them. In condensed-matter physics, many different Hamiltonians belong to the same universality class because they produce identical large-scale behavior. Similarly, different neuronal architectures may give rise to equivalent effective energy landscapes even though their microscopic connectivity differs substantially.

This observation suggests an intriguing research direction. Rather than attempting to recover the brain's connectome uniquely from a learned energy function, it may be possible to characterize the family of neural architectures capable of realizing that energy function.

Some insight into this problem comes from the development of modern Hopfield networks. Classical Hopfield networks employed pairwise interactions between neurons and consequently possessed relatively simple quadratic energy functions. Later work by Hopfield and Krotov demonstrated that much richer energy functions could be constructed by introducing hidden variables, dramatically increasing the representational capacity of the network while retaining biologically plausible pairwise neuronal interactions. The resulting microscopic architecture differed substantially from the original network, yet both implemented energy-minimization dynamics.

This example illustrates an important general principle. A complicated effective energy function need not imply equally complicated direct interactions between the observable variables. Instead, much of the apparent complexity may be absorbed into hidden variables whose collective interactions generate the effective energy observed at the macroscopic level.

The same possibility may exist for the energy functions learned by modern generative AI models. A transformer, diffusion model, or other neural-network architecture should not necessarily be interpreted as the microscopic implementation of the computation. Rather, it may represent one member of a much larger family of computational architectures that realize approximately the same effective energy landscape.

![](https://subirvarma.github.io/GeneralCognitics/images/stat96.png)

**Figure 18:** Conceptual illustration of one possible realization of a learned effective energy function through a network of visible and hidden units interacting via biologically plausible pairwise connections. The realization is not unique; many different microscopic architectures may produce the same effective energy landscape.

This viewpoint suggests a new inverse problem for computational neuroscience. Rather than asking whether artificial neural networks resemble cortical circuits, one may instead ask:

> **Given a learned effective energy function, what classes of microscopic neural architectures are capable of realizing it?**

Unlike the inverse-connectome problem, this question does not seek a unique reconstruction of the brain's circuitry. Instead, it asks what architectural constraints are implied by the observed large-scale dynamics.

At present this problem remains largely unexplored. It lies somewhere between inverse statistical mechanics, realization theory in control systems, and computational neuroscience. Understanding this correspondence may ultimately provide a bridge between effective theories learned by modern AI systems and the biological mechanisms that implement cognition.

Whether such a correspondence exists remains an open question. Nevertheless, the effective-theory perspective developed throughout this paper suggests that this may be a more fruitful direction than searching directly for transformer layers, attention mechanisms, or diffusion processes within the brain's anatomical circuitry.

# Conclusions

The central question addressed in this paper is how recent advances in generative artificial intelligence should be interpreted within computational neuroscience. Rather than asking whether transformers, diffusion models, or other neural-network architectures resemble the brain's anatomical circuitry, we have argued that these models are more naturally understood as **effective theories of cognition**. Like thermodynamics in physics, their significance lies not in reproducing microscopic mechanisms but in capturing the large-scale dynamical laws governing observable behavior.

This viewpoint leads naturally to a reformulation of predictive processing within an energy-based framework. We introduced the **Latent Energy-Based Predictive Processing (LEPP)** architecture, which decomposes predictive processing into three computational components: latent-state inference, temporal prediction, and percept generation. The inference module was implemented using predictive coding, while temporal prediction was formulated as stochastic optimization over a learned energy landscape using diffusion-based energy models. Both modules were shown to operate through local energy-minimization dynamics, providing a unified computational interpretation of predictive processing that is more compatible with biological implementation than conventional backpropagation-based learning.

Building upon this formulation, we proposed a second model, **Direct Energy-Based Predictive Processing (DEPP)**. Unlike LEPP, DEPP does not explicitly represent latent causes. Instead, it models the observable evolution of perceptual states directly through a learned effective energy landscape. Importantly, DEPP does not deny the existence of latent internal representations. Rather, it asks whether they are required to appear explicitly within an effective computational theory. In this sense, LEPP and DEPP should not be regarded as competing theories, but as descriptions of cognition at different levels of abstraction.

This distinction mirrors the historical relationship between statistical mechanics and thermodynamics. Statistical mechanics explains macroscopic phenomena by modeling microscopic constituents explicitly. Thermodynamics instead characterizes the observable dynamics of macroscopic systems without requiring an explicit representation of their microscopic structure. Likewise, LEPP retains an explicit latent-state representation, whereas DEPP models perceptual dynamics directly through an effective energy function. Both descriptions may be simultaneously valid, depending upon the scientific questions being asked.

The effective-theory viewpoint also provides a different perspective on the success of modern generative AI. The remarkable capabilities of diffusion models, transformers, and large language models need not imply that these architectures reproduce the organization of the cerebral cortex. Rather, they suggest that highly expressive function approximators are capable of recovering effective dynamical laws directly from observable behavior. The parameters learned by these models should therefore be interpreted not as models of neuronal circuitry, but as compact representations of the large-scale energy landscapes governing perception, language, and cognition.

This interpretation has broader implications for computational neuroscience. Much current research seeks direct correspondences between artificial neural-network architectures and biological neural circuits. The perspective developed here suggests an alternative research program. Instead of searching for cortical implementations of transformers, attention mechanisms, or diffusion processes, one may seek the effective dynamical principles that these architectures approximate. Once those principles have been identified, the remaining challenge is to understand the classes of biological mechanisms capable of realizing them.

The ideas developed here also suggest several directions for future research. One concerns the relationship between effective energy functions and the microscopic neural architectures capable of implementing them. Another concerns the extent to which cognition, planning, and reasoning can be understood as different modes of operation of a common predictive world model. More generally, the framework proposed here suggests that many questions traditionally formulated in terms of internal representations may admit complementary formulations in terms of effective dynamical laws.

Ultimately, the enduring lesson of modern generative artificial intelligence may be methodological rather than architectural. Complex systems need not always be understood by reconstructing their microscopic mechanisms. Sometimes it is sufficient to discover the effective dynamical laws governing their observable behavior. If this perspective proves fruitful, then the greatest contribution of modern generative AI to neuroscience may not be a new model of the brain's circuitry, but a new way of thinking about cognition itself.


