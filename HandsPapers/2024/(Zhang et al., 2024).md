---
tags:
  - weakly-supervised
  - HandMesh
Institute: Rensselaer Polytechnic Institute, IBM
Corresponding Author: Qiang Ji
Year: "2024"
Publisher: ECCV
---
# Weakly-Supervised 3D Hand Reconstruction with Knowledge Prior and Uncertainty Guidance
## Motivation
1. Lack of data -> weakly supervised training
2. Existing weakly-supervised methods (ARXIV:1902.03451, ARXIV:2103.11703, @kulonWeaklySupervisedMeshConvolutionalHand2020, @spurrWeaklySupervised3D2020) train images on real images and 2D annotations. Typically, there are two loss terms:
	1. Prior term on 3D hand prediction -> realism;
	2. Data term on consistency between the projection of 3D and 2D image.
3. Challenges: 
	1. No sufficient dataset that captures *realistic hand movement patterns*;
	2. the data term overlook *uncertainty in image observations* -> degraded model performance (ref: CorpusId:71134)

## Method
Use [[MANO]] for mesh representation
### Solving Realism problem
1. A loss that punishes out-of-bound joint angles
2. **Hand functional anatomy**: 
	1. MCP bending restricts its splaying (CorpusId:22071427)
	2. PIP and DIP (CorpusId:68051515) bends with each other.
		![[hand anatomical constraints.png]]
3. **Hand Physics**: Non-penetration
4. Shape regularization like in [[(Chen et al., 2021)]] & [[(Kulon et al., 2020)]]
### 2D uncertainty
Assume the joint position on an image is modelled as a Gaussian distribution -> is a weighted average of 2D JPE actually.....
NLL loss is also found in [[Cyclehand]]
## Experiments
SOTA among weakly-supervised methods on [[FreiHand (Zimmermann et al., 2019)]], [[DexYCB (Chao et al., 2021)]], and [[HO3D]].
