---
tags:
  - HandMesh
  - Multi-view
Institute: Beihang, Chinese Academy of Science, etc.
Corresponding Author: Zhaoxin Fan
Code: https://github.com/jackyyang9/MLPHand
Year: "2024"
Publisher: ECCV
---
# MLPHand: Real Time Multi-View 3D Hand  Reconstruction via MLP Modeling
## Motivation
multi-view 3D hand reconstruction methods tend to be heavy-load. There is a need to create light-weight method.
> [!quote] 
> can we develop a real-time hand reconstruction method without sacrificing accuracy?
## Method
Input: $N$ RGB images from different cameras $\mathcal{I} = \{\mathbf{I}_n\}^N_{n=1}$.
1. multi-view hand skeleton estimator (CNN) -> skeletons $\bar{\mathbf{X}}\in\mathbb{R}^{21\times 3}$ and image feature maps $\{\mathbf{F}_n^{2D}\}_{n=1}^N$
2. bone level geometry features $G_k^B$ and $\bar{\mathbf{X}}$ are fed into the Multiview Geometry Feature Fusion Prediction (MGFP) module -> mesh
Output: [[MANO]]-style surface mesh.  (ARXIV:2201.02610)
![[MLPHand framework.png]]
### MV hand skeleton estimator
2D skeletons - triangulation -> 3D
### Skeleton2Mesh Model
1. Per-Bone reconstruction: non-convex hand shape -> 20 bone-wise convex meshes (c). And estimates them with shared params.
	1. Order (which bone) is obtained by positional encoding of $b = [x_1, x_2]$, and $o$ (one-hot vector of 20 dims)
2. Tri-Axis modelling: 3 MLPs to estimate xyz independently.
![[Pasted image 20241010155909.png]]

### MGFP
This module is proposed to utilize visual features to enhance the performance of Skeleton2Mesh
Joint-related features - concat -> bone-level geometry features $G_k^B$
> [!note]
> It is intuitive to use bones as the paper is modelling meshes as the unite of bone-wise meshes.

* MFI: 
## Experiment
### Datasets
* [[DexYCB (Chao et al., 2021)|DexYCB-MV]];
* [[HO3D|HO3D-MV]];
* [[OakInk|OakInk-MV]]: 
* [[FreiHand (Zimmermann et al., 2019)|FreiHand]].
* Much smaller than [[POEM (Yang et al., 2023)]].
![[Pasted image 20241010165858.png]]