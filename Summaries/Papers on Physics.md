## On hand-object
* [[(Zhang et al., 2024)]]
	* Anti-penetration
* [[HOIC (Hu et al., 2024)]]
	* Use RL: calculate the reward by simulating using a physical simulator.
* [[MS-MANO (Xie & Xu et al., 2024)]]
	* Use a Muscular-Skeletal informed MANO model to fit hand motion
* [[Physics-Aware HOI Denoising (Luo et al., 2024)]]
	* Auto-encoder inserting a mapping that learns by supervising with physical losses.
* [[D-Grasp]]
	* Needs a static reference;
	* Generating dynamic motion by simulation
* [[Stability-Driven Contact Reconstruction From Monocular Color Images (Zhao et al., 2022)]]
	* By simulative shaking experiment in a physical engine.
* [[MACS (Shimada et al., 2024)]]
	* Training with one object with multiple masses.
	* More likely to be a motion interpolation, lacks adaptivity.
* [[Physical Interaction: Reconstructing Hand-object Interactions with Physics]]
	* optimizing the contact points.
	* Only slightly corrects the optimization, which is not trivially applicable to generation.
* [[Synthesizing Diverse and Physically Stable Grasps With Arbitrary Hand Structures Using Differentiable Force Closure Estimator]]
	* Use Force Closure constraint
## On human motion
* [[PhysDiff]]
	* Include physical correction in the diffusion process.
* Learned Neural Physics Simulation for Articulated 3D Human Pose Reconstruction
	* A new pipeline for physical simulation.
* Physics-Augmented Autoencoder for 3D Skeleton-Based Gait Recognition
	* Use an auto-encoder to estimate force & torques
* InterDiff: Generating 3D Human-Object Interactions with Physics-Informed Diffusion
	* Generate first, correct with physics after that.
* 3D Human Pose Estimation via Intuitive Physics
	* Estimate pressure from SMPL interacting w/ the environment
	* Encourage CoM to overlap with Centre of Pressure

## Important papers:
* [[GMD| Guided Motion Diffusion for Controllable Human Motion Synthesis]] defines a way to do guidance in a classifier-based manner
	* No re-training needed, we can simply use the original pretrained model.