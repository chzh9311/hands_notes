---
tags:
  - HandMesh
  - HandAvatar
Institute:
  - ETH
  - MPI
Corresponding Author:
  - Siyu Tang
Code: https://korrawe.github.io/harp-project/
aliases:
  - "@karunratanakulHARPPersonalizedHand2023"
Year: "2023"
Publisher: CVPR
---
# HARP: Personalized Hand Reconstruction from a Monocular RGB Video
## Motivation
Existing hand-avatar methods are quite limited in addressing textures. [[LISA (Corona et al., 2022)]] use implicit representations, but requires multi-view setup for training a new instance.
hand avatar should be accurate, scalable, robust and efficient.
## Representation
### Template
* Built upon [[MANO]], but higher resolution. 778 -> 3093.
* Extend with forearm.
### Geometry Refinement
* Each vertex is allowed to deform by a personalized displacement $D$.
$$V=\mathcal{S}(MANO(\theta, \beta)) + D$$ where $\mathcal{S}:\mathbb{R}^{778\times 3}\mapsto \mathbb{R}^{3093\times 3}$.
### Texture
* A Lambertian surface with an albedo map $a$.
* A UV-space normal map for surface normals.

## Rendering
Use only explicit geometry & appearance representations w/o neural implicit representations.