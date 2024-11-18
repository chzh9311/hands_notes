---
tags:
  - HandMesh
  - Representation
  - HandAvatar
Institute:
  - ICL
  - Cosmos Design
Corresponding Author:
  - Stefanos Zafeiriou
Code: https://github.com/rolpotamias/handy
aliases:
  - "@potamiasHandyHighFidelity2023"
Year: 2023
Publisher: CVPR
---
# Handy: Towards a high fidelity 3D hand shape and appearance model
## Motivation
Current methods rely on [[MANO]], which is low-polygon, lacks diversity in terms of age, gender and ethnicity, and no hand textures.
1. [[MANO]] is low-polygon, and only models adults' hands. Children's hands are very different and MANO will lead to errors;
2. Absence of high-reso texture models. [[HTML]] utilizes PCA of low-reso UV maps, so the textures tend to be blurry.
**Handy** captures subjects aged from 1 to 81. The texture model is built using a style-GAN
## Method
The model is originated from a large-scale hand scan dataset.
## The training dataset
containing 1208 subjects with diversity in age, gender and ethnicity
Two resolution templates
1. Low polygon: MANO
2. High polygon: 8407 vertices
To register, apply Non-rigid Iterative Closest Point (NICP@ambergOptimalStepNonrigid2007) algorithm:
> [!Note]- NICP
> Is the algorithm to minimize the difference between two point clouds. ICP keeps one fixed while transforming the other. Steps:
> 1. Each point, match the closest point in the reference PC.
> 2. Estimate the translation and rotation regarding the above pairs;
> 3. transform
> 4. iterate back to 1.
> NICP is the non-rigid version. The transform params are a set of 3 x 4 transformation matrices $\mathbf{X}_i$ per template vertex: $$\mathbf{X}\overset{\Delta}{=}[\mathbf{X}_1, \dots, \mathbf{X}_n]^T$$
> So a cost function will minimize the difference between transformed templates and results: $$E_d(\mathbf{X}) = \sum w_id^2(\mathcal{T}, \mathbf{X}_i\mathbf{v}_i)$$
> Another stiffness term is sued to regularise the deformation. With a weighting matrix $\mathbf{G}:=\text{diag}(1, 1, 1, \gamma)$ ->$$E_x(\mathbf{X}) :=\sum_{(i,j) \in \mathcal{E}}\|(\mathbf{X}_i - \mathbf{X}_j)\mathbf{G}\|^2_F$$ The third term is a simple landmark term. Landmarks are predefined template and target point pairs. This term is simply minimizing this.
> The overall cost function is: $$E = E_d + \alpha E_s + \beta E_l$$ where $\alpha$ is the stiffness.
> Then the process is :
> 1. Initialize $\mathbf{X}_0$;
> 2. Iterate over different stiffness $\alpha^i, i\in[1, n], \alpha^i > \alpha^{i+1}$ , 
> 	1. Until $\|\mathbf{X}^j - \mathbf{X}^{j-1}\|<\varespilon$;
> 		1. Find preliminary correspondences for $\mathbf{X}^{j-1}$;
> 		2. $X^{j}$ as the optimal deformation for the above correspondence

With the registered models, use method like in [[MANO]] to get the result
### Appearance model
Manually design a UV template, and use GAN to generate realistic UV map

## Experiments

Done on [[FreiHand (Zimmermann et al., 2019)]] and Synthetic datasets
