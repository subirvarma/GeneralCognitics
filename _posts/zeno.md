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

Consider an arrow that is in flight from Point A to Point B, and assume that it passes through point C on the way at time $t_C$ and $t_D$ respectively. We will assume that $t_C$ and $t_D$ are atomic instants of time, so that they cannot be sub-divided into smaller parts. The question that Zeno asked is: Can we tell if the arrow is in motion at time instant $t_C$? Lets assume that arrow occupies a set of points in space at $t_C$ which correspond to the shape of the arrow. In order to be in motion, the arrow will have to occupy space that exceed the size of the arrow. But this leads to the conclusion that arrow will be in two different places at the same instant of time, which is an absurdity. From this Zeno concluded that at any atomic instant of time, the arrow is actually at rest, i.e., not moving. So if we now look at the all instants of time that lie in the interval $[t_A, t_B]$, then at any one of those instants the arrow is at rest. Then the question arises, how does the arrow get from point A to point B?
If time is indeed made up of these atomic time instances, then how does the arrow get from one time instance to another, i.e., how is it moving in-between the time instances?

Fundamental to the statement of the paradox is the notion of atomic instances of time. Aristotle was one of the first philosophers who tried to resolve the paradox, and he did so by questioning whether these instances do in fact exist. He suggested that time is instead made up of intervals of finite duration, and during these intervals the arrow is indeed allowed to travel through space. This was not a wholly satisfactory resolution, since mathematically speaking, the concept of time interval of finite duration is something that can very well exist, event though it is difficult to imagine this from the point of view of human perception, it is easier to picture instants of time. If a finite time interval does exist, is must be made up of an infinity of these atomic time instances each of duration zero. But then again, how can a finite duration arise from an infinity of time instances of duration zero? One can see that the paradox of the arrow is really a question about the deep nature of time and space, and also the nature of infinity. It is said that the Ancient Greeks where so disturbed by these paradoxes that they completely left out the concept of infinity in their development of Math and Science, most of which happened after the time of Zeno. This prevented them developing infinitesmal calculus, even though they had all fundamental concepts needed to do so.

The arrow paradox raises several questions, that are actually all related to each other:

- What is meant for an object to be in motion?
- What is the nature of space and time? Are they intervals, or is there a smallest atomic unit beyond which they cannot be sub-divided further?
- What is the nature of infinity? How can an interval of finite duration arise out of an infinity of constituent parts each of which is a dimensionless point.

More fundamentally, what is the true nature of reality and what is its relation to mathematics? If we confine ourselves to the mathematical world, we can clearly go about subdividing an interval into smaller and smaller parts, and continue to do this indefinitely. But is this is something that can be done in the real world, either to space or to time? So the paradox raised some very deep questions, which philosophers were not in a poisition to answer, until the first glimmerings appeared with the Scientific Revolution in the 17th century.

## How Can an Object be in Motion?

The paradox of the arrow asks the question of how the arrow can be in motion if it is motionless as any one time instant.
The discovery of differential calculus gave scientists a tool that they could use to probe into this problem. The attack on the problem happened in two phases: Phase 1 was in the 17th century when calculus was discovered by Newton and Leibnitz and Newton then applied it in coming up with his Three Laws of Motion. However as we show below, their solution to the problem was not entirely satisfactory, and a fuller resolution had to wait for Phase 2 which happened in the 19th century, when subject of calculus was placed on firmer theoretical foundations.

Galileo, Newton and others introduced the concept of the average velocity of an object, which was defined as follows:

$$ v_{avg} = {\delta x\over{\delta t}} $$

where $\delta x$ is the distance covered by an object over a time duration $\delta t$. If this calculation is carried out for time intervals that infintesmally small, then $v_{avg}$ becomes the instantaneous velocity $v(t)$ at some time instant t. Hence 

$$  v(t) = {\delta x\over{\delta t}}  $$

for the case when $\delta t = 0$.
They introduced the critical idea that the velocity of an object can be non-zero, and this quantity can be well defined even for atomic instants of time. Hence when the arrow travels between points A and B, then at every time instant between $t_A$ and $t_B$, it has a well defined velocity, even though at any particular time instant it is seen to be completely stationary. Hence according to Newton, Zeno was right that arrow is stationary at any one instant of time, however it does not follow from this that it has zero velocity.

This use of differential calculus in mechanics worked well in practice, it enabled scientists to compute velocities and higher order quatities such as acceleration. However it side stepped the problem of whether time progresses in instants or in intervals. Also Newton had a simple solution to the problem of where the arrow was located in between two time instants which was his First Law of Motion: In the absence of a force, the arrow will keep moving at a fixed velocity, so that at time instant t, it is located at $x(t) = vt$ units from the starting point. Even in the presence of a force, such as gravity, Newton and Galileo came up with the formula

$$ x(t) = {1\over 2} gt^2 $$

for the location of the arrow. These formulae enable us to compute the location of the arrow at arbitrary instants of time.

We saw earlier that the calculation of the derivative involves very small, but finite, time intervals, which are set to zero in order to get the final answer. However this leads to the mathematical problem of dividing by zero. Indeed in part of the calculation $\delta t$ is treated like a very small but finite quantity, while in other parts of the calculation its value is to set to zero. For example consider the case when motion is defined by the equation$ $x(t) = t^2$, as a function of time. Then

$$ \delta x = x(t+\delta) - x(t) = (t+\delta t)^2 - t^2 = 2t\delta + \delta^2  $$

so that

$$ v_{avg} = {\delta x\over{\delta t}} = {2t\delta + \delta^2\over\delta} $$

If we treat $\delta$ as a finite quantity such that $\delta > 0$, then we can divide the numerator and denominator by this quantity to get

$$ v_{avg} = {2t + \delta} $$

Newton and Leibnitz's methodology called for setting $\delta = 0$, to get the final answer

$$ v(t) = 2t $$

Notice how $\delta$ was simultaneously treated as a quantity that is non-zero in the first step (in order to avoid dividing by zero), AND it was set equal to zero in the second step.
Newton or Liebnitz didn't have a solution to the problem of obtaining a more rigorous definition of the derivative, and the first steps in this direction had to wait for Cauchy in the early 1800s, when he introduced the concepts of limits and convergence of a series into calculus. Later in the 1850s Karl Weierstrass fully developed these ideas and gave the definition of the derivative which is still in use today, namely

$$ v(t_1) = \lim_{t_2\rightarrow t_1}{{x(t_2) - x(t_1)}\over{t_2 - t_1}}  $$

The $\lim$ or the limit operation is defined as follows: For every $\epsilon >0$, there exists a $\delta >0$, such that if $|t_2 - t_1| < \delta$, then $|x(t_2) - x(t_1)| < \epsilon$. Hence the velocity $v(t_1)$ at time $t_1$ is defined as the limit to the sequence of average velocities ${{x(t_2) - x(t_1)}\over{t_2 - t_1}}$, as the time instants $t_2$ gets closer and closer to $t_1$. In this definition we are no longer dividing by zero, and instead defining the derivative as the limit of a convergent sequence, and this limit always exists if the function $x(t)$ is continuous at point $t$ (i.e., there are no jumps in the function at $t$). Note that this definition does not involve the concept of intervals of either time or space, everything is in term of individual instants of time and points in space. 
The definiton assumes that the next point $t_2$ can be made as close as we wish to $t_1$, without ever actually 'touching' it.

Once the idea of differentiation was put on a firm theoretical basis, Zeno's paradox of the arrow had the following (partial) resolution: Zeno was right in stating that arrow was stationary at any one time instant, however he was wrong in concluding from this that the arrow does not move at al. In fact the arrow posesses a finite velocity, which can also be defined at atomic instants of time by using the concept of the derivative of a function. 
Was there all that there is to it in resolving the paradox? Not quite, since we still haven't clarified about how the arrow actually moves from one point in space to another.

*The arrow traverses a continuum of points, in a continuum of time, not a series of discrete points at discrete times. The latter is impossible, since it is not possible to decribe the real line as a series of discrete points, since there always another point between any two discrete points ad infinitum. The human mind has difficulty grasping the continuum, we are more comfortable with discrete points. Time and space are continuums. Later Cantor put the concept of a continuum on a more rigorous basis by defining the notion of cardinality, and differentiating it from length of a segment. Cardinality is the number of points in a segment of a continuum, and Cantor proved that this number which he called c, is greater than the number of integers.*

## When does the Arrow Actually Move?

In the Newtonian/Differential Calculus picture of the arrow's flight, the arrow has a finite velocity at all point in time i.e., the arrow has a vertain velocity while at point A at time $t_A$, and this enables it to move to point B at a later time instant $t_B$. Since it is ""not in motion at both these time instants, when does it actually move from A to B?
We can try to pin down the arrow's trajectory by looking at intermediate instants of time, for example if $t_C = {t_A + t_B\over 2}$, then the arrow will be at the point $x(t_C)$ at $t=t_C$. But this not enough to pin down the motion, since we still don't know how the arrow got from $x(t_A)$ to $x(t_C)$. We can continue this procedure of halving the time intervals *ad infinitum*, but however many times we do it, it is still impossible to pin down the instant at which the arrow is actually moving!

This description of the arrows flight implicitly assumes that both space and time are made up of discrete points, so that the arrow is moving from one discrete point to another as time progresses. This is clearly not a satisfactory picture, since given the starting point $x(t_A)$, clearly there is no 'next' point that the arrow can go to, since if there was any such point, one can always find another point that is closer to the starting point by using the halving procedure. 

It turns out that trying to pin down when the motion actually happens is another very difficult problem having to do with the concept of infinity, and one that was not solved until the latter half of the 19th century. The main contributor to this were the the German mathematicians Richard Dedekind and George Cantor. Dedekind gave a rigorous proof of the fact that there exist numbers that are neither integers nor fractions, but belong to category that he called Real Numbers. When expressed as a decimal, they have a never ending series of digits after the decimal point irrational numbers such $sqrt{2}$ for example belong to this category. When Real Nunbers are taken into accouint, an interval no longer consists of a set of discrete points, but becomes what is called a continuum. 

The idea of a continuum was poorly understood, until it was clarified in a brilliant series of papers by George Cantor in the latter half of the 19th century.
He realized that the fundamental problem with the arrow paradox is the lack of understanding of the nature of infinity.
He made a number of important contributions to understanding it, specifically he was able to prove the following:

- If the cardinality of a set is defined as the number of elements in it, then obviously the cardinality of the set of Integers is infinity. Cantor gave this infinity a symbol $\aleph_0$. Cantor further showed that the cardinality of set of all Rational Numbers (those which can be expressed as fractions of Integers) is also $\aleph_0$.
- Then Cantor made the surprising discovery that the cardinality of the set of Real Numbers is not $\aleph_0$. In fact it is another type of infinity, whose cardinality he called $c$, and furthermore the two infinities can be compared, and that $c > \aleph_0$.
- His most surprising conclusion was that the cardinality of any subset of the Real Line, say the interval [0,1], is the same as that of the entire Real Line! This means that there as many numbers between [0,1] as there are over the entire line.

Cantor's discoveries pointed to the fact that number of points in an interval are not a good indication of how long the interval is, since intervals of different sizes can have the same number of points (whose number is equal to c). This means that trying to understand the movement of the arrow, as something that is moving from point to point in space, does not make sense. The arrow is in fact moving over the continuum of points, which is why it is impossible to find out the point where it will be at the very next instant, **since the next instant does not exist as such**.

If the number of points in an interval of the continuum cannot be used to characterize it, what is a good indicator of the length of an interval or the duration of time? It turns out that in order to do so, one has to define something called a metric over the continuum, which assigns a number to each point in the continuum. The length of an interval is then defined as the difference in the metric values between the two points. Note that this definition is completely independent of the constituents of the continuum itself. Hence the length of an interval cannot be expressed as a function of the number of points that it contains, which is something that Zeno was trying to do.

Going back to Zeno's paradox, note that both space and time are continuums. Hence the concepts of the length of a segment of space or the duration of time are well defined using the idea of metrics. 
Given a segment of length L, an arrow moving with velocity v will traverse the space in time t = L/v.
But note that the arrow is now moving in a continuum, hence the question of defining the set of points that it traverses during the journey is not well formulated. 

Admittedly it is difficult to visualize motion in a continuum, our brains are wired to recognize motion as a discrete set of positions at discrete points in time. If the arrow were replaced by a fundamental particle, say the electron, can we carry out an experiment using a very powerful microscope, in which we try to see how it behaves while its moving over the continuum? Such an experiment was indeed carried out about a hundred years ago, and the results only deepened the mystery. This topic is discussed in the next section.

**since there is no such thing as a sequence of points that make up an interval. So the arrow is not moving from point to point, but instead it is moving a, a long a continuum of points. In order to understand what a continuum is, mathematicians had more fully understand what infinity is. Is there a difference between the number of points in a continuum vs an infinite set of discrete points. It turned out that there was
The problem here whether we can look at space (and time) as a set of discrete points, or as a continuum of points. The idea of a continuum was poorly understood, until it was clarified in a brilliant series of papers by Cantor in the latter half of the 19th century. He showed that the continuum has a fundamentally different structure then the set of discrete points, indeed the number of points or cardinality of the the continuum, that he called c, is greater than the cardinality of intgeres or the rationals. The continuum is characterized not just by points that it contains, but also measure of its length (or duration).** 

## Quantum Mechanics and the Paradox

![](https://subirvarma.github.io/GeneralCognitics/images/zeno1) 

Figure 1

The photograph in Fig. 1 shows the path several elementary particles as captured in a device called a Bubble Chamber. If we focus on the path of any one of these particles, we can see that it consists of a series of white dots. These are points where the particle is interacting with the contents of the Bubble Chamber, and so these dots can be regarded as a series of observations that fix the position the particle at successive time instants. What is the particle doing at times that are in-between two of the white dots? If we go by Newton's Laws of Motion, the particle will be located at a position whose value can be determined exactly since the particle's velocy is also known.
On the other hand, Quantum Mechanics has a very surprising answer to this question: We cannot have a precise determination of the particle's position while it is in the in-between area. The only way to do would be take another measurement at the precise time, which will result in another white dot along the particle's trajectory.

![](https://subirvarma.github.io/GeneralCognitics/images/zeno2.png) 

Figure 2

In order to get a better understanding of the situation, consider what happens when elementary particles such as electrons behave when passing through a screen with a single slit. When an electron passes through the slit, it's position becomes known with an uncertainity that is equal to the width of the slit, so this is like making a measurement to determine position. The electron then strikes a detector placed after the screen, at which its position once again becomes known. But what happens in-between the slit and the detector, where is the particle located at those times? 

This is analogous to the question we asked about the arrow's behavior between two successive measurements or the question about the location of the elementary particle between two successive white dots in Fig. 1.
Quantum Mechanics tells us that in between two measurements, the particle essentially does not exist 'in the form of what we normally think of as a particle'. Then what does it look like? The short answer to this question is: We don't know. The only way to talk about the particle in between two successive measurements is by using the language of mathematics, and here is what the math is telling us: 
All of space is permeated by a 'particle' field, which you can think of as similar to the electromagnetic field but for matter. This matter field contains energy, and this energy is not diffused througout space, but is concentrated in energy quanta. These quanta of energy is what we call particles.
It is possible to extract information about the location and momemntum of these energy quanta, and if the uncertainity in its location is $\Delta x$ and the uncertainity in its position is given by $\Delta p$, then these two connected by the following equation

$$  \Delta x \Delta p \ge {h\over 2\pi} $$

Hence if a particle's position is completely known, then we can have absolutely no information about its momentum and conversly if its momentum is known exactly, then it can be located anywhere in space.

Going back to the single slit experiment in Fig. 2, when the particle goes through the slit, the uncertainity in its verticle location is $\Delta y = \plusminus B$ where $B$ is the length of the slit. Hence the Uncertainity Principle tells us that there is also an uncertainity in the component of its momentum in the vertical direction given by 

$$ \Delta p \ge {h\over 2{\pi B}}   $$

This uncertanity in the y momentum causes the trajectory of the particle of spread out after the screen Moreover the the existence of the null points in the diffraction pattern on the screen are exactly what we would observe if this experiment where to be carried out with light waves. From this we can conclude that in-between the two measurements, the particle no onger exisHow can this be so?ts as a particle, but has acquired wave like properties. How can this be so? We don't know. All that we can say is that the mathematical equations that this mysterious entity obeys, is precisely the same as that of a wave propagating through space.

Going back to Zeno's paradox, QM and QFT tell us that a particle exists as what we understand to be a particle, only at the times at which it is being observed. Hence Zeno was not wrong to ask how does the particle move between successive instants, though his conclusion that particle cannot actually move was the wrong one. The truth is even stranger. The partcle does move, since differential calculus tells us that it has a non-zero velocity as atll time instants, however QM tells us that it is impossible to visulaize its movement, since it no longer exists as a partcle.

## So Where Does That Leave us? Immanuel Kant's take on the Paradox

The great philosopher Immanuel Kant also spent time thnking deeply about Zeno's paradox, and the conclusions that he drew from this investigation led his work *Critique of Pure Reason*. Kant concluded that there is a difference between the world that exists out there, which he called the Noumenon, and the picture of the world that our brain presents to us, which he called the Phenomenon. He though that the reason why we have so much difficulty in visualizing the movement of the arrow between successive points, is that because the movement actually happens in the Noumenon, to which we have no access. The only time our senses perceive the arrow are at discrete points in time, wince those are the only instants that our senses are able to interact with the object. This point of view is in surprisingly good accordance with the conclusions from Quantum Mechanics, if we accept the fact that Kant's Noumenon corresponds to the mathematcal picture of all matter arising from these mysterious Quantum Field pervading through space.
Kant also though that the idea of infinite divisability of space and time is a mathematical concept, and may not apply to the Noumenon. In fact he though that the very idea of space and constructs of our brains, and these quantities do not really exist in the Noumenon.

## The Future of the Paradox

We can see that Zeno's Paradox has inspired some of the deepest ideas that we have about the nature of space, time and the concept of infinity. I find it amazing that the speculations of Ancient Philosopher who lived at the very dawn of our civilization, have led to so much progress in human knowledge. To compete with this kind of immortality, can you think of a question or paradox that people will still be talking about 2500 years from now? That is a very difficult undertaking.

We still don't know about the ultimate nature space. Does it exist as discrete atoms, like matter? If so, when a particle is moving in space, is it hopping from one atom of space to another? These are questions that Zeno though about, and to which we still don't have an answer. 
