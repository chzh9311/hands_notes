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
* [[Spectral Graphormer (Tse et al., 2023)]]
## Representation
* [[Hand Avatar (Chen et al., 2023)]]
* [[Handy (Potamias et al., 2023)]]
* [[PHRIT (Huang and Chen, 2023)]]
* [[gSDF (Chen et al., 2023)]]
## Hand Object
* [[HFL-Net (Lin et al., 2023)]]
* [[CHORD (Li et al., 2023)]]
* [[DHANet (Leng et al., 2023)]]
* [[RUFormer (Xie et al., 2023)]]
* [[In-Hand Scanning (Hampali et al., 2023)]]
* [[DiffHOI (Ye et al., 2023)]]
# New Sensors
## Egocentric
* [[DiffHOI (Ye et al., 2023)]]
* [[EgoPCA (Xu et al., 2023)]]
* [[HTT (Wen et al., 2023)]]
## Tactile Sensor
* [[VTacO (Xu & Yu et al., 2023)]]
## RF-Vision
* [[OCHID-Fi (Zhang & Zheng, 2023)]]
# Synthesis
## Motion Synthesis
* [[Affordance Diffusion (Ye et al., 2023)]]
* [[CAMS (Zheng, Zheng and Fang, 2023)]]
* [[HO-NeRF]]
## Rendering
* [[RelightableHands (Iwase et al., 2023)]]
* [[LiveHand (Mundra et al., 2023)]]
## ImageSynthesis
* [[HandAppearanceRecovery (Zhao et al., 2023)]]
# Motion Prediction
* [[Gesture Prediction from dynamics (Qi et al., 2023)]]
* [[EgoHandTrajPred]]
# Dataset
* [[ARCTIC (Fan et al., 2023)]]
* [[AffordPose (Jian et al., 2023)]]
* [[AssemblyHands (Ohkawa et al., 2023)]]
* [[RenderIH]]
* [[BlurHandNet (Oh & Park et al., 2023)]]
* [[ShowMe (Swamy et al., 2023)]]
* [[HMDO (Xie et al., 2023)]]