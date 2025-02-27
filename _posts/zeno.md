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

Zeno of Elea was an ancient Greek philosopher who lived around 500 BC. He was a disciple of the philosopher Parmenides, who believed that all of reality consisted of an un-differentiated, unchanging motionless whole, which did not consist of any parts. Hence  aspects such as motion, change and plurality were illusions according to him. In support of this point of view, Zeno came up with several paradoxes, which have continued to puzzle philosophers and scientists, even to the present day. 

Fundamentally, these paradoxes drill through to the very base of aspects of reality such as the nature of time, space and motion, as well as the nature of infinity, so that their resolution requires a deep understanding of mathematics as well as physics. This level of understanding didn't begin to develop until the 17th century, with the development of infintesmal calculus as well the revolution in Physics that was bought about by Newton and his contemprories. However a more complete resolution had to await the 19th century, in which mathematicians such as Cauchy, Weierstrass, Dedekin and Cantor laid the subject of calculus and the nature of infinity on a firmer mathematical footing and it seemed that the paradoxes had finally met their resolution. This state of affairs was shaken in the 20th century with the discovery of Quantum Mechanics, which upended our understanding of how microscopic particles  behave. This led to a re-evaluation of the paradoxes in the light of the Uncertainity Principle and the fact that matter seems to have both wave and particle properties. As we will see towards the end of the essay, Zeno's understanding of the nature of reality is similar to the picture of nature that Quantum Mechanics paints for us.

In this essay we will focus on one of Zeno's paradoxes, called the Paradox of the Arrow, and we will trace how our understanding of this paradox has changed since the time of Zeno, and continues to evolve even today. 

## Zeno's Paradox of the Arrow

Consider an arrow that is in flight from Point A to Point B, and assume that it passes through points C and D on the way at time $t_C$ and $t_D$ respectively. We will assume that $t_C$ and $t_D$ are atomic instants of time, so that they cannot be sub-divided into smaller parts. The question that Zeno asked is: Can we tell if the arrow is in motion at time instant $t_C$? Lets assume that arrow occupies a set of points in space at $t_C$ which correspond to the shape of the arrow. In order to be in motion, the arrow will have to occupy space that exceed the size of the arrow. But this leads to the conclusion that arrow will be in two different places at the same istant of time, which is an absurdity. From this Zeno concluded that at any atomic instant of time, the arrow is actually at rest, i.e., not moving. So if we now look at the all instants of time that lie in the interval $[t_A, t_B]$, then at any one of those instants the arrow is at rest. Then the question arises, how does the arrow get from point A to point B?
If time is indeed made up of these atomic time instances, then how does the arrow get from one time instance to another, i.e., what is it doing in-between the time instances?

Fundamental to the statement of the paradox is the notion of atomic instances of time. Aristotle was one of the first philosophers who tried to resolve the paradox, and he did so by questioning whether these instances do in fact exist. He suggested that time is instead made up of intervals of finite duration, and during these intervals the arrow is indeed allowed to travel through space. This was not a wholly satisfactory resolution, since mathematically speaking, the concept of time interval of finite duration is something that can very well exist, event though it is difficult to imagine this from the point of view of human perception, it is easier to picture instants of time. If a finite time interval does exist, is must be made up of an infinity of these atomic time instances each of duration zero. But then again, how can a finite duration arise from an infinity of time instances of duration zero? One can see that the paradox of the arrow is really a question about the deep nature of time and space, and also the nature of infinity. It is said that the Ancient Greeks where so disturbed by these paradoxes that they completely left out the concept of infinity in their development of Math and Science, most of which happened after the time of Zeno. This prevented them developing infinitesmal calculus, even though they had all fundamental concepts needed to do so.

The arrow paradox raises several questions, that are actually all related to each other:

- What is meant for an object to be in motion?
- What is the nature of space and time? Are they intervals, or is there a smallest atomic unit beyond which they cannot be sub-divided further?
- What is the nature of infinity? How can an interval of finite duration arise out of an infinity of constituent parts each of which is a dimensionless point.

More fundamentally, what is the true nature of reality and what is its relation to mathematics? If we confine ourselves to the mathematical world, we can clearly go about subdividing an interval into smaller and smaller parts, and continue to do this indefinitely. But is this is something that can be done in the real world, either to space or to time? So the paradox raised some very deep questions, which philosophers were not in a poisition to answer, until the first glimmerings appeared with the Scientific Revolution in the 17th century.

## How Can an Object be in Motion?

The paradox of the arrow asks the question of how the arrow can be in motion if it is motionless as ny one time instant.
The discovery of differential calculus gave scientists a tool that they could use to probe into this problem. The attack on the problem happened in two phases: Phase 1 was in the 17th century when calculus was discovered by Newton and Leibnitz and Newton then applied it in coming up with his three laws of motion. However as we show below, their solution to the problem was not entirely satisfactory, and a fuller resolution had to wait for Phase 2 which happened in the 19th century, when subject of calculus was placed on a firmer theoretical foundations.

Galileo, Newton and others introduced the concept of the average velocity of an object, which was defined as follows:

$$ v_{avg} = {\delta x\over{\delta t}} $$

where $\delta x$ is the distance covered by an object over a time duration $\delta t$. If this calculation is carried out for time intervals that infintesmally small, then $v_{avg}$ becomes the instantaneous velocity at some time instant t. Hence $v = {\delta x\over{\delta t}}$ for the case when $\delta_t = 0$.
They introduced the critical idea that the velocity of an object can be non-zero, and this quantity can be well defined even for atomic instants of time. Hence when the arrow travels between points A and B, then at every time instant between $t_A$ and $t_B$, it has a well defined velocity, even though at any particular time instant it is seen to be completely stationary. Hence according to Newton, Zeno was right that arrow is stationary at any one instant of time, however it does not follow from this that it has zero velocity.

This use of differential calculus in mechanics worked well in practice, it enabled scientists to compute velocities and higher order quatities such as acceleration. However it side stepped the problem of whether time progresses in instants or in intervals. Also Newton had a simple solution to the problem of where the arrow was located in between two time instants: In the absence of a force, the arrow will keep moving at a fixed velocity, so that at time instant t, it is located at $x = vt$ units from the starting point. Even in the presence of a force, such as gravity, Newton and Galileo came up with the formula

$$ x = {1\over 2} gt^2 $$

for the location of the arrow. These formulae enable us to compute the location of the arrow at all instants of time.

We saw earlier that the calculation of the derivative involves very small, but finite, time intervals, which are set to zero in order to get the final answer. However this leads to the mathematical problem of dividing by zero. Indeed in part of the calculation $\delta_t$ is treated like a very small but finite quantity, while in other parts of the calculation its value is to set to zero. Newton or Liebnitz didn't have an answer to this problem, and it had to wait for Cauchy in the early 1800s, when he introduced the concepts of limits and convergence of a series into calculus. Weirstrass fully developed these ideas and gave the definition of the derivative which is still in use today.

$$ v = \lim_{t_2\rightarrow t_1}{{x(t_2) - x(t_1)}\over{t_2 - t_1}}  $$

The $\lim$ operation is defined as follows: For every $\epsilon >0$, there exists a $\delta >0$, such that if $t_2 - t_1 < \delta$, then $y(t_2) - y(t_1) < \epsilon$. Hence the velocity $v(t_1)$ at time $t_1$ is defined as the limit to the sequence of average velocities ${{y(t_2) - y(t_1)}\over{t_2 - t_1}}$, as the time instants $t_2$ gets closer and closer to $t_1$. In this definition we are no longer dividing by zero, and instead using the idea of the derivative as the limit of a convergent sequence, which always exist if the function $x(t)$ is continuous.

Once the ideas of differentiation was put on a firm theoretical basis, Zeno's paradox of the arrow had the following (partial) resolution: Zeno was right in stating that arrow was stationary at any one time instant, however he was wrong in concluding from this that the arrow does not move at al. In fact the arrow posesses a finite velocity, which can also be defined at atomic instants of time by using the concept of limit. 

*The arrow traverses a continuum of points, in a continuum of time, not a series of discrete points at discrete times. The latter is impossible, since it is not possible to decribe the real line as a series of discrete points, since there always another point between any two discrete points ad infinitum. The human mind has difficulty grasping the continuum, we are more comfortable with discrete points. Time and space are continuums. Later Cantor put the concept of a continuum on a more rigorous basis by defining the notion of cardinality, and differentiating it from length of a segment. Cardinality is the number of points in a segment of a continuum, and Cantor proved that this number which he called c, is greater than the number of integers.*

## How Does the Arrow Move from One Point to Another

It turns that this is the wrong question, since there is no such thing as a sequence of points that make up an interval. So the arrow is not moving from point to point, but instead it is moving a, a long a continuum of points. In order to understand what a continuum is, mathematicians had more fully understand what infinity is. Is there a difference between the number of points in a continuum vs an infinite set of discrete points. It turned out that there was.

After Weirstrass has settled the issue that the arrow actually had a non zero velocity at any instant of time, even though it was not actually moving at the instant, the next next problem was: How does the arrow actually get from point A to point B? Clearly the arrow is at A at time t_A and at B at time t_B, and since there is always a point C in-between A and B, it will be at C at time t_C. But how is it actually getting from one point to another? 
This question imoplicitly assumes that space is made up of discrete points, and so is time made up of discrete instants, so that the arrow is moving from one discrete point to another as time progresses. This is clearly not a satisfactory picture, since given a point, clearly there is no 'next' point that the arrow can go to next (since if there was any such point, one can always find anothet point that is closer). 
The problem here whether we can look at space (and time) as a set of discrete points, or as a continuum of points. The idea of a continuum was poorly understood, until it was clarified in a brilliant series of papers by Cantor in the latter half of the 19th century. He showed that the continuum has a fundamentally different structure then the set of discrete points, indeed the number of points or cardinality of the the continuum, that he called c, is greater than the cardinality of intgeres or the rationals. The continuum is characterized not just by points that it contains, but also measure of its length (or duration). Both space and time are continuums. Hence in either case we cannot talk of the number of discrete points in space or discrete instants of time, but instead the length of segment of space or the duration of time. 
Given a length L, an arrow moving with velocity V will traverse the space in time T = L/V.
But note that the arrow is now moving in a continuum, hence the question of defining the set of points that it traverses during the journey does not arise.


### Quantum Mechanics and the Paradox

- Differential calculus gives us a procedure for computing the velocity of a particle, based on positions where the particle is to be found at points in the future.
- 



### The Uncertainity Principle




### Quantum Field Equations for a Particle




## So Where Does That Leave us? Kant's take on the Paradox

### Do Infinitely Small Quanitities Actually Exist?

### Do Time and Space Actually Exist?
