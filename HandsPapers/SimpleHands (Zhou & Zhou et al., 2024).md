---
tags:
  - HandMesh
  - LightWeight
Institute: Jiiov Technology
Corresponding Author: Jiajun Liang
Code: http://simplehand.github.io
Year: "2024"
Publisher: CVPR
---
# A Simple Baseline for Efficient Hand Mesh Reconstruction (CVPR 2024)

## Main Idea
The mesh decoder could be decoded into two main components:
* **Token generator**. Prior Information + image features -> Task specific features
	* [[FastMETRO (Cho et al., 2022)]]: Weak-perspective; [[MobRecon (Chen et al., 2022)]]: stacked encoding. [[PointHMR (Kim & Gwon et al., 2023)]] sample features from 3D -> 2D.
	* The key is **to sample discriminating and representative points**.
* **Mesh regressor**.
	* [[FastMETRO (Cho et al., 2022)]]: [[Mesh-Graphormer (Lin et al., 2021)]]
	* The key is to **upsample sparse keypoints into dense meshes**.
## Method
### Token Generator
With an image of ${H, W}$, the backbone extracts features $X_b\in H/32 \times W/32 \times C$. Then a token generator $T$ takes $X_b$ as input and produces tokenized mesh feature $X_m\in N\times C$, $N$ is the number of sampled points. This process is 
$$
	X_m=T(X_b).
$$
**Tokenizer**: 
* A single spatial pooling is already competitive:
![[Pasted image 20241002151924.png]]
* Further, changing this to grid sampling results in better performance, but keypoint-guided point sampling as in [[MobRecon (Chen et al., 2022)]] does not increase.
* 7x7 is too low, upsample to 14 x 14 and 28 x 28 helps.
* **Conclusion**: keypoint-guided point sampling at an appropriate resolution is a crucial structure for the token generator. while feature enhancement & exhaustive point sampling are not.
**Mesh regressor**
The mesh regressor is a series of decoder layers:
$$
	R = H_kH_{k-1}\dots H_0
$$
Each layer consists of a *dimensional reduce layer*, a *metaformer*, and upsample layer:
$$
	H_k(X_k) = U_k(MF_k(P_k(X_k)))
$$
The upsample and dimension reduce layers are MLPs. 
Because spatial information is important, the paper adds a positional embedding param $emb_k$ to the output tensor $X_k$:
$$
	X_k = X_k + emb_k
$$
**Framework Design**
![[Pasted image 20241002205403.png]]
The sample is keypoint guided sampling
**Loss Functions**
![[Pasted image 20241002205755.png]]
Use the 2D joints $J_{2d}$ and 3D vertices $V_{3D}$ to guide the training. The 3D joints are calculated using matrix $J$: $J_{3d}=J\times V_{3d}$. 
![[Pasted image 20241002210339.png]]
As 2D keypoints are only used for token generation, they are weighted lighter than the others. $w_{3d}, w_{2d}, w_{vert}$ are 10, 1, 10 respectively.

## Experiments
HRNet and FastViT-MA36 are used as backbones for non-real-time and real-time methods.
### Results on [[FreiHand (Zimmermann et al., 2019)]]
![[Pasted image 20241002210854.png]]
The Params means those not including the backbone. These methods are all **transformer-based**.
### Results on [[DexYCB (Chao et al., 2021)]]
![[Pasted image 20241002211048.png]]
## Limitations
The challenges in previous work still exists.