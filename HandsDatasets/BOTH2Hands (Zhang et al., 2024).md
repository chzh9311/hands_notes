---
tags:
  - HandMesh
  - Dataset
  - textDriven
Institute: ShanghaiTech Univ
Corresponding Author: Lan Xu
Year: "2024"
Publisher: CVPR
Code: https://github.com/Godheritage/BOTH2Hands
aliases:
  - BOTH57M
  - "@zhangBOTH2HandsInferring3D2024"
n_frames: 57.4M
n_views: "32"
real: R
data_link: https://github.com/Godheritage/BOTH2Hands?tab=readme-ov-file#both57m-dataset
extra: 4,140 words annotations
n_subjects:
---
# BOTH2Hands: Inferring 3D Hands from Both Text Prompts and Body Dynamics
## Motivation
Previous text-to-motion advances focuses on body motion and lacks hand motion annotations; body-to-hand setting cannot provide direct controls of hand motions.
-> *Need a method to generate hand motions from text prompts and body dynamics*
## The dataset: BOTH57M
* 1,384 motion clips
* 57.4M frames;
* 23,477 annotated motions;
* 4,140 words
* 32 camera views
## Motion Generation: BOTH2Hands
1. MDM: two parallel motion diffusion models: from texts & from body motions
2. Body2Hand: Use SMPLH (22 body joints + 30 hand joints) add noise to the hand and denoise conditioned on the body pose.
3. Text2Hand: Discard body rotations, use hand 6D rotation as GT, and generate at local coordinates.
4. Cross-attention blending. text and body embeddings are first embedded into a common latent space then processed by MHCA