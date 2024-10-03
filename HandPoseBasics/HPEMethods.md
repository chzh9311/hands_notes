# Hand Pose Estimation Methods

## Applications

* Virtual Reality

* Augmented Reality

* Mixed Reality

* Human-Computer Interaction

## Methods

### Non-parametric model

$$
Joints = Model(Image)
$$

## MANO

Take the hand vertices from SMPL as the template.

### Data Collection

1. Scan the hands;

2. Manually separate the arms and hands

3. Automatically segment out the objects as they are painted green.

![8342abb6-d2a4-4928-9b08-9548e5e589f7](file:///E:/Dropbox/TechNotes/Figures/8342abb6-d2a4-4928-9b08-9548e5e589f7.png)

### Model Alignment (Registration)

A repeated minimization process:

![3784e8dc-1978-4fb0-94a4-a4eae4dbaddc](file:///E:/Dropbox/TechNotes/Figures/3784e8dc-1978-4fb0-94a4-a4eae4dbaddc.png)

where $\mathbf{V}$ is the registration, and $\mathbf{S}$ is the scan. Note that $\mathbf{V}$ is not the model, but independent vertices that are optimized to fit the model. This enables the registrations to faithfully suit the hands.

### The model

MANO contains:

* 15 joints + 1 global orientation

* 

The model is mostly identical to SMPL, except:

1. The pose blend shapes $B_P$ relies more on the local joints.

2. The zero pose is a flat hand, far from the mean pose.
   
   1. When computing the zero pose, the template take into account the pose blend shapes between mean pose and zero pose.
   
   2. Extreme poses are assigned lower weights ($w=d^{-2}$) in order to avoid unnatural knuckles.

3. Symmetry is attained by creating right hands from right and mirrored left hands, and then mirror them all to create left hands.

4. Use neutral poses for shape space.

## Model


