---
tags:
  - HandMesh
  - Representation
Institute:
  - Institut de Robòtica i Informàtica Industrial
  - Meta
Corresponding Author:
  - Lingni Ma
Code: https://www.iri.upc.edu/people/ecorona/lisa/
aliases:
  - "@coronaLISALearningImplicit2022a"
Year: 2022
Publisher: CVPR
---
# LISA: Learning Implicit Shape and Appearance of Hands
## What is a 3D Avatar?
A 3D avatar is one's virtual identity in metaverse. In this work:
> [!Quote] LISA
>  is a **do-it-all** neural model of human hands. It can capture accurate hand shape and appearance, generalize to arbitrary hand subjects, provide dense surface correspondences, be reconstructed from images in the wild, and can be easily animated.

## Motivation
1. [[MANO]] model has a low resolution, cannot model textures.
2. To explore how well implicit representations apply to articulated objects.
## Method
Input: A dataset of multi-view RGB video seq + camera calibrations. 
Goal: Learn a hand model which reconstructs hand geometry, deformation & appearance. -> learn to map from parametric skeleton (MANO) to a hand model of shape & appearance: $$M^+: (\theta, \beta^+, \gamma)\mapsto \psi$$, where $$\psi:(x, d)\mapsto (s, c)$$. It maps the point and direction (like in [[NERF]]) to SDF value $s$ and color $c$. Generally, merging the above we have $$G:(x, \theta, \beta^+, \gamma) \mapsto (s, c)$$ as the learning goal.
### Representation
The model is split by $n_b$ (the number of bones) parts (inspired by [[NASA (Deng et al., 2020)]] & [[Neural parts (Paschalidou et al., 2021)]]). Each MLP make prediction regarding one bone. For each bone, using a standalone MLP to predict its SDF and colour, and use their weighted average as the result.
MLPs can leverage $w$ to avoid learning SDF from far-away points.
### Rendering
Infer the volume density from the SDF:$$\sigma(x) = \alpha \Psi_\beta(-s)$$. $s$ is the signed distance, and $\Psi$ is the CDF of Laplace distribution.