---
layout: post
title: Deformable DETR
categories: Paper Reading
excerpt: Deformable DETR
status: visible
---

生成初始的采样点位置：
<img src="/images/reset_param.png" alt="ELF Header" width="1000"/>

在这里，将注意力权重与value进行weighted sum的实现是调用了用CUDA来实现的版本，因为Pytorch版性能比较差，不过我们也可以看看Pytorch的实现，了解其中的逻辑。

<img src="/images/msda.png" alt="ELF Header" width="1000"/>

以下就是基于采样点位置插值出对应的采样特征(value)：

<img src="/images/msda1.png" alt="ELF Header" width="1000"/>

最后就是将注意力权重和采样特征进行weighted sum：

<img src="/images/msda2.png" alt="ELF Header" width="1000"/>

以Pytorch为例，总的来说需要实现3个文件，setup.py负责运行编译流程；xxx.cpp，这是C++函数声明以及负责绑定CUDA Kernel函数部分；xxx_cuda.cu，这是真正实现你设计的某个算子操作。而这里面又包括真正运算的kernel函数，以及负责输入转换检查之类的launcher函数。

https://blog.csdn.net/qq_34488063/article/details/52162454
threadIdx，blockIdx, blockDim, gridDim之间的区别与联系
