---
tags:
  - HandPose
Institute:
  - University at Buffalo
  - Microsoft
Corresponding Author:
  - Zicheng Liu
Code: https://linhuang17.github.io/NVF
aliases:
  - "@huangNeuralVotingField2023"
Year: 2023
Publisher: CVPR
---
# Neural Voting Field for Camera-Space 3D Hand Pose Estimation
## Motivation
1. Previous works mainly focus on root-relative pose, while camera space pose is important in applications like AR
2. Camera-space pose needs
	1. dense local evidence;
	2. hand global geometry
3. Important to alleviate 2D-to-3D ambiguity.
=> Based on [[PIFu]], 
4. Dense regression [[A2J]], [[A2J-Transformer (Jiang et al., 2023)]] performs better than holistic regression.
## Method
### NVF
The NVF is defined as:  $f_{NVF}$ as a MLP that: for each point $p$ in camera space, it maps from pixel-aligned image feature $S(F, \pi(p))$, depth $Z(p)$ to the SDF and offset.
$$f_{NVF}(S(F, \pi(p)), Z(p)) = (s, V)$$
It's like an extension from [[PIFu]], the input is the same, while the output is changed to more complicated SDF & offset. The result is by taking the average over $V$ where $s$ is smaller than a threshold (nearby the surface)