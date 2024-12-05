---
tags:
  - HandPose
  - DNN/Transformer
  - "#Discriminative"
Institute:
  - Sungkyunkwan Univ.
  - Alibaba
Corresponding Author:
  - Jong Hwan Ko
Code: https://github.com/cwc1260/HandDAGT
Year: 2024
Publisher: ECCV
aliases:
  - "@chengHandDAGTDenoisingAdaptive2024"
---
# HandDAGT: A Denoising Adaptive Graph Transformer for 3D Hand Pose Estimation
## Motivation
The self- and intra- occlusions of hands with objects is currently unsolved.

## Method
Input: depth image $D$ & randomly sampled point cloud $P$.
Output: 3D joint coordinates.
### Super Points Generation
Use point set conv layer [[PointNet]] to process the points => super points
* subsampled from $N$ points to get $N/2$ points;
* Each point with local geometric features.
The features from point cloud are $d_{3d}$, from depth are $d_{2d}$, then the final feature is $F\in\mathbb{R}^{N/2\times (d_{2d} + d_{3d})}$.
![[HandDAGT.png]]
### Adaptive Graph Transformer
Keypoint embeddings are first augmented w/ a GCN and fed into a transformer block.
Use Hadamard product to replace dot products => channelwise multiplication.

### Denoising training
Different from diffusion , only introducing noise during training. Only for the first transformer layer. (data augmentation?)

Experiments are done on [[ICVL]], [[NYU]], [[DexYCB (Chao et al., 2021)]].