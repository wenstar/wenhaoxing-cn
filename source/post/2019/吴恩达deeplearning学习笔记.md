```toml
title = "吴恩达Deeplearning学习笔记 1.1 and 1.2"
slug = "04-24-15-13-05"
desc = "吴恩达Deeplearning学习笔记 1.1 and 1.2"
date = "2019-04-24 15:13:05"
update_date = "2019-04-24 15:13:05"
author = "皓星"
tags = ["学习"]
```

# Neural Network and Deep Learning
来自[deeplearning.ai的课程](https://www.deeplearning.ai/deep-learning-specialization/)，共五个部分。其中第一部分分为五周的课程。
这里是第一个部分Neural Network and Deep Learning第一周深度学习概论和第二周神经网络基础的学习笔记。Neural Network and Deep Learning，主要还是入门和概念介绍为主，比较简单。

最近找实习的过程中，觉得自己还是需要系统的学习更多关于深度学习的内容，找到这个课程，希望能有所帮助。

### 什么是神经网络，监督学习
- 神经元Neural：一个非线性函数就可以是一个single神经元。多个神经元组合得到网络。
- 不同的数据/应用领域使用不容的神经网络类型。CNN for 视觉，RNN for 一维序列输入，标准神经网络 for 预测房价。
- 更好的广告推荐系统等输入结构化数据的神经网络也有很大的价值。

### 为什么神经网络学习会兴起
- 传统学习算法在（带标签）数据较少时随数据量增大而精度提高，但是数据量足够大时精度提高存在上限。不能很好地利用海量数据。
随着神经网络规模扩大，精度上限就会很高，高于其它学习算法，但是需要很大的数据，和长时间训练。
- 数据大量积累，计算能力硬件上升，神经网络的优势凸显。（数据量少时，各种学习算法精度优势不确定，有时取决于设计者）
- 算法创新也很重要，很多算法创新使神经网路运行得更快。（sigmoid函数很多区域梯度趋近于0，学习速度很慢，RELU梯度下降更快）
- 数据，计算能力和算法的进步决定了深度学习的兴起。

### Binary Classification, Logistic Regression and Loss Function
- 每条训练数据x按照视为列向量，按列堆叠成矩阵X，n行m列，则有m条数据，每条数据n维。这样比按行向量堆叠简单。Y对应是1*m的向量。
- 线性模型的输出不是一个概率，所以使用sigmoid函数，sigmoid的输出是从0到1的平滑曲线。
- LR回归中平方误差损失函数是非凸的，梯度下降可能找到局部最优。（均方误差MSE指向最小二乘法）
- 一般使用交叉熵损失函数（根据《统计学习方法》，根据最大似然估计推导得到）

### 梯度下降 Gradient Desent
- 对于LR而言，交叉熵损失函数是凸函数，所以初始值无所谓，一般取0。
- 梯度下降的证明：[使用泰勒展开证明梯度下降法合理性](https://blog.csdn.net/weixin_42278173/article/details/81511646)

### 计算图
- 一切复杂的计算都可以分解成计算图，计算图的每个节点都是最简单的运算。
- 通过计算图和链式法则，可以简单地实现反向传播。
- 向量化的实现（使用np，而不是for loop来计算每一个参数）可以使用numpy提供的内置函数，利用SIMD并行加速运算（百倍加速度量级）。

### 广播 broadcasting
- 针对numpy，可以让向量与实数相加，矩阵与向量相除等。python会自动展开（复制）维度不足的数字到维度相同，进行加减乘除操作。
- 为了bug free，不要使用shape为(5,)的一维数组，它和其转置完全相同，会导致问题。使用shape为(5，1)的列向量（或行向量）。

### 几率与概率
- 几率是![](http://chart.googleapis.com/chart?cht=tx&chl=\\frac{p}{1-p})，与概率不同。
LR回归中，sigmoid函数视为p，求几率,得![](http://chart.googleapis.com/chart?cht=tx&chl=\\frac{1}{e^{-x}}={e^x})，取对数，得x。

