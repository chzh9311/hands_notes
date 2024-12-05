---
tags:
  - HandPose
  - two-hand
Institute:
  - Beihang Univ
  - UHK
  - Sense Research
  - Shanghai AILab
  - Univ of Sydney
Corresponding Author:
  - Wanli Ouyang
  - Ping Luo
Code: https://menghao666.github.io/HDR/
aliases:
  - "@meng3DInteractingHand2022"
Year: 2022
Publisher: ECCV
---
# 3D Interacting Hand Pose Estimation by Hand De-occlusion and Removal
## Motivation
* hand-hand occlusion
* similarity
* Currently no *amodal segmentation* dataset of interactive hands
>[!note] amodal segmentation
>The segmentation of one instance with visible & invisible parts.

![[HDR_framework.png]]
## Method
1. Hand Amodal Segmentation Module (HASM): Simply use SegFormer (ARXIV:2105.15203).
2. Hand De-occlusion Removal Module (HDRM): The network is based on (ARXIV:1804.07723)
3. Isolated hand pose estimation
