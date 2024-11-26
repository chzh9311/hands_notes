---
tags:
  - HandPose
  - Egocentric
  - DNN/Transformer
  - actionRecognition
Institute:
  - UHK
  - Microsoft
Corresponding Author:
  - Wenping Wang
Code: "https://github.com/\rfylwen/HTT"
aliases:
  - "@wenHierarchicalTemporalTransformer2023"
Year: 2023
Publisher: CVPR
---
# Hierarchical Temporal Transformer for 3D Hand Pose Estimation and Action Recognition from Egocentric RGB Videos
## Motivation
Occlusions and depth ambiguity affects the results => temporal
No current framework are doing pose estimation together with action recognition
![[Pasted image 20241121172507.png]]
## Method
### Hierarchical Temporal Transformer(HTT)
Action recognition consists of two low-level tasks: (hand motion + object)
The Transformer consists of two parts:
* Action block $A$, aggregate the hand motion & object label, in a long-term timespan to recognize actions.
* Pose block $P$ estimate the pose and object label, applied to a shorter timespan (to leverage adjacent frames to alleviate occlusion)