---
tags:
  - Hand-Object
  - DNN/Diffusion
Institute:
  - CMU
  - Meta
Corresponding Author:
  - Shubham Tulsiani
Project: https://judyye.github.io/ghop-www/
Year: 2024
Publisher: CVPR
aliases:
  - "@yeGHOPGenerativeHandObject2024a"
---
# G-HOP: Generative Hand-Object Prior for Interaction Reconstruction and Grasp Synthesis
## Motivation
Goal: build a computational system that generates plausible hand-object configurations. (previous work only focus on generating hand grasps)
Learn a diffusion model that captures the joint distribution of hand and object during interaction; Given a category-conditioned description the model can generate both;
Build a model that captures the joint distribution, and $\mathbf{C}$ is the text of an object category.
$$p(\textbf{O}, \textbf{H}|\textbf{C})$$
## Method
*interaction grids*: a concatenation of latent SDF grid of the object and a skeletal distance field of the hand.
### Object Representation
use SDF to capture. [[VQ-VAE]] to compress.
### Hand Representation
Previous works ([[Guided Motion Diffusion|@karunratanakulGuidedMotionDiffusion2023]], [[MDM|@tevetHumanMotionDiffusion2022]]) generate hand/human shape by diffusing in the pose space. However, this space is not ideal. 
-> pose-parameterized distance field in 3D grid indicating the distance of each grid to each joint -> some kind of distance field, so it's better fit with with object SDF
### Learning the distribution
Use text embedding + noisy 3D interaction grid $\mathbf{x}_i$ -> trained to restore a clean grid.
### Generation
Use Score Distillation Sampling ([[DreamFusion|@pooleDreamFusionText3DUsing2022]]) to approximate log-probability gradients

**To reconstruct interaction clips:**
**Render**:
Like [[DiffHOI (Ye et al., 2023)|@yeDiffusionGuidedReconstructionEveryday2023a]], decomposes the HOI scene into 3 parts:
1. time-persistent object SDF;
2. time-varying hand pose;
3. relative poses between them
**Reconstruction**:
Unlike [[DiffHOI (Ye et al., 2023)]], use 3D priors instead of 2D.

**To synthesize grasps**
From object mesh to synthesize human grasps. equals to sample from the distribution $p(\mathbf{H | O, C})$. The Joint distribution $p(\textbf{O}, \textbf{H}|\textbf{C})$ cannot be directly inferred to the conditional distribution. So the authors optimize at *test time* and constraining the object shape to the given shape, then rank all grasps and take the best ones.

## Experiments
On [[HOI4D]], an egocentric dataset recording people interacting with different objects.

Baselines:
* [[iHOI]]
* [[HHOR]]
* [[DiffHOI (Ye et al., 2023)]]