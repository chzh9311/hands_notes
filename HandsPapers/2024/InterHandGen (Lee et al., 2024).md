---
tags:
  - MotionSynthesis
  - two-hand
  - Hand-Object
Institute:
  - KAIST
  - Meta
  - ICL
Corresponding Author:
  - Tae-Kyun Kim
Code: https://github.com/jyunlee/InterHandGen
aliases:
  - "@leeInterHandGenTwoHandInteraction2024"
Year: 2024
Publisher: CVPR
---
# HOIDiffusion: Generating Realistic 3D Hand-Object Interaction Data
## Motivation
* Interacting two-hand generation is underexplored
	* There're models for hand-object [[Grasp'D]], [[Grasping Field (Karunratanakul et al., 2021)]]
* Challenge: high data complexity caused by the combination of hand articulations
	* => decompose the two-hand inter to one hand + the other hand conditioned on this hand: $$p_\phi(\mathbf{x}_l, \mathbf{x}_r) = p_\phi(\mathbf{x}_l)p_\phi(\mathbf{x}_r|\mathbf{x}_l)$$
## Method
Following the above equation, learn the prior using two models.
* Learning $p_\phi(x_r)$ from training samples of $x_r$ & $\Gamma(x_l)$;
* Learning $p_\phi(x_r|x_l)$ from training samples of $(x_r, x_l)$ and $(\Gamma(x_l), \Gamma(x_r))$.
Here $\Gamma$ means spatially flipping the hand. (left hand will become right hand, and vice versa).
During training, only one unified model is trained (by taking conditions at some samples and not taking conditions at the rest samples).
plus a anti-penetration loss to avoid penetration.