---
tags:
  - Hand-Object
  - Contact
  - non-rigid
Institute:
  - Southeast Univ
Corresponding Author:
  - Yangang Wang
aliases:
  - "@xieNonrigidObjectContact2023"
Year: 2023
Publisher: ICCV
---
# Nonrigid Object Contact Estimation With Regional Unwrapping Transformer
## Motivation
* Current contact estimation methods are difficult to apply to nonrigid objects;
* hard to store contact in a feature-aligned space.
## Method
Input:
* RGB image;
* object mesh template.
Output:
* Contact areas of hand-object pair;
* Object deformation.
### Representations
Hands: [[MANO]];
Object: 6D pose;
They are then transformed to regional unwrapping profiles (RUPs from @zhaoSUPPLEExtractingHand2021). 
![[Pasted image 20241107144917.png]]
### Procedure
1. Surface initialization with [[StabilityDriven Contact|@zhaoStabilityDrivenContactReconstruction2022]]. 
2. Unwrapping: Unwrap the 16 parts and the object as RUPs => $$R(\theta, \varphi) = \arg\min_{\rho}\{s(\rho)|s\in(\vec{O_iR}\cap\partial S)\}$$. Which means iterate the $\theta, \varphi$ of the sphere coordinates, the value is the length to the first intersection with the surface. The centres are inside the hand parts, then we have the intersection maps of the hand (hand-RUP), nearest object surface (object-RUP), farthest object surface (object-f-RUP).
	1. Note that Initial surfaces include some intersections, that's why both near & far object RUPs are needed.
3. crop image patches regarding MANO joints;
4. RUFormer Encoder: Predict 16 parts' contact maps both on hands & objects & deform degrees;
5. RUFormer Decoder: Predict a deformation graph in @sumnerEmbeddedDeformationShape2007 

## Experiments
1. [[HMDO (Xie et al., 2023)]]
2. [[HO3D]]
3. [[FPHB]]
4. [[ContactPose]]