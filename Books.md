---
layout: default
title: "Books"
---

# Internet Congestion Control

**Chapter 1: Introduction** 
This chapter is an introduction to the subject of congestion control, and covers some basic results in this area, such as the Chiu-Jain result on the optimality of AIMD control, descriptions of fundamental congestion control algorithms such TCP Reno, TCP Vegas and RED based Active Queue Management. A detailed description of TCP Reno is provided including algorithms such as: Congestion avoidance, Fast Re-transmit and Fast Recovery, Slow Start, TCP Timer operation etc. Active Queue Management or AQM techniques are introduced and the Random Early Detection or RED algorithm is  described. 

Key Words
Congestion Control definition and objectives; TCP Reno; TCP Vegas; Active Queue Management; AQM; Random Early Detection; RED; Congestion Avoidance; Fast Re-transmit; Fast Recovery; Slow Start.

**Chapter 2: Analytic Modeling of Congestion Control**
This chapter has a detailed discussion of TCP models, starting from simple models using fluid approximations to more sophisticated models using stochastic theory. The well known “Square Root” formula for the throughput of a TCP connection is derived, and is further generalized to AIMD congestion control schemes. These formulae have proven to be very useful over the years, and have formed an integral part of the discovery of new congestion control protocols, as shown in Part 2 of this book. A general procedure for deriving an expression for the throughput of a congestion control algorithm is also presented. This chapter also analyzes systems with multiple parallel TCP connections, and derives expressions for the throughput ratio as a function of the round trip latencies.

Key Words
TCP Throughput Models; Additive Increase Multiplicative Decrease; TCP Square Root Formula; TCP Throughput with Link Errors; Fluid Flow Models of TCP; Congestion Control Analytic Modeling; Congestion Control Stochastic Models; Multiple Parallel TCP Connections.

**Chapter 3: Optimization and Control Theoretic Analysis of Congestion Control**
In this chapter Optimization Theory and Control Theory are applied to a differential equation based fluid flow model of the packet network. This results in the decomposition of the global optimization problem into independent optimizations at each source node and the explicit derivation of the optimal source rate control rules as a function of a network wide utility function. In the case of TCP Reno, the source rate control rules are known, but then the theory can be used to derive the network utility function that Reno optimizes. In addition to the mathematical elegance of these results, the results of this theory have been used recently to obtain optimal congestion control algorithms using Machine Learning techniques. The system stability analysis techniques using the Nyquist Criterion that we introduce in this chapter, have become an essential tool in the study of congestion control algorithms. By using a linear approximation to the delay-differential equation describing the system dynamics, this technique enables us to derive explicit conditions on system parameters in order to achieve a stable system.

Key Words
Congestion control and optimization theory; congestion control and optimal control theory; Fluid Flow model of congestion control; Congestion control and Nyquist Stability; Congestion Control Lagrangian Optimization; Congestion Control Dual Optimization problem; Congestion Control Primal Optimization problem; Active Queue Management; AQM; Random Early Detection; RED; Proportional Controller; Proportional plus Integral Controller; The Averaging Principle; TCP Utility Function

