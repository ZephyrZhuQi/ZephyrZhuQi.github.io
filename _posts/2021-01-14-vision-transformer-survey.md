---
layout: post
title: "Transformers in Vision: A Survey"
categories: Paper Reading
excerpt: Transformers in Vision
status: visible
---

# 简介
## Success factors of Transformers
1. self-attention: expressivity

    对于长距离依赖的编码，增加了模型的表达能力。假定最少的归纳偏置。
2. self-supervision: generalization

    对于问题结构最小化先验知识,增加了模型的泛化能力。

## Applications of Transformers in vision

1. recognition
    1. image classification
    2. object detection
    3. action recognition
    4. segmentation
2. generative modeling
3. multi-modal tasks
    1. visual-question answering
    2. visual reasoning
    3. visual grounding
4. video processing
5. low-level vision
6. 3D analysis

# 基础知识
## 自监督学习SSL（一种学习范式paradigm）
1. 一种基本的思想是**填空**。
2. 另一种Framework：对比学习（contrastive learning），例如MoCo、SimCLR、MoCo V2。通过将数据分别与正例样本和负例样本在特征空间进行对比，来学习样本的特征表示。Contrastive Methods主要的难点在于如何构造正负样本。

PS: 很多研究者认为，深度学习的本质就是做两件事情：Representation Learning（表示学习）和 Inductive Bias Learning（归纳偏好学习）。

## Self-Attention
**Question**: The main difference of self-attention with convolution operation is that the weights are dynamically calculated instead of static weights (that stay the same for any input) as in the case of convolution. 

**Question**: Note that, different from regular convolutional networks where feature aggregation and feature transformation are simultaneously performed (e.g., with a convolution layer followed by a non- linearity), these two steps are decoupled in the Transformer model i.e., self-attention layer only performs aggregation while the feed-forward layer performs transformation. 

# 视觉中的Transformer
## Image Recognition

卷积网络：平移等变性（translation equivariance）
CNN编码先验知识（归纳偏置例如平移等变性）。

### ViT
ViT：Vision Transformer，号称16x16个单词顶一张图（An Image is Worth 16x16 Words）
- 化难为易。把图片拆分成16*16个patches，每个patch做一次线性变换降维后再送入Transformer，避免像素级attention运算。
- 大道至简。降维后的向量直接送入Transformer，最大限度保留Transformer纯正的味道。
- 暴力美学。舍弃了CNN的归纳偏好之后（inductive biases  such as translation equivariance and locality），反而更加有利于在超大规模数据上学习知识，即大规模训练胜于归纳偏好（large scale training trumps inductive bias），在众多图像分类任务上直逼SOTA。

把image patch之后再每个patch做一次linear projection，这恰恰就是convolution。

### DeiT
此外，我们介绍了特定于transformers的师生策略。它依靠蒸馏token确保学生通过注意力向老师学习。我们展示了这种基于token的蒸馏的attention，尤其是在使用卷积网络作为教师时。这使我们能够报告与卷积网络相比在Imagenet（我们可以获得高达84.4％的准确性）和迁移到其他任务时具有竞争力的结果。

## Object Detection

### DETR
事实上，文章所做的工作，就是将transformers运用到了object detection领域，取代了现在的模型需要手工设计的工作（例如 非极大值抑制 和 anchor generation），并且取得了不错的结果。在object detection上DETR准确率和运行时间上和Faster RCNN相当；将模型generalize到panoptic segmentation[3]任务上，DETR表现甚至还超过了其他的baseline.

第一个是用transformer的encoder-decoder架构一次性生成所有box prediction。其中是一个事先设定的、比远远大于image中object个数的一个整数；第二个是设计了bipartite matching loss，基于预测的boxes和ground truth boxes的二分图匹配计算loss的大小，从而使得预测的box的位置和类别更接近于ground truth.

Object queries有  个（其中  是一个事先设定的、比远远大于image中object个数的一个整数），输入Transformer Decoder后分别得到  个decoder output embedding，经过FFN（后面会讲）处理后就得到了  个预测的boxes和这些boxes的类别。具体实现上，object queries是  个learnable embedding，训练刚开始时可以随机初始化。在训练过程中，因为需要生成不同的boxes，object queries会被迫使变得不同来反映位置信息，所以也可以称为learnt positional encoding （注意和encoder中讲的position encoding区分，不是一个东西）。

此外，和原始的Transformer[4]不同的是，DETR的Transformer Decoder是一次性处理全部的object queries，即一次性输出全部的predictions；而不像原始的Transformer是auto-regressive的，从左到右一个词一个词地输出。

### Deformable - DETR
DETR的缺陷是小物体检测比较困难，收敛得很慢，计算代价相对来说也比较高。平方级别的复杂度也限制了DETR不能使用multi-scale的层级特征，这个层级特征对检测小物体是有效的。
由deformable卷积启发，deformable DETR提出deformable attention。

Deformable DETR提出的Deformable Attention可以可以缓解DETR的收敛速度慢和复杂度高的问题。同时结合了deformable convolution的稀疏空间采样能力和transformer的关系建模能力。Deformable Attention可以考虑小的采样位置集作为一个pre-filter突出所有feature map的关键特征，并且可以自然地扩展到融合多尺度特征，并且Multi-scale Deformable Attention本身就可以在多尺度特征图之间进行交换信息，不需要FPN操作。

而Deformable DETR的Deformable Attention只关注参考点周围的一小部分关键采样点，为每个query分配少量固定数量的key，可以缓解收敛性和输入分辨率受限制的问题。



