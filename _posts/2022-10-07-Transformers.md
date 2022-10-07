---
title: "Transformers"
date: 2022-10-07
---

# Transformers

## Introduction

![](images/trans4.png)

*Figure 1*

Transformers are a new kind of Neural Network Architecture, that were introduced in 2017 by [Vaswani et.al.](https://arxiv.org/abs/1706.03762). They were originally targeted at NLP applications, but since then they have been successfully applied to Image Processing as well. In NLP they overcome some of the difficulties with RNN/LSTMs, and result in much improved performance in applications such as Machine Translation. In addition, they are much better at Transfer Learning for NLP, so that Transformer models trained on huge amounts of data can be fine tuned and used for smaller datasets, just like for ConvNets.

Transformers were originally used to do Machine Translation, whereby the name comes from (they "Transform" a sentence in language 1 to language 2). Since then they have been successfully applied to other NLP applications such as Classification and Language Modeling. Indeed it was soon realized that Transformers are a versatile general purpose tool, which can be used in any Machine Learning application, as long as the input can be formatted in a way that can be ingested by them. Recently Transformers have been used for Image Processing tasks, where they have shown themselves to perform better than the best performing ConvNets.

In contrast to older architectures, Transformers have a much higher modeling capacity, which also means it is possible to scale up these models to very large sizes (see Figure 1) with corresponding improvements in performance. Indeed some of the more recent Transformer models have hundreds of billions of parameters, which take days to train even with powerful computing infrastructure. Recall that models with large number of parameters require a correspondingly large amount of training data in order to avoid the overfitting problem. In the case of Transformers this problem was addressed by using self-supervised learning on massive text datasets.

This process, whereby larger and larger models trained on bigger and bigger datasets lead to better and better performance, has not reached its limits yet, indeed the latest Transformer features over a trillion parameters!

## Why RNNs are Not Good Enough

![](images/rnn38.png)

*Figure 2*

Consider the Bi_directional RNN shown in Figure 2: Assuming that the data being fed in the network consists of NLP sequences, with the sequence  $𝑋_𝑖,1\le i\le 𝑁$  being the embedding or representation for the corresponding word sequence. Note that this representation does not take into account the surrounding context from the other words in the sentence. The corresponding hidden state sequence  $𝑍1_𝑖,1\le 𝑖\le 𝑁$ , can be considered to be the new representation for the sequence  $𝑋_𝑖,1\le 𝑖\le 𝑁$ , such that the representation  $𝑍1_𝑖$  is modified by the words  $𝑋_1,...,𝑋_𝑖$  that came at or before  $𝑍1_𝑖$ . In a Bi-Directional RNN, each word  $𝑋_𝑖$  has two such representations, with the representation  $𝑍1_𝑖$  modified by the words  $𝑋_1,...,𝑋_𝑖$ , and the representation $𝑍2_𝑖$  modified by the words  $𝑋_{𝑖+1},...,𝑋_𝑁$ . Can these word representations be further improved? This RNN model has some shortfalls in this area:

RNN representations such as  $𝑍1_𝑖$  or  $𝑍2_𝑖$  for the word  $𝑋_𝑖$  are most influenced by other other words that are in  $𝑋_𝑖$ 's immediate neighborhood. The influence from words that are further away becomes progressively smaller due to the Vanishing Gradient problem (this is less of an issue in LSTMs, but the problem does not completely go away). It is well known that word sentences contain patterns that are strongly non-local, and this is not well captured by the RNN/LSTM type models.

Lack of Parallelizability: Note that future RNN states cannot be computed before past RNN states have been computed. This is a significant restriction, since modern GPUs are capable of performing multiple independent computations at the same time. This causes a significant slowdown when training on very large datasets.

In order to develop better NLP models, it is important to come up with systems that are able to develop even better context dependent representations for words by allowing all the words in a sequence to interact with each other.

Just as NLP models can be improved by allowing better interactions between all the words in a sentence, as opposed to only the nearby words, it turns out that exactly the same reasoning can be applied to Image Processing as well. If we replace the word embeddings in NLP by patch embeddings in Image Processing (as we will see later in this chapter), then ConvNets can be considered to be a special type of model in which only the neighboring patches are allowed to influence each others representations. Better Image Processing models can be developed which allow ALL the patches in an image to interact with each other, which is the main idea behind a class of Transformer models for Image Processing called Vision Transformers (or ViT).
