---
tags:
  - MotionSynthesis
  - Hand-Object
Institute:
  - ETH
  - MPI
  - KAIST
Corresponding Author:
  - Jie Song
  - Otmar Hilliges
Code: https://eth-ait.github.io/d-grasp/
aliases:
  - "@christenDGraspPhysicallyPlausible2022"
Year: 2022
Publisher: CVPR
---
# D-Grasp: Physically Plausible Dynamic Grasp Synthesis for Hand-Object Interaction
## Motivation
* Previous methods mostly focus on static motions;
* Model the motion in a dynamic way is important!
## Method
6D Object pose + static grasp + target 6D pose => dynamic grasping motion 
![[Pasted image 20250124142109.png]]
## The representation of the Contact
$$ F = (C, P, D) $$ include the contact map $C$, part map $P$ & direction map $D$.
All maps are defined on **$N$ points $O\in\mathbb{R}^{N\times 3}$ sampled from the object surface**
The contact map $C\in\mathbb{R}^{N\times 1}$: each value is within $[0, 1]$, 
These maps are learnt from a CVAE model
![[Pasted image 20250124144302.png]]
The CVAE model is proposed 