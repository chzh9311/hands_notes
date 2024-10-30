---
tags:
  - DNN/Mamba
Institute: UCAS, Huawei
Corresponding Author: Yunfan Liu
Code: https://github.com/MzeroMiko/VMamba
Year: "2024"
Publisher: NeurIPS
aliases:
  - "@liuVMambaVisualState2024"
---
# VMamba: Visual State Space Model
## Motivation
Apply [[Mamba]] to vision. 
The main problem is how to model the 2D image context within a 1D model.

Previous trials: [[S4DN|@nguyenS4NDModelingImages2022]] reformulates SSM with convolutional operations, but loses the input-dependence.
## Method
### Architecture
![[VSS vs. Mamba.png]]
From Vanilla to VSS is mostly due to efficiency.
### SS2D
![[Cross-scan.png]]
One input patch undergoes 4 different directions of scans (Cross-Scan), processed by 4 S6 blocks, and merged to get the final output.