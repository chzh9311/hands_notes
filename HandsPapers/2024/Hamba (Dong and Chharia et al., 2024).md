---
tags:
  - HandMesh
  - Mamba
  - "#Model-based"
  - "#Discriminative"
Institute:
  - CMU
Corresponding Author:
  - Fernando De la Torre
Code: 
Year: 2024
Publisher: NeurIPS
aliases:
  - "@dongHambaSingleview3D2024a"
---
# Hamba: Single-view 3D Hand Reconstruction with Graph-guided Bi-Scanning Mamba

This method is based on [[Mamba|@guMambaLinearTimeSequence2024]]. 
## Motivation
**Explore Mamba's potential in 3D hand reconstruction.**
	Mamba cannot effectively capture local-relations (semantic), so combine it with graph
*Graph-based bi-directional scan* (GBS) to scan image tokens -> fewer tokens needed

Previous trial to apply Mamba to 2D images: [[VMamba (Liu et al., 2024)|@liuVMambaVisualState2024]] proposes VSS Block, which replaces sequence scanning with 2D scanning: SS2D

## Method
The overall architecture:
![[Hamba framework.png]]
These blocks are:
1. **JR(Joint Regressor)**: stacked SS2D blocks + MLP head => [[MANO]] params
2. **TS(Token Sampler)**: to avoid GSS from being influenced by the bg. Sample tokens around joints estimated from JR.
3. **GBS(Graph-guided Bidirectional Scan)** => the GCN leans invariant weight matrix for joint edges: how much they affect their neighbour. Each layer output was concatenated with global features before fed into the next layer.

## Experiments
The method is trained on multiple datasets, totally 2.7M hand samples;
Evaluations are done on [[FreiHand (Zimmermann et al., 2019)]], [[HO3D]], & [[HO3D-v3]], + [[HaMeR (Pavlakos et al., 2024)|HInt]].
Achieves SoTA on all benchmarks