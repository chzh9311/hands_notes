---
tags:
  - HandPose
  - Hand-Object/Known-object
  - two-hand
Institute:
  - Graz Univ of Tech
  - LIGM
Corresponding Author:
  - Vincent Lepetit
Year: 2022
Publisher: CVPR
---
# Keypoint Transformer: Solving Joint Identification in Challenging Hands and Object Interactions for Accurate 3D Pose Estimation
Hand poses are estimated by bottom-up pattern:
![[Pasted image 20241212104446.png]]
1. All keypoints in one heatmap;
2. sample keypoints and extract with transformer.
For objects, the same manner:
Randomly sample $N=20$ points from the segmentation map and refer to them as object keypoints, use object corner loss to supervise.