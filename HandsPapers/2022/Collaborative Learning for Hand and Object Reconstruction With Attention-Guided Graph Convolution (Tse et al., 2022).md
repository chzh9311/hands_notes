---
tags:
  - Hand-Object/Object-agnostic
Institute:
  - Univ of Birmingham
  - UNIST
Corresponding Author:
  - Hyung Jin Chang
aliases:
  - "@yangArtiBoostBoostingArticulated2022"
Year: 2022
Publisher: CVPR
---
## Motivation
 Try to learn the physical constraints between hands and objects implicitly instead of explicit constraints.
 ![[Pasted image 20241203135841.png]]
## Method
1. Hand mesh: use [[MANO]]
2. Object mesh: use [[AlexNet]] to predict
### Attention-guided GCN
Assume the input vertices an unordered set => Dynamically construct neighborhoods using attention (a connection is formed iff the attention > threshold)
## Dataset
1. [[FHB]]
2. [[ObMan]]
3. [[DexYCB (Chao et al., 2021)]]
4. [[HO3D]]
