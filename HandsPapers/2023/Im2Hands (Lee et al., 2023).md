---
tags:
  - HandMesh
  - ImplicitRepresentation
  - two-hand
  - Model-free
  - Discriminative
Institute:
  - KAIST
  - ICL
Corresponding Author:
  - Tae-Kyun Kim
Code: "https://github.\rcom/jyunlee/Im2Hands"
aliases:
  - "@leeIm2HandsLearningAttentive2023"
Year: 2023
Publisher: CVPR
---
# Im2Hands: Learning Attentive Implicit Representation of Interacting Two-Hand Shapes
## Motivation
* Try to use implicit representation in two-hand reconstruction
## Method
![[Im2Hand framework.png]]
Input: image
Output: Occupancy network that outputs the occupancy probabilities for each hand $o_l^i$ & $o_r^i$ conditioned on the image for each query point.
The framework is partly based on [[HALO (Karunratanakul et al., 2021)]]. (single-hand method)
**Problem with HALO**: cannot model shape-dependent deformations, which is important due to inter-hand contact.
=> additional per-query shape feature $f_x^\phi$.

Next: **To model coherence**: 
Refine in the original pose space. Then predict Point cloud based on the hand surfaces, and predict features based on the anchor points via [[Point Transformer]]. 
## Exp
on [[InterHand2.6M]], the result is good.