---
tags:
  - DNN/Transformer
  - HandPose
Institute:
  - CMU
  - Salesforce Research
Corresponding Author:
  - Kris M. Kitani
Year: 2023
aliases:
  - "@fuDeformerDynamicFusion2023"
Publisher: ICCV
---
# Deformer: Dynamic Fusion Transformer for Robust Hand Pose Estimation
## Motivation
In video input:
* Motion blur
* Occlusion
are important factors that cause degraded performance.
For training, the fingertips tend to have larger errors than those around the palm
## Method
![[Deformer2023.png]]
1. Temporal-Spatial transformers.
2. Dynamic Fusion Module=>motivation: the prediction of spatialtemporal transformer is still heavily affected by the current frame. We hope to utilize nearby frames when the current one is severely occluded or blurred.
	Predict a pair of forward and backward motion $(d\theta_t^{fw}, d\theta_{t}^{bw})$. GT is the MANO pose difference between this frame and the next/previous frame.
	With this, every frame can forward and backward infer the pose of all frames.
	The final pose is the weighted average of all inferred results.

### Training
$$L = L_{mesh} + L_{adv} + L_{aux}$$
**maxMSE Loss**: Inspired by [[focal loss]], adjusts the weights for every location $w_i = \frac{(\mathcal{P}_i - \mathcal{P}_i^\prime)^2}{\sum_{i=1}^N(\mathcal{P}_j-\mathcal{P}_j^\prime)}$ (according to Cauchy Inequality, this weight maximizes MSE).
The loss is used for mesh and joints. -> $L_{mesh}$
**Motion Discriminator**: Following [[VIBE]], use multi-layer GRU as the discriminator. train it together with the Deformer (generator). -> $L_{adv}$.
**Auxiliary Constraints**: $L_{aux}$  include 2D loss, monocular loss for MANO params, motion loss for $d\theta$ to be consistent with former/latter frames; smooth loss for decreasing derivatives.

## Exp
on [[HO3D]] & [[DexYCB (Chao et al., 2021)]].
sota performance for both benchmarks.