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

To get to an understanding of how OFDM works, it is necessary to know a mathematical technique called the Fourier Transform. It was first published by Joseph Fourier of France in the 1820s, and since then it has become one of the most powerful tools in the arsenal for mathematicians and engineers.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm22.png) 

Figure 1: Decomposition of a time domain signal into its frequency domain components

The fundamental idea behind the transform is illustrated in Fig. 1, which shows a periodic time domain signal with period T. Fourier proposed that any such signal can be written as a simple linear combinations of sine and cosine functions, as follows:

$$ x(t) = a_0 + \sum_{n=1}^N [a_n \cos {2\pi n\over T}t + b_n \sin {2\pi n\over T}t] $$

This decomposition of $x(t)$ ino simpler functions is known as the Fourier Series. The co-efficients are given by 

$$ a_0 = {1\over T}\int_{-{T\over 2}}^{T\over 2} x(t) dt $$
$$ a_n = {1\over T}\int_{-{T\over 2}}^{T\over 2} x(t)\cos{{2\pi n\over T}t} dt,\ for\ n\ge 1 $$
$$ b_n = {1\over T}\int_{-{T\over 2}}^{T\over 2} x(t)\sin{{2\pi n\over T}t} dt,\ for\ n\ge 1 $$

By using the Euler Formula $e^{j\theta} = \cos\theta + j\sin\theta$, it can also be written as

$$ x(t) = \sum_{n=-N}^N c_n e^{{2\pi n\over T}t}\ where\ c_n = {1\over T}\int_{-{T\over 2}}^{T\over 2} x(t)e^{-{2\pi n\over T}t} dt  $$

The quantity $2\pi\over T$ is referred to as the angular frequency $\omega$, and using this notation the equations become

$$ x(t) = \sum_{n=-N}^N c_n e^{n\omega t}\ where\ c_n = {1\over T}\int_{-{T\over 2}}^{T\over 2} x(t)e^{-n\omega t} dt  $$


where $c_n$ is now a complex number. 

Since the Fourier Series can only be used for perioidic signals, what about aperiodic signals. This is where the Fourier Transform comes into the picture, and is given by the formulae:

$$ x(t) = {1\over 2\pi}\int_{-\infty}^{\infty} X(\omega)e^{\omega t} d\omega  $$
$$ X(\omega) = \int_{-\infty}^{\infty} x(t) e^{-\omega t} dt $$



![](https://subirvarma.github.io/GeneralCognitics/images/ofdm3.png) 

Figure 2: Fourier Transform of a Baseband Rectangular Pulse


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm5.png) 

Figure 3: Effect of Pulse Width on Bandwidth


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm6.png) 

Figure 4: Fourier Transform of a Passband Rectangular Pulse



In an earlier article, I wrote about how a lot of complex system can be organized using the 2-layer principle. This states that it is possible to transform something that looks very complicated, such as a color image with hundreds of thousands of pixels, into another simpler object such as a vector, by abstracting out its critical components. The mathematical transformation that converts an image into the vector (called the Latent Vector), was represented by a Neural Network. This transform works in both directions, so it is possible to recover the original image from its Latent Vector representation.

### The Discrete Fourier Transform



## Single Carrier Modulation 

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

