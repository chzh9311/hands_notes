---
tags:
  - Hand-Object
  - Representation
Institute:
  - Inria
Corresponding Author:
  - Ivan Laptev
Code: https://github.com/zerchen/gSDF
Year: 2023
Publisher: CVPR
aliases:
  - "@chenGSDFGeometryDrivenSigned2023"
---
# gSDF: Geometry-Driven Signed Distance Functions for 3D Hand-Object Reconstruction
## Motivation
1. [[MANO]] meshes have limited resolutions;
2. Previous SDF based works ([[Grasping Field (Karunratanakul et al., 2021)]], [[AlignSDF]]) does not solve more complex hand motions.
## Method
![[gSDF-framework.png]]
## Kinematics feature
encodes *he position of the hand under local coordinates*
1. Use IK to predict the MANO pose params from joint locations. For objects only regress the centre position of the object 
2. (There are 17 joints) The kinematic feature is defined as the local coordinates of a query point $x$ under for each joint. then concat
	$$e_h = [x, x_1, x_2, \dots x_n]$$.
3. For objects, the feature is defined as the local coordinates transformed object centre $x_{oc}=x - t_{oc}$, also transformed to the hand wrist coordinate system: $x_{ow}$, and concatenate: $$e_o = [x, x_{oc}, e_{o1}, \dots, e_{o21}, x_{ow}]\in \mathbb{R}^{72}$$
>[!note]
> The pose estimator predicts 21 joints, but only 17 of them are used in generating hand geometry features
### Visual Features
Simply use ResNet + Spatial-Temporal Transformer

## Training
### Stage I
Train the pose estimator
### Stage II
Freeze hand joint predictor, and train the whole model.

## Experiments
Dataset used: [[ObMan]], [[DexYCB (Chao et al., 2021)]]

The structure: Asymmetric is the best:
![[Pasted image 20241030181944.png]]
