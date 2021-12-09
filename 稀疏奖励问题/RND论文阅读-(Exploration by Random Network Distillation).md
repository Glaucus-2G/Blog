# RND论文阅读-(Exploration by Random Network Distillation)

## motivation

好奇心机制的一种新实现，前面的工作设计的intrinsic reward，有基于动力学模型预测误差的好奇心机制ICM，也有基于各种信息增益的VIME。

这种方式设计的初衷是基于对状态访问的计数(count-based)来定义intrinsic reward，而由于是高维连续空间，因此这个计数更多的是密度估计。如果访问到的状态次数较少，则对应的intrinsic reward值就更多，反之亦然。

## methods

本文利用了两个不同随机参数的网络，一个更新(predictor)  $\hat{f}: \mathcal{O}\rightarrow \mathbb{R}^k$，一个不更新(target)$f: \mathcal{O}\rightarrow \mathbb{R}^k$。target网络有个前提是对于不同的原始输入，其输出也不同，也就是简历observation到R之间的一一映射关系。因为predictor会进行更新，所以当同样的observation作为predictor输入时，利用MES $||\hat{f}(x;\theta) - f(x)||^2$即可计算差异性。

其实目的就在于，当我的predictor的输入数据被访问以及训练后，新输入的observation对应的$\hat{f}$和$f$之间的差异就会变小，说明当前状态已经访问过，随着次数的增多，则奖励会越来越小。因此当智能体遇到新状态时，会获得更多的intrinsic reward，从而鼓励其去访问更新的状态。



