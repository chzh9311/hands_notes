---
tags:
  - Hand-Object
Institute: ETH, MPI
Corresponding Author: M. J. Black, Otmar Hilliges
Code: https://github.com/zc-alexfan/hold
Year: "2024"
Publisher: CVPR
---
# HOLD: Category-agnostic 3D Reconstruction of Interacting Hands and Objects from Video
## Motivation
* Most HO reconstruction methods assumes a prescanned object template
	* [[ARCTIC (Fan et al., 2023)|ArcticNet-SF]]
	* [[Photometric]]
	* [[UnconstrainedHOR(Hasson et al., 2021)]]
	* [[CPF (Yang et al., 2021)]])
* Other methods without predefined object templates lacks generalization.
	* [[Learning R of HO (Hasson, et al., 2019)]]
	* [[Implicit for Grasp (Karunratanakul et al., 2020)]]
	* [[What's in ur hands (Ye et al., 2022)]]

## Problem
*category-agnostic reconstruction of hands and objects from a monocular video*.
**Key insight**: hand and objects in interaction provide complementary cues to each other's shapes and poses.

## Method
Inspired by [[Vid2avatar (Guo et al., 2023)]], [[Volume rendering of neural implicit surfaces]]
### Initial hand pose estimation <- hand regressor
Simply use [[HShapeTransformer (Lin et al., 2021)]].
### Object pose <- structure from motion
Following [[Hampali et al., 2023]]:
1. Create object-only images by masking out the object pixels via [[SAM (Kirillov et al., 2023)]].
2. Use HLoc [[SuperGlue (Sarlin et al., 2020)]] to perform SfM -> a point cloud defining the object and its rotation $R\in SO(3)$ & translation $t\in R^3$.
3. Leverage optimization procedure to encourage hand-object contact while matching 2D projections. This process gets scale $s\in R$. 
### HOLD-Net
Like [[NERF]], [[NERF++]], it models the observation space along the rays
![[Pasted image 20241003150319.png]]

**Hand Model**: modelled as an SDF (in canonical space) and driven by MANO pose, rotation & translation. 
Points from observation space are mapped back using inverse LBS.

**Object Model**: similar to hand by SDF, but it is rigid. Only driven by scale, rotation & translation.

**Backgrond**: Define a bounding sphere of hands and objects, and predict SDF for points outside this sphere.

**Compositional Volumetric rendering**: Refer to [[Volume rendering of neural implicit surfaces]]. It's actually rendering back to the original image.

**Losses**:
1. RGB values should align with the input image:
	$$
		\mathcal{L}_{rgb} = \sum_{\mathbf{r}}\|C(\mathbf{r}) - \hat{C} (\mathbf{r})\|
	$$
	where $\mathbf{r}$ stands for a ray that is casted from a sample pixel on the image.
2. Encourage disentaglement between hand, object, and background -> multiclass segmentation loss:
	$$
		\mathcal{L}_{segm} = \sum_{\mathbf{r}}\|S(\mathbf{r}) - \hat{S} (\mathbf{r})\|
	$$
	 The $S\in\mathbb{R}^3$ is a one-hot vector representing the predicted class of a pixel (hand, object, bg). Obtained with SAM.
3. Enforce MANO priors to be on the predicted hands:
	$$
		\mathcal{L}_{sdf} = \sum_{\mathbf{x}\in\mathcal{X}}\|f_h(\mathbf{x}) - SDF (\mathbf{x})\|
	$$
	$\mathcal{X}$ is a set of randomly sampled points in canonical space. $f_h$ is the SDF of predicted hand, and SDF is that of MANO mesh. MANO is subdivided by [[Loop subdivision (Loop, 1987)]].
4. Enforce the ray far away from the model to have density 0. The [[Amodal Instance Segmentation (Li & Malik, 2016)|amodal]] mask probility is forced to be 0 outside the hands and objects:
	$$
		\mathcal{L}_{sparse} = \sum_{\mathbf{r}\in\mathcal{F}_h}\|M_h(\mathbf{r})\| - \sum_{\mathbf{r}\in\mathcal{F}_o}\|M_o(\mathbf{r})\|
	$$
### Pose Refinement
1. Train HOLD-Net for a small number of epochs to get a rough estimation.
2. Refine hand-object pose params with mesh-based constraints. like in [[Hi4D (Yin et al., 2023)]]
3. Encourage contact between frequently contacted hand vertices $V_{tips}$ from [[Learning R of HO (Hasson, et al., 2019)]]. The loss is the distance between $V_{tips}$ and the nearest object vertex.
### Training
With the refined pose params, we can fully train the model.
## Experiments
### Datasets
[[HO3D]] for in-the-lab scenes; Captured a dataset themselves for in-the-wild scenes.
$CD_h$: the hand-relative Chamfer Distance for the object.
Results:
![[Pasted image 20241003170804.png]]
The increase is obvious.
Ablation study proves that modelling hands and objects together helps to increase the performance.

## Limitations
* Thin or textureless objects;
* May not be able to reconstruct rarely observed object regions.