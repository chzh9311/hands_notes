---
tags:
  - HandMesh
  - DNN/Transformer
Institute:
  - UT Austin
  - Univ of Michigan
  - UC Berkeley
  - NYU
Corresponding Author:
  - Jitendra Malik
Code: https://github.com/geopavlakos/hamer
Year: 2024
Publisher: CVPR
aliases:
  - HInt
  - "@pavlakosReconstructingHands3D2024"
---
# Reconstructing Hands in 3D with Transformers
## Motivation
Simple but high capacity models + huge amout of data => good performance. e.g., [[HMR (Kanazawa et al., 2018)]] & [[HMR2.0 (Goel et al., 2023)]]
This paper takes this philosophy to Hand mesh recovery.
## Method
The [[MANO]] model is utilized for representing the mesh.
### Problem
An RGB image $I$ => 3D hand mesh ([[MANO]] Parameters). + camera params $\pi$.
### Architecture
HaMeR utilizes the full transformer design. [[ViT]]-H as the backbone
![[HAMER.png]]
### Losses
3d supervision $$\mathcal{L}_{3D} = \|\theta - \theta^*\|_2^2+ \|\beta - \beta^*\|_2^2+\|X - X^*\|_1$$
where $\theta$, $\beta$ are the params of MANO, and $X$ is the 3D joints. * indicates GT.
plus 2D supervision: $$\mathcal{L}_{2D} = \|x - x^*\|_1$$
plus, discriminators $D_k$ for hand shape $\beta$, hand pose $\theta$, and hand joint angles (ref. [[HMR (Kanazawa et al., 2018)]]) are trained. Then apply an adversarial loss: $$\mathcal{L}_{adv} = \sum (D_k(\Theta) - 1)^2$$
### Training
The dataset is the consolidation of multiple datasets, including: [[FreiHand (Zimmermann et al., 2019)]], [[HO3D|HO3D]], [[MTC]], [[RHD]], [[InterHand2.6M]], [[H2O3D]], [[DexYCB (Chao et al., 2021)]], [[COCO WholeBody]], [[Halpe]], & [[MPII NZSL]]. Totally 2.7M training examples.
## Dataset: HInt (Hand Interactions in the wild)
* Frames are sources from [[Hands23]], [[Epic-Kitchens]], and [[Ego4D (Grauman et al., 2021)]]
* Initialize the annotation procedure with an existing keypoint detection model (from [MMPose](https://github.com/open-mmlab/mmpose)).
* Annotation consistency check
## Experiments
### 3D pose Acc
* Use the [[FreiHand (Zimmermann et al., 2019)]] and [[HO3D|HO3D-v2]] 
![[HaMeR - FreiHand.png]]![[HaMeR - HO3D.png]]
But for in-the-wild dataset (HInt), the result is much better:
![[HaMeR - HInt.png]]The ablation study also shows that large scale training data and large model are key to good performance.
![[HaMeR - Ablation.png]]