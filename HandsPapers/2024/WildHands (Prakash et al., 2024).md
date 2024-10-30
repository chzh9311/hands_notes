---
tags:
  - HandPose
  - Egocentric
Institute: UIUC
Corresponding Author: Saurabh Gupta
Code: https://bit.ly/WildHands
Year: "2024"
Publisher: ECCV
---
# 3D Hand Pose Estimation in Everyday Egocentric Images
## Goal: Achieve generalization in the wild.

## Insights
1. Croping the image is suboptimal because the location of hands is important
	1. It carries information about its pose. 
	2. Different locations are in correspondence to different distortions.
	To feed the 2D location, it's better to use *angular location in the camera's filed of view*, which is implemented by [[KPE]].
2. Joint training on 3D supervision from lab datasets and 2D auxiliary supervision on in-the-wild data (hand masks & grasp labels [[(Cheng et al., 2023)]]) The grasp labels see [[(Cheng et al., 2023)#Grasp Labels]]

Use *Zero-shot* strategy to validate the generality:
> If the model performs well on a dataset without having seen any images from it, then it is likely to generalize well.
## Method
![[WildHands Framework.png]]

**Hand Encoder**: Crops the image to 224 x 224 and process it with [[ResNet]]50 backbone -> 7 x 7 x 2048. Pooling to get global features.
**KPE (Intrinsics-Aware Positional Encoder)** See [[KPE#Sparse KPE]], zhe resulting encoding is of 5 x 4 x K. 5 means 4 corners and 1 center; 4 means the sin and cos of $\theta_x, \theta_y$; K is predefined.
**Hand Decoder**: like in [[HMR (Kanazawa et al., 2018)]] but MANO version.
## Experiments
### Datasets
2 in-the-lab datasets: [[ARCTIC (Fan et al., 2023)]] and [[AssemblyHands (Ohkawa et al., 2023)]];
2 in-the-wild datasets: [[Epic-Kitchens]] and [[Ego-Exo4D]].