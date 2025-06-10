## Pytorch3D
[facebookresearch/pytorch3d: PyTorch3D is FAIR's library of reusable components for deep learning with 3D data](https://github.com/facebookresearch/pytorch3d)
### Q&A
Q: `gcc: error trying to exec 'cc1plus' : execvp: No such file or directory`.
A: Install `g++` of the same version as `gcc`. e.g., `gcc-9` is installed, then `g++-9` should be also installed.

Q: `/usr/include/linux/types.h:12:27: error: expected initializer before ‘__s128’`.
A: According to [Ubuntu23.10系统配置PointNeXt运行环境（OpenPoints）教程-CSDN博客](https://blog.csdn.net/weixin_45413193/article/details/136723799). It might be the problem of incompatible versions. Try updating the pytorch3D to the newest version.

![[Pasted image 20250610112325.png]]