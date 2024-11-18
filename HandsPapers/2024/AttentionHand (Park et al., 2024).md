---
tags:
  - ImageSynthesis
  - HandMesh
Institute:
  - Sogang Univ.
Corresponding Author:
  - Suk-Ju Kang
Code: https://github.com/redorangeyellowy/AttentionHand
Year: 2024
Publisher: ECCV
---
# AttentionHand: Text-driven Controllable Hand Image Generation for 3D Hand Reconstruction in the Wild
## Motivation
1. In-the-wild data are scarce and expensive to label;
2. Synthetic datasets are unnatural.
AttentionHand can generate images with only four modalities: an RGB image, hand mesh image, bounding box, text.
## Method
1. Use [[CLIP]] to get text embedding.