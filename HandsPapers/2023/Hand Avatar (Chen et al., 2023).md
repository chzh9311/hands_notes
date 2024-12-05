---
tags:
  - HandMesh
  - Representation
  - HandAvatar
  - Model-based
Institute:
  - Xiaobing.AI
Corresponding Author:
  - Heung-Yeung Shum
aliases:
  - "@chenHandAvatarFreePose2023"
Year: 2023
Publisher: CVPR
---
# Hand Avatar: Free-Pose Hand Animation and Rendering from Monocular Video
## Motivation
Many works focus on human avatars, while hand avatar are not so well studied (i.e., [[LISA (Corona et al., 2022)]]). Challenges are not addressed:
1. Deformation is hard to model;
2. Illumination and shadow patterns are important but not yet modelled.

## Method
### MANO-HD
A high-resolution version of [[MANO]] with:
1. 12,337 vertices;
2. 24,608 faces.
This model is gotten by adding new points on edge middle. After that, the blending weights are derived by optimizing norm constraints (like in MANO) for sparse skinning weights; Laplacian term for mesh smoothness, and Chamfer distance for fitting MANO-HD to MANO.

The param $\beta$ is replaced by an MLP for more personalization.

### PairOF: Local-Pair Occupancy Field
Given query point $q$, PairOF predicts the occupancy value to describe whether it locates in or out of the surface.
Like [[NASA (Deng et al., 2020)]], also divide hand mesh to per-bone part meshes and uniformly sample $N^p$ points on each mesh to get a point cloud, encode with [[PointNet]].
Local-pair decoder is based on PointNet and fuse each pair encodings.

## SelF: Self-Occlusion-Aware Shading Field
Predict the albedo and illumination values

The rendering results is more realistic than [[LISA (Corona et al., 2022)]].
