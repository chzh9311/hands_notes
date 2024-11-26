---
tags:
  - HandMesh
  - two-hand
  - Dataset
Institute:
  - Southeast Univ
  - ByteDance
Corresponding Author:
  - Yangang Wang
Code: "https://github.\rcom/binghui-z/InterPrior_pytorch"
aliases:
  - "@zuoReconstructingInteractingHands2023"
Year: 2023
Publisher: ICCV
---
# Reconstructing Interacting Hands with Interaction Prior from Monocular Images
## Motivation
1. Existing methods localize and identify joints, but can be misguided by the regional occlusion and local similarities;
2. Rely heavily on 2D joint estimator, more data or larger models.
So the solution is
1. construct interaction prior;
2. sample from this prior manifold using interaction cues.
For dataset: [[InterHand2.6M]] contains *simple background* and only *8.5k interaction patterns*.
-> a dataset with 500K patterns
![[Pasted image 20241119104836.png]]
## Method
![[Pasted image 20241119113037.png]]
### Feature Extraction
for an image, extract:
1. Interaction Adjacency Heatmap (IAH);
>[!note]- IAH
>IAH is defined as the mixture coordinate distribution of this joint and other two-hand joints within its coordinate neighborhood. IAH is proposed due to the difficulty of localising exact joint, and modelling adjacent joints.
2. Instance saliency maps;
3. Left-to-right relative translation.
### Interacting Feature Fusion
use attention to get the fused features $x$.
### Interacting State Sampling
Use a VAE to encode the pose and get latent space. 
**Feature Alignment**: align the features from ViT and prebuilt features.

### Exp
on [[InterHand2.6M]] achieves sota, but relatively marginal in MPJPE and MPVPE