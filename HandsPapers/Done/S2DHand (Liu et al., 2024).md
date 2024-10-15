---
tags:
  - Egocentric
  - HandPose
  - weakly-supervised
Institute: University of Tokyo
Corresponding Author: Yoichi Sato
Code: https://github.com/ut-vision/S2DHand
Year: "2024"
Publisher: CVPR
---
# Single-to-Dual-View Adaptation for Egocentric 3D Hand Pose Estimation
## Motivation
Drawbacks of single-view methods:
* limited field-of-view
* depth ambiguity.
Why multi-view?
1. Solves the above problems.
2. Align with industry trends. e.g., Apple Vision & Meta Quest;
Why multi-view is difficult?
1. Training needs multi-view labels, and are costly to annotate.
2. Limited to the same camera parameters.

## Previous Multi-view Work
* [[MVHM (Chen et al., 2021)]]
* [[UmeTrack (Han et al., 2022)]]
* [[MuViHandNet (Khaleghi et al., 2023)]]
processes hand pose with a multi-view feature fusion method.

## Method
### Problem Settings
Single-to-Dual View Adaptation.
We have unlabelled dual-view data $\mathcal{D}=\{\mathbf{x}_i^{v1}, \mathbf{x}_i^{v2}|_{i=1}^N\}$ where there are no GT or camera parameters. The goal is to get the camera poses as well as the hand pose.
### Solution
1. With a pretrained single-view 3D pose estimator, we estimate the two images from the dual-view data, get $J_i^{v1}$ and $J_i^{v2}$. The rotation matrix $R$ is estimated by:
	$$
		R^{(0)} = \frac{1}{N}\sum rot(J_i^{v1}, J_i^{v2})
	$$
2. Update a momentum estimator by $\bar{\mathcal{H}}(\bar{\theta})$ : $$\bar{\theta}^{(T)} = \eta\bar{\theta}^{(T-1)}+(1-\eta)\theta$$
3. Use the momentum estimator to generate pseudo-labels.
	1. Predict the 3D poses from both views;
	2. *Attention Based Merging*: Propose attention to each of the predicted joints as the confidence. The attention is generated regarding the maximum heatmap value. Further studies show that taking only the joint with the larger confidence gives the best performance.
	3. Generate the pseudo-labels with the attention.
		![[pseudo-label.png]]
	4. Rotate the hand joints properly to keep the rotation between the joints from two-views consistent.
		![[Pasted image 20241008181649.png]]
	5.  The final pseudo-label is a weighted average of $\hat{y}_{abm}$ and $\hat{y}_{rgr}$.
	6. $R$ is also updated during training, using the moving average of Joints.
![[S2DHands.png]]

## Experiments
* [[AssemblyHands]] is employed as the evaluation set.
1. Largely exceeds baseline;
2. SoTA in cross-dataset settings;
3. RGR is useful when prediction errors are large (> 60mm)