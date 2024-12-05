---
tags:
  - HandMesh
  - DNN/Diffusion
  - DataAugmentation
  - "#Model-based"
  - "#Discriminative"
Institute:
  - CUHK
  - Univ of Electronic Sci & Tech of China
Corresponding Author:
  - Chi-Wing Fu
Code: https://github.com/hxwork/HandBooster_Pytorch
Year: 2024
Publisher: CVPR
aliases:
  - "@xuHandBoosterBoosting3D2024"
---
# HandBooster: Boosting 3D Hand-Mesh Reconstruction by Conditional Synthesis and Sampling of Hand-Object Interactions

## Motivation
1. Data-driven is cool, but the performance is limited by the training data (lacks diversity)
2. Synthetic data can accomplish both accuracy and diversity, but unrealistic (domain gap)
> [!quote]
> how to generate realistic & diverse hand-object interaction images with reliable annotations?

Previous methods are categorised to render-based and generative-based. 
* Render-based methods ([[GAN-HAND]], [[AffordPose (Jian et al., 2023)]], and [[Artiboost (Yang et al., 2022)]]) are prone to produce unrealistic images;
* Generative-based methods ([[HOGAN]] / [[AffordanceDiff]]) generate graspings on RGB images. but diversity is limited, and annotations are missing.
## Method
![[HandBooster.png]]
### H-O Image synthesizer
Input: 3D hand mesh + Conditions (texture map + normal map)
Output: realistic image
**training this model**: $x_0\in\mathbb{R}^{128, 128, 3}$ is the image used for reconstruction, we aim to generate a realistic sample $\hat{\mathbf{x}}_0$ with the diffusion model:$$ \hat{\mathbf{x}}_0=f_\theta(\text{Concat}(\mathbf{n}, \mathbf{c}), \mathbf{h}_q, PE(t))$$
Supervise with the original image to train the model.
> [!question] What is the hand orientation $\mathbf{h}_q$ for ?

## Reconstruction
[[MANO]]-based method
