---
tags:
  - Hand-Object/object-agnostic
  - Discriminative
Institute:
  - Beihang Univ
  - TUM
  - Politecnico di Torino
  - Zhongguancun Lab
Corresponding Author:
  - Xiaohui Liang
aliases:
  - "@lengDynamicHyperbolicAttention2023"
Year: 2023
Publisher: CVPR
---
# Dynamic Hyperbolic Attention Network for Fine Hand-object Reconstruction
## Motivation
Hyperbolic space better preserves the geometric properties of meshes.
-> Place the hand-object task in hyperbolic space.
## Preliminaries
> [!note]- Riemannian manifold
> A special smooth manifold where many **geometric notions like distance, angles, length, and curvature are defined**. Euclidean space is a special case of Riemannian **manifold**.

HGNN (Hyperbolic Graph Neural Network)
## Method
![[Pasted image 20241107110209.png]]
### Image-to-mesh estimation
Use two ResNet18 as the encoders for hands & objects.
Hand decoder outputs [[MANO]] params;
Object decoder outputs the mesh $(v, f)$, $v$ is the vertices and $f$ is the faces.
### Dynamic HGCN
The graph is constructed dynamically via kNN algorithm;
Hyperbolic Graph Convolution: based on the constructed graph:
$$v^l = \sigma(AGG(Mobius(exp(v^{l-1}))))$$