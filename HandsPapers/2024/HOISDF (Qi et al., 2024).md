---
tags:
  - Hand-Object/Known-object
  - ImplicitRepresentation
  - Discriminative
Institute:
  - EPFL
Corresponding Author:
  - Alexander Mathis
Code: https://github.com/amathislab/HOISDF
aliases:
  - "@qiHOISDFConstraining3D2024"
Year: 2024
Publisher: CVPR
---
# HOISDF: Constraining 3D Hand-Object Pose Estimation with Global Signed Distance Fields
## Motivation
**Occlusion** is still a major challenge, which is due to the 3D shape representation method:
Existing methods rely on explicit intermediate representations
SDF should do this better.
## Method
1. Image features are extracted by a standard encoder-decoder (UNet).
2. SDF learning: 
	1. is done in original space (not canonical like in [[AlignSDF (Chen et al., 2022)]], and [[gSDF (Chen et al., 2023)]]), allowing to learn global features.
	2. for a query point $p\in\mathbb{R}^3$, project to 2D image to get the feature via a MLP$$\mathbf{f}_{img}=MLP(cat_{i\in X}\mathbf{F}^i_{dec}(\pi_{3D\rightarrow 2D}))$$, features from all the decoder layers $X$ are concatenated together.
	![[SDF_learning.png]]
	3. The feature $\mathbf{f}_{img}$, is concatenated with $p$ and position encoding and together fed into SDF:$$d_\delta = \mathbb{SDF}_\delta(p\oplus\mathbf{f}_{img}\oplus\mathbf{f}_{pos})$$ where $\delta \in \{hand, object\}$
	4. Finally get the distances of $N$ sampled points.
3. Field-guided pose regression
![[Field-Guided Pose Regression.png]]
	1. Sample Points near the surface
	2. At certain query point, there is only a scalar distance, not enough info. They convert it to volume density: $\sigma = \alpha^{-1}sigmoid(-d_h/\alpha)$, motivated by [[StyleSDF]], and augment $\mathbf{f}_{img}$ with $\sigma$.
	3. SDFs cannot model interactions. Send object query points to hand SDF to get contact points.
	4. Use MHSA to regress poses, utilizing [[MANO]] for priors
## Experiments
Datasets:
* [[DexYCB (Chao et al., 2021)]],
* [[HO3D]]
The hand MJE is obviously decreased.