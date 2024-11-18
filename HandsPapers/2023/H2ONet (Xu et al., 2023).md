---
tags:
  - HandMesh
  - LightWeight
Institute:
  - CUHK
Corresponding Author:
  - Chi-Wing Fu
Code: https://github.com/hxwork/H2ONet_Pytorch
aliases:
  - "@xuH2ONetHandOcclusionOrientationAwareNetwork2023"
Year: 2023
Publisher: CVPR
---
# H2ONet: Hand-Occlusion-and-Orientation-aware Network for Real-time 3D Hand Mesh Reconstruction
## Motivation
Recent methods do not address occlusion well, especially for real-time frameworks. The goal is to meet the requirements:
1. utilize inter-frame information;
2. alleviate the interference of occlusions.
## Method
![[H2ONET framework.png]]
1. Images are first fed into an hourglass block and dual encoders. The encoders are blocks in MobileNet for efficiency.
### Hand mesh reconstruction
>[!Note] Assumption
>The transformation of adjacent frames are nearly rigid.
1. prepare occlusion labels: mask the rendered mesh by gt mask, then outside regions are occluded
![[H2ONet occlusionlabel.png]]
2. Occlusion prediction: predict finger-level occlusion label and if all fingers are occluded, regard the hand as occluded.
3. Orientation regression: Update an auxiliary frame with time and fuse with current frame.

## Exp
Real-time (35FPS), though not very real-time compared to [[MobRecon (Chen et al., 2022)]] (59 FPS). But performance better.