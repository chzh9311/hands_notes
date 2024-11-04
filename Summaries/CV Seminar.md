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