---
tags:
  - HandMesh
  - two-hand
  - Model-free
  - Discriminative
Institute:
  - ByteDance
Corresponding Author:
  - Shilei Wen
aliases:
  - "@wangMeMaHandExploitingMeshMano2023"
Year: 2023
Publisher: CVPR
---
# MeMaHand: Exploiting Mesh-Mano Interaction for Single Image Two-Hand Reconstruction
## Motivation
Two kinds of representations: **MANO** and **direct triangular mesh**, have their own pros and cons.
-> Estimate the mesh vertices & [[MANO]] simultaneously.
## Method
The framework consists of 3 parts:
![[MeMaHand.png]]
1. Image Encoder-Decoder: Use ResNet-50;
2. Mesh-Mano interaction module: MMIB (Mesh-Mano Interaction Block)
![[MeMahand_MMIB.png]]
Two kinds of queries: $f_v$: the vertex query; $f_m$: the MANO param query. $f_v$ is processed by Graph Residual Block [[@ge3DHandShape]] & [[@liInteractingAttentionGraph2022]]. 
Intra-hand MHA + Inter-hand MHA.

### Mesh Alignment Refinement
Inspired by [[pyMAF]]. 
* Project the mesh vertices onto the multi-scale image features => image feature $\phi$.
* Use GCN to model spatial relations.

## Exp
done on [[InterHand2.6M]] dataset.