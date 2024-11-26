---
tags:
  - ImageSynthesis
  - Hand-Object
Institute:
  - Columbia University
Corresponding Author:
  - Richard Zemel
Year: 2024
Publisher: ECCV
aliases:
  - "@sudhakarControllingWorldSleight"
---
# Controlling the World by the Sleight of Hand
A novel task
> [!quote]
> Given an image, and the shape/location of a desired hand interaction, CoSHAND, synthesizes an image of a future after the interaction has occurred.
## Motivation
1. Easy-to-acquire modalities are not enough. How to enable machines to imagine interactions?
2. with the shape & location of hands

## Method
use diffusion to find such a function:
$$f(x_t, h_t, h_{t+1}) = x_{t+1}$$
where $x$ is the image and $h$ is the binary hand mask.
Exp proves that using hand masks produces much better results than no condition or text condition 