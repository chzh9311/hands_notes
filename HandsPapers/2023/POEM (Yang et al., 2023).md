---
tags:
  - HandMesh
  - Multi-view
Institute:
  - SJTU
  - Shanghai Qi Zhi Institute
Corresponding Author:
  - Cewu Lu
Code: github.com/lixiny/POEM
aliases:
  - "@yangPOEMReconstructingHand2023"
Year: 2023
Publisher: CVPR
---
# POEM: Reconstructing Hand in a Point Embedded Multi-view Stereo
## Motivation

1. Multi-view settings have innate advantages over single-view, and MV devices are developing fast recently (Apple Vision Pro, Google VR ..)
2. How to fuse features:
    1. fuse in 2D is holistic via epipolar;
    2. fuse in 3D-2D projection via features near the 2D points
3. => fuse the above two.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/e4468c5d-ee9c-41d3-90da-e47122fd269e/f9b792eb-dcc6-4ed8-a9b6-bb4416d2940c/image.png)

A set of base points in the intersection of camera FOV.

## Method: 2 stages

$$ P(X, V|I) = P(V|X, I)P(X|I) $$

X is the joint, V is the vertices, I is the images.

### Stage1: X=f(I)

Kps from mv images: use DLT method.

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/e4468c5d-ee9c-41d3-90da-e47122fd269e/85eccd3d-5b78-4584-93dc-5270a9b0b02e/image.png)

### Stage2: V=f(X, I)

1. determine point cloud: M=N(views) x W x H (image size) x D (depth). The coordinate is in (u, v, d) form, that is: (pixel x, pixel y, depth).
2. Determine relative points from the point cloud. Learn a reverse mapping from X to V, and select points nearby.
3. Hand vertices positions are iteratively updated with cross-attention w/ the points around.