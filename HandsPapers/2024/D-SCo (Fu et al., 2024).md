---
tags:
  - Hand-Object
  - DNN/Diffusion
Institute:
  - Tsinghua Univ.
  - TUM
  - Google
Corresponding Author:
  - Xiangyang Ji
  - Federico Tombari
Year: 2024
Publisher: ECCV
aliases:
  - "@fuDSCoDualStreamConditional"
---
# D-SCo: Dual-Stream Conditional Diffusion for  Monocular Hand-Held Object Reconstruction
## Motivation
1. Diffusion model is beneficial for modelling uncertainties and underconstrained problems.
2. Two challenges encounters:
	1. the centroid position of the object can deviate during diffusing; -> keep the centroid stable
	2. Not modelling hand-object interaction or addressing the uncertainty by occlusions; -> use two diffusion process to diffuse both object shape and image priors.
![[Pasted image 20241014160520.png]]
## Method
### Problem formulation
Input: A single RGB image $I$;
Output: the 3D object shape as 3D point cloud.
![[Pasted image 20241014161300.png]]
(I) Use [[Learning R of HO (Hasson, et al., 2019)]] & [[FrankMocap]] to estimate hand pose and camera view;
(II) Predict the object centroid;
Use a simple network $\mathcal{G}$: [[PointNet]]-like model to constrain the object -> [[ResNet]]-18 to learn global features -> 2 MLPs to get 3D & 2D centroids.
(III) A centroid-fixed diffusion network which fixes the centroid at the predicted position;
Motivation: directly using diffusion to learn object's shape & pose can be challenging (ref. [[CCD-3DR]])
How to keep centroid: add zero-mean noise.
(IV) Dual-stream diffusion for sematic and geometric embedding.
Sematic: project 3D features back to 2D image plane; for occluded object points, use [[MANO]] and the to predict.
Geometric: hand pose

## Experiments
### Datasets
Synthetic: [[ObMan]]
Real-world: [[HO3D]], [[MOW]], [[DexYCB (Chao et al., 2021)]].
![[Pasted image 20241014173818.png]]
-> More robust.