---
tags:
  - Hand-Object
  - physics
Institute: Tsinghua Univ.
Corresponding Author: Feng Xu
Code: https://github.com/hu-hy17/HOIC
Year: "2024"
Publisher: SIGGRAPH
---
# Hand-Object Interaction Controller (HOIC): Deep Reinforcement Learning for Reconstructing Interactions with Physics
## Motivation
Physical constraints are introduced for better feasibility, but currently not satisfactory:
1. time-consuming optimization;
2. strong assumption that limits application scheme.
Imitation learning in human motion cannot be directly applied to HOI:
1. More complex: not only the hand motion, but the forces and contacts;
2. traditional simulators uses point contacts, which is not the case in HOI (surface contacts)

## Method
Monocular video stream -> hand pose & object position.
1. Use [[ManipNet (Zhang et al., 2021)]] to estimate hand pose $\mathbf{q}_t$ & object pose $\mathbf{o}_t$ as an initialization
2. Each policy takes the refined frame and future frames as input. $\pi=\{\mathbf{q}_t, \mathbf{o}_t\}$. 
The DRL framework tries to learn the joint torques, and also some compensation forces (that does not exists actually) to help converge.
The PD-controller:
$$\boldsymbol{\tau}_t = k_p\circ(\hat{q}_t-q_t)-k_d\circ\dot{q_t}$$
### Contact model
one contact point is stretched to 5 points, 