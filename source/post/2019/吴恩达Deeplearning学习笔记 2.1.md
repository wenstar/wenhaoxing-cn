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

### regularization 正则化方法
- L2正则化最常用，梯度下降时，正则化项的导数相当于给W额外减去了一个梯度值，也被称为权重衰减（weight decay）。
    - 损失函数L2正则化项(Frobenuis norm here)，l代表第l层的参数： ![](@media/L2loss.gif)
    - 权重衰减：![](@media/weight_decay.gif)
- dropout 之后除以keep-prob使得该层输出期望值不变（inverted dropout）
- dropout 能work的原因：
    - 减小网络结构，用类似正则化的方法避免过拟合
    - 使一个神经元不能依赖任何一个特征（任何一个输入都有可能被drop），从而要分散权重，产生了类似L2正则的效果。
- 不同层可以使用不同的keep-prob，对于复杂的大层，过拟合的可能性强，keep-prob可以设置的低一点。简单测小层，可以设置的高一些。
- dropout目的是防止过拟合。对于视觉问题，输入的像素很多，数据相对不足，过拟合问题严重，所以普遍使用dropout，但是对于其它领域，应当在发生了过拟合后再考虑dropout。
- dropout的一个缺点是导致没有明确良好定义的cost函数，每次迭代都随机失活一些神经元，所以梯度下降是很难进行复查的。
明确良好定义的cost函数应当再每一轮梯度下降迭代中下降，但是dropout使此不可能。一个debug方法是关闭dropout，确保cost降低后再打开。
- 数据增强（data augmentation）扩充数据可以防过拟合。包括：翻转，裁剪，放大，旋转等。
对于数字等，还可以扭曲，旋转。
- 早停（early stopping）观测dev set误差，在dev set error不再下降时停止迭代。
如果认为训练过程中W的参数值是从小（接近0）到大的过程，早停的效果也和L2正则化类似。
早停的缺点是不能独立地降低bias和降低variance，早停后bias也不再降低了。

### normalizing inputs 输入归一化
- 零均值（减去均值），归一化方差（除以方差）。用同样的均值和方差处理train和test set，不要单独计算。
- 如果输入特征的不同维度处于不同的范围（scales）且相差较大，则cost函数会细长狭窄，梯度下降速度较慢。
- 如果输入特征的不同维度本身的范围就相当，则归一化作用可能不是很大。但是输入归一化总没有什么坏处，所以是一般的处理方法。
   