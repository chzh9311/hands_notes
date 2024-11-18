---
tags:
  - HumanMesh
  - Representation
  - Frequency
Institute:
  - State Univ of New York at Buffalo
  - OPPO US
Corresponding Author:
  - Junsong Yuan
Code: https://github.com/tyluann/FreqHand
aliases:
  - "@luanHighFidelity3D2023"
Year: 2023
Publisher: CVPR
---
# High Fidelity 3D Hand Shape Reconstruction via Scalable Graph Frequency Decomposition
## Motivation
1. Most existing methods cannot reconstruct high-fidelity hand meshes;
2. [[MANO]]'s expression ability is suppressed.
3. Low-frequency components makes up most parts, modelling purely in spatial domain causes bias.
4. Previous methods mainly focus on graph spectrum analysis of the whole system (spectrum GCN)

## Method
1. Generate MANO mesh w/ [[EfficientNet]]. (purple)
![[FreqHand_framework.png]]
2. Process with multiple GCNs (green, yellow, red)
3. U-Net w/ skip connection form.
### High-fidelity hand model
MANO: 778 vertices -> subdivision -> 12,338 vertices.
The subdivision is based on [[Loop subdivision (Loop, 1987)]]
### Hierachical GCN
It uses different graphs in different layers. With the above subdivision matrix for upsampling.
### Graph Frequency Decomposition
The Laplacian matrix of the graph is defined as $\mathbf{L}:\mathbf{D}-\mathbf{A}$. $D$ is the diagonal degree matrix, $A$ is the adjacency matrix. Then the spectrum decomposition is (SVD)
$$\mathbf{L} = \mathbf{U}^\top\boldsymbol{\Lambda}\mathbf{U}$$
Then a graph function $x\in\mathbb{R}^{N\times d}$, (N is the num of points, d is the feature dim) can be decomposed to $N$ components:
$$x=\sum_{i=1}^N\mathbf{U}_i(\mathbf{U}_i^\top x)$$
![[freqHand cumulate result.png]]
### Loss function
The graph freq decomposition loss is
$$L_F = \frac{1}{F}\sum_{f=1}^F\log\left(\frac{\|\mathbf{U}_f^\top(\hat{V}-V_{gt})\|}{\|\mathbf{U}_f^\top\hat{V}\|\|\mathbf{U}^\top_fV_{gt}\|}+1\right)$$
* $F$ is the number of freq components ($F=N$);
* $\hat{V}$ and $V_{gt}$ are the predicted vertex locations and gt. $\in \mathbb{R}^{N\times 3}$.
Importantly, this loss allows **different components to have the same attention**, thus allows high-freq components to be better reconstructed.
* The overall loss adds $L_F$ with joint & vertex location errors.

## Exp
Done on [[InterHand2.6M]], 