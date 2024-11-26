---
tags:
  - Hand-Object
  - MotionSynthesis
  - ArticulatedObject
Institute:
  - Tsinghua Univ.
  - Shanghai Qi Zhi Institute
  - Shanghai AILab
Corresponding Author:
  - Li Yi
Code: https://cams-hoi.github.io/
Year: 2023
Publisher: CVPR
---
# CAMS: CAnonicalized Manipulation Spaces for Category-Level Functional Hand-Object Manipulation Synthesis
## Motivation
Previous works have various limitations
1. generating *static* grasps (@brahmbhattContactGraspFunctionalMultifinger2019, @jiangHandObjectContactConsistency2021);
2. Dynamic manipulation synthesis restrict their scope to rigid objects [[ManipNet (Zhang et al., 2021)]]
## Method
Use [[CVAE]] to extract features.
Input: 
1. Object mesh from a known object category. May contain different parts for an articulated object.
2. Goal sequence (The object (or each part of the object)'s 6D pose sequence) of $M$ key frames
3. Initial hand pose.
=> Goal: generate a sequence of human-like motions represented by pose sequence
### CAnonicalized Manipulation Spaces (CAMS)
1. Contact targets: $C = \{(c_{i,j,k}, V_{i,j,k}, N_{i,j,k})\}_{i,j,k}$. where $i$ indicates the finger index, $j$ indicates the key frames; $k$ indicates the object part index. $c$ is a binary flag of whether finger $i$ is in contact with $k$ at $j$ frame, $V$ & $N$ are positions and normal directions of the contact.
The gt contact points are obtained by a matching process.
![[Pasted image 20241122162902.png]]
### CVAE-based planner
1. Feature embedding from input
Encoding: encode the feature of CAMS using CVAE encoder to get the gaussian $\mu$ and $\sigma$ of the latent space. (Done at training stage)
Decoding (inference), sample the latent space, concat with feature embeddings (conditions), then decode the motion in CAMS.

### Optimization-based synthesizer
Create a complete sequence from the keyframes of CAMS.
optimize contact and penetration, and smooth the motion.