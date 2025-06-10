---
tags:
  - Hand-Object
  - MotionSynthesis
  - DataAugmentation
Institute:
  - SJTU
  - Shanghai Qi Zhi Institute
Corresponding Author:
  - Cewu Lu
Code: https://github.com/lixiny/ArtiBoost
aliases:
  - "@yangArtiBoostBoostingArticulated2022"
Year: 2022
Publisher: CVPR
---
# ArtiBoost: Boosting Articulated 3D Hand-Object Pose Estimation via Online Exploration and Synthesis (Oral)
## Motivation
For Hand-Object Pose Estimation (HOPE) task:
1. the required amount of data is more than the current dataset;
## Method
![[Pasted image 20241210100929.png]]
Overview:
1. Construct CCV-space (including object types, hand pose, & viewpoints).
2. Predict hard examples for data enhancement.
Input: 
Input image $I$ with a single hand & a certain object.
Output:
3D hand joints and object 6D pose.
### The CCV-Space
1. Valid Hand Pose: Parametric model [[MANO]]. -> narrow it down by applying certain constraints;
2. Further narrow down with predefined hand-object poses.
	1. Construct the offset surface of the object;
	2. get the approaching direction
	3. Sample valid contact points from the contact-feasible region.
	4. Generate the interacting pose by fitting the hand to the contact points.
![[Pasted image 20241203130818.png]]
5. Viewpoints are simply sampled uniformly.

### Apply Artiboost in training
1. Generate a weight map for all samples in CCV-space
2. After each epoch, re-weight according to the sample weights.