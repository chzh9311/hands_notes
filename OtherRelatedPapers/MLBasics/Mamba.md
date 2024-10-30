---
tags:
  - DNN/Mamba
aliases:
  - "@guMambaLinearTimeSequence2024"
---

# What is Mamba?
## Introduction
Mamba is one of the **State Space Models (SSMs)**. 
> [!quote]
> Importantly, for the first time, Mamba promises similar performance (and crucially similar [_scaling laws_](https://arxiv.org/pdf/2203.15556.pdf)) as the Transformer whilst being feasible at long sequence lengths (say 1 million tokens). To achieve this long context, the Mamba authors remove the “quadratic bottleneck” in the Attention Mechanism. Mamba also runs _fast_ - like “up to 5x faster than Transformer fast” 
> -- ref [Mamba Explained (thegradient.pub)](https://thegradient.pub/mamba-explained/)

Advantages are:
* Capable of handling long sequence
* faster inference
## How is Mamba Designed?
Foundation model backbones usually include two components:
1. Communication between tokens; (attention in transformer)
2. Computation within a token. (MLP in transformer)
Mamba is designed by improving Transformer on these two operations. Mamba replace the attention module with SSM (inspired by Control Theory)
![[mamba.png]]
>[!note] State Space Model
>Let $u$ be the input, $x$ be the hidden state, and $y$ is the output, then for a system:
>$$\dot{\mathbf{x}}(t) = \mathbf{A}(t)\mathbf{x}(t) + \mathbf{B}(t)\mathbf{u}(t)$$
>$$\mathbf{y}(t) = \mathbf{C}(t)\mathbf{x}(t) + \mathbf{D}(t)\mathbf{u}(t)$$
>where $\mathbf{A, B, C, D}$ are state matrix, input matrix, output matrix, feedforward matrix.
>![[SSM.png]]

In real life, we get observations in discrete timesteps, so we need to discretize the above model. Mamba uses [Zero-Order Hold (ZOH)](https://en.wikipedia.org/wiki/Zero-order_hold) discretization:
$$h_{t+1} = (I+\Delta A)h_t + \Delta Bx_t$$
then $$\begin{array}{ll} h_t &=\bar{A}h_{t-1} + \bar{B}x_t\\ y_t&=Ch_t\end{array}$$Similar to an RNN.

## Put theory into practice
Transformers are effective but not efficient. They store everything from the past using dot-product.
RNNs are opposite. They are efficient (with a small state) but not so effective.
SSMs are just like RNNs, but we can modify the state matrices **dynamically**.
### Selection Mechanism
Mamba is a Selective State Space Model. $A, B, C, D$ are learned matrices, and also functions of input $x$ e.g. $A = A_{\theta(x)}$. 
![[SSSM.png]]

This helps to determine which to remember and which to forget, but also make the state functions lose convolutional form. So some hardware optimisations are introduced.