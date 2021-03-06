```toml
title = "吴恩达Deeplearning学习笔记 1.3 and 1.4"
slug = "04-28-15-50-44"
desc = "吴恩达Deeplearning学习笔记 1.3 and 1.4"
date = "2019-04-28 15:50:44"
update_date = "2019-04-28 15:50:44"
author = "皓星"
tags = ["学习"]
```

## 1.3 浅层神经网络
第一部分Neural Network and Deep Learning第三周浅层神经网络的学习笔记。

### 神经网络的表示 representation
- 隐藏层 hidden layer：监督学习中，训练集数据包含输入对应输入层和label对应输出层，其它中间层节点的真正数值在训练集数据中是不知道的。所以命名为隐藏层。 
- 计算网络层数时约定不计算输入层（第0层）。只有一个隐藏层的网络是2层神经网络。

### 激活函数
- tanh 总是比sigmoid更好，相当于一个均值为0，值域(-1, 1)的平移缩放的sigmoid。
- sigmoid 函数的导数在0点最大，为1/4，tanh 的导数在0点最大，为1。
- ReLu是default选择，x为0的导数未定义，实践中定为为0即可，因为实际上x精确为0的概率很小，对计算的影响也很小。x为正，导数为1。没有梯度消失的问题，学习速度更快。

### 初始化
- 对于LR回归，全零初始化是ok的。但是对于神经网络，不能使用全零初始化。如果使用全零初始化，每一层的所有神经元都是对称的，学习的结果也相同，导致不论训练多久，每一层的每个神经元参数都相同。
- 神经网路应该使用随机初始化W，对于b可以使用全0，因为W不同时，就不存在对称问题了。一般倾向于使用很小的（接近0）的W初始值。因为对于Sigmoid或者tanh函数而言，输入值接近0的梯度更大，下降更快。太大的输入值导致梯度饱和。

## 1.4 深层神经网络

- 实现深层神经网络debug的一个重要方法是核对矩阵的维数。
- 课程里的DNN不涉及卷积层，这个也是被面试问到而我不太清楚的部分。（问我CNN和DNN有什么区别。苦笑，这个完全是定义上的文字游戏，但是不知道确实尴尬了。）
此处一个神经元的定义是：一个线性函数加上一个激活函数为一个神经元。一层中有几个线性函数（和激活函数）就有几个神经元。一个LR实际上可以看成是一个神经元。

### 为什么使用深层表示
- 直觉上（intuitively），可以把神经网络的前几层看成是探测简单特征的函数（例如边缘检测），在后面的层把这些特征组合在一起，就可以学习到复杂的函数。
由浅到深也是从简单细节到全体复杂特征的变化（考虑感受野在扩大）。
- 电路（circuit）理论，对于一个窄的L层DNN能够计算的函数，如果需要使用浅网络计算，需要指数倍更多的隐藏神经元。

### 超参数
- 参数例如W、b等，超参数例如学习率、循环次数、隐含层数等，超参数需要手动设置，实际上决定了最终W和b，所以叫超参数。
