---
n_views:
---
# Bimanual articulated-object manipulation
## Related work

Generally, few works are found. There're works on articulated objects:
* [[CAMS (Zheng, Zheng and Fang, 2023)]]
* [[ARCTIC (Fan et al., 2023)]]
And about bimanual manipulation of one/multiple object(s)
* [[Keypoint Transformer (Hampli et la., 2022]]
* [[ARCTIC (Fan et al., 2023)]]
* [[OakInk2]]
* [[TACO]]
[[ARCTIC (Fan et al., 2023)|ArcticNet-SF]] is the baseline of this problem, but only handles certain kinds of articulated objects.
[[TACO]] is for two-part objects, w/ one hand holding one part, separately.

# Physics-aware manipulation
## State Space Model
e.g.: RLC circuits.
![[Pasted image 20250119161421.png]]
According to voltage properties:
$$
u_1(t) = Ri(t) + Li'(t) + u_2(t);
$$
For a capacitance, there holds:
$$
	i(t) = Cu_C'(t)
$$
Therefore, 
$$
	u_1(t) = CRu_2'(t) + CLu_2''(t) + u_2(t)
$$
The state space model of this framework is:
$$
	\begin{bmatrix}\dot{u}_2\\ \ddot{u}_2\end{bmatrix} = \begin{bmatrix}0 & 1 \\ -\frac{1}{LC} & -\frac{R}{L}\end{bmatrix}\begin{bmatrix}u_2 \\ \dot{u}_2\end{bmatrix} + \begin{bmatrix}0 \\ \frac{1}{LC}\end{bmatrix}u_1 
$$ $$
	u_2 = \begin{bmatrix}1 & 0\end{bmatrix}\begin{bmatrix}u_2 \\ \dot{u}_2\end{bmatrix}
$$
Which makes it in SSM form. 

## For articulated object
The state should be: $x = [\bf{s}, \boldsymbol{\theta}, \varphi]^T$, where $\bf{s}\in\mathbb{R}^3$ is the translational position, $\boldsymbol{\theta}\in\mathbb{R}^3$ is the rotational position, and $\varphi\in\mathbb{R}$ is the articulation angle. The state is $[x, \dot{x}]\in\mathbb{R}^{14}$.  The form is:
$$
	\begin{bmatrix}\dot{x}\\ \ddot{x}\end{bmatrix} = \begin{bmatrix}0 & I \\ A_1 & A_2\end{bmatrix}\begin{bmatrix}x \\ \dot{x}\end{bmatrix} + \begin{bmatrix}0 \\ B\end{bmatrix}F 
$$
![[Pasted image 20250119164648.png]]
Here $A$ & $B$ does not have to be totally precise, they can vary with time.
## RP: How to generate the ideal contact regarding the object & hand?

### Circumstances
The man is operating large objects / articulated object / heavy object, that requires both hands to manipulate.
Currently, focus on general object, then on **articulate objects**.
### Assumptions
1. The object is of even density;
2. Only 1 DoF of articulation (rotate, translate, twist);
3. The object is held steadily, only in contact with hands.
4. **The objective**: humans always look for the most efficient way of doing a manipulation -> the sum of the force values should be the objective.

**Some details**:
1. the object surface fraction ratio is set empirically to $\mu=0.7$;
2. 
### Known variables:
* **Articulated Object shape**: $M_o = (\{M_i\}_{i=1,2}, T)$,
	* $M_i=\{V, F\}$ is the articulated parts;
	* $T$ is the allowed relative transformations between the two parts.
	* Also know the CoM of each part $O_i$ (by [Assumption#1]. )
* **Evenly sampled points from the object surface**: $P_o\in\mathbb{R}^{N\times 3}$;
* **Normal directions of each point**: $n_i\in\mathbb{R}^3$
* **Refence Contact Map**: $C_{ref}\in\mathbb{R}^{N}$.
* **A relative transformation indicator** $\alpha\in\mathbb{R}$ that indicates the transformation of the object. (Could be replaced by text prompt).
### Unknown variables:
* **Target contact map**: $C_{target}\in\mathbb{R}^N$;
* **The contact force** of each contact point.
### The objective function (From [assumption#4])
$$f(\mathcal{F}) = \sum_{i=1}^NF_i$$ where $F_i\in\mathbb{R}^+$ is the value of contact force.
### Constraints
1. According to Newton's Law, if the object is stably held ([Assumption#3]), then:
$$\sum_{i=1}^M{\bar{F}_i} + mg = ma; \quad\sum_{i=1}^Ml_i\times\bar{F}_i=J\alpha$$
where $\bar{F}_i = N_i + f_i = F_i(n_i + \gamma_i b_i + \beta_i t_i), (\gamma_i, \beta_i\in[-\mu, \mu])$ is a usual way of linearizing friction cones; $\|b_{i}\|, \|t_{i}\| = 1$ are already known as a function of vertex norm.
![[Pasted image 20250129100339.png]]
And $\|a\| \leq \epsilon_a, \|\alpha\|\leq\epsilon_\alpha$  are accelerations that ensemble a shaking experiment.
Assume we have $M$ contact points, then
$$\begin{bmatrix}n_1, n_2, \dots, n_M\end{bmatrix}[F_1, F_2, \dots, F_M]^T +[b_1, b_2, \dots, b_M][\beta_1 F_1, \beta_2 F_2, \dots, \beta_M F_M]^T + [t_1, t_2, \dots, t_M][\gamma_1F_1, \gamma_2F_2, \dots, \gamma_MF_M]^T = m(a-g)$$
Assume $n_i' = l_i\times n_i$, etc., then:
$$\begin{bmatrix}n_1', n_2', \dots, n_M'\end{bmatrix}[F_1, F_2, \dots, F_M]^T + [b_1', b_2', \dots, b_M'][\beta_1 F_1, \beta_2 F_2, \dots, \beta_M F_M]^T + [t_1', t_2', \dots, t_M'][\gamma_1F_1, \gamma_2F_2, \dots, \gamma_MF_M]^T = J\alpha$$
Further,
$$\left(N+B\Lambda_{\beta}+T\Lambda_{\gamma}\right)F=m(a-g)$$ $$(N'+B'\Lambda_\beta+T'\Lambda_\gamma)F=J\alpha$$
That's how we finally get the upper & lower bounds of all rows, because F > 0; 
Say we have the upper bound of Force equation as $U_{F}F = m(a_u - g)$, and lower bound eq: $L_FF=m(a_l-g)$. ($a_u = [\epsilon_a]^3$, $a_l=-a_u$).
Then this becomes a linear programming problem:
$$\min 1^TF, s.t. U_FF\geq a_u-g; L_FF\leq a_l-g; \;U_MF\geq \alpha_u;\; L_MF\leq \alpha_l\;\text{and}\; F_i\geq 0$$
This makes sure the applied force can cover all the acceleration ranges.
1. The holding area constraint.
Once we know the object geometry, we know the possible contact areas as a distribution:$P(C|O)$. Here, only the local geometry is considered, so a diversity of data could be used to train this model.
### How to use this constraint to optimize the model?
According to classifier guidance diffusion, we need the gradient of the classifier to guide the model in diffusion;
![[Pasted image 20250205172951.png]]
However, **the classifier does not necessarily need to be differentiable, as we only need its gradient**. The problem becomes:
We have: 
* $M$ contact points (take only one point from a contact region to represent, so we have more smoothed $n_i$'s).
* $M'$ potential contact points (which means the hand hovers on the object at a small distance).
A solution to the LP problem above;
So what we do is just move all the intersection lines towards the origin.
![[Pasted image 20250205175554.png]]
### Theoretical Analysis
With $P(C|O)$, if we have a stability score $f(C)$, then can we modify $P$ according to $f$, s.t. $$\max\mathbb{E}_{C\sim P'(C|O)}f_O(C)$$
Further, say S=stable, C=contact, O=object, then we know:
* The prior, i.e. $P(C|O)$, done by previous works (via CVAE ([[ContactGen]]), etc.)
* The stability measure (probability): $P(S|C, O)$; ($S={0, 1}$, 1 represents stable, 0 otherwise.)
We want:
$$P(C|S=1, O)=\frac{P(S=1|C, O)P(C|O)}{P(S=1|O)}\propto P(S=1|C,O)P(C|O)$$
In our case, we only want the contact distribution regarding the object, so $P(S=1|O)$ is constant if we eliminate $C$.
So we just need to fit the stability measure.
### How to implement?
2. $P(C|O)$ can work out-of-the-box from previous works;
3. $P(S=1|C,O)$ measures the stability, so we can say $$P(S=1|C,O)=f_S(C,O)$$,which returns continuous value in [0, 1].
4. $P(C_{tar}|O, C_{ref})$ which is easy to get through SMPL priors.
However, we want to sample from $P(C|S=1,O, C_{ref})$, which means we need to multiply the three together. How to implement via diffusion?
**Solutions**:
5. One intuitive way of implementing this is through injecting the PDFs during the sampling process:
	1. Take $N$ samples from the original distribution;
	2. Apply this score function to these samples;
	3. Take the top-k samples as the final output.

## Motivation Q&A
Q: Why not use a physics engine to provide the GT score?
A: 
1. Infinite force combinations. In a grasping with several contact points, the force applied on each point can vary from a certain range, and their relationship to the most acc tolerance could be difficult to find. So, **it's hard to find the most efficient case w/ the least force regarding a fixed acc tolerance.**
2. Even though we find the most efficient way of grasping, it is still not guaranteed that the shaking experiment covers all possible accelerations;
3. The hand robot is different from real hand, so the contact areas are inevitably different.
4.  Datasets usually does not include negative samples.
Q: 
## Future work
### Address data scarcity?
Few dataset focuses on bimanual manipulation, most on one-hand. Is it possible to use one-hand grasping dataset to train a bimanual synthesis model?
5. learning grasping object w/ one-hand, the model learns the relation between hand pose & local object geometry;
6. Infer the grasping area of the other hand w/ stability measure;
7. Apply the pretrained model to synthesize hand.
### Feature space correspondence?
From $N(0, 1)$ to the distribution of hand pose, what kind of correspondence?
Measure plausibility in this latent space?

# Reformulate the idea
## Hypothesis & Support
1. Physical constraints helps improve motion estimation ([[Physics-Aware HOI Denoising (Luo et al., 2024)]], [[Stability-Driven Contact Reconstruction From Monocular Color Images (Zhao et al., 2022)]]);
2. More importantly, physical constraints are useful in motion synthesis ([[MACS (Shimada et al., 2024)]], [[D-Grasp|@christenDGraspPhysicallyPlausible2022]], @liuSynthesizingDiversePhysically2022a, [[PhysDiff]])
=> Most existing works use iterative physics engine to estimate the stability, and integrate the physics engine into the optimization process, which in turn makes it slow.
What do I want?
* A physics-aware module that ensures the generated interaction is stable (or satisfies certain accelerations)
* The least required force for this grasp pose to resist the highest wrench.
## What I have now
The pipeline:
The following is the ContactOpt Pipeline
1. noise hand pose + object pose --(Differentiable SDF calculator)--(SDF to contact map)--> Predicted $C_{pred} = f(SD(H, O))$;
2. Estimated contact map - predicted contact map => $L_{contact} = |C_{est} - C_{pred}|$. 