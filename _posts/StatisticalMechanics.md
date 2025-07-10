---
layout: default
title: "From Statistical Mechanics to Neurel Networks"
---

# From Statistical Mechanics to Neural Networks



## Introduction

The science of Statistical Mechanics was founded in the mid-1800s, the pioneers were the great physicists James Clerk Maxwell and Ludwig Boltzmann. The main idea behind this was to seek an explanation for the macroscopic properties of a large number of interacting particles. This was at a time when atomic theory was still a controversial subject, not every scientist was convinced that matter is made up of atoms or molecules.
The science of classical mechanics, as founded by Newton, was not of much use in a analyzing the behavior of a large number of particles, in fact the math becomes unsolvable for even a system of three interacting particles.
Nevertheless, There was a strong motivation to understand the properties of these systems, 

A deeper understanding of the behavior of matter had become a more pressing problem due to the recently discovered science of Thermodynamics, which had found practical applications in the design and analysis  of efficient steam engines. Scientists such as Carnot, Helmholtz and Clausius had discovered the First Law of Thermodynamics (Energy is conserved in any physical interaction) and the Second Law (the Entropy of a system always increases over time). 
and the concept that underlay this new science was that of heat. But what was heat? The prevalent theory from the early 19th centure considered heat to be a type of fluid that flows between objects. The atomic hypothesis on the other hand, postulated that heat is caused due to the motion of these tiny particles called atoms, and all matter is composed of atoms.
The great project that was started by Maxwell and mostly completed by Boltzmann, was to explain the macroscopic laws of Thermodynamics within the framework of the atomic hypothesis. 

Classical Newtonian machanics is a deterministic theory. Once we know the initial conditions for a system of particles, it was thought that it should be theoretically possible to predict the future behavior of the system by using Newton's Laws. The conceptual leap that Statistical Mechanics made, was to give up on making exact predictions when the number of particles is very large and this was done by basing the new theory on the mathematics of Probability Theory. The theory embraced the fact that all predictions for these systems are statistical in nature, hence it results of the theory were in the form of averages, standard deviations of distributions for various quantities of interest. 

It explained the nature of heat by postulating that heat is caused by the motion of particles, hence there was a direct relationship between the energy of particles and the temperature of a physical system.
Note that temperature is a macroscopic property, so how would one go about connecting it to microscopic energies of individual particles? This problem was solved by Boltzmann in the form of the Boltzmann Distribution, which gives the probabilties for the system to be in various energy states, under equilibrium conditions. Fundamental to deriving a formula for this distribution was the idea that the amount of disorder in a system could be precisely quantified by using the concept of entropy. Entropy had been introduced a few decades before Boltmann's work by Clausius and others in the formulation of the Second Law of Thermodynamics, but there was complete lack of understanding about it nature. Boltzmann showed that the entropy of a system is connected to our lack of knowledge of the precise details about the evolution of a system, and hence it is entirely a function of the probabilty distribution for the energy states of the system. He theorized that a system in equilibrium achieves a state of maximum entropy, i.e., our uncertainity about the state that it is in is at maximum, and this allowed him to dervive his eponymous distribution. Once the Boltzmann distribution for a system is known, macroscopic properties such average energy or entropy can be derived.

This definition of entropy introduced a new concepy: A physical quantity that is a function of both the observed system and the observer, since it is a measure of how much the observer does not know aboout the system. This was also something new to physics, and has been a source of some confusion about the nature of entropy. In the twentieth century the concept of physical quantities that depend on the observer becaome central to all of physics with the discovery of quantum mechanics. 

Statistical Mechanics became a broadly theory after atomic theory amassed a huge amount of evidence early in the 20th century and stopped being a controversial subject for physicists. It also spawned a number of




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



