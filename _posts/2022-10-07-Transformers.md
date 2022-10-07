---
title: "Transformers"
date: 2022-10-07
---

# Transformers

## Introduction

Transformers are a new kind of Neural Network Architecture, that were introduced in 2017 by [Vaswani et.al.](https://arxiv.org/abs/1706.03762). They were originally targeted at NLP applications, but since then they have been successfully applied to Image Processing as well. In NLP they overcome some of the difficulties with RNN/LSTMs, and result in much improved performance in applications such as Machine Translation. In addition, they are much better at Transfer Learning for NLP, so that Transformer models trained on huge amounts of data can be fine tuned and used for smaller datasets, just like for ConvNets.

Transformers were originally used to do Machine Translation, whereby the name comes from (they "Transform" a sentence in language 1 to language 2). Since then they have been successfully applied to other NLP applications such as Classification and Language Modeling. Indeed it was soon realized that Transformers are a versatile general purpose tool, which can be used in any Machine Learning application, as long as the input can be formatted in a way that can be ingested by them. Recently Transformers have been used for Image Processing tasks, where they have shown themselves to perform better than the best performing ConvNets.

In contrast to older architectures, Transformers have a much higher modeling capacity, which also means it is possible to scale up these models to very large sizes (see Figure trans4) with corresponding improvements in performance. Indeed some of the more recent Transformer models have hundreds of billions of parameters, which take days to train even with powerful computing infrastructure. Recall that models with large number of parameters require a correspondingly large amount of training data in order to avoid the overfitting problem. In the case of Transformers this problem was addressed by using self-supervised learning on massive text datasets.

This process, whereby larger and larger models trained on bigger and bigger datasets lead to better and better performance, has not reached its limits yet, indeed the latest Transformer features over a trillion parameters!
