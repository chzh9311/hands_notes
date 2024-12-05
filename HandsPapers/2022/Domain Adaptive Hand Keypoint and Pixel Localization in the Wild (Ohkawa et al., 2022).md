---
tags:
  - HandPose
  - DomainAdapt
Institute:
  - Univ of Tokyo
  - CMU
Corresponding Author:
  - Yoichi Sato
Code: https://tkhkaeio.github.io/projects/22-hand-ps-da/
aliases:
  - "@chenAlignSDFPoseAlignedSigned2022"
Year: 2022
Publisher: ECCV
---
# Domain Adaptive Hand Keypoint and Pixel Localization in the Wild
## Motivation
the pseudo-labels are not accurate.
## Method
1. A confidence estimation method based on the divergence of the predictions from two teacher networks.
![[Sato (ECCV22).png]]
Lower the weights of pseudo-labels that two teachers disagree with each other.