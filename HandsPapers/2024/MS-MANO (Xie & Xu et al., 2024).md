---
tags:
  - HandMesh
  - physics
  - "#Model-based"
  - "#Discriminative"
Institute:
  - Southeast Univ, SJTU
Corresponding Author:
  - Zhenjun Yu, Cewu Lu
Code: https://github.com/panoanx/ms-mano-unity
Year: 2024
Publisher: CVPR
---
# MS-MANO: Enabling Hand Pose Tracking with Biomechanical Constraints
MS: musculoskeletal
## Motivation
Existing hand models often produce unnatural motions, and a musculoskeletal system emulates the *dynamics* of muscles and tendons so the hand movement will be realistic.

Previous methods [[BASH]] & [[Rcare world (Ye et al., 2022)]] focus on full-body motions and do not model hands.

## Method
The hand is modelled with a [[Hill-type model (Hill, 1938)]]
![[Hill-type model.png]]
Each muscle (the red line in (b)) is controlled by: 1. contractile element (CE); 2. parallel elastic element (PEE); 3. serial elastic element (SEE).
The torque for a joint is:
$$ \tau_m = f(F, x)\left\|(q-j)\times\frac{s_c}{\|s_c\|}\right\|$$
> where F is the contractile force, x is the muscle state, q is the point where the muscle is attached to the bone, j is the joint to apply torque on, and $s_c$ is the muscle segment. Refer to [[Rcare world (Ye et al., 2022)]] for details
### map muscles to joints
1. Use [[MyoHand (Caggiano et al., 2022)]] model to map joint names to [[MANO]] model
2. Convert the displacement of a joint to a MyoHand bone to the displacement to MANO joint.
## BioPR
1. Video sequence -- off-the-shelf pose estimation algorithm --> predicted poses.
2. Calculate the velocity at time $t$ => $v_t$.
3. Use IDNet (inverse dynamics network) to estimate the excitation signals
4. Forward dynamics to get reference pose and velocity.
5. Use a small MLP to produce a refined pose. $p^{refined} = \mathcal{M}(p^{pred}, p^{ref})$ and use GT to supervise this.
![[BioPR.png]]
## Experiments
Manually designed methods like [[TOCH (Zhou et al., 2022)]] may not fully capture the dynamics.
