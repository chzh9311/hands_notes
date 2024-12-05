---
tags:
  - Hand-Object/Known-object
  - physics
  - Discriminative
Institute:
  - Tsinghua Univ.
  - Shanghai AILab
Corresponding Author:
  - Li Yi
Code: N/A
Year: 2024
Publisher: CVPR
aliases:
  - "@luoPhysicsawareHandobjectInteraction2024"
---
# Physics-aware Hand-object Interaction Denoising
## Motivation
Even the sota trackers will produce obvious errors. It is crucial to increase *physical plausibility*.
Previous works are not doing well:
* [[HOTrack (Chen et al., 2023)]] optimize hand poses by *minimizing low-level penetration and attraction*, but it get stuck in local optima easily.
* [[ContactOpt (Grady et al., 2021)]] & [[Toch (Zhou et al., 2022)]] utilize DNN for pose refinement, but risk overfitting and over-smoothing, and no guarantee that the result is physically aware (?).

## Method
### Problem Formulation
*Known*: 
1. a noisy hand pose trajectory during HO interaction over $T$ frames $\tilde{H} = (\tilde{H}^i)_{1\leq i \leq T}$ where each $\tilde{H}^i\in\mathbb{R}^{K\times 3}$.
2. The object's geometry & dynamic information. $O = (O^i)_{1\leq i\leq T}$ denotes the object vertices.
*Target*: Refine the trajectory to get more plausible result $\hat{H}$.
### Dual-HOI representation
With hand [[MANO]] meshes $H$ and object vertices  $O$ over T frames, the whole HOI representation is $$ F^i = (S^i, \mathcal{T}^i)$$
$S$ represents the 21 keypoints from the vertices. $\mathcal{T}^i=\{\mathcal{C}_j^i\}_{j=1}^N$. $N$ points *randomly sampled* on the object surface in the $i$ th frame, and $\mathcal{C}_j$ represents the corresponding *hand* point of the jth object point from an implicit representation in [[Toch (Zhou et al., 2022)]]. The points are determined by the norm vector of the object point's first hit.
This is what the network refines. Final output is derived by fitting [[MANO]] mesh to the sample points.
![[physics-inference.png]]
### How to denoise?
Use an *auto-encoder*: 
Use [[PointNet]] to process the [[Toch (Zhou et al., 2022)]] field $\mathcal{T}$ to a **global object feature** -> concat with the hand centric part $S^i$ to form the HOI frame feature $x^i$ -> process with RNN -> the refined representation $\hat{F}$.
### Training
Stage 1. $$ \mathcal{L}_I = \alpha_T\mathcal{L}_T(\hat{\mathcal{T}}, \mathcal{T}_{GT}) + \alpha_S\mathcal{L}_S(\hat{S}, S_{GT})$$
$S$ and $\mathcal{T}$ are the two different parts.
![[physics-train.png]]
Stage II: Plug a mapping layer $\phi$ (MLP w/ residual) between encoder and decoder. The loss of this stage contains 4 parts:
1. $\mathcal{L}_{grasp}$ the grasp credibility loss.
2. $\mathcal{L}_{manip}$ the manipulation feasibility loss.
3. velocity regulation
4. loss from the first stage.
#### The grasp credibility
>[!quote]
>While many recent works, such as [13], [10] and [4], focus on mitigating hand-object penetration during hand pose estimation, they tend to be helpless when dealing with deep penetration cases where the hand penetrates through the object completely instead of just entering the object surface, which are common when dealing with thin and delicate object parts.

The method utilizes penetration depth (PD)
![[Pasted image 20241009140738.png]]
This metrics is only calculated for points with small shifts.
#### The manipulation feasiblility
1. Force Error (FE) : the possible friction vs.  $m(-g + a)$. But is only binary, indicating whether the move is feasible.
2. Manipulation Expense (ME): The minimum force needed to accomplish this acceleration.

## Experiments
### Datasets
* [[GRAB]]
* [[HO3D]]
### Metrics
* MPJPE
* IV (Intersection Volume)
* Penetration Depth
* Contact IoU
* Plausible Rate: an overall metric. PD < 1.5cm (following [[ManipNet (Zhang et al., 2021)]]) & FE < 0.1
#### Ablations
![[Pasted image 20241009145535.png]]
$L_{manip}$ actually lowers the MPJPE but encourages the hand to contact the object.