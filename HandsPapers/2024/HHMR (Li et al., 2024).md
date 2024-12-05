---
tags:
  - HandMesh
  - DNN/Diffusion
  - "#Model-free"
  - "#Generative"
Institute:
  - Tsinghua Univ.
  - Beijing Normal Univ
Corresponding Author:
  - Yebin Liu
Year: 2024
Publisher: CVPR
aliases:
  - "@liHHMRHolisticHand2024"
---
# HHMR: Holistic Hand Mesh Recovery by Enhancing the Multimodal Controllability of Graph Diffusion Models
## Motivation
* One-way regression strategy limits the performance of more advanced hand mesh recovery tasks, i.e., inpainting, generation.
* Requires finetuning for different tasks.
=> Propose an All-in-One framework readily for different tasks without any additional finetuning or inversion.
![[Pasted image 20241126112215.png]]
## Method
Goal: a diffusion model takes the task-specific conditions $f_\theta(x_t, \mathbf{c}, t)$ as input.
Different conditions $c$ correspond to different tasks: if $\mathbf{c}$ is :
* RGB image => mesh reconstruction
* 2D skeleton => mesh fitting
* 3D skeleton => mesh inpainting
* $\emptyset$ => unconditional generation
### How to encode different conditions into the same space?
3D & 2D skeletons: use MLP to encode;
RGB image condition: use ViT to encode.
The final input condition is $\mathbf{c} = \mathbf{c}_{image}|\mathbf{c}_{skel2d}|\mathbf{c}_{skel3d}$.
While training, the masks are randomly set to $\emptyset$. 