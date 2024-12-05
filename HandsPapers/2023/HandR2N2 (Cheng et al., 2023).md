---
tags:
  - HandPose
  - Discriminative
Institute:
  - Sungkyunkwan Univ.
Corresponding Author:
  - Jong Hwan Ko
Code: "https://github.com/\rcwc1260/HandR2N2"
aliases:
  - "@chengHandR2N2Iterative3D2023"
---
# HandR<sup>2</sup>N<sup>2</sup>: Iterative 3D Hand Pose Estimation Using a Residual Recurrent Neural Network
## Motivation
Current methods are not flexible for varying resource constraints and accuracy targets.
## Method
![[Pasted image 20241120145202.png]]
Task: *from depth(point cloud) to hand pose*.

The core module: RRU consists of 
1. resampler: Resample the points nearby each estimated joints
2. Residual graph GRU: Combine GCN with GRU
3. Regressor: update with estimated residual.