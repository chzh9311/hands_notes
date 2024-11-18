---
tags:
  - Hand-Object
Institute:
  - South China Univ of Tech
  - Pazhou Lab
  - Tencent AI Lab
Corresponding Author:
  - Changxing Ding
Code: https://github.com/lzfff12/HFL-Net
aliases:
  - "@linHarmoniousFeatureLearning2023"
Year: 2023
Publisher: CVPR
---
# Harmonious Feature Learning for Interactive Hand-Object Pose Estimation
## Motivation
* Hand and object are competitive in feature learning
* when using two separate backbones:
	* model size becomes large
	* the feature space becomes independent -> cannot deal with mutual features
=> share low-level and high-level features of one ResNet50
![[HFL-Net framework.png]]
## Method
### Backbone
In ResNet50: Stage 0, 1, and 4 are not changed; stage 2 & 3 are adopted separately for hands and objects.
Use 2 FPNs to combine features from 1 to 4 for hands and objects separately. The difference are the stages 2 & 3 the FPN fuse
### Interaction Module
**Object to hand**: concat object features with hand features -> attention;
**Hand to object**: cross attention from hand to objects
The difference is due to the flexibility (hand > object) and rigidity (object > hand)

## Several Different Backbone Design
![[Pasted image 20241105184834.png]]
double stream has the best performance, but also the most params