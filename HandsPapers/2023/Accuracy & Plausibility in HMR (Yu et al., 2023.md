---
tags:
  - HandMesh
  - weakly-supervised
Institute:
  - NUS
  - Huawei
Corresponding Author:
  - Angela Yao
aliases:
  - "@yuOvercomingTradeAccuracyPlausibility2023"
Year: 2023
Publisher: CVPR
---
# Overcoming the Trade-off Between Accuracy and Plausibility in 3D Hand Shape Reconstruction
## Motivation
[[MANO]]: plausible; Non-parametric: accurate
This paper proposes to combine them.
## Method
![[Pasted image 20241115105903.png]]
### Joint regression
Image =>ResNet50 => latent feature $z\in\mathbb{R}^{1000}$
$z$ => pose decoder => $J_{pred}\in\mathbb{R}^{21\times 3}$. 
$z$ => non-param model (like [[@ge3DHandShape]] or [[METRO (Lin et al., 2021)]]). => hand mesh $M_{np}=(V, F)$ => Use $\mathcal{J}$ in MANO to regress joints $\hat{J}$. => VAE => refined joints $\tilde{J}$. 
The loss is 
$$L_{joint} = \|\hat{J}-J\| + \|\tilde{J}-J\| + \|\hat{J}-\tilde{J}\| + \lambda L_{KL}$$
$L_{KL}$ is the KL divergence used in VAE.

### Parametric Mesh reconstruction
Use estimated joints to estimate twist rotation matrix $\varphi$ to predict MANO param
### Interaction refinement
Use the MANO model to predict SDF, and penalize the penetrations.
### Weakly-Supervised
It also works on the connection of hand-object.