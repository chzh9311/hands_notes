---
tags:
  - ImageSynthesis
  - Hand-Object
  - textDriven
Institute:
  - UCSD
  - NVIDIA
Corresponding Author:
  - Xiaolong Wang
Code: " https://mq-zhang1.github.io/HOIDiffusion"
Year: 2024
Publisher: CVPR
---
# HOIDiffusion: Generating Realistic 3D Hand-Object Interaction Data
## Motivation
Generate realistic images with GT hand pose & labels.
-> Use physical constraints + Diffusion
## Method
Stage I:
A object model of arbitrary pose -> generate a hand trajectory to reach it.
Use [[GrabNet]] (generates hand grasps conditioned on body part segmentation)
Stage II:
1. to generate hands with the right number of fingers, we project hand skeleton to the image space as visual control -> $s_i$.
2. Use segmentation to provide boundaries.
3. Apply a normal map for lighting.
![[HOIDiffusion.png]]

