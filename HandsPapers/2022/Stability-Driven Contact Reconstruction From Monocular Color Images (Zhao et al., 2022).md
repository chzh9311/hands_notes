---
tags:
  - Hand-Object/Known-object
  - physics
  - Dataset
Institute:
  - Southeast Univ
Corresponding Author:
  - Yangang Wang
Year: 2022
Publisher: CVPR
---
# Stability-Driven Contact Reconstruction From Monocular Color Images
## Motivation
monocular reconstruction of hand-object rely on diverse data.
-> Reconstruct the contact pattern driven by the physical criteria via a physical engine.
## Method
1. Represent the hand-object as a series of ellipsoids, because it is best for efficiently modelling collisions
![[Pasted image 20241204150701.png]]
![[Pasted image 20241204160403.png]]
### Regression
**H-O State representation**
The hand mesh is segmented and converted by part to the above ellipsoids
Estimate the state of hand and object $S$ to initialize them in the physics engine ([bulletphysics/bullet3: Bullet Physics SDK: real-time collision detection and multi-physics simulation for VR, games, visual effects, robotics, machine learning etc.](https://github.com/bulletphysics/bullet3))
The contact evaluated by the stability cost:
$$C=C_{\mathcal{S}}() + C_{\mathcal{R}}()$$
Where $C_S$ measures the change before/after the simulation, and $C_R$ measures the physical relationship (F - ma).
The optimization is done in a sample-redistribution scheme.
## Dataset