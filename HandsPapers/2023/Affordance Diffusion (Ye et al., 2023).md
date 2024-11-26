---
tags:
  - ImageSynthesis
  - Hand-Object
Institute:
  - CMU
  - NVIDIA
Corresponding Author:
  - Sifei Liu
  - Shubham Tulsiani
Code: https://judyye.github.io/affordiffusion-www
aliases:
  - "@yeAffordanceDiffusionSynthesizing2023"
Year: 2023
Publisher: CVPR
---
# Affordance Diffusion: Synthesizing Hand-Object Interactions
## Motivation
Current methods lacks the understanding of affordance, cannot synthesize well based on image input (Previous methods usually use texts as input).
Affordance: the function that environment could offer, but how to represent it is still an open question. Previous works map images to categories ([[EGO-TOPO|@nagarajanEGOTOPOEnvironmentAffordances2020]], ) predict heatmaps (ARXIV:1812.04558). Recent works predict contact distance ([[Grasping Field (Karunratanakul et al., 2021)|@karunratanakulGraspingFieldLearning2020]]), action trajectories ([[Where2Act|@moWhere2ActPixelsActions2021]]) & grasp categories ([[@goyalHumanHandsProbes2022]]). While this work proposes to simplify, only synthesize HOI images.

## Method
**Key idea**: <u>the synthesis follows a coarse-to-fine process</u>. **where** to interact => **how** to interact.
![[AffordanceDiff_framework.png]]
### The "Where": LayoutNet
An iteration. $\bf{l}_{t-1}\sim\phi(\bf{l}_{t-1}|\bf{l}_t, \mathbf{I})$. The layout param $\mathbf{l} = (a,x, y, b_1, b_2)$: $a$: the hand palm radius; $x, y$, hand palm location; $\arctan(b_1, b_2)$: the approaching direction.
Because multiple $l$ can result in identical mask, use mask of  $l$ for the loss calculation, plus the loss on $l$ itself.
### The "How": ContentNet
Image conditioned diffusion: $D_\phi(\mathbf{I}_t^{hoi}, t, (\mathbf{I}^{obj}, M(\mathbf{l})))$. The condition includes the original image and the LayoutNet output.

### Constructing training data
1. Extract hand mask & remove the pixels;
2. Use image Inpainting to recover the object pixels.
3. Use [[SDEdit]] to remove the discrepancy, and mix them with images without SDEdit. 
![[Pasted image 20241122112106.png]]

## Exp
* [[HOI4D]]
* [[Epic-Kitchens]]