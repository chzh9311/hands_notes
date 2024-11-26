---
tags:
  - ImageSynthesis
Institute:
  - Southeast Univ
Corresponding Author:
  - Yangang Wang
Year: 2023
Publisher: CVPR
aliases:
  - "@zhaoSemiSupervisedHandAppearance2023"
Code: https://www.yangangwang.com
---
# Semi-supervised Hand Appearance Recovery via Structure Disentanglement and Dual Adversarial Discrimination
## Motivation
Marker-based MoCap: reliable but appearance not bare; Marker-less: needs an estimator so not reliable.
=> combine them.
## Method
Domains: $A$ => hand images with diverse appearance degradations; $B$ => bare hand appearances
*No sync data considered*
![[Pasted image 20241118165408.png]]
### Structure Disentanglement
$$X\rightarrow \mathbf{t}(X)\rightarrow\mathbf{t}_{[M]}(X)\rightarrow \mathbf{t}_s(X)\rightarrow S(X)$$
1. X-> t(X): via [[DINO-ViT]], extract visual tokens;
2. t(X) -> $t_{[M]}(X)$: use a MLP to regress <u>patch-wise saliency</u>
3. Use edge, depth map, IUV map, & normal map to form a standarised domain $S$ for prior extraction.
4. Use a VAE to establish map-token conversion $S\leftrightarrow t_s$.
5. Use a ViT decoder $\mathcal{E}_s$ for $t_{[M]}(X)\rightarrow t_s(X)$. 
6. Use a set of deconvolution layers $\mathcal{F}$ for extracting $S(X)$, the bare hand structure
### Appearance Wrapping
Use a Dual Adversarial Discrimination (DAD) in semi-supervised scheme, for extracting the hand appearance.