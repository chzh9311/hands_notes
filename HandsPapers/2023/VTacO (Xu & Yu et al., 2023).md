---
tags:
  - Hand-Object
  - multi-modality
Institute:
  - SJTU
  - Shanghai Qi Zhi Institute
  - Cornell University
Corresponding Author:
  - Cewu Lu
Code: https://sites.google.com/view/vtaco/
aliases:
  - "@xuVisualTactileSensingHand2023"
  - VTacOH
Year: 2023
Publisher: CVPR
---
# Visual-Tactile Sensing for In-Hand Object Reconstruction
## Motivation
**Vision-based tactile sensor**: Small units with dense pressure sensor array on them. This paper uses DIGIT: ARXIV:2005.14679 for the sensing.
These sensors can enhance in:
1. Local geometry refinement;
2. Deformation at contact;
3. Hand-Object contact state.
## Overview
Input: point cloud and tactile maps
How the tactile sensor is fused: by transform the local point clouds to the world coordinate sys
![[vtaco.png]]