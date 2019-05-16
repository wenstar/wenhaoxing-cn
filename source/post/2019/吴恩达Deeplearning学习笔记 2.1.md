```toml
title = "吴恩达Deeplearning学习笔记 2.1"
slug = "05-16-11-45-19"
desc = "吴恩达Deeplearning学习笔记 2.1"
date = "2019-05-16 11:45:19"
update_date = "2019-05-16 11:45:19"
author = "皓星"
thumb = ""
tags = ["学习"]
```

## 2.1 浅层神经网络
第二部分改善DNN，第一周Setting up your ML application的学习笔记。

### train/dev/test sets
- 用train set训练，用dev set寻找超参数，即找到最好的模型/算法等，用test set评估习得模型的精度。
- 在小数据量（万级）时，3/7分或者6/2/2分是经验最优的分割数据集的方法。
- 在大数量级（百万级）时，1%甚至更低的dev和test量级就够了。

### mismatched train/test distribution
- 确保train和test set符合同一分布是必要的。

### bias 和 variance
- 定义base error，（optical error）是问题的基本误差，是学习精度的上限。
- 假设base error很低，train 和 dev set同分布：
    - train set error 和 base error 的差距是bias。
    - train set error 和 dev set error 的差距是variance。
- 训练时的基本步骤：
    - 首先需要降低bias：需要增强学习能力，例如更大的网络，训练更长时间，采用更优算法/网络结构。
    - 在bias符合要求时，降低variance：防止过拟合，例如更多数据，regularization，更改网络结构等。
    - 更多数据对于高bias的情况一般没有什么帮助。
- 机器学习的早期，人们会讨论bias和variance的tradeoff，因为当时没有太多工具可以在降低一方面的时候不影响另一方面。
但是，在大数据和深度学习的今天，我们有工具（更大的网络，更多数据，正则化等）可以在降低bias时不影响variance，或反之，或同时降低两者。
所以，在深度学习领域不太涉及这个tradeoff。一个带有regularization的更大的网络通常表现更好，主要代价是训练时间。

### regularization 正则化
- L2正则化最常用，梯度下降时，正则化项的导数相当于给W额外减去了一个梯度值，也被称为权重衰减（weight decay）。
    - 损失函数L2正则化项： ![](@media/L2loss.gif)