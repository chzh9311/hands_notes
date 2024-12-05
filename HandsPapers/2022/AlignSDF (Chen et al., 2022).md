---
tags:
  - Hand-Object
  - ImplicitRepresentation
Institute:
  - Inria
Corresponding Author:
  - Ivan Laptev
Code: https://zerchen.github.io/projects/alignsdf.html
aliases:
  - "@chenAlignSDFPoseAlignedSigned2022"
Year: 2022
Publisher: ECCV
---
# AlignSDF: Pose-Aligned Signed Distance Fields for Hand-Object Reconstruction
## Motivation
address the low-resolution of mesh models.
Geometry depends both on pose and shape -> disentangle pose and shape
## Method
Predict hand pose and object pose separately;
For a query point, transform it to the canonical hand/object space, and predict the SDF in this space.