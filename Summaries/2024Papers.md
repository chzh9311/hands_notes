# RGBD-based Hand Pose & Shape Estimation 
## Hand Pose
* [[HandDAGT (Cheng et al., 2024)]]
	* CL: occlusion
	* SLN 
		* local-geometry with super-points
		* GCN + Transformer
## Hand Mesh
* [[MLPHand (Yang & Li et al., 2024)]]
	* CL: Efficiency of MV Reconstruction methods
	* SLN 
		* bone-wise mesh;
		* xyz channel separation.
	* Model-free; 
* [[(Zhang et al., 2024)]]
	* CL
		* weakly-supervised -> implausibility
		* 2D uncertainty
	* SLN
		* Apply anatomy constraints;
		* point -> Gaussian
	* Model-based
* [[SimpleHands (Zhou & Zhou et al., 2024)]]
	* CL: Simple baseline
	* SLN: Estimator = Token Generator + Mesh regressor
	* Model-free
* [[HandBooster (Xu et al., 2024)]]
	* CL: Generate realistic images & annotations
	* SLN: Synthesize w/ GT mesh as condition.
	* Model-based
* [[HHMR (Li et al., 2024)]]
	* CL: All-In-One Generation Framework
	* SLN: Concat Different Conditions and randomly mask.
	* Model-free
* [[MS-MANO (Xie & Xu et al., 2024)]]
	* CL: Implausibility
	* SLN: Use MuscularSkeletal Model.
	* Model-based
* [[HaMeR (Pavlakos et al., 2024)]]
	* CL: Accuracy
	* SLN: big data + big model
	* Model-based
* [[Hamba (Dong and Chharia et al., 2024)]]
	* CL: 
		* Accuracy;
		* Mamba in Vision is not working well.
	* SLN: Combine Mamba with GCN.
	* Model-based
## Hand & Object
* [[HORSE (Prakash et al., 2024)]]
	* CL: Hand-held object
		* lack of data -> self-supervised
		* cannot predict novel-object in the wild
	* SLN: Combine MV supervision w/ shape priors.
* [[C2F-SDF (Liu & Ren et al., 2024)]]
	* CL: Efficiency in implicit representation
	* SLN: C2F w/ PIFu & heatmap-based MarchingCubes
* [[D-SCo (Fu et al., 2024)]]
	* CL: Hand-held object
		* Centroid unstable -> implausibility
		* only on image features -> occlusions
	* SLN:
		* centroid-fixed diffusion
		* semantic (use MANO for occluded points) + geometric
	* generative
* [[NL2Contact (Zhang et al., 2024)]]
	* NT: NL-guided HO contact modelling
	* SLN: NL -> contact -> pose
	* generative
* [[G-HOP (Ye et al., 2024)]]
	* CL: category-level H-O generation
	* SLN: represent hand as distance field -> unify with object SDF.
* [[HOISDF (Qi et al., 2024)]]
	* MV: Implicit representations should be better than explicit
	* SLN: Aggregate point features around surface
* [[HOLD (Fan et al., 2024)]]
	* CL: Object-agnostic HO Reconstruction
	* SLN: 
		* SfM -> Object
		* NeRF -> model H-O in rays and render back
* [[Physics-Aware HOI Denoising (Luo et al., 2024)]]
	* CL: plausibility
	* SLN: 
		* Use physical losses to refine hoi pose.
* [[HOIC (Hu et al., 2024)]]
	* Model hand-object w/ Deep RL.
# New sensors
## Egocentric
* [[WildHands (Prakash et al., 2024)]];
	* CL: Generalization in the wild for Egocentric
	* SLN: 
		* bbox position matters;
		* 3D supervision in the lab + 2D supervision in the wild
* [[HOI-Synth (Leonardi et al., 2024)]];
	* CL: HO Detection in Egocentric
* [[Egocentric Benchmark (Fan, Ohkawa, and Yang et al., 2024)]]
* [[S2DHand (Liu et al., 2024)]]
	* CL: Single-view to Dual-view adaptation
	* SLN: Generate pseudo-label with multiple-views
## Event camera
* @park3DHandSequence
* @jiangComplementingEventStreams2024
# Image/Motion Synthesize
* [[AttentionHand (Park et al., 2024)]];
	* CL: In-the-wild data generation for hand mesh
	* SLN: Generate in-the-wild images with mesh
* [[CoSHAND (Sudhakar et al., 2024)]]
	* NT: Image + desired hand mask => generate the image after the motion
	* SLN: Use Diffusion
* [[InterHandGen (Lee et al., 2024)|@leeInterHandGenTwoHandInteraction2024]]
	* CL: Generate two-hand 
		* Complex space
	* SLN: p(left, right) = p(right)p(left|right)
* [[HOIDiffusion (Zhang and Fu, 2024)]]
	* CL: generate realistic images for HO
	* SLN: Diffusion + Rendering
* @zhouGEARSLocalGeometryaware2024
* [[Text2HOI]]
	* CL: Generate H-O based on text
	* SLN: contact -> pose + refine
# Motion Prediction
* [[HandDGP (Valassakis and Garcia-Hernando, 2024)]]
* @tangPromptingFutureDriven
# Dataset
* [[BOTH2Hands (Zhang et al., 2024)|BOTH57M]]
* [[HOGraspNet (Cho et al., 2024)]]
%% # Robotics
* @sheLearningCrosshandPolicies %%