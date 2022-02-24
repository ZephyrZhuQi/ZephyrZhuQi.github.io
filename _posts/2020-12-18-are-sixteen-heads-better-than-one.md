---
layout: post
title: Are Sixteen Heads Really Better than One?
categories: Paper Reading
excerpt: The Role of Heads in Transformer
status: visible
---

[NeurIPS 2019](https://arxiv.org/pdf/1905.10650.pdf)


What are the relations between different attention heads? Can they interact?\\
"To allow the different attention heads to interact with each other, transformers apply a non-linear
feed-forward network over the MHA’s output, at each transformer layer (Vaswani et al., 2017)."  (MHA: multi-headed attention)

# 3 Are All Attention Heads Important?
How was the experiment done?\\

"We perform a series of experiments in which we remove one or more attention heads from a given
architecture at test time, and measure the performance difference. We first remove a single attention
head at each time (§3.2) and then remove every head in an entire layer except for one (§3.3)."

We test for statistical significance using the t-test.

"3.3 Ablating All Heads but One" tells us a single head in a certain layer can do the job.

"3.4 Are Important Heads the Same Across Datasets?"

" We use this iterative, heuristic approach to
avoid combinatorial search, which is impractical given the number of heads and the time it takes to
evaluate each model.
5"

# 6 Dynamics of Head Importance during Training\\
"This suggests that the important heads are determined early (but not immediately) during the training
process. The two phases of training are reminiscent of the analysis by Shwartz-Ziv and Tishby (2017),
according to which the training of neural networks decomposes into an “empirical risk minimization”
phase, where the model maximizes the mutual information of its intermediate representations with
the labels, and a “compression” phase where the mutual information with the input is minimized. A
more principled investigation of this phenomenon is left to future work."