---
tags:
  - HandMesh
  - Representation
Institute:
  - Wuhan Univ
  - TUM
  - Tencent AI Lab
Corresponding Author:
  - Zhigang Tu
Code: 
aliases:
  - "@huangPHRITParametricHand2023"
Year: 2023
Publisher: ICCV
---
# PHRIT: Parametric Hand Representation with Implicit Template
## Motivation
* Parametric models are efficient and provide dense correspondence with the canonical pose, but requires supervision to learn deformation of each vertex;
* Implicit representations are high-fidelity, but lack the correspondence and requires time-consuming post-processing.
PHRIT combines both advantages. Inspired by [[MANO]] and [[DHM (Moon, 2020)]].
![[PHRIT_framework.png]]
## Method
### RefNet
it encodes a canonical hand mesh $M$ in SDF, compatible with [[MANO]] mesh.
### DeformNets
Split hand to 16 parts based on MANO skinning weights. Each part is deformed with an independent DeformNet. 
### Deformation Field
The field is a *one-to-one mapping function that transforms a 3D point $X_c$ in canonical space to $X_d$ in the deformed space.* $\phi: X_c \mapsto X_d$. The result follows:
$$SDF_d(X_d) = SDF_d(\phi(X_c)) = SDF_c(\phi^{-1}(X_d))$$
### Training
introduce an inverse counterpart InvDeformNet, to restore 
### Inference
1. RefNet -> Canonical hand mesh $M$
2. Marching Cubes -> mesh and skinning weights
3. Use DeformNet -> deform vertices in $M$.
Step 1 is only done once.