# Datasets on 3D Human Hands

![1633980a-2568-4b48-a901-41a6a675971f](file:///E:/Dropbox/TechNotes/Figures/1633980a-2568-4b48-a901-41a6a675971f.png)

> From Survey of Deep Learning Based Hand Pose Estimation

## Metrics

* CDev (Contact Deviation, Introduced by ARCTIC): For a given frame, $\{(\mathbf{h}_i, \mathbf{o}_i)\}_{i=1}^C$ are $C$ pairs of in-contact (< 3mm) hand-object vertices according to GT, and $\{(\hat{\mathbf{h}}_i, \hat{\mathbf{o}}_i)\}_{i=1}^C$ are the predictions. Then 
  
  $$
  \text{CDev} = \frac{1}{C}\sum_{i=1}^C\|\hat{\mathbf{h}}_i - \hat{\mathbf{o}}_i\|.
  $$
  
  
