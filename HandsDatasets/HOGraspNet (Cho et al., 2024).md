---
tags:
  - Dataset
  - Hand-Object
Institute:
  - KAIST
  - ICL
  - ByteDance
Corresponding Author:
  - Tae-Kyun Kim
Code: https://hograspnet2024.github.io/
Year: 2024
Publisher: ECCV
aliases:
  - "@choDenseHandObjectHOGraspNet"
n_frames: 1.5M
n_views: "4"
real: R
---
# Dense Hand-Object(HO) GraspNet with Full Grasping Taxonomy and Dynamics
## Motivation
Existing datasets cannot fulfil the requirement of scale, variations, and annotation equality.
## The dataset: HOGraspNet
Based on the grasping taxonomy ([[(Feix et al., 2015)]]), it refines 28 of the 33 grasps
Contains:
* 1.5M RGBD frames
* 4 viewpoints
* Annotations for 3D meshes, 3D keypoints, contact, grasp labels.
	* Hand meshes are labelled by [[MANO]] and [[HALO (Karunratanakul et al., 2021)|@karunratanakulSkeletonDrivenNeuralOccupancy2021]]
![[Pasted image 20241025112243.png]]
