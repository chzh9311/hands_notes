## Pytorch3D
[facebookresearch/pytorch3d: PyTorch3D is FAIR's library of reusable components for deep learning with 3D data](https://github.com/facebookresearch/pytorch3d)
### Q&A

Q: Where can I find the problem?
A: Scroll up the terminal, and find the red `error` word.
![[Pasted image 20250610112325.png]]
Mostly, it should be 

Q: `gcc: error trying to exec 'cc1plus' : execvp: No such file or directory`.
A: Install `g++` of the same version as `gcc`. e.g., `gcc-9` is installed, then `g++-9` should be also installed.

Q: `/usr/include/linux/types.h:12:27: error: expected initializer before ‘__s128’`.
A: According to [Ubuntu23.10系统配置PointNeXt运行环境（OpenPoints）教程-CSDN博客](https://blog.csdn.net/weixin_45413193/article/details/136723799). It might be the problem of incompatible versions. Try updating the pytorch3D to the newest version.

## 前言

[Pytorch3D](https://github.com/facebookresearch/pytorch3d) 是由 Meta 开发的基于 Pytorch，针对 3D 视觉的 Python 第三方库。它提供了很多方便的功能，诸如旋转表示的转换、点云的匹配等等。由于其易用性和完备性，最近的很多三维视觉的工作都会用到它。Pytorch3D 第一个版本发布于 2020 年 1 月 23 日，彼时的 Pytorch 还只更新到 1.5。如今，已经过去了 5 年多，这个库也在计算机技术飞速的更新迭代下逐渐上了年纪。上次版本更新到 0.7.8 则是在 7 个月前，可以说更新的也不是很频繁。你知道的，**老项目+不频繁更新=屎山**。而屎山代码库的最大问题就在第一步，也就是安装上。

由于笔者就是在做 3D 视觉的研究，自然而然的就免不了在各种虚拟环境中安装。在最开始，笔者所用的 Linux 服务器环境还算干净，所以安装起来倒是没有受什么苦。但是随着研究的进行，需要复现的工作也越来越多，服务器的依赖版本逐渐变得乱糟糟的。再加上我没有做好版本的管理，于是，屎山代码+屎山管理=锟斤拷烫烫烫。我一度花了一个下午调试各种依赖版本，企图复现最开始纯净环境下的成功安装，最终在对齐了 gcc 和 g++ 的版本后终于在漫长的编译之后没有再看见满屏的报错，我成功了。
鉴于 Pytorch3D 虽然开始向屎山发展，但短期内还是没有替代，所以我就打算记录一下我安装过程中遇到的问题以及解决方案。
## 环境与安装
笔者所用的 Linux 是 24.04 LTS，也就是默认背景是皇冠的那个。在这个基础上，使用 anaconda 管理虚拟环境。

参考[官方的安装流程](https://github.com/facebookresearch/pytorch3d/blob/main/INSTALL.md)，我这里把一些重点摘出来：

* PyTorch 版本支持：2.1.0, 2.1.1, 2.1.2, 2.2.0, 2.2.1, 2.2.2, 2.3.0, 2.3.1, 2.4.0 or 2.4.1
	* 笔者在测试的时候发现其实 1.x 也是可以的，只是一定要和 cuda 版本对应上。参考 [Pytorch 的安装指南](https://pytorch.org/get-started/previous-versions/)。
* gcc & g++ $\geq$ 4.9
	* 测试下来发现 gcc & g++ 的版本还需要在 10 以下（不包括 10）。
	
一般来说在安装好 Pytorch + cuda 之后就可以直接安装 PyTorch3D 了。可以用
```shell
pip install "git+https://github.com/facebookresearch/pytorch3d.git@stable"
```
或者如果想安装以前的版本，就把 `stable` 换成 `va.b.c`，比如：
```shell
pip install "git+https://github.com/facebookresearch/pytorch3d.git@v0.7.2"
```

## 报错了…… 怎么办？
授人以鱼不如授人以渔，所以我觉得与其把所有问题都列出来，不如写一下怎么排查错误。

Pytorch3D 包含了一些 C++ 实现的功能，所以需要 gcc 来编译。在出错之前终端上是没有信息的，一旦出错就会把所有的 log 全打印出来，于是重要的信息就淹没在几十页的终端输出里了。

想把信息找出来也很简单，只要往回翻，找到 `error` 字样就可以了。如果你跟我一样用的是 MobaXterm，`error` 还会被自动高亮：



你要说不想一行行找，有没有更简单的方法呢？有的兄弟，有的。只要把终端报错输出到文件里就行。在安装命令后面加上 `> error.txt 2>&1`，例如：
```python
pip install "git+https://github.com/facebookresearch/pytorch3d.git@stable" > error.txt 2>&1
```
那么所有的报错就都会输出到当前目录下 error.txt 这个文件里。只要在这个文件里搜索 `error` 即可。
## 笔者遇到的问题
这里记录一下笔者在安装时遇到的问题，其实都是版本的问题：

**Q1:**
```
RuntimeError:
		The detected CUDA version (xx.x) mismatches the version that was used to compile
		PyTorch (yy.y). Please make sure to use the same CUDA versions.
```

**A1:** 按它说的来换一下版本就好；

**Q2:** ```gcc: error trying to exec 'cc1plus' : execvp: No such file or directory.```

**A2:** 这个问题是因为 gcc 和 g++ 版本不一致，改一下版本让它们一致即可。注意版本要在 4.9 到 10 中间。

**Q3:** ```/usr/include/linux/types.h:12:27: error: expected initializer before ‘__s128’```

**A3:** 这个问题笔者是在安装低版本 (0.7.2) 的 Pytorch3D 时遇见的，是因为 linux 新版本的头文件定义发生了变化，要么换版本低一些的 ubuntu 服务器，要么更新 Pytorch3D 到最新版，参考 [Ubuntu23.10系统配置PointNeXt运行环境（OpenPoints）教程](https://blog.csdn.net/weixin_45413193/article/details/136723799)。个人当然更推荐后者，测试下来最新版本没有出现报错的情况。毕竟现在更新都讲究向后兼容，复现的时候跟原代码库要求的版本对不太上也是 OK 的。