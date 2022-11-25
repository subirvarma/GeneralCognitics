---
layout: default
title: "Books"
---

# Internet Congestion Control

![](https://subirvarma.github.io/GeneralCognitics/images/CongestionControl.png)

**Internet Congestion Control** was published by Morgan Kaufmann in 2015. It can be purchased at Amazon using the following [link](https://www.amazon.com/Internet-Congestion-Control-Subir-Varma-ebook/dp/B0148FPPO8/ref=sr_1_3?crid=1VVYTVTIB8XOS&keywords=internet+congestion+control&qid=1669339227&sprefix=internet+congestion+control%2Caps%2C131&sr=8-3). A short summary of each of the chapters in the book is provided below.

**Chapter 1: Introduction** 
This chapter is an introduction to the subject of congestion control, and covers some basic results in this area, such as the Chiu-Jain result on the optimality of AIMD control, descriptions of fundamental congestion control algorithms such TCP Reno, TCP Vegas and RED based Active Queue Management. A detailed description of TCP Reno is provided including algorithms such as: Congestion avoidance, Fast Re-transmit and Fast Recovery, Slow Start, TCP Timer operation etc. Active Queue Management or AQM techniques are introduced and the Random Early Detection or RED algorithm is  described. 

Key Words: 
Congestion Control definition and objectives; TCP Reno; TCP Vegas; Active Queue Management; AQM; Random Early Detection; RED; Congestion Avoidance; Fast Re-transmit; Fast Recovery; Slow Start.

**Chapter 2: Analytic Modeling of Congestion Control**
This chapter has a detailed discussion of TCP models, starting from simple models using fluid approximations to more sophisticated models using stochastic theory. The well known “Square Root” formula for the throughput of a TCP connection is derived, and is further generalized to AIMD congestion control schemes. These formulae have proven to be very useful over the years, and have formed an integral part of the discovery of new congestion control protocols, as shown in Part 2 of this book. A general procedure for deriving an expression for the throughput of a congestion control algorithm is also presented. This chapter also analyzes systems with multiple parallel TCP connections, and derives expressions for the throughput ratio as a function of the round trip latencies.

Key Words:
TCP Throughput Models; Additive Increase Multiplicative Decrease; TCP Square Root Formula; TCP Throughput with Link Errors; Fluid Flow Models of TCP; Congestion Control Analytic Modeling; Congestion Control Stochastic Models; Multiple Parallel TCP Connections.

**Chapter 3: Optimization and Control Theoretic Analysis of Congestion Control**
In this chapter Optimization Theory and Control Theory are applied to a differential equation based fluid flow model of the packet network. This results in the decomposition of the global optimization problem into independent optimizations at each source node and the explicit derivation of the optimal source rate control rules as a function of a network wide utility function. In the case of TCP Reno, the source rate control rules are known, but then the theory can be used to derive the network utility function that Reno optimizes. In addition to the mathematical elegance of these results, the results of this theory have been used recently to obtain optimal congestion control algorithms using Machine Learning techniques. The system stability analysis techniques using the Nyquist Criterion that we introduce in this chapter, have become an essential tool in the study of congestion control algorithms. By using a linear approximation to the delay-differential equation describing the system dynamics, this technique enables us to derive explicit conditions on system parameters in order to achieve a stable system.

Key Words:
Congestion control and optimization theory; congestion control and optimal control theory; Fluid Flow model of congestion control; Congestion control and Nyquist Stability; Congestion Control Lagrangian Optimization; Congestion Control Dual Optimization problem; Congestion Control Primal Optimization problem; Active Queue Management; AQM; Random Early Detection; RED; Proportional Controller; Proportional plus Integral Controller; The Averaging Principle; TCP Utility Function

**Chapter 4: Congestion Control in Broadband Wireless Networks**
This chapter is on congestion control in broadband wireless networks. This work was motivated by finding solutions to the performance problems that TCP Reno has with wireless links. Since the algorithm cannot differentiate between congestion losses and losses due to link errors, decreasing the window size whenever a packet is lost has a very detrimental effect on performance. We describe TCP Westwood, that solved this problem by keeping an estimate of the data rate of the connection at the bottleneck node. Thus when Duplicate ACKs are received, the sender reduces its window size to the transmit rate at the bottleneck node (rather than blindly cutting the window size by half, as in Reno). This works well for wireless links, since if the packet was lost due to wireless errors, then the bottleneck rate my still be high and this is reflected in the new window size. We also describe techniques such as Split-Connection TCP and Loss Discrimination Algorithms, that are widely used in wireless networks today. The combination of TCP at the end-to-end transport layer and Link Layer Re-transmissions (ARQ) or Forward Error Correction (FEC) coding on the wireless link is also analyzed, using the results from Chapter 2. The large variation in link capacity that is observed in cellular networks, has led to problem called bufferbloat. We describe techniques using AQM at the nodes as well as end-to-end algorithms to solve this problem.

Key Words:
TCP and wireless systems; congestion control in wireless networks; Split Connection TCP; ABE; Available Bandwidth Estimator; LDA; Loss Discrimination Algorithm; Zero Receive Window ACK; TCP Westwood; TCP Westwood Plus; TCP and Forward Error Correction (FEC); TCP and ARQ; Bufferbloat; Adaptive RED; Controlled Delay (CoDel) AQM; TCP LEDBAT.

**Chapter5: Congestion Control in High Speed Networks**
This chapter is on congestion control in high-speed networks with long latencies. One of the consequences of the application of control theory to TCP congestion control was the realization that TCP Reno was inherently unstable as the delay-bandwidth product of the network became large, or even for very large bandwidths. As a result of this, a number of new congestion control designs were suggested with the objective of solving this problem such as HSTCP, TCP BIC, TCP CUBIC and CTCP, which are described in this chapter. Currently TCP CUBIC serves as the default congestion control algorithm for Linux servers, and as a result is as widely deployed as TCP Reno. CTCP is used as the default option for Windows servers, and is also very widely deployed. We also describe the XCP and RCP algorithms that have been very influential in the design of high speed congestion control protocols. Finally we make connections between the algorithms in this chapter and the stability theory from Chapter 3, and give some general guidelines to be used in the design of high speed congestion control algorithms.

Key Words:
Congestion Control in High Speed Networks; TCP over high speed links; TCP Response Function; HSTCP; High Speed TCP; TCP BIC; TCP CUBIC; CTCP; Compound TCP; FAST TCP; XCP Congestion Control; RCP Congestion Control; Scalable TCP; Yeah-TCP; TCP Africa; TCP Illinois.

**Chapter 6: Flow Control for Video Applications**
This chapter is on congestion control for video streaming applications. With the explosion in video streaming traffic in recent years, there arose a need to protect the network from congestion from these types of sources, and at the same time ensure good video performance at the client end. The industry has settled on the use of TCP for transmitting video, even though at first cut it seems to be an unlikely match for video’s real time needs. This problem was solved by a combination of large receive playout buffers which can smoothen out the fluctuations due to TCP rate control, and an ingenious algorithm called HTTP Adaptive Streaming (HAS) or Dynamic Adaptive Streaming over HTTP (DASH). HAS runs at the client end and controls the rate at which “chunks” of video data are sent from the server, such that the sending rate closely matches the rate at which the video is being consumed by the decoder. Chapter 6 describes the work in this area, including several ingenious HAS algorithms for controlling the video transmission rate.

Key Words:
Video congestion control; Video streaming over TCP; HTTP Adaptive Streaming; HAS; Dynamic Adaptive Streaming over HTTP; DASH; Adaptive Bit Rate; ABR; Microsoft HTTP Smooth Streaming; HSS; Apple HTTP Live Streaming; HLS; Adobe HTTP Dynamic Streaming; HDS; Netflix Adaptive Streaming; FESTIVE video congestion control; Video congestion control using Model Predictive Control; PANDA video congestion control.

**Chapter 7: Congestion Control in Data Center Networks**
This chapter is on congestion control in Data Center Networks (DCN). This is the most current, and still rapidly evolving area, due to the enormous importance of DCNs in running the Data Centers that underlie the modern Internet economy. Since DCNs can form a relatively autonomous region, there is also the possibility of doing a significant departure from the norm of congestion control algorithms if the resulting performance is worth it. This has resulted in innovations in congestion control such as, the application of ideas from Earliest Deadline First (EDF) scheduling and even in-network congestion control techniques. All of these are driven by the need to keep the end-to-end latency between two servers in a DCN to values that are in the tens of milliseconds or smaller, in order to satisfy the real time needs to applications such as Web Search or Social Networking. 

Key Words
Congestion control in Data Center Networks; DCN; Tree based DCN; Bi-Section Bandwidth; VL2 Inter-Connection Network; Fat Tree Inter-Connection Network; Data Center TCP; DCTCP; HULL and DCTCP; Deadline Aware Data Center TCP; D2TCP; D3 Congestion Control Algorithm; Pre-emptive Distributed Quick Flow algorithm; PDQ; Multipath TCP; Incast Problem; P-Fabric congestion control algorithm; Detail congestion control algorithm.

**Chapter8: Congestion Control in Ethernet Networks**
This chapter is on the topic of congestion control in Ethernet networks. Traditionally Ethernet, which operates at Layer 2, has left the task of congestion control to the TCP layer. However recent developments such as the spread of Ethernet use in applications such as Storage Area Networks (SANs) has led the networking community to re-visit this design, since SANs have a very strict requirement that no packets be dropped. As a result, the IEEE 802.1 Standards group has recently proposed a congestion control algorithm called IEEE802.1Qau or Quantum Congestion Notification (QCN) for use in Ethernet networks. This algorithm uses several advances in congestion control techniques that we described in the previous chapters, such as the use of rate averaging at the sender, as well as AQM feedback which takes the occupancy as well as the rate of  change of the buffer size, into account.

Key Words:
Ethernet Congestion Control; Quantum Congestion Notification; QCN; Reaction Point or RP Algorithm; Control Point or CP Algorithm; QCN Stability Analysis; IEEE802.1Qau.

**Chapter 9: Emerging Topics in Congestion Control**
This chapter discusses three different topics that are at the frontiers of research into congestion control: (1) We describe a project from MIT called Remy, that applies techniques from Machine Learning to congestion control. It discovers the optimal congestion control rules for a specific (but partially observed) state of the network, by doing an extensive simulation based optimization of network wide utility functions. 
(2) Software Defined Networks or SDNs have been one of the most exciting developments in networking in recent years. Most of their applications have been in the area of algorithms and rules that are used to control the route that a packet takes through the network. However we describe a couple of instances in which ideas from SDNs can also be used to improve network congestion control. (3) Lastly we describe an algorithm called Google Congestion Control (GCC), that is part of the WebRTC project in the IETF, and is used for controlling real time in-browser communications. This algorithm has some interesting features such as a unique use of Kalman Filtering at the receiver, to estimate whether the congestion state at the bottleneck queue in the face of a channel capacity that is widely varying.

Key Words:
Project Remy; Remy Congestion Control Algorithm; Machine Learning and Congestion Control; Software Defined Networking and Congestion Control; Google Congestion Control; GCC; Kalman Filtering and Congestion Control.


# Deep Learning

![](https://subirvarma.github.io/GeneralCognitics/images/DeepLearning.png)

This is joint work with Professor Sanjiv Das at Santa Clara University. I use this book as the main text book for my course on Deep Learning at SCU. This is a work in progress, and I have been adding new material as needed in order to incorporate new developments in this rapidly changing field. 

