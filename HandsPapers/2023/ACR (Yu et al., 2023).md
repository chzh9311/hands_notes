---
tags:
  - HandMesh
  - two-hand
  - Model-free
  - Discriminative
Institute:
  - Tencent AI Lab
  - Durham University
Corresponding Author:
  - Shaoli Huang
Code: https://github.com/ZhengdiYu/Arbitrary-Hands-3D-Reconstruction
Year: 2023
Publisher: CVPR
aliases:
  - "@yuACRAttentionCollaborationBased2023"
---
# ACR: Attention Collaboration-Based Regressor for Arbitrary Two-Hand Reconstruction
## Motivation
* Previous methods require both two hands are seen in the input, sensitive to truncation & occlusions.
## Method
Contributions are:
* Take the first step towards reconstructing two hands at arbitrary scenes;
* center & part based representations
* cross-hand prior reasoning module
The backbone outputs 4 maps:
* parameter map; $M_p\in\mathbb{R}^{218\times H\times W}$. 109 for each hand, including: 16x6+10 MANO params + 3 camera params;
* hand centre map; $A_c\in\mathbb{R}^{2\times H \times W}$.
* part segmentation map. $A_p\in\mathbb{R}^{33\times H\times W}$ 33 = 16 parts x 2 hands + 1 background.
* cross-hand prior map; $M_c\in\mathbb{R}^{218\times H\times W}$ for inverse feature query. Based on the idea that two-hand features are highly correlated.
![[ACR framework.png]]
### How to solve ambiguity of two hands
1. Use hand centre map
2. Generate new centres if they are too close to each other.
3. Mutual reasoning: inversely query the left/right hand centre for the right/left hand prior feature.