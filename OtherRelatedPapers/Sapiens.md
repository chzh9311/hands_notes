---
tags:
  - HumanMesh
Institute: Meta
Corresponding Author: Shunsuke Saito
Code: https://github.com/facebookresearch/sapiens
Year: "2024"
Publisher: ECCV
---
# Sapiens: Foundation for Human Vision Models
Sapiens is a family of models for four fundamental human-centric vision tasks: 2D HPE, body-part segmentation, depth estimation, surface normal prediction.
## Motivation
### About model
*provide a unified framework.*
**Human-centric models should satisfy**:
1. generalization -> to unseen conditions;
2. broad applicability -> versatility
3. high fidelity -> precise
### About training
Q: What type of data is most effective for pretraining?
A: 1. Data Curation 2. Large-scale pretraining.
## Method
### Pretraining
Use MAE approach for pretraining.
The following tasks are implemented using a common encoder and specific decoders.
### 2D HPE
Simply use ViTPose.
### Segmentation Model
Estimate per-pixel class (semantic information) to create a probability map $\hat{p}\in\mathbb{R}^{H\times W\times C}$ such that $\hat{p}=\mathcal{S}(\mathbf{I})$. 
### Depth
the model is identical to segmentation.
### Surface Normal Estimation
Similar to previous tasks, except the output channels are set to 3 (3D vectors).
## Experiments
![[Sapiens on Human-5K.png]]
> [!note] Important Note
> The input image sizes are different. Sapiens takes images 16 times larger as input, this could be the reason for high performance. As shown in the motivation, this model is 
### The Effect of Pretraining Params
![[Sapiens-pretrain.png]]
* Specialized > General;
* More Data > Less Data
* ![[Sapiens - Unique.png]]
* More Unique persons > less