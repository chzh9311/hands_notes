---
tags:
  - HandMesh
  - ImplicitRepresentation
Institute:
  - ETH
Corresponding Author:
  - Siyu Tang
Year: 2021
aliases:
  - "@karunratanakulSkeletonDrivenNeuralOccupancy2021"
Publisher: 3DV
---
# A Skeleton-Driven Neural Occupancy Representation for Articulated Hands
## Motivation
1. Transforming posed hands to canonical space typically rely on iterative IK, which is **not differentiable**.
2. An obvious gap between skeleton-based & mesh-based representations.

## Method
### Canonicalization of 3D Hand Skeleton
* axis-angle rotations does not work due to unconstrained twist of bones.
Inspired by [[Spurr et al., 2020|@spurrWeaklySupervised3D2020a]], define consistent local coordinate system for each bone.
![[HALO_rotations.png]]
* Each bone motion is modelled by two rotation angles: flexion and abduction
* Define a set of unique transformations based on this coordinate system.

### Occupancy Network
Like in [[NASA (Deng et al., 2020)]], 
The query point is actually transformed back to the canonical space
![[Pasted image 20241114173234.png]]

the result is defined by the maximum of all occupancies. i.e., **if the query point was inside one finger after transformation, then the occupancy is 1**.

### Grasp Generation
1. Use VAE to generate keypoints;
2. Use HALO to obtain the surface.

## Exp
Obvious increase compared to [[NASA (Deng et al., 2020)]]
