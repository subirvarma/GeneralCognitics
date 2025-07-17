---
layout: default
title: "From Statistical Mechanics to Neurel Networks"
---

# From Statistical Mechanics to Neural Networks



## Introduction

The steam engine was invented in the late 1700s, the inventors were brilliant tinkerers who made this advance solely through smart experimentation. But soon after, the question arose about how to make a better engine, and in particular how could one get the most work out of it. This question led to the launch of the science of thermodynamics, and the biggest early contribution was made by the great French engineer Sadi Carnot. Carnot came up with a model for an ideal engine, and showed that the efficiency of any engine is upper bounded by that of his model. This was the genesis of the second law of thermodynamics, also called the law of entropy and soon after this was joined by the first law, called the law of conservation of energy, with the efforts of Count Rumsfeld, James Joule and others. The concepts of the flow of heat and that of entropy were introduced as part of these laws, but it was a big mystery as to what exactly these were.

The first efforts in coming up with an explanation was made in the latter half of the nineteenth century, and the names associated with this are that of James Clerk Maxwell, and more importantly that of the Viennese physicist Ludwig Boltzmann. They started from the single hypothesis, that all matter is made up of tiny particles called atoms, and through a brilliant series of mathemtical investigations they were able to explain not just the true nature of heat, but also that of the mysterious entropy, and a lot more besides. In the process they founded the science of statistical mechanics, and launched a revolution in physics whose effects are being felt even to the present day. Statistical mechanics connected the microscopic properties of atoms, mainly their energy and the way they interact with each other, with macroscopis quantities that we can measure, such as temperature, specific heat etc.

Classical Newtonian machanics is a deterministic theory. Once we know the initial conditions for a system of particles, it was thought that it should be theoretically possible to predict the future behavior of the system by using Newton's Laws of motion. The conceptual leap that statistical mechanics made, was to give up on making exact predictions when the number of particles is very large and this was done by basing the new theory on the mathematics of probability theory. The theory embraced the fact that all predictions for these systems are statistical in nature, hence the results of the theory were in the form of statistical quantities such as averages and distributions. 

The biggest conceptual leap was a precise definition for the entropy of a collection of particles. Entropy had been introduced in the mid-1800s by Clausius as way of restating Carnot's results for the efficiency of the ideal steam engine, and it is something that could be measured, but what was its true nature?
Boltzmann showed that entropy was connected to our lack of knowledge of what was happening at the microscopic, and gave a formula for entropy which was entirely in terms of the probability dsitribution for the energy for the particles in the system. This did not entirely clear up the matter, since the definition implied that entropy was somehow connected to the observer, hence it was a subective quantity rather than an objective property of matter. There were paradoxes such as that of Maxwell's Demon that were thought up to illustrate this point, and this is where things stood until Claude Shannon came along.

In the 1940s Shannon was looking for a measure of information contained in a message, and he hit upon a formula that was precisely the same as Boltzmann's definition of entropy (though Shannon was not aware of it as that time). Hence Shannon defined the amount of information in a message as a function of our uncertainity about the contents of the message, the more ignorant we are, greater the information, and this precisely what Boltzmann had identified as the entropy of a system.
Shannon actually derived the formula by purely probabilistic reasoning, by looking for a measure of the amount of uncertainity in a probability distribution and this definition was applicable to any distribution whatsoever, whether it arose in statistical mechanics or information theory.
This led to a reformulation and re-thinking of statistical mechanics, in which entropy is now the primary quantity, and it was shown that the rest of the statistical mechanics could be derived starting from this. The only physical assumption required was an ennumeration of the microscopic particles and their energy levels, the rest of it was purely probabilistic analysis. Hene in some sense statistical mechanics can be considered to be a sub-branch of probability theory.

One of the mysteries that statistical mechanics cleared up was that of phase transitions. This is defined as the phenomenon observed when the physical properties of a collection of particles suddenly change, either as a result of variation of temperature or pressure. For example when water suddenly turns to steam at its boiling point or into ice at its freezing point. In the 1870s Van der Waals showed that phase transitions could be explained if we add a force of attraction between particles that are near each other. Thus he introduced the important concept of an interacting particle system.

Some of the biggest advances in physics in the last 100 years have been a result of applying statistical mechanics to areas which at first glance are remote its origins as a theory of gas particles. These include the following:

- The light inside a heated cavity can be considered to be a type of gas, but made up of photons rather than atoms. Hence it can be analyzed using the tools of statistical mechanics, however the first attempts to do so did not agree with experiments. This inspired Max Planck to come up with the quantum hypothesis that energy levels in the cavity are discrete, and the rest as they is history.
- Statistical maechanics can be applied to solids as well as to gases or liquids, and Albert Einstein did so in 1907 to understand the specific heat behavior with temperature for a solid. He did so by modeling it as a system of fixed particles, each of which is a simple harmonic oscillator with discrete energy levels. This model successfully predicted the experimental observations in the high temperature range. The low temperature part was corrected by Peter Debye a few years later, with his theory of phonons.
- The electromagnetic radiation within a closed chamber can be considered to be a cloud of light photons, and its physics can be analyzed using the methods of statistical mechanics. This is precisely what Max Planck did in 1901, when he noticed that in order to get agreement with experimental data, energy levels have to come in discrete chuncks, thus launching the science of quantum mechanics.
- Statistical mechanics has been used to create a model for the phenomena of electrical conduction in metals. This is done by regarding the metal as some sort of closed box that contains a cloud of electrons. The initial analysis of this model was done by < > before the sdvent of quantum mechanics, and later Sommerfield made the quantum corrections in 1927.
- in the 1920s the physicist Lenz and his student Ising came up with a model for ferro magnetism using statistical mechanics. The significance of this model is that it explained magnetism as a property of phase change in the material.

Since physicists have applied atatistical mechanics to explain the behavior of all kinds of systems, some of which are far removed from it original area of application, why not apply to systems in which the atomic units happen to be huamns? This is an active area of research, and a for a good introduction see the book
"Critical Mass: How One Thing Leads to Another" by the science writer Phillip Ball. 
For example the economy of a country can be modeled as a system whose micro dynamics are driven by individuals making decisions on things such what to buy, how much to save etc. Even racial segregation cities can be modeled as an interacting particle sysem, in which individual home purchasing decisions can often lead from a mixed neighborhood to a phase transiion that separate out the areas in which various races reside. Other interesting applications of these models have been to study alliances between countries or even between companies jockeying for an advantage in a changing industry, also as phase transitions.

In the last few decades Statistical Mechanics has been extended to non-traditional systems, and one of these is to a type of material called spin glasses. These are created in the lab by creating an alloy of a cunductimg material such as copper with a small amount of a magnetic material. When the temperature was decreased, the magnetic portion tried to align itself in the same direction, but was prevented from doing so by the surrounding cunductor. This created islands of magnetism, in the alignment was all in different directions.
Spin glasses by themselves haven't become commercially important, but the models that were built to explain their behavior had an unexpected side effect. They inspired the first generation of neural network models that were proposed in 1980s, initially by John Hopfield at Caltech, and later by Geoffrey Hinton and his collaborators. They regarded their networks a type of spin glass, and showed that the resulting system can be made to function as an associative memory.
The neural networks that that we see today are a direct descendant of these early models and use similar principles.

## System with a Large Number of Interacting Particles: The 1-D Ising Model


### Energy, Entropy, Temperature



### The Boltzmann Distribution and the Partition Funtion



### Macro Properties from the Partition Function



## The Higher Dimensional Ising Model and Phase Transitions



## Spin Glass Models




## From Spin Glass to Hopfield Networks




## From Hopfield Networks to Boltzmann Machines



## From Boltzmann Machines to Modern Neural Networks




## Diffusion Models as Overloaded Hopfield Networks


Physics of IPS
- [ ] Can macro properties be derived micro behavior of particles?
- [ ] Main macro properties: Energy, Entropy, Temperature, Pressure, The nature of heat.  What is it, why does it flow from hot to cold bodies? Phase transitions.
- [ ] Heat is due to the motion of particles at the micro level. Define S,E in terms of particles, T as a function of S and E. Show that resulting system behaves as expected at macro level.
- [ ] Micro canonical system: systems with fixed E and T
- [ ] Canonical systems: systems with fixed T but varying E
- [ ] Simplest case: No interactions
- [ ] Boltzmann theory: derivation of equilibrium quantities
- [ ] Equilibrium as the solution to Entropy Maximization problem?
- [ ] Addition of interactions
- [ ] Phase transitions as a result of interactions 
- [ ] Ising models  for magnetism

From Susskind 
- [ ] Temperature, energy and entropy definition
- [ ] The Boltzmann distribution from maximum entropy principle
- [ ] The Z function
- [ ] Formula for energy, entropy etc from Boltzmann distribution 
- [ ] The Ising model, analysis using the Z function and mean field approximation 
- [ ] Equilibrium energy levels in Ising model 
- [ ] Phase transitions by varying temperature in the Ising model

Spin glasses
- [ ] When system can exist in multiple equilibra at the same time

Spin Glasses and neural networks
- [ ] Hopfield model, relation to spin glasses
- [ ] Boltzmann Machines
- [ ] Phase transitions in the Hopfield model, leading to diffusion model
- [ ] Modern neural networks. The effect of the residual connection on the energy landscape.



