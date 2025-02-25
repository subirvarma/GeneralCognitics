---
layout: default
title: "Zeno's Paradox"
---

# Zeno's Paradox of the Arrow

 [online book on this subject](https://srdas.github.io/DLBook2/)


- Zeno’s paradox of the arrow 1) paradox of velocity 2) paradox of movement 
- Why it’s a paradox, if the arrow is not moving at any point in time, how does it get from point A to point B?
- Differential calculus view of the paradox 
- Integral calculus view
- Kant’s view of the paradox 
- Quantum Mechanics and the paradox, the Heisenberg uncertainty principle 
- The quantum field representation for a particle 
- We have replaced one paradox by another: how can an object be in motion and not in motion at the same time to, how can an object exhibit both particle and wave like properties?


## Introduction

Zeno of Elea was an ancient Greek philosopher who lived around 500 BC. He was a disciple of the philosopher Parmenides, who beleived that all of reality consisted of an undifferentaited, unchanginf motionaless whole, which did not consist of any parts. Hence  aspects such as motion, change and pluraity were illusions according to him. In support of this point of view, Zeno came up with several paradoxes, which have continued to puzzle philosophers and scientists, even to the present day. Fundamentally, these paradoxes drill through to the very nature of fundamental aspects of reality such as the nature of time, space and motion, as well as the nature of infinity, so that their resolution requires a deep understanding of mathematics as well as physics. This level of understanding didn't begin to develop until the 17th century, with the development of infintesmal calculus as well the revolution in Physics that was bought about by Newton and his contemprories. However a more complete resolution had to await the 19th century, in which mathematicians such as Cauchy, Weierstrass, Dedekin and Cantor laid thesubject of calculus and the nature of infinity on a firmer mathematical footing and it seemed that the paradoxes had finally met their resolution. This state of affairs was shaken in the 20th century with the discovery of Quantum Mechanics, which upended our understanding of how microscopic particles  behave. This led to a re-evaluation of the paradoxes in the light of the Uncertainity Principle and the fact that matter seems to have both wave and particle properties. In this essay we will focus on one of Zeno's paradoxes, called the Paradox of the Arrow, and we will trace how our understanding of this paradox has changed since the time of Zeno, and continues to evolve even today. 

## Zeno's Paradox of the Arrow

Consider an arrow that is in flight from Point A to Point B, and assume that it passes through points C and D on the way at time t_C and t_D respectively. We will assume that t_C and t_D are atomic instants of time, so that they cannot be sud-divided into smaller parts. The question that Zeno asked is: Can we tell if the arrow is in motion at time instant t_C? Lets assume that arrow occupies a set of points in space at t_C which correspond to the shape of the arrow. In order to be in motion, the arrow will have to occupy space that exceed the size of the arrow. But this leads to the conclusion that arrow will be in two different places at the same istant of time, which is an absurdity. From this Zeno concluded that at any atomic instant of time, the arrow is actually at rest, i.e., not moving. So if we now look at the all instants of time that lie in the interval [t_A, t_B], then at any one of those instants the arrow is at rest. Then the question arises, how does the arrow get from point A to point B?

Fundamental to the statement of the paradox is the notion of atomic instances of time. Aristotle was one of the first philosophers who tried to resolve the paradox, and he did so by questioning whether these instances do in fact exist. He suggested that time is instead made up of intervals of finite duration, and during these intervals the arrow is indeed allowed to travel through space. This was not a wholly satisfactory resolution, since mathematically speaking, the concept of time instant of duration zero, is something that can very well exist event though it is difficult to imagine this from the point of view of human perception. If so, any finite time interval is made up of a multitude of these atomic time insyances each of duration zero. But then again, how can a finite duration arise from a bunch of time instances of duration zero?

Hence the arrow paradox raised at least of couple of questions, that are actually related to each other:

- What is meant for an object to be in motion?
- What is the nature of time? Is it a continuum, or is there a smallest atomic unit beyond which is cannot be sub-divided further?
- A Mathematical Question: What is the nature of infinity? How can an interval of finite duration arise out of an infinity of constituent parts each of which is a dimensionless point.

More fundamentally, what is the true nature of reality and what is its relation to mathematics? If we confine ourselves to the mathematical worls, we can clearly go about subdivdinbg an interval into smaller and smaller parts, and continue to do this indefenitely. But is this is something that can be done on the real worls as well, eother to space or to time. So the paradox raised some very deep questions, which philosophers were not in a poisition to answer, until the first glimmerings appeared with the Scientific Revolution in the 17th century.

## How Can an Object be in Motion?

The discovery of differential calculus gave scientists a tool that they could use to probe into the problem of motion. The attack on this problem happened in two phases: Phase 1 was in the 17th century when calculus was discovered by Newton and Leibnitz. However as we explainn below, their solution to the problem was not entirely satisfactory, and a fuller resolution had to wait for Phse 2 which happened in the 19th century, when subject of calculus was placed on a firmer theoretical foundations with the work of several mathematicians.

Galileo, Newton and others introduced the concept of the average velocity of an object, which was defined as follows:

$$ v_{avg} = {\delta y\over{\delta t}} $$

where $\delta y$ is the distance covered by an object over a time duration $\delta t$. If this calculation is carried out for time intervals that infintesmally small, then $v_{avg}# becomes the instantaneous velocity at some time instant t. Hence the introduced the critical idea that the velocity of an object can be non-zero, even though the interval during which it is being measured is indistuisbale from zero, which was in direct contradiction to Zeno. Hence when the arrow travels between points A and B, then at every time instant between t_A and t_B, it has a well defined velocity, even though at any particular time instant it is seen to be completely stationary.

This resolution to the arrow paradox worked well in practice, it enabled scientists to compute velocities and higher order quatities such as acceleration using differential calculus. However it side stepped the problem of whether time progresses in instants or in intervals. The calculation of the derivative involves very small, but finite, time intervals, which are set to zero in order to get the final answer. However this loeads to the mathematical problem of dividing by zero. Indeed in part of the calculation $\delta t]$ is treated like a very small but finite quantity, while in other parts of the calculation its value is to set to zero. Newton or Liebnitz didn't have an answer to this problem, and it had to wait for Cauchy in the early 1800s, when he introduced the concepts of limits and convergence of a series into calculus. Weirstrass fully developed these ideas and gave the definition of the derivative which is still in use today.

$$ v = \lim_{t_2\rightarrow t_1}{{y(t_2) - y(t_1)}\over{t_2 - t_1}}  $$

The $\lim$ operation is defined as follows: For every $\epsilon >0$, there exists a $\delta >0$, such that if $t_2 - t_1 < \delta$, then $y(t_2) - y(t_1) < \epsilon$. Hence the velocity $v(t_1)$ at time $t_1$ is defined as the limit to the sequence of average velocities ${{y(t_2) - y(t_1)}\over{t_2 - t_1}}$, as the time instants $t_2$ gets closer and closer to $t_1$. Hence this definition ofvelocity goes back to the idea of time existing at atomic instances (rather than as a interval as in the Newton-Leibniz definition), with the caveat that two such instants can be made arbitrarily close to each other. 

Once the ides of differentiation was put on a firm theoretical basis, Zeno's paradox of the arrow had the following resolution: Zeno was right in stating that arrow was stationary at any one time instant, however he was wrong in concluding from this that the arrow does not move at al. In fact the arrow posesses a finite velocity, which can also be defined at atomic instants of time by using the concept of limit. 

### How Can Finite Intervals arise from Point Quantities?



### Integral Calculus or How to Add Up Infinitely Many Infinitely Small Quanitities


## Quantum Mechanics and the Paradox

### The Uncertainity Principle




### Quantum Field Equations for a Particle




## So Where Does That Leave us? Kant's take on the Paradox

### Do Infinitely Small Quanitities Actually Exist?

### Do Time and Space Actually Exist?
