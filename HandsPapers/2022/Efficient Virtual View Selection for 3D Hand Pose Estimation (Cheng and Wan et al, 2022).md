---
tags:
  - HandPose
  - Depth-based
  - Efficiency
Institute:
  - Chinese Academy of Science
  - Univ of Chinese Academy of Science
  - Alibaba
  - Simon Fraser Univ
  - Google
Corresponding Author:
  - Xiaoming Deng
  - Yinda Zhang
Year: 2022
aliases:
  - "@chengEfficientVirtualView2022"
Publisher: AAAI
---
## Motivation
Existing methods cannot perform well due to **view variation** and **occlusion** of human hands.
ML methods may favour some viewpoints more than the others.

## Method
1. Project the point cloud to uniformly sampled viewpoints;
2. predict confidence for each view
3. fuse the result of top-N confidence from all $M$ candidate views.