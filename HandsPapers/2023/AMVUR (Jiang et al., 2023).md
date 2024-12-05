---
tags:
  - HandMesh
  - DNN/Transformer
  - ProbabilisticModel
  - Model-free
  - Discriminative
Institute:
  - Lancaster Univ
  - Oxford Univ
Corresponding Author:
  - Bryan M. Williams
Year: 2023
Publisher: CVPR
Code: https://github.com/ZhehengJiangLancaster/AMVUR
aliases:
  - "@jiangProbabilisticAttentionModel2023"
---
# A Probabilistic Attention Model with Occlusion-aware Texture Regression for 3D Hand Reconstruction from a Single RGB Image
## Motivation
* Model-based methods can capture priors, but are limited to model space;
* Model-free methods address the above problem, but cannot capture dependencies;
=> combine them by relaxing the solution space of  [[MANO]] .
+ Textures are important => a new method for occlusion-aware texture regression.
## Method
Input: 2D image $I$
Output: 2D hand joints + 3D hand joints + 3D mesh vertices + camera params.
MANO is modelled in a prior-net.
According to the following DAG, we model MANO & AMVUR as the production of conditional probabilities, and supervise them to be close to each other.
![[Pasted image 20241111101002.png]]
Assume AMVUR $Q(V_{3D}|I; \phi)$ and MANO $P(V_{3D}|I; \delta)$ are Gaussian distributions $N_{\phi}(\mu_\phi, diag(\sigma_\phi))$, $N_{v}(\mu_v, diag(\sigma_v))$, learnt from their respective models =>
$$\mathcal{L}_{3D}=-\ln Q(V_{3D}|I; \phi) + \ln\frac{ Q(V_{3D}|I; \phi)}{P(V_{3D}|I; \delta)} = \ln Q(V^{GT}_{3D}|I;\phi) + D_{KL}[Q||P]$$
> [!Caution]
> This equation in the paper is problematic. KL divergence is actually $D_{KL}(Q||P) = Q\log (Q/P)$. The above derivation is more likely to be designed so, i.e., the second term is designed to be a KL divergence to penalize the difference between the distributions.

The rest losses are all calculated in the same way: - Probability + KL-divergence.
### Weakly-supervised setting
Treat J3D, V3D and C as hidden variables and only supervise with J2D. (see the graph above). The inference is also done by KL-divergence. $$\mathcal{L} = -\ln P(J_{2D}|J_{3D}, V_{3D}, C, I;\delta) + D_{KL}[Q||P]$$
## Exp
obvious in both supervised and weakly-supervised.