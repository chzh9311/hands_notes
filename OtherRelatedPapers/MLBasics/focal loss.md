# Focal loss for dense object detection
$$FL(p_t) = -(1-p_t)^{\gamma}\log(p_t)$$
Focal loss is indeed adding a modulating term $(1-p_t)^\gamma$ to the cross entropy to lower the weight of well-classified classes. 
That means, the larger $p_t$ is, the smaller loss it will get, which indicates better classified classes receive lower attention.
![[Focal Loss.png]]