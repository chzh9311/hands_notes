---
tags:
  - Hand-Object
  - Dataset
Institute:
  - SJTU
  - Shanghai Qi Zhi Institute
  - South China Univ of Tech
  - XREAL
Corresponding Author:
  - Cewu Lu
Code: https://kailinli.github.io/CHORD
aliases:
  - "@liCHORDCategorylevelHandheld2023"
  - COMIC
Year: 2023
Publisher: ICCV
---
# CHORD : Category-level Hand-held Object Reconstruction via Shape Deformation
## Motivation
Previous works mostly work on known template shapes; Others are not robust.
-> due to the lack of shape prior
## Method
Input: 
* RGB image
* Estimated [[MANO]] params
* Pose of a category-level object prior
Output:
* Reconstructed shape of the object.

The MANO hand shape is obtained following [[MonoRT | @zhouMonocularRealTimeHand2020]]. 
Object 6D pose is obtained following [[FS-Net | @chenFSNetFastShapebased2021]]. 
### 2D deformation
Estimated Meshes of hands and objects -> $\mathcal{D}_H, \mathcal{N}_H$ and $\mathcal{D}_O, \mathcal{N}_O$, for the depth and normal maps of hands and objects.
![[Pasted image 20241106104909.png]]
### 3D deformation
For a point, we require:
1. 2d pixel-aligned features in normal maps and depth maps;
2. 3D shape features interpolated within its region on the object prior
3. 3D articulated features
The 2D features are just the $\mathcal{N}$ aqnd $\mathcal{D}$ as stated in [[#2D deformation]];
For 3D shape features, CHORD learns to regress hands and objects separately from a common feature space. They are both obtained in canonical space. The object here is a template.
![[Pasted image 20241106112514.png]]
After that, the features are concatenated to form a input to $\mathcal{G}_s$.
$$\mathcal{G}_S: (\mathbf{x}, \mathbf{x}^{\Theta}, \mathcal{F}_I(\mathbf{x}), \mathcal{F}_A(\mathbf{x}), \mathcal{F}_S(\mathbf{x}), \mathcal{F}_P(\mathbf{x}))\mapsto s(\mathbf{x})$$
$s$ is the SDF of the object.
### Shape prior
With a set of objects of the same category, use 3 approaches to find prior:
1. voxel mean.
2. Deep latent mean. Use [[DeepSDF]] to learn a latent code and take the mean;
3. Deep implicit template ([[DIT]]), the best of all

## COMIC Dataset: Category-level and contains rich Objects, Materials, Interactions and Camera-views.

Use [[OakInk]] as the source of the dataset.

## Experiments
Compared to [[AlignSDF]] and [[iHOI]] on COMIC, results are better.
![[Pasted image 20241106154149.png]]