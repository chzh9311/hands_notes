---
tags:
  - Hand-Object/Object-in-hand
  - weakly-supervised
  - "#Discriminative"
Institute:
  - UIUC
Corresponding Author:
  - Saurabh Gupta
Code: https://github.com/ap229997/wild-hoi/
Year: 2024
Publisher: ECCV
---
# 3D Reconstruction of Objects in Hands without Real World 3D Supervision
## Motivation
Problem: *single image* hand-held object reconstruction.
1. Lack of 3D supervision in-the-wild is a major challenge
2. Past works [[Learning R of HO (Hasson, et al., 2019)]], [[H2O]], [[iHOI (Ye et al., 2022)]] cannot predict novel objects in-the-wild
3. We have:
	1. in-the-wild videos with multiple views of hand-held objects;
	2. large catalogues of 3D object shapes
	which can serve as supervision
There is an assumption:
> [!assumption]
> Hand pose relative to the object is constant during manipulation of rigid objects.

## Method
Following [[iHOI (Ye et al., 2022)]], use implicit shape representations (Occupancy & SDF).
### 2D mask guided 3D sampling
Goal: Sample points for training SDF / Occupancy
If a point is inside the mask at all views, then this point is considered inside the object.
=> Occupancy labels $M\in \{0, 1\}$.
**For camera poses**: Utilize [[FrankMocap]] to register hand pose in different views; according to the assumption above, we can get the object pose.
**Balanced sampling**: Use projection like above to sample points.
Use CE to train this $\mathcal{F}$.

### Shape prior
Train a discriminator $\mathcal{D}$ to discriminate object from shapes from [[ObMan]]
The discriminator sees different randomly sampled 2D slides that helps to distinguish different objects.

## Training
Train $\mathcal{F}$ and $\mathcal{D}$ alternatively

## Constructing Wild Object dataset
Labelling 3D objects in [[Epic-Kitchens|VISOR]] to construct such a dataset.

## Experiments
### Train
Use [[ObMan]], [[Epic-Kitchens|VISOR]], [[HO3D]], [[HOI4D]] for training and [[MOW]], [[HO3D]] for evaluation.
On MOW, the results are 
![[Pasted image 20241011152449.png]]
## Limitations
1. Inaccurate hand pose (based on FrankMocap)
2. Limited object views. The views do not cover 360$\degree$ of the object.