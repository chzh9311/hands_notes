---
tags:
  - physics
  - Generative
  - MotionSynthesis
Corresponding Author:
  - Gerard Pons-Moll
Institute:
  - University of Tubingen
  - MPI
  - Meta
  - Huawei
Publisher: CVPR
Year: 2024
Code: https://virtualhumans.mpi-inf.mpg.de/force/
---
# FORCE: Physics-Aware Human-Object Interaction
## Key insight

> human motion is dictated by the interrelation between the force exerted by the human and the perceived resistance.

## Method

![[Pasted image 20250609152134.png]]
### Physics Encoding
1. $\mathcal{F}_i=\{F_i, R, c_i\}$. $F$ is the 3D human force, $R$ is the resistance scale, and $c$ is the binary contact label of hands. Sampled from $\tau = 13$ frames.
	1. The human force is calculated by accelerations.