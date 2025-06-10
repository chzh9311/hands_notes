---
tags:
  - Hand-Object
  - Contact
Institute:
  - Univ of Birmingham
  - UNIST
  - South China Univ of Tech
Corresponding Author:
  - Hyung Jin Chang
Code: https://eldentse.github.io/s2contact
aliases:
  - "@tseS$^2$ContactGraphBasedNetwork2022"
Year: 2022
Publisher: ECCV
---

# S$^2$Contact: Graph-Based Network for 3D Hand-Object Contact Estimation with Semi-supervised Learning
## Motivation
1. Lack of contact data;
2. PointNet+GCN consumes too much time;
3. Applying geometric and visual consistencies on contact maps
## Method
Noisy estimate of hand and object meshes -> estimate contact between hand and object
1. Use KNN to determine neighbours and extract features with adjacency
2. Semi-supervised pipeline:
	1. Pre-training: pretrain with a small labelled dataset;
	2. Pseudo-label generation: use an EMA teacher;
	3. Losses:
		1. contact consistency: ||student - teacher|| with random transformations;
		2. geometric consistency: CD < threshold;
		3. Visual Consistency: render the estimation to image and compare.