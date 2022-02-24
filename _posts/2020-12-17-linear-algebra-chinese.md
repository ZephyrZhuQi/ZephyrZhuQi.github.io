---
layout: post
title: 大学教的线性代数与MIT18.06视频课的区别：
status: visible
---

大学教的线性代数与MIT18.06视频课的区别：

2017年春季学期，我大一下，修读了使用西北工业大学教材的线性代数课程，虽然最后接近满分，却没有学会什么东西，在后期学习机器学习、阅读论文时成为了一个巨大的短板，比如对基本的vector space, rank, matrix decomposition没有直观的想象。
2020年冬天，三年多过去了，我终于下定决心好好学一下这门课，于是打开了MIT18.06多年前录制的视频，很多东西虽然没有弹幕里说的那样醍醐灌顶、神乎其神，但是也呈现了原本学校老师教的不同面貌。这篇文章总结一下两种教法的不同，也是我自己日后复习、给别人讲解的参考，希望大家也能获得一些总结的知识。
在下文中，用NPU来指代我们学校的教法，用MIT来指代麻省理工的教法。

一、引入的方式

MIT的引入方式是从问题出发，一个线性方程组的解有什么几何解释？并且给出了三种不同的角度来解释方程组的解：行的角度、列的角度、矩阵的角度。行的角度就是我们熟知的，每一行是一个可能的线或者平面，所有行的解就是线或者平面的交点。列的角度是MIT教授偏爱的，我们需要求出合适的对于列向量的线性组合。矩阵的角度就是简单的矩阵写法了。
列的角度也可以用来解释矩阵乘法，矩阵A乘以向量x就等于用x的每一项作为系数，给A的列作线性组合，即，Ax是A的列向量的线性组合，这个看法是比较新鲜有趣的；而常规的以A的行为单位进行点乘早已为人熟知。
（在引入的第一讲就讲到，线性代数的根本问题是解决n个方程n个未知数的方程组）
与之相反，NPU的引入方式是先上来行列式，并且兜头就来了二元一次方程组的解的公式(用二阶行列式来表示)。由此开始的整个第一章都非常反人类，看起来非常痛苦而且看不懂，包括各种奇怪而且当头一棒的知识点，例如逆序数、余子式、Cramer法则等等。这中间的motivation以及intuition严重缺失，只是一味堆积公式。
在MIT的第18讲(课程过半)，才开始介绍行列式。之后才有代数余子式(cofactor)以及克拉默法则。并且一开始就说了讲行列式的原因：求特征值(The big reason we need the determinants is for Eigen values.)
教授说他绝对不会先给复杂公式：“我一股脑儿给你们一个复杂的关于行列式的式子？不行，复杂的式子包含太多信息了。”(Do I give you a big formula for the determinant, all in one gulp? I don’t think so! That big formula has got too much packed in it.)
所以老师先从行列式的性质介绍。性质三告诉我们行列式是一个线性函数(每一行的线性性linear for each row)。讲了整整一节课性质之后，才开始介绍公式。关于克莱默法则，教授说这个公式算起来非常麻烦，比消元法更低效，Matlab会用消元来计算方程组，而不是克莱默法则。

二、实用软件的介绍

MIT的Gilbert教授总是会提到，这个算法，在Matlab中是怎么用的、甚至，在Matlab中是怎么实现的。而我们的教材、作业以及考试完全以做题为导向，根本不用碰软件、也不用写一行代码。例如，行最简式在Matlab中就是用rref来表示的。讲到上三角行列式是对角线元素相乘时，也说到任何科学计算软件例如Matlab就是用这种方法来算的，(In fact, the way computers find the determinants of large matrices is to first perform elimination (keeping track of whether the number of row exchanges is odd or even) and then multiply the pivots)。

三、关于消元

MIT的课程中，教授开心的带着大家一起消消乐，让原矩阵变成上三角矩阵U，在这个过程中自然的告诉我们什么是主元、什么是主元列、主元不能为0，否则需要进行行交换、什么是消元矩阵、什么是置换矩阵(左乘的行交换矩阵或者右乘的列交换矩阵)。并且由消元矩阵自然地引出了逆矩阵的概念。(每一步消元的操作都是可逆的)
(The product of a matrix (3x3) and a column vector (3x1) is a column vector (3x1) that is a linear combination of the columns of the matrix. The product of a row (1x3) and a matrix (3x3) is a row (1x3) that is a linear combination of the rows of the matrix. )
但我们的教材根本不怎么提这回事，也导致我对消元有很不好、不全面的印象，认为太简单太重复太无聊。

四、矩阵乘法

这个小小的概念(NPU教材只有一个定义)，Gilbert教授用了四种方法来解释！点乘、行的线性组合、列的线性组合、列乘以行然后求所有的sum。

五、矩阵A的LU分解

矩阵的LU分解对于理解矩阵的性质非常有帮助。在上述消元的过程中，A变到了上三角矩阵U，这个消元的过程就是一个理解LU分解的方式。EA = U, A = LU = E^(-1)U. E就是一系列消元矩阵相乘的结果。

六、向量空间、子空间

NPU教材的4.4节讲了向量空间，当时为了复习考试我费了巨大的脑力去理解它。当然考完试全部忘光了。在MIT的讲法中，向量空间的引入非常自然，在解方程组的时候我们已经看到了列向量，列向量的线性组合，以及列向量的线性组合是否能表示空间中所有的向量，也就是解是否存在的问题。这时候理解向量空间就非常容易了，就是一个对线性组合这种运算封闭的集合。
关于子空间，这个在NPU的教材是第七章，不考。而MIT的老师告诉了我们，四种子空间非常重要。列空间的意义是，当Ax=b中的b在A的列空间中时，这个方程组是可解的。零空间则是说，所有的x，使Ax=0.
求解零空间，在消元的过程中，不一定要得到上三角的形式，而是得到了一个阶梯形R，由阶梯形，我们可以看出来矩阵的秩是多少：主元(主变量)或者主元列的个数。我们得到了主变量和自由变量，于是给自由变量赋上1、0或者0、1这样的值，回代求解主变量，得到了Ax=0的特解。需要求的特解的个数就是自由变量的个数n-r，也是零空间的维度，因为零空间是这些特解的线性组合。于是我们也得出了Ax=0的解。用行最简阶梯形，可以一眼看出来(-F)。
Gilbert教授说，四个子空间是线性代数的核心内容(This is really the heart of this approach to linear algebra)。why?矩阵的子空间可以用来干什么？后面讲到的话，补上来。
四个子空间：列空间C(A)、零空间N(A)、行空间R(A)=C(A转置)、A转置的零空间(左零空间)。

七、方程组的解

求解Ax=b的问题：Ax=b有解的条件是，b在A的列空间中。
Ax=b的通解是一个特解加上零空间的所有向量。求特解的方法是，将所有的自由变量设为0，求出主变量。
矩阵的秩非常重要，告诉了我们关于解的个数的所有信息。(The rank tells you everything about the number of solutions.)满秩矩阵有很多种：列满秩、行满秩、行列满秩，这些矩阵的解呈现不同的特点。
两种教法最大的区别就是MIT会更强调直观、具体的解释，是为了让人明白。就像教授说的：I can give you the abstract definition, and I will, but I would also like to give you the direct meaning.(我会给你抽象的定义，也会给你具体的解释)

八、知识的连贯与融合

这一特点在线性相关、基、维度这一讲特别明显(第九讲)。矩阵A的列向量线性无关，等价于矩阵A的零空间只有零向量，所有的列都是主元列，矩阵A的秩为n(列的个数)，矩阵中没有自由变量。A的秩r=主元列的个数=A的列空间的维度。A的零空间的维度=自由变量的个数=n-r.Ax=0的特解就是零空间的基。
向量空间的基告诉了我们关于向量空间的所有信息。(The basis of a space tells us everything we need to know about that space. )
R^n空间中的n个向量构成一组基，等价于这n个向量是一个可逆矩阵的列向量。(In general, n vectors in R^n form a basis if they are the column vectors of an invertible matrix. )
老师提供了一些思维的扩展：向量空间不一定由向量组成，矩阵也可以组成向量空间，微分方程的解也可以是向量空间，只要他们满足加法和数乘的封闭性。线性微分方程的一个重要内容就是寻找解空间中的一组基。
秩为1的矩阵可以分解成一个列向量与一个行向量点乘的形式：A=UV^T.这种矩阵行列式很简单，特征值很有意思，就像搭建其他矩阵的积木。
第11讲开始介绍了图论和线性代数的关系，介绍了小世界图(六度分离原理)。

九、线性代数的应用

一个重要的应用就是图论。例如电路图，在电路中如何使用线性代数呢？我们可以用Incidence Matrix(关联矩阵)A来表示节点之间边的关系，行表示每一条边，列表示每一个节点，在这一行，-1表示由该列节点出发，1表示到达该列节点，其他节点的位置都是0。可以观察到，电路中的回路，在矩阵中呈现线性相关。
求解A的零空间，Ax=0，如果x是节点电势，Ax是描述每条边电势差的向量。解得x1 = x2 = x3 = x4，零空间的维度是1，例子中的图是5行(边的个数)4列(节点的个数)，秩为3(节点个数-1)。求解A的左零空间，左零空间的维度是m-r，即为回路的个数，# loops = # edges − (# nodes − 1)，得到连接图的欧拉公式：number of nodes − number of edges + number of loops = 1. 。
矩阵A告诉我们电势差的信息。A^Ty=0得到满足基尔霍夫电流定律的电流y。A的转置的零空间中的向量就是满足基尔霍夫定律的电流。
A的行空间。
欧拉公式，任何图都有的拓扑性质。


线性代数的基本定理表明四个基本子空间之间的关系。第一部分关于子空间的维度。第二部分是关于他们的正交性。第三部分是关于它们的正交基。

矩阵的行空间正交于零空间，列空间正交于左零空间。

十、子空间投影

从介绍子空间开始，我一直在好奇这个东西是用来干嘛的，因为前期在讲维度、正交等等的关系，并没有讲到实际应用。
在投影这一部分，终于看到了应用。子空间投影是为了求线性方程组Ax=b的近似解。如果b不A的列空间中，则求出b在列空间上的投影p。
在三维或者更高维的空间中，求解一个向量到超平面的投影的过程，可以得到正规方程(normal eqation)!同时，也可以看到左零空间和列空间的正交关系！实际应用中，这就是通过最小二乘拟合一条直线。最小二乘法需要用到正规方程(线性回归)。拟合一条直线是统计学中重要的知识，线性回归是统计学中的词汇，outlier也是这里的一个词汇，最小二乘比较容易受到outlier的影响。
有两种看待最小二乘的方式。第一种就是用一条直线去拟合一些点。第二种就是将一个向量(待拟合点)，投影到A的列空间得到拟合点p，投影到左零空间得到误差e，p和e正交。这里用到了子空间的正交性。
证明A^TA可逆的过程，用到了零空间的性质。
标准正交向量组(orthonormal)，由投影的方法，可以很容易的得到格拉姆-施密特标准正交化方法。A=QR.R是上三角矩阵。a1=（a1Tq1)*q1+(a1Tq2)*q2，前一个括号表示a1在q1上的投影，后一个括号表示a1在q2上的投影。

十一、特征值与特征向量。

These eigenvectors span the space. They are perpendicular because B = BT (as we will prove). 
An n by n matrix will have n eigenvalues, and their sum will be the sum of the diagonal entries of the matrix: a11 + a22 + · · · + ann. This sum is the trace of the matrix. 
Symmetric matrices have real eigenvalues. For antisymmetric matrices like Q, for which AT = −A, all eigenvalues are imaginary (λ = bi). 

应用部分，讲到对角化，可以简化运算。也可以用来求解差分方程。
特征值是计算矩阵幂的一种方法。
纯粹的特征值、特征向量方法，都需要n个线性无关的特征向量，否则无法对角化。

十二、矩阵分解

消元法中的LU分解
格拉姆-施密特正交化中的QR分解
奇异值分解


The subject of positive definite matrices brings together what we’ve learned about pivots, determinants and eigenvalues of square matrices. 

酉矩阵 unitary matrices 共轭转置
类似于orthogonal matrices正交矩阵
傅立叶矩阵
quadratic form 二次型
数值计算不再需要若而当型



？、总结

越分析越来气，只能说，有上等的教材和视频课程，为什么要去看垃圾呢？希望后来者可以避开这些坑。
我会继续看视频学下去，也会把新的心得发上来。





