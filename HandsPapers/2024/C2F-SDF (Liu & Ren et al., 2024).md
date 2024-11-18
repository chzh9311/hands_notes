---
tags:
  - Hand-Object
  - ImplicitRepresentation
Institute:
  - Beijing Univ of Posts and Telecommunications
Corresponding Author:
  - Zirui Zhuang
Year: 2024
Publisher: ECCV
Code: https://github.com/ru1ven/C2F-SDF
aliases:
  - "@liuCoarseFineImplicitRepresentation"
---
# Coarse-to-Fine Implicit Representation Learning  for 3D Hand-Object Reconstruction from a Single  RGB-D Image
## Motivation
1. Implicit representations ([[AlignSDF]], [[Grasping Field]]) can capture objects with arbitrary topology at arbitrary resolutions;
2. Existing SDF-based methods suffer from heavy computational budgets. e.g., [[Marching Cube]] involves a large number of points far from the surface.
## Method
### Point-Cloud features
Use two-branch hourglass to extract global image feature $F_{global}\in\mathbb{R}^C$ & visual feature $F_{visual}\in\mathbb{R}^{H\times W\times C}$. Follow [[2 heads better than 1 (Ren et al., 2023)]] to get point cloud features.

### Coarse-to-Fine
1. Coarse level feature is obtained by sampled 3D query points $x$ in 3D space.
2. Fine level:
	[[PIFu]] describes a surface as the zero-level set of a function:
	$$ f(F(\pi(x)), Z(x)) = 0.$$
	$x$ is the query point in 3D, $Z(x)$ is the depth in camera coordinate system; $\pi(x)$ is the 2D projection location of $x$; $F(\pi(x))$ is the pixel aligned image feature.
	* PIFu lacks global context info and is prone to depth ambiguity.
* **3D PIFu** is proposed to solve it.
	$$f(F_{PA}, x) = 0$$
### SDF to 3D mesh
Introduce **volumetric sematic heatmap** -> 
1. Use $F_{global}$ to predict a low-resolution heatmap;
2. Use 3x3x3 avg filter to smooth out outliers;
3. Predict [[MANO]] vertices to complete the hand point clouds;
![[Pasted image 20241014150911.png]]
Select the sampled features to conduct Marching cubes.

### Experiments
[[[DexYCB (Chao et al., 2021)]]] & [[ObMan]].
Exceeds the previous sota [[gSDF (Chen et al., 2023)]] on both datasets.
![[Pasted image 20241014151526.png]]
**ObMan dataset**
![[Pasted image 20241014151658.png]]
![[Pasted image 20241014151732.png]]