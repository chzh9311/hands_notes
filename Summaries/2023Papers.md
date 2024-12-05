# RGBD-based Hand Pose & Shape Estimation
## Hand Pose
* [[A2J-Transformer (Jiang et al., 2023)]]
	* CL: Occlusions
	* SLN: enable local + global regressor
* [[Cross-Domain 3D Hand Pose Estimation with Dual Modalities (Lin & Yang, 2023)]]
	* Depth maps for domain adaptation
* [[NVFHand (Huang et al., 2023)]]
	* NVF for hand pose estimation
* [[HaMuCo (Zheng et al., 2023)]]
	* CL: MV supervise mono
	* SLN: collaborative learning w/ cross-view feature & consistency 
* [[HandR2N2 (Cheng et al., 2023)]]
	* Use stacked refine structure to suit the model for different scales
* [[Deformer (Fu et al., 2023)]]
	* CL: occlusions & blur
	* SLN: predict motions forward & backward
## Hand Mesh
* [[ACR (Yu et al., 2023)]]
	* CL: Complexity in two-hand scene vs. constraints of inputs
	* SLN: 
		* part-based representation. Separate two hands
		* cross-attention
* [[AMVUR (Jiang et al., 2023)]]
	* Model-based + model-free via Probability Dist
* [[H2ONet (Xu et al., 2023)]]
	* Lightweight & occlusion-aware HMR
* [[HARP (Karunratanakul et al., 2023)]]
	* Personalized reconstruction for mono input
* [[FreqHand (Luan et al., 2023)]]
	* Decompose hand shape in frequency domain;
* [[Im2Hands (Lee et al., 2023)]]
	* Implicit model for two hands
* [[MeMaHand (Wang & Zhu et al., 2023)]]
	* Model-based + model-free via cross-attention
* [[Accuracy & Plausibility in HMR (Yu et al., 2023]]
	* Model-based + model-free
* [[POEM (Yang et al., 2023)]]
	* MV HMR by points around w/ features
* [[Spectral Graphormer (Tse et al., 2023)]]
	* Two hand HMR by spectral clustered part features.
## Representation
* [[Hand Avatar (Chen et al., 2023)]]
	* High-reso MANO + textures
* [[Handy (Potamias et al., 2023)]]
	* MANO-like param model from a more diverse dataset
* [[PHRIT (Huang and Chen, 2023) 1]]
	* paramer-controllable SDFs
* [[gSDF (Chen et al., 2023)]]
	* Use all joint positions to predict an SDF.
## Hand Object
* [[HFL-Net (Lin et al., 2023) 1]]
	* CL: Hands & Objects are competitive in feature learning
	* SLN: Use separate, but not totally separate networks.
* [[CHORD (Li et al., 2023)]]
	* CL: Category-level object agnostic HOR
	* SLN: Use a shape template to deform to the object in the category
* [[DHANet (Leng et al., 2023)]]
	* HOR in hyperbolic space
* [[RUFormer (Xie et al., 2023)]]
	* Use RUP to capture deformation of objects in HOR
* [[In-Hand Scanning (Hampali et al., 2023)]]
* [[DDF-HO]]
* [[HOTrack|Tracking and Reconstructing Hand Object Interactions from Point Cloud Sequences in the Wild]]
# New Sensors
## Egocentric
* [[DiffHOI (Ye et al., 2023)]]
	* Use Diffusion to guide the HOI reconstruction.
* [[EgoPCA (Xu et al., 2023)]]
* [[HTT (Wen et al., 2023)]]
	* Action Recognition + Pose estimation
## Tactile Sensor
* [[VTacO (Xu & Yu et al., 2023)]]
## RF-Vision
* [[OCHID-Fi (Zhang & Zheng, 2023)]]
# Synthesis
## Motion Synthesis
* [[Affordance Diffusion (Ye et al., 2023)]]
	* CL: Generate hand based on image input
	* SLN: A C2F process
		* Where to interact
		* How to interact
* [[CAMS (Zheng, Zheng and Fang, 2023)]]
	* A standard representation for HO generation, suitable for articulated objects.
* [[HO-NeRF]]
	* CL: Hard to do NVS only with sparse views
	* SLN
		* fit to predefined hand model
		* encourage contact
## Rendering
* [[RelightableHands (Iwase et al., 2023)]]
* [[LiveHand (Mundra et al., 2023)]]
## ImageSynthesis
* [[HandAppearanceRecovery (Zhao et al., 2023)]]
	* Marker-based -> Marker-less
# Motion Prediction
* [[Gesture Prediction from dynamics (Qi et al., 2023)]]
	* 
* [[EgoHandTrajPred]]
# Dataset
* [[ARCTIC (Fan et al., 2023)]]
	* Hands & Articulated Objects
* [[AffordPose (Jian et al., 2023)]]
	* Object Affordance
* [[AssemblyHands (Ohkawa et al., 2023)]]
* [[RenderIH]]
* [[BlurHandNet (Oh & Park et al., 2023)]]
* [[ShowMe (Swamy et al., 2023)]]
* [[HMDO (Xie et al., 2023)]]