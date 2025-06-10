## Related papers
1. [[GraspDiff (Zuo et al.)]]: Use a stable diffusion model to do generation.
	Contact -> Pose: contact used as the condition via cross-attention;
	Refine: Use RefineNet 3 times (same as [[GRAB]])
2. [[InterHandGen (Lee et al., 2024)]]: Use diffusion to generate both hands; The object point cloud is used as the condition.
3. [[ContactGen]]: 
4. [[GraspTTA (Jiang et al. 2021)]]: Use a CVAE to generate hand pose, a ContactNet (Including two PointNetEnc and a Conv Decoder) to predict contact map, 
	Contact -> Pose: Use a Test-Time-Adaptation

