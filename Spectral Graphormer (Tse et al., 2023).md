---
tags:
  - HandMesh
  - two-hand
Institute:
  - Google
  - Univ of Birmingham
Corresponding Author:
  - Bardia Doosti
  - Hyung Jin Chang
aliases:
  - "@tseSpectralGraphormerSpectral2023"
Year: 2023
Publisher: ICCV
---
# Spectral Graphormer: Spectral Graph-based Transformer for Egocentric Two-Hand Reconstruction using Multi-View Color Images
## Motivation
1. Current methods do not provide absolute root pose recovery.
2. Need estimations including forearms, but no suitable datasets.

## Method
Framework
![[Graphormer.png]]
Input: N multi-view RGB images $x\in \mathbb{R}^{N\times 224 \times 224 \times 3}$. 
The multi-view features are fused by max pooling.
The mesh is segmented via Spectral clustering, and the segmentation results are concatenated with image features $f_{t}\in\mathbb{R}^{V'\times (C+3)}$, and $V'$ is the coarse hand mesh vertex number.
The feature is finally upsampled to a fine mesh representation 

## Training
Besides vertex positions, we apply edge length regularization $\mathcal{L}_{edge}$ for smoothness of the mesh (minimizing the variance of edge lengths).
Manage self-penetration by minimizing penetration loss at inference via optimization.
## Dataset
* Sync: Commercial 3D hand models for both left & right (4023 vertices and 4008 quad faces => 8016 triangular faces)
* Real: 18 cameras, NeRF-based reconstruct pipeline.
## Exp
Baseline: [[METRO (Lin et al., 2021)]]
