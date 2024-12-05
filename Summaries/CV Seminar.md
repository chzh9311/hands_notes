# CV Seminars
## Not All Language Model Features Are Linear
Presented by Han Hu

* Linear representation hypothesis: words are (high-dim) vectors.
	* King - man + woman = Queen
	* small - middle - large => on a line.
**Linear** means 1-D. Some features are of high-D
**Nonlinear features**: e.g. Monday - Sunday. -> *Circular feature*

## Graph Diffusion Transformer
Task: inverse molecules design: design drug molecule with specific properties.
**Limitations of diffusion on graph data**: treat nodes and edges independently.
**Graph Diffusion Transformer** (Graph DiT): 

# NIPS'24 Accepted Papers
### How to find multi-dim representations?
$$Task \overset{LLM}{\rightarrow} hidden state \overset{autoencoder}{\rightarrow}\overset{PCA}{\rightarrow} features$$

* ALS: Adaptive Layer Sparsity for LLM
* No Free Lunch Theorem
	* There's a lower bound for running time $$T_{A, F} \geq f(n)$$
* Bit2Bit: 1-Bit Quanta Video Reconstruction 
* Neural Model Checking

## Real-time 3D-aware portrait generation.
1. Efficient Geometry-aware 3D GAN
2. Input image directly
3. Downstream tasks

## Constrained and Layer-wise Training of NN
by *Dr. Tiffany Vlaar* from U of Glasgow
1. As model size up, the performance up
2. only pretrain part may degrade the performance
3. Dataset labels have bias
SGD -> SGLD -> Langevin Dynamics framework.
SGD-MCMC (Noci et al., Nips 2021)
### Param regularization
Better training 
Each step, project it back to the constraint manifold. (hard constraints)

### Layer-wise partitioning
Related papers:
* Different layers are more data-hungry
* Are all layers created equal?
* Training BatchNorm and Only BatchNorm
	* $\beta$ & $\gamma$ , <1% but important for performance.
* Sharpness-Aware Minimization (SAM)
**Flat minimums tend to perform better**.

### Multirate (fast and slow changing weight)
Set the final layers fast and the pretrained parts slow.


## Defense capability of LLMs
*Stop generating harmful info* #jailbreakAttack 
A new dataset to judge jailbreak attacks: **JailJUDGE**
multi-agent judger
dataset: https://github.com/usail-hkust/Jailjudge

## C2C: Component-to-Composition Learning for Zero-Shot Compositional Action Recognition.
Open a door + Close a book => close a door.
Something to something #Dataset 

## Atomic Inference
Challenges:
1. what are atomic inferences

Segment a NL inference hypothesis into spans
Each span are encoded separately 
> [!note] Max
> Max is a logical operator.

| Sentence label | Cont. spans | Neutral span |
| -------------- | ----------- | ------------ |
| Contradition   | >=1         | Unknown      |
| Neutral        | None        | >=1          |
| Entailment     | None        | None         |
### Interpretable
Decompose the premise to facts.
Blog: [Creating Interpretable Models with Atomic Inference - Marek Rei](https://www.marekrei.com/blog/creating-interpretable-models-with-atomic-inference/)

### DomainAdapt
1. Debiasing: we can only debias one kind of bias. (When and Why Does Bias Mitigation work?)