---
tags:
  - Egocentric
  - Hand-Object
  - HandPose
Institute: ETH, MPI, Meta, etc.
Corresponding Author: Jiajun Liang, Otmar Hilliges, Hyung Jin Chang, etc.
Year: "2024"
Publisher: ECCV
---
# Benchmarks and Challenges in Pose Estimation for Egocentric Hand Interactions with Objects (ECCV'24)
## Basics
* [[High DoF Visual Tracking (Rehg and Kanade, 1994)]]
## Challenges
* High DoFs;
* Ambiguous texture;
* heavy occlusions.
## Contributions
* A sota baseline 
* A thorough analysis on 3D hand(-object) reconstruction tasks.
## Methods for [[AssemblyHands (Ohkawa et al., 2023)]]
> [!info]
> AssemblyHands is mainly a Pose Estimation Dataset. The major metrics is MPJPE.

* ResNet50 + 2.5D representations ([[2.5D Representation (Iqbal et al., 2018)]]). This is the baseline that is proposed by this paper;
* [[SimpleHands (Zhou & Zhou et al., 2024)]]. An existing simple baseline for MLP.
* PICO-AI. Based on RegNet320 [[RegNet (Radosavovic et al., 2020)]]
* Phi-AI. A method that adapts [[MinimalHand (Zhou et al., 2020)]] + ResNet50 backbone
* FRDC: regression + heatmap. [[HandOccNet (Park et al., 2022)]].
![[Pasted image 20240929111752.png]]
## Methods for [[ARCTIC (Fan et al., 2023)]]

> [!info]
> ARCTIC is mainly focused on HO contact, and the major metrics is Contact Deviation (CDev).

* [[ARCTIC (Fan et al., 2023)|ArcticNet-SF]]. A single-frame baseline.
* [[JointTransformer (Zeid 2023)]]. Ehances ArcticNet-SF by replacing MLP with transformer decoder.
* [[WildHands (Prakash et al., 2024)]]. 
* UVHand. Uses [[Swin-L Transformer]] & [[Deformable DETR (Zhu et al., 2021)]]
* [[DIGIT (Fan et al., 2021)]]. Uses HRNet-W32 backbone.
## Experiments
### Datasets
* [[AssemblyHands (Ohkawa et al., 2023)]]
![[Pasted image 20240929160209.png]]
The two rows are in one line originally, split up due to page width limit. Each row, the 3 red colored blocks are the highest ones, and blue blocks are the lowest ones.
* [[ARCTIC (Fan et al., 2023)]]
![[Pasted image 20240929160410.png]]

![[Pasted image 20240929161031.png]]
## Future work
* Multi-view egocentric cameras;
* Leveraging 3D foundation priors to regularize template-free hand-object reconstruction.
* More expressive representations;
* Motion + temporal modelling
* Diverse egocentric interacting scenarios;
* Action recognition from captured hand poses;
* Learning robotic grasping from HO pose sequences.