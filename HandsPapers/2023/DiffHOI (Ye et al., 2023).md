---
tags:
  - Hand-Object
  - DNN/Diffusion
  - Egocentric
Institute:
  - CMU
Corresponding Author:
  - Shubham Tulsiani
Code: https://judyye.github.io/diffhoi-www/
aliases:
  - "@yeDiffusionGuidedReconstructionEveryday2023a"
Year: 2023
Publisher: ICCV
---
# Diffusion-Guided Reconstruction of Everyday Hand-Object Interaction Clips (Oral)
## Motivation
1. single-view 3D reconstruction approaches are data-driven, cannot obtain precise due to single-view input;
2. video-based HOI reconstruction methods rely on geometry-driven optimization, only suited for in-hand scanning but not applicable for everyday scenes. (**short video clips**)
=> This method unifies the above.

## Method
Input:
* a monocular video of a hand interacting with a rigid object $\hat{I}^t$.
* hand object masks $\hat{M}^t = (\hat{M}_h^t, \hat{M}_o^t)$.
Output:
* Constant object implicit field $\phi$ ;
* hand meshes $H^t = MANO(\theta_A^t, \beta)$.
* Relative poses of hand and object $T^t_{h\rightarrow o}$ ;
* camera poses $T^t_{c\rightarrow h}$.
Also added a per-frame intrinsics $K^t$ to account for zoom-in effects.
The params to be optimized are:
$$\phi, \theta_A^t, \beta, T^t_{h\rightarrow o}, T^t_{c\rightarrow h}, K^t$$
### Prior
The prior is expressed as: $p(\phi^t|H^t, C)$. Optimize:
$$\log p(\phi^t|H^t, C)\approx \mathbb{E}_{v\sim V}\log p(\pi (\phi^t; v)|\pi(H^t;v), C)$$
$v$ is the viewpoint drawn from a prior distribution, $C$ is the category label, $\pi$ is the rendering func.
The model is trained to recover a noisy object rendering given hand rendering and text prompts:
![[DiffHOI.png]]
### The optimization
1. Reprojection Error of the mask: 
2. Loss to appear more likely from a novel view (Use diffusion output to supervise the projection) [[SDS]] (Scored Distillation Sampling) to approximate the gradient step. 
3. Eikonal loss to encourage $\phi$ to be a valid SDF.
4. Difference between adjacent frame poses to ensure smoothness.
### Initialization
use [[FrankMocap]] as the off-the-shelf reconstruction system to initialize hand shape and camera pose. Object SDF is initialized as a coarse sphere.
## Experiments
* [[HOI4D]];
* [[Epic-Kitchens]] for in the wild.