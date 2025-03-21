---
layout: default
title: "The Technology That Made Broadband Wireless Possible"
---

# The Technology That Made Broadband Wireless Possible


## Introduction

Those of you who are old enough will recall the era before 2010 when Nokia, Motorola and Blackberry dominated the market for wireless handsets. These phones had become quite proficient in handling mobile voice calls, but when it came to data, the bitrates that they provided was not quite good enough. It was possible to do some text based web surfing, but when it came to full graphics based web pages, or youtube video streaming, they were not quite up to the task. All this changed in 2011, when suddenly phones suddenly became as good as desktop terminals in running even the most graphics laden content, and streaming video became omnipresent. 

It was not due to the iPhone, since this handset was launched in 2007. So what changed? 
The wireless technology did, as the transition from 3G networks to 4G happened right around that time. This article is about a key technology in 4G wireless that enabled higher data rates, called Orthogonal Frequency Division Multiplexing or OFDM. The name sounds rather formidable, but I think it is possible to explain the essence of how OFDM works even to the non specialist with some knowledge of college level maths, and I am going to make an attempt to do so. OFDM exists at the bottom of the communications protocol stack, and most people don't even know about its exisence, since most of the attention is grabbed by handsets such as the iPhone and the applications running on it. But without OFDM, high speed communications on the iPhone would not have been possible.

Before I launch into OFDM and 4G wireless, I want to briefly mention the technology that they replaced, namely 3G wireless. The latter was launched in 2001, and was the first technology that seriously tried to integrate voice AND data communications capability into the handset. Unfortunately the 3G protocol was designed in the era when voice was still based on an older technology called circuit switching, and thats what went into 3G. Data was considered to be the less important feature, hence its design was an add-on, based on a voice centric technology called circuit switching. Unfortunately circuit switching is not the best way to handle data, which does better with a technology called packet switching, and this handicapped 3G phone performance. 
The other big issue with 3G was the PHY or physical layer protocol that was used, which was based on a technology called Code Division Multiple Access or CDMA. CDMA paired well with circuit switching, but it was not very well suited for data. '
However it had a very strong political backing, in the form of the companies Qualcomm and Ericsson which held a number of important CDMA patents.
So the transition from CDMA to OFDM is also a story of how an insurgent technology, promoted by a few small start-ups, was able to overcome the powerful forces that were aligned against it.

I had some personal involvement in the transition from 3G to 4G wireless, and had a first hand view of the politics involved. I was a co-founder of a start-up called Aperto Networks that did some of the work that ultimately resulted in 4G, and for a number of years I was a member of the IEEE 802.16 Standards Committee that was working on 4G, even chairing the Medium Access Control or MAC group for a while. The MAC protocol lies on top of PHY layers such as CDMA or OFDM, and it had to completely re-designed for packet based wireless communications. But this article is not about the MAC, perhaps it will be a subject of a future article.

## The Fourier Transform

To get to an understanding of how OFDM works, it is necessary to know a mathematical technique called the Fourier Transform. It was first published by Joseph Fourier of France in the 1820s, and since then it has become one of the most powerful tools in the arsenal for mathematicians and engineers. The Fourier Transform is another example of the 2-Layer Principle for organizing complex data, that I talked about in an earlier article called "Latent Varibales and Latent Spaces". The principle states that data can often be represented in two ways: (1) As it exists in the real world, and thus can be measured using instruments, and (2) In an abstract mathematical space, which we can access only by performing some mathematical operations on the real world data. Moreover the two represenations can be transformed into one another using math.
The abstract representation is often easier to manipulate and analyze, and a mumber of difficult problems in the real world can be solved, by first solving the problem in the abstract space. Other examples of this 2-Layer Principle from the earlier article include:

- Representing data such as images and language using Latent Variables. The mathematical transformation in this case is represented by Artificial Neural Networks. This representation lies at the heart of all the progress being made in this field.
- Representing physical measurements using the idea of Fields. This started with Maxwell and the Electromagnetic Field, and went on to represent matter using Quantum Fields. Also the Schrodinger Wave Function for a particle can be represented either in terms of its location x in space, or its momentum p, and and these two representation $\psi(x)$ and $\psi(p)$ are Fourier Transforms of each other!
- Representing Biological data using the DNA code. In this case the abstract Layer 2 representation actually exists in the real world too.

It can be argued that a great deal of scientific progress in the last 200 years has been made by exploting the 2-Layer Principle. 
This principle was first discovered by Joseph Fourier more than 200 years ago, with his invention of the Fourer Transform.
This transform can be used to represent a signal that exists in time, such as the ones that are used in communications networks, in an abstract representation that is instead based on the frequencies that signal occupies. Its not an exaggeration to say that almost all of communications theory is based on the frequency based representation which is also called the Spectrum of the signal.  By using the spectral representation, we are able to manipulate time based signals in various ways, which would be impossible to do otherwise.

Before launching into the Fourier Transform, I am going to introduce a simpler version, that was also discovered by Fourier, called the Fourier Series.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm22.png) 

Figure 1: Decomposition of a time domain signal into its frequency domain components

The fundamental idea behind the Fourier Series is illustrated in Fig. 1, which shows a periodic time domain signal with period T (in approximate square wave shape, in the lower left of the figure). Fourier proposed that any such signal can be represented as a linear combination of sine and cosine functions, whose frequencies are integer multiples of the base frequency ${2\pi\over T}$, as follows

$$ x(t) = a_0 + \sum_{n=1}^N [a_n \cos {2\pi n\over T}t + b_n \sin {2\pi n\over T}t] $$

This decomposition of $x(t)$ into simpler functions is known as the Fourier Series. You can see why x(t) is constrained to be a periodic function with period T, since both sine and cosine are periodic with this period. In this case the Layer 2 representation for the signal $x(t)$ is the set of coefficients ${a_0, a_1, b_1, a_2, b_2, ...}$. Hence we have replaced a complex time based periodic function, by an equivalent representation which consists of a bunch of numbers, which is a huge amount of simplification.
Fourier's insight was his realization that this decomposition could be done for any periodic function $x(t)$.
Fourier showed that these co-efficients can be computed using the formulae:

$$ a_0 = {1\over T}\int_{-{T\over 2}}^{T\over 2} x(t) dt $$
$$ a_n = {1\over T}\int_{-{T\over 2}}^{T\over 2} x(t)\cos{{2\pi n\over T}t} dt,\ for\ n\ge 1 $$
$$ b_n = {1\over T}\int_{-{T\over 2}}^{T\over 2} x(t)\sin{{2\pi n\over T}t} dt,\ for\ n\ge 1 $$

There is an equivalent representation of the Fourier Series using complex numbers, which utilizes the Euler Formula $e^{j\theta} = \cos\theta + j\sin\theta$:

$$ x(t) = \sum_{n=-N}^N c_n e^{{2\pi n\over T}t}\ \ \ where\ \ \ c_n = {1\over T}\int_{-{T\over 2}}^{T\over 2} x(t)e^{-{2\pi n\over T}t} dt  $$

where $c_n$ is now a complex number. 
The quantity $1\over T$ is the frequency $f$, and using this notation the equations become

$$ x(t) = \sum_{n=-N}^N c_n e^{2\pi nf t}\ \ \ where\ \ \ c_n = {1\over T}\int_{-{T\over 2}}^{T\over 2} x(t)e^{-2\pi nf t} dt  $$

Since the Fourier Series can only be used for perioidic signals, what about aperiodic signals that occur just once in time.
This is where the Fourier Transform comes into the picture, and is given by the formulae:

$$ x(t) = \int_{-\infty}^{\infty} X(f)e^{2\pi f t} df  $$
$$ X(f) = \int_{-\infty}^{\infty} x(t) e^{-2\pi f t} dt $$

Thus the Fourier Transform of an aperiodic time function $x(t)$ ia another aperiodic function $X(f)$ that exists in the frequency space.
Hence if $x(t)$ is aperiodic, the frequencies $f$ needed to represent it is no longer form a discrete set, but instead become a function $X(f)$ that exists over a continuum of frequences! In order to get an intuitive understanding for why this is the case, note that in the Fourier Series representation, two neighboring frequencies are separated by $\Delta f = {1\over T}$. We can convert a periodic $x(t)$ into a aperiodic function by making $T$ larger and larger, and in the limit as $T\rightarrow\infty$, we can see that the separation between adjacent frequencies in its Fourier Series representation goes to zero, which is the same as saying that the frquencies now form a continuum (also the product $nf$ approaches a finite quantity, as $n$ goes to infinity and $f$ goes to zero).

### The Discrete Fourier Transform

The Fourier Transform works well enough for signals that are continous in time, but we live in a digital world, and the computers that we depend on can only process discrete numbers. In order to enable this, a continous signal has to be discretized, and the first step in this direction was taken by by the eminent scientist Harry Nyquist, who worked in Bell Labs in the period prior to World War 2.



## Single Carrier Modulation 

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm3.png) 

Figure 2: Fourier Transform of a Baseband Rectangular Pulse


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm5.png) 

Figure 3: Effect of Pulse Width on Bandwidth


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm6.png) 

Figure 4: Fourier Transform of a Passband Rectangular Pulse


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm7.png) 

Figure: Modulation using Phase Shift Keying


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm8.png) 

Figure: Modulation using 8-PSK


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm9.png) 

Figure: Generating I and Q Components of a QAM signal


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm10.png) 

Figure: A Single Carrier based QAM Modulator


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm11.png) 

Figure: A Single Carrier based QAM De-Modulator







## The Wireless Channel

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm12.png) 

Figure: Sources of Multipath Interference


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm13.png) 

Figure: Inter-Symbol Interference due to Multipath




### Problems with SCM in Broadband Wireless Systems


Figure: Inter-Symbol Interference in Single Carrier Systems





## OFDM: How to Pack More Bits into a Single Large Symbol

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm17.png) 

Figure: Generating an OFDM Symbol

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm14.jpg) 

Figure: Generating an OFDM Symbol

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm15.jpg) 

Figure: Inter-Symbol interference in OFDM


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm16.jpg) 

Figure: Effect of Channel Distortion in OFDM



### The OFDM Transmitter and Receiver


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm21.gif) 

Figure: The Overall System using OFDM, Transmitter + Receiver


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm18.jpg) 

Figure 18: OFDM Sub-Carriers


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm19.jpg) 

Figure: OFDM vs Regular Frequency Division Multiplexing


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm20.ppm) 

Figure: Using Inverse Discrete Fourier Transform in an OFDM Transmitter






## OFDM Implementation using the Fourier Transform

