---
layout: default
title: "The Technology That Made Broadband Wireless Possible"
---

# The Technology That Made Broadband Wireless Possible


## Introduction

Those of you who are old enough will recall the era before 2010 when Nokia, Motorola and Blackberry dominated the market for wireless handsets. These phones had become quite proficient in handling mobile voice calls, but when it came to data, the bitrates that they provided was not quite good enough. It was possible to do some text based web surfing, but when it came to full graphics based web pages, or youtube video streaming, they were not quite up to the task. All this changed in 2011, when suddenly phones suddenly became as good as desktop terminals in running even the most graphics laden content, and streaming video became omnipresent. 

So what changed? It was not due to the iPhone, since this handset had been launched a few years earlier in 2007. 
The wireless technology did, as the transition from 3G networks to 4G happened right around that time. This article is about a key technology in 4G wireless that enabled higher data rates, called Orthogonal Frequency Division Multiplexing or OFDM. The name sounds rather formidable, but I think it is possible to explain the essence of how OFDM works even to the non specialist with some knowledge of college level maths, and I am going to make an attempt to do so. OFDM exists at the bottom of the communications protocol stack, and most people don't even know about its exisence, since most of the attention is grabbed by handsets such as the iPhone and the applications running on it. But without OFDM, high speed communications on the iPhone would not have been possible.

Before I launch into OFDM and 4G wireless, I want to briefly mention the technology that they replaced, namely 3G wireless. The latter was launched in 2001, and was the first technology that seriously tried to integrate voice AND data communications capability into the handset. Unfortunately the 3G protocol was designed in the era when voice was still based on an older technology called circuit switching, and thats what went into 3G. Data was considered to be the less important feature, hence its design was an add-on, based on a voice centric technology called circuit switching. Unfortunately circuit switching is not the best way to handle data, which does better with a technology called packet switching, and this handicapped 3G phone performance. 
The other big issue with 3G was the PHY or physical layer protocol that was used, which was based on a technology called Code Division Multiple Access or CDMA. CDMA paired well with circuit switching, but it was not very well suited for data. '
However it had a very strong political backing, in the form of the companies Qualcomm and Ericsson which held a number of important CDMA patents.
So the transition from CDMA to OFDM is also a story of how an insurgent technology, promoted by a few small start-ups, was able to overcome the powerful forces that were aligned against it.

I had some personal involvement in the transition from 3G to 4G wireless, and had a first hand view of the politics involved. I was a co-founder of a start-up called Aperto Networks that did some of the work that ultimately resulted in 4G, and for a number of years I was a member of the IEEE 802.16 Standards Committee that was working on 4G, even chairing the Medium Access Control or MAC group for a while. The MAC protocol lies on top of PHY layers such as CDMA or OFDM, and it had to completely re-designed for packet based wireless communications. But this article is not about the MAC, perhaps it will be a subject of a future article.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm19.jpg) 

Figure: OFDM vs Regular Frequency Division Multiplexing

The basic idea behind OFDM is not that difficult to grasp, and an analogy can be made with the shift in the computer hardware industry that happened in the early 2000s. 
After the launch of the web in the mid 1990s, focus shifted to building more and more powerful servers that could be used for serving web pages, and for a time companies such as SUN Microsystems thrived by supplying this market. However it soon became clear that even the most powerful single machine could not keep up with the demand. Fortunately companies such as Google pioneered the concept of a datacenter made up of thousands of cheap commodity Dell type servers. By working together in parallel, these machines became capable of scaling up to serve even the most demanding workload. At the same time, this "Datcenter as Computer" architecture made the system more robust, since it could easily recover from the loss of a few of the machines at any one time, due to the redundancy that was built into the system.
Hence there was a shift from single monlithic system that was expensive and prone to failure, to a distributed robust system with thousands of subsystems, which could easily scale up.

Exactly the same dynamic occured in wireless system. The broadband wireless technolgies that came before OFDM (called single carrier modulation) worked by having each transmission occupy the entire channel spectrum (see top part of above figure). Using up all the bandwidth increased the resulting bit rate to braodband speeds, and this technology is still is use for cable model systems. However for wireless transmission single carrier systems came up against a fundamental limit to how much a single channel could support, and this was first pointed out by Claude Shannon in the 1940s. Shannon showed that the ultimate capacity C of channel with bandwidth B Hertz, is given by the following rather simple looking formula:

$$ C = B\ \log (1 + {S\over N}) $$

Here ${S\over N}$ is the signal to noise ratio for the channel, and this ultimately limits the capacity of a channel. Wireless transmissions are subject to all kinds of channel impairments, due to the fact that they are completely exposed to the environment, hwich causes them to have a lower ${S\over N}$ compared to cable modem systems for example, in which all tranmissions occur in a heavily shielded wired medium. Using an entire channel is similar to using up an entire CPU in a server, and the only way to scale up single CPU systems was by making the clock speed faster and faster. This ultimately runs up against the fundamental physics of semiconductor technology, which can be considered to be a type of Shannon capacity limiing the speed of single CPUS. Computer systems got around this bottleneck by using thousands of less powerful CPUs working together to solve a problem, 
and as shown in the bottom part of the figure, communication engineers came up with a similar strategy.

OFDM can likened to splitting up that data stream and carrying it on hundreds of smaller peices of spectrum, called sub-carriers in the jargon. Each of these sub-carriers is now carrying much less data compared to single carrier system, but since there are thousands of them, they make up for lower capacity by working in parallel, and thus are able to acheive at least an equivalent data rate, and a much higher data rate in practice. This is due to the fact that different sub-carriers in OFDM can adaptively be tuned so that part sof of the specturm that are less noising carry more data. This luxury is not available to single carrier systems, in which transmissions are effectively done at the lowest common denominator of the speeds that are available.

Morover OFDM systems are much more robust in an unforgiving wireless environment. Problems in the wireless channel are often limited to local parts of the spectrum, called frequency selective fading. In an OFDM system this affects only some of the sub-carriers, and using channel coding techniques it is even possible to recover the lost data. Single carrier systems on the other hand don't work very well in this environment, since problems that are localized in the spectrum end up affecting the entire transmission.
Also much higher data rates are acheivable in OFDM by adding additional sub-carriers, assuming a wider channel is available. Single carrier systems can also increase their data rate by using a wider channel, however in doing so they run up against the wireless channel, which becomes much less hospitable to transmissions as the channel width increases. This has to do with a phenomenon called multipath fading, which we will talk about in more detail later in this article.

## The Fourier Transform

To get to an understanding of how OFDM works, it is necessary to know a mathematical technique called the Fourier Transform. It was first published by Joseph Fourier of France in the 1820s, and since then it has become one of the most powerful tools in the arsenal for mathematicians and engineers. The Fourier Transform is another example of the 2-Layer Principle for organizing complex data, that I talked about in an earlier article called "Latent Varibales and Latent Spaces". The principle states that data can often be represented in two ways: (1) As it exists in the real world, and thus can be measured using instruments, and (2) In an abstract mathematical space, which we can access only by performing some mathematical operations on the real world data. Moreover the two represenations can be transformed into one another using math.
The abstract representation is often easier to manipulate and analyze, and a number of difficult problems in the real world can be solved, by first solving the problem in the abstract space. Other examples of this 2-Layer Principle from the earlier article include:

- Representing data such as images and language using Latent Variables. The mathematical transformation in this case is represented by Artificial Neural Networks. This representation lies at the heart of all the progress being made in this field.
- Representing physical phenmenona using the idea of Fields. This started with Maxwell and the Electromagnetic Field, and went on to represent matter using Quantum Fields. Also the Schrodinger Wave Function for a particle can be represented either in terms of its location x in space, or its momentum p, and and these two representation $\psi(x)$ and $\psi(p)$ are Fourier Transforms of each other!

It can be argued that a great deal of scientific progress in the last 200 years has been made by exploting the 2-Layer Principle. 
The Fourier Transform can be considered to be the original example of this principle, and hence it fitting that the fundamental duality of matter in terms of waves and particles is intimately connected with it. 
Within the realm of communications systems, 
this transform can be used to represent a signal that exists in time, into an abstract representation that is instead based on the frequencies that signal occupies. It is not an exaggeration to say that almost all of the progress in communications theory in the last 100 years is based on expoliting the properties of the frequency based representation which is also called the spectrum of the signal.  By using the spectral representation, we are able to manipulate time based signals in various ways, which would be impossible to do otherwise. 

Before launching into the Fourier Transform, I am going to introduce a simpler version, that was also discovered by Fourier, called the Fourier Series.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm22.png) 

Figure 1: Decomposition of a time domain signal into its frequency domain components

The fundamental idea behind the Fourier Series is illustrated in Fig. 1, which shows a periodic time domain signal with period T (in approximate square wave shape, in the lower left of the figure). Fourier proposed that any such signal can be represented as a linear combination of sine and cosine functions, also called tones, whose frequencies are integer multiples of the base frequency ${2\pi\over T}$, as follows

$$ x(t) = a_0 + \sum_{n=1}^N [a_n \cos {2\pi n\over T}t + b_n \sin {2\pi n\over T}t] $$

This decomposition of a complicated function into its tones is known as the Fourier Series. The transform can also be understood by thinking in terms of musical notes. Expert musicians are said to have the ability to make out individual tones in a complex piece of music, their brain is essentially carrying out the Fourier Transform!

You can see why x(t) is constrained to be a periodic function with period T, since both sine and cosine are periodic with this period. In this case the Layer 2 representation for the signal $x(t)$ is the set of coefficients ${a_0, a_1, b_1, a_2, b_2, ...}$. Hence we have replaced a complex time based periodic function, by an equivalent representation which consists of a bunch of numbers, which is a huge amount of simplification.
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
Hence if $x(t)$ is aperiodic, the frequencies $f$ needed to represent it is no longer form a discrete set, but instead become a function $X(f)$ that exists over a continuum of frequences! In order to provide an heuristic justification for these formulae, note that in the Fourier Series representation, two neighboring frequencies are separated by $\Delta f = {1\over T}$. We can convert a periodic $x(t)$ into a aperiodic function by making $T$ larger and larger, and in the limit as $T\rightarrow\infty$, we can see that the separation between adjacent frequencies in its Fourier Series representation goes to zero, which is the same as saying that the frquencies now form a continuum (also the product $nf$ approaches a finite quantity, as $n$ goes to infinity and $f$ goes to zero).

### The Discrete Fourier Transform

The Fourier Transform works well enough for signals that are continous in time, but we live in a digital world, and the computers that we depend on can only process discrete numbers. In order to enable this, a continuous signal has to be discretized, before any further processing can be applied to it and furthermore the Fourier Transform has to take this into account. The next few figures go through the discretization process, and the resulting transform called the Discrete Fourier Transform or DFT. OFDM utilizes DFT in its design, hence the foucus on this.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm22a.png) 

Figure: Fourier Transform (in red) for a signal (in blue)

As before, let $x(t)$ be a continuous time signal that is defined over the onterval $[0,1]$ with Fourier Transform $\tilde X(f)$.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm22b.png) 

Figure: Fourier Transform (in red) for a signal that is sampled in time (in blue)

Let $x[n]$ denote samples of this signal, taken at the rate of $f_s={1\over T_s}$ samples/second, where $T_s$ is the sampling period. Furthermore assume that N samples are taken over the interval $[0,1]$, so that $N = {1\over T_s}$.
Thus we have

$$ x[n] = x(nT_s), \ \ \ for\ \ \  0\le n\le N-1\ \ \ and\ \ \  0\ \ \ otherwise $$

Furthermore assume that $X(f)$ is the Fourier Transform of $x[n], 0\le n\le N-1$, so that

$$ X(f) = \sum_{n=0}^{N-1} x[n] e^{-j2\pi fn},\ \ \ 0\le f\le 1  $$

From this equation we can see that $X(f)$ is a periodic function. Hence discretization in the time domain causes periodicity in the frequency domain.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm22c.png) 

Figure: Inverse Fourier Transform (in blue) for a signal that is sampled in frequency (in red)

If, instead of discretizing the time domain signal $x(t)$, what would happen if we discretized the frequency domain signal $\tilde X(f)?
If we evaluate $X(f)$ only at discrete values of frequency $[0, \Delta f, 2\Delta f,..., (N-1)\Delta_f]$, where $\Delta f = {1\over N}$, and defining $X_k = {\tilde X}(k\Delta f]$, then what is its Inverse Fourier Transform? The result of this operation is shown in the above figure and as can be seen, it results in a periodic and continuous  function in time.


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm22d.png) 

Figure: Fourier and Inverse Fourier Transforms for a signal that is sampled in both time and frequency

Finally, what would be the result if both the time domain and frequency domain functions were to be discretized as shown in the above figure? This results in the Discrete Fourier Transform, whose equations are given by:

$$ X_k = \sum_{n=0}^{N-1} x[n] e^{-j2\\pi {k\over N}n},\ \ \ for\ \ \ k=0,1,...,N-1  $$

This formula can be inverted to obtain

$$ x[n] = {1\over N}\sum_{k=0}^{N-1} X_k e^{j2\pi {k\over N}n} \ \ \ for\ \ \ n=0,1,...N-1 $$

The last two equations constitute the Discrete Fourier Transform and the Inverse Discrere Fourier Transform respectively. Note that these transforms allow all signals to be processed in the digital domain.

You may be wondering that by discretizing a continuos time signal, we may be throwing away useful information. 
But in fact this is not the case, as was proven by Harry Nyquist, who worked in Bell Labs in the period prior to World War 2. This work was further extended by Claude Shannon, so the work is referred to as the Nyquist-Shannon Sampling Theorem. 
The theorem states that as long as we sample a signal fast enough, it is always possible to re-create the original signal from the samples. The minimum sampling rate for perfect re-construction is $2B$, where $B$ is the maximum frequency in the Fourier Transform of $x(t)$. This is an amazing result, and one can get an intuitive understanding of why is is true by examining Fig. xx. It shows that if a continuous time signal is discretized, then its resulting Fourier Transform is just the periodic continuation of $\tilde X(f)$, where the latter was the Fourier transform of the continuous time signal. Hence if we were to filter out just one of these shapes, and take its Inverse Fourier Transform, the we would have  recovered the original signal $x(t)$!

## The Wireless Channel

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm12.png) 

Figure: Sources of Multipath Interference


![](https://subirvarma.github.io/GeneralCognitics/images/ofdm13.png) 

Figure: Inter-Symbol Interference due to Multipath



## Digital Baseband Communications OR How Data is Sent on a Fiber Optic Link

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm23.png) 

Figure: Sending Morse Code Data

At the dawn of the Communications Age, when Samuel Morse was experimenting with ways in which he could send the code pulses across, he noticed that received pulses tended to get smeared out in time (see above figure), and thus interfere with neighboring pulses. In order to avoid this, he left enough of a gap between pulses, as shown in the figure. This solved his problem, but at the cost of a reduced data rate. In our own digital age, all data is in the form of 1s and 0s, and the communications engineers working in the early years of digital transmission, faced exactly the same problem, i.e., how to reliably get the bits across the channel.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm24.png) 

Figure: Sending the Sequence 101101 using Square Wave Pulses

The most straightforward way of solving the problem was to use a square pulse, and the above figure shows the resulting signal when 101101 is sent using these.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm25.png) 

Figure: The Received Signal

Once again we see the spreading of individual pulses, also called symbols, at the receiver which can lead to high bit error rates, a phenomenon known as Inter Symbol Interference or ISI. Note that the received signal is the sum of the amplitudes from all the symbols that are active at any one point in time.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm4.png) 

Figure: Fourier Transform of a Square Pulse

So how should we modify the pulse shape to avoid ISI? The Fourier Transform comes to our rescue in solving this problem. The above figure shows the Fourier Transform for a square pulse $x(t)$ in the time domain and this results in the so called sinc function $X(f)$ in the frequency domain, given by

$$ X(f) = {\sin \pi f T\over{\pi f}} $$

where $T$ is the pulse duration, which we will also refer to as the Symbol Time. Note that the Fourier Transform $X(f)$ has zeroes at the points ${n\over T}$ for integer values of $n$.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm30.png) 

Figure: Fourier Transform of a Sinc Pulse

Consider a sinc function that is defined in the time domain given by $x(t) = {\sin \pi F t\over{\pi t}}$. From the prior discussion it follows that its Fourier Transform is given by a square pulse $X(f)$ in the frequency domain, as shown in the above figure. It turns out that the time domain sinc pulse is the optimum way to send digital data over a channel, and this was discovered by Nyquist. In order to make these shapes realizable using circuitry, he derived a slightly modified form of the sinc pulse, now known as a Raised Cosine Pulse, and these are in use for digital communications even today. 

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm26.png) 

Figure: Resulting waveform in time when sending 1011 Using 4 Sinc Pulses

Note the time version of the sinc has zeroes at $nT$ for integer values of $n$, and this property is very useful when sending a train of pulses back to back, separated by the period $T$. The above figure shows the resulting waveform when the bit sequence 1011 in time using sinc pulses. Just as in the case of square pulses, the signal for a particular pulse leaks over to other pulses, but with one big distinction: The peak of a pulse, co-incides with the zeroes of all the neighboring pulses! This property follows from the fact that the sinc has zeroes at integer multiples of $T$. This property implies that is no inter symbol interference between neighboring sinc pulses.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm31.png) 

Figure 3: Effect of Sinc Pulse Width on Bandwidth

Another very important property of sinc pulses is the variation of bandwidth with the width of a pulse. In general, as the pulse width, i.e., T increases, the bandwidth required for transmission decreases, as shown in the above figure (for the case $T=1$). In general the required bandwidth is ${1\over{2T}}$, i.e., one half the symbol rate. This is a very important property that comes into use in the design of OFDM. The sinc function has the property that its Fourier Transform X(f) uses up the least amount of bandwidth, and a more efficient function has not been found.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm27.png) 

Figure: End to End Baseband Communication System

If were designing a baseband digital communications system, this is almost all we need to know, and the end-to-end block diagram of such a system is shown above. The bits stream that originates from the source on the left, gets shaped by three filters on the way to the destination, the Transmit and Receive Filters, as well as the frequency response of the channel itself. The Nyquist sinc type filter that we have discussed, actually gets implemented as two filters, one at the transmitter and the other at the receiver. These filters, called Root Raised Cosime Filters or RRC, are designed such that their serial operation results in the Raised Cosine pulse shape.
Note that more than 1 bit can be mapped on to the same symbol, for example by using a set of sinc pulses with different amplitudes. If four amplitudes are used, then 2 bits can be mapped on to each symbol, so that the bitrate f the channel would be twice the symbol rate.

Baseband communication systems are an important topic in their own right, and are used in sending digital data over Fiber Optic communications for example. However, for wireless and cable systems the basedband signal has to be upconverted to the appropriate frequency slot, before it can be transmitted, and this is the subject of the next section.

## Single Carrier Modulation OR How Data is Sent over a Cable Modem

Data transmission over a wireless or cable systems requires that the signal energy be confined to an assigned frequency slot in the spectrum, called a channel (for example cellular 4G communications happens over channels that are allocated in various frequency bands between 600 MHz and 2.4 GHz).  How can we shift our signal from the  baseband to another to channel that exists at a higher frequency in the spectrum? Once again the Fourier Transform comes to the rescue, as shown in the figure below.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm36.png) 

If we take a baseband signal and multiply it by a carrier wave, then the Fourier Transform tells us that the resulting signal now occupies a channel whose center frequency co-icides with that of the carrier. This can be shown using the following calculation:
If $X(f)$ is the Fourier Transforms of $x(t)$, then the Fourier Transform of $x_g(t) = x(t) e^{j2\pi gt}$ is given $X(f-g)$ (see above figure).
An application of the Euler Formula $e^{j\theta} = \cox\theta+j\sin\theta$ then leads to the result that Fourier Transform of $x(t)\cos (2\pi f_0 t)$ is given by ${X(f-f_0)+X(f+f_0)\over 2}$. This is precisely the property that we are looking for, i.e., the ability to shift the spectrum occupied by the baseband pulse. The resulting waveform is known as a passband pulse and the cosine function used to do the translation is the carrier wave.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm6.png) 

Figure 4: (a) A Baseband Sinc Pulse and its Fourier Transform (b) A Passband Sinc Pulse and its Fourier Transform. The baseband pulse has been shifted by 7.5 GHz.

The shift in frequency of a baseband sinc pulse from 0 GHz to 7.5 GHz is illustrated in the above figure. Note that as a result of the shift, the bandwidth occupied by the passband pulse is double that of the baseband pulse, i.e., for a pulse of width $T$, the baseband bandwidth that it occupes is ${1\over{2T}}$ while its passband bandwidth usage is ${1\over T}$.

The use of the carrier wave results in some interesting new possibilities that did not exist in the baseband case. In particular it allows us to use the parameters of the carrier wave as another way in which sinc pulses can be differentiated. In the baseband case we were confined to using the amplitude of the sinc pulse as means of differentiation, but now in the passband we can also make use of the phase of the carrier wave. Hence it is now possible to define a so called constellation of passband sinc pulses, with differing amplitudes and phases, and this is called Quadrature Amplitude Modulation or QAM. One of the simplest QAM constelations is called Quadrature Phase Shift Keying or QPSK, and we will describe that next.

The basic idea behind QPSK is quite simple and goes as follows: 
The incoming bit stream gets grouped together two bits at a time, followed by a mapping to one of four waveforms, for $0\le t\le T$, where $T$ is the symbol time:

- Bit pattern 00 gets mapped on to the carrier wave $\sqrt{2}A\cos(2\pi f_c t + {\pi\over 4})$.
- Bit pattern 10 gets mapped on to $\sqrt{2} A\cos (2\pi f_c t + {3\pi\over 4})$.
- Bit pattern 11 gets mapped on to $\sqrt{2} A\cos (2\pi f_c t + {5\pi\over 4})$.
- Bit pattern 01 gets mapped on to $\sqrt{2} A\cos (2\pi f_c t + {7\pi\over 4})$.

Hence we can see that the different bit patterns are differentiated based solely on the phase of the carrier wave. This mapping can be nicely represented in the complex plane as follows:
- Bit pattern 00 gets mapped on to the complex number $({1\over{\sqrt 2}}, {j\over{\sqrt 2}}) $
- Bit pattern 10 gets mapped on to $(-{1\over{\sqrt 2}}, {j\over{\sqrt 2}})$
- Bit pattern 11 gets mapped on to $(-{1\over{\sqrt 2}}, -{j\over{\sqrt 2}})$
- Bit pattern 01 gets mapped on to $({1\over{\sqrt 2}}, -{j\over{\sqrt 2}})$

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm37.png) 

Figure: Passband Modulation using Quadrature Phase Shift Keying or QPSK

The 4 values can also be plotted on the complex plane as shown above

Using this mapping the QPSK waveform can be written as:

$$ x(t) = \sqrt{2} A [Re(a)\cos(2\pi f_c t) - Im(a)\sin(2\pi f_c t),\ \ \ 0\le t\le T $$

where the complex number $a$ takes on one of the four values from the mapping above, depending upon the bits being transmitted. The numbers $\sqrt{2} A \Re{a}$ and $\sqrt{2} A \Im{a}$ are also referred to as the I and Q amplitudes of the signal $x(t)$.
Using this equations, the QPSK transmitter can be implemented as shown below:

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm32.png) 

Figure: A Single Carrier based QPSK Modulator

The figure shows that the incoming bit stream on the left is first converted to consecutively occuring pairs of bits in the Serial to Parallel Converter. Since 2 bits map to a single symbol, the resulting symbol rate $R_s$ is half of the bitrate $R_b$. The mapping from bitpairs to the imaginary number $a$ is then used to determine the Real and Complaex parts of $a$, which determine the I and Q amplitudes of signal. Next the baseband pulse for the signal is generated by using the Nyquist Root Raised Cosine (RRC) Filter in order to avoid Inter Symbol Interference, as discussed in the prior section. This is followed by multiplication of the I and Q components of the amplitude by $\cos(2\pi f_c t)$ and $\sin(2\pi f_c t)$ resepectively, in order to shift the pulse to the center frequency $f_c$. Finally the two compnents are added to generate the signal to be transmitted.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm11.png) 

Figure: A Single Carrier based QPSK De-Modulator

A QPSK receiver is shown above. The incoming pulse is first multiplied by the carrier so as to shift it in frequency to the baseband, and isolate its I and Q components. This is followed by the receive RRC filtering, and finally sampling to recover the bits.

![](https://subirvarma.github.io/GeneralCognitics/images/ofdm38.png) 

Figure: Higher Level Signal Constellation (a) QPSK (b) 8-PSK (c) 32-QAM (d) 16-QAM (e) 128-QAM

The bitrate for a single carrier system can be increased over that of QPSK by packing more bits into a single symbol. This can be done by increasing the number of shapes, which can be done either by varing the phase of the carrier or its amplitude. As for QPSK, this can be conveniently illustrated on the complex plane, as shown in the above figure, which shows the I and Q components, for a few higher order modulations. For example 128-QAM maps 7 bits to each symbol, so that the resulting bit rate is 3.5x that of QPSK (for the same symbol rate).
So how far can this process go, i.e., can we keep increasing the constellation size and realize greater and greater bitrates? It turns out that with more sophisticated  systems, it is possible to incraese it by quite a bit. For example the cable modem standard DOCSIS specifies that 4096-QAM is mandatory, while 8192-QAM and 16,384-QM are optional on cable modems!
But ultimately, this technique runs into the Shannon Channel Capacity limit $C = B\log (1+{S\over N})$, since packing more constellation points means that they will move closer and closer to each other, and at some point the noise in the channel will make it impossible to differentiate one symbol from another. In fact DOCSIS 3.1, which is the latest iteration of the standard, now specifies that OFDM be used instead of QAM, which allows even higher bitrates by increasing the channel bandwidth $B$ without compromising on the error performance.


### Problems with SCM in Broadband Wireless Systems


Figure: Inter-Symbol Interference in Single Carrier Systems





## OFDM OR How Data is Sent over a Broadband Wireless Link

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




![](https://subirvarma.github.io/GeneralCognitics/images/ofdm20.ppm) 

Figure: Using Inverse Discrete Fourier Transform in an OFDM Transmitter






## OFDM Implementation using the Discrete Fourier Transform

