---
tags:
  - NVS/exo-to-ego
Institute: Meta, UT Austin, etc.
Corresponding Author: Bertasius and Grauman
Code: https://klauscc.github.io/4diff
Year: "2024"
Publisher: ECCV
---
# 4Diff: 3D-Aware Diffusion Model for Third-to-First Viewpoint Translation

## Dataset
[[Ego-Exo4D]]

## Challenges
* Numerous objects and actor movements
* Sharp viewpoint changes between exo and ego views.
* The dataset [[Ego-Exo4D]] only provides a few views.
Current methods are not satisfactory:
* Geometry-free methods generates geometrically imfeasible images;
* Geometry-based approaches generates non-photorealistic images.
## Main Idea
* Egocentric point cloud rasterization
* 3D-aware rotary cross-attention layers.

## Previous work
### Exo-to-ego
* GAN-based models
	* [[X-fork&X-Seq]]. 
### Novel View Synthesis (NVS)


## Method
### Problem Formulation
Given an *exocentric* image $x \in \mathbb{R}^{h\times w\times 3}$ and the *relative* camera pose $P\in\mathbb{R}^{4\times 4}$ from exo camera to the ego camera. Our goal is to synthesise an egocentric image $y\in \mathbb{R}^{h\times w\times 3}$:
$$
	p(y|x, P)
$$
* The relative camera pose ($P$) is known.
![[4Diff.png]]
The two main techniques are: **Point Cloud Rasterization** and **3D-aware Rotary Cross-Attention**.
### Egocentric Point Cloud Rasterization
1. Use a depth estimator (Based on [[MiDaS]]) to get the depth $D$. Use a feature encoder to get features. Combine the two to get a *feature point cloud*. Then this point cloud is rendered (using [[SynSin]], with some adjustment by adding a point cloud) into an egocentric prior.
	$$
	H^{prior} = [x^{prior}, F^{prior}] = render([x, F^{exo}, D, P])
	$$
### 3D-Aware Diffusion Image Transformer
1. The predicted noise each step is conditioned on egocentric prior $H^{prior}$ and exocentric semantic features $F^{exo}$.

### 3D-aware Rotary Cross-Attention