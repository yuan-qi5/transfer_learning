# Learning both Weights and Connections for Efficient Neural Network

(NIPS 2015 , 8785 citation on Google Scholar by 2025/04/25)

## Background

神经网络既是计算密集型，也是内存密集型，使其很难在嵌入式系统上部署，希望能在不影响精度的前提下减少**内存**与**计算**开销。

为解决该问题，考虑通过学习网络中重要连接，将不重要连接删掉以减少冗余。使用三步方法修剪冗余连接，先训练网络以确定重要连接，再删除不重要连接，最后重新训练网络微调剩余连接权重。

## Method

![prune_method](./picture/prune_method.png)

prune connections 通过删去低于阈值的权重，来将密集网络变为稀疏网络。

接着介绍不同组件对 prune 影响

### Regularization

- 如果不进行 retrain ，L1-regularization 效果更好（因为 L1-regularization 惩罚非零参数使得更多参数接近 0）

- 如果进行 retrain ，L2-regularization 效果更好

- 且整体上，L2-regularization 效果更好

### Dropout Ratio Adjustment 

Dropout 用于阻止 over-fitting，由于剪枝已经降低了模型容量，所以 retraining dropout ratio should be smaller。 

![dropout_ratio](./picture/dropout_ratio.png)

### Local Pruning and Parameter Co-adaptation

- 在 retraining 时，最好加载 initial training 时权重而不是重新初始化

- 由于神经网络易受梯度消失问题（此时 resnet 还未问世 qwq），采用交替冻结，分步重训练，即 retrain FC 时冻结 conv ，剪枝完 FC 后，再冻结 FC 剪枝 conv 

### Iterative Pruning

- 与单步剪枝相比，重复剪枝可在不损失精确度前提下，将剪枝率从 5 倍提高到 9 倍在 AlexNet 上。

- 每次迭代使用 greedy search 能找到最好的连接，尝试过基于参数绝对值的概率性剪枝方法，但这样做效果差。

### Pruning Neurons

- 剪掉部分连接后，若某个神经元的输入连接全为 0 或输出连接全为 0，那这个神经元可以被安全地删除，因此剪枝可进一步扩展为: 把与被减除神经元相连地所有连接也一并删除

- retraining 中会通过梯度下降和正则化自动清理无效神经元，因为若一个神经元若无输入或输出连接，在前向传播时不会对最终损失函数产生任何影响，所以在反传时梯度为 0，此时只有正则化项会调整这些权重从而将其压缩为 0 .

## Experiment

使用 Caffe，在 Lenet-300-100, Lenet-5 on MNIST, AlexNet and VGG-16 on ImageNet 上进行实验

### LeNet on MNIST

剪枝 retrain 时采用原始学习率的 1/10

![Lenet_prune](./picture/Lenet_prune.png)

Act% : 剪枝后非零激活百分比
Weights% : 剪枝后非零权重百分比

### AlexNet on ImageNet  

ImageNet ILSVRC-2012 : 1.2M training examples and 50k validation examples 

剪枝后 rentrain 采用原始网络的 1/100 学习率，再不损失精度情况下参数量是原始的 1/9

![prune_alexnet_imagenet](./picture/prune_alexnet_imagenet.png)

### VGG-16 on ImageNet

数据集使用 ImageNet ILSVRC-2012

剪枝后是原始参数量的 7.5% 

![prune_vgg-16_imagenet](./picture/prune_vgg-16_imagenet.png)

## Discussion

- retrain 对精度很重要，但在一定范围内也能有 “free lunch”（如在剪去一半连接时即使不 retrain 也不会损失精度）

- 剪枝后 (not retrain) L1 正则化优于 L2 正则化，但 retrain 后 L2 的表现优于 L1，因为 L1 正则化已经没有动力再将值推向 0 。

- 可以考虑使用 L1 正则化进行剪枝，再使用 L2 正则化进行训练，但这并不简单地比两个极端都是用 L2 正则化好。因为一种模式参数不能很好地适应另一种模式。

- 剪枝在一定程度上可以略微提高精度，可能是由于修剪找到了网络地正确容量，从而缓解了过拟合。

![trade-off_curve](./picture/trade-off_curve.png)

- 虽然 conv 和 FC 都可以被剪枝，但敏感性不同，可通过敏感性结果来找到每一层最好的阈值。

![prune_sensitivity](./picture/prune_sensitivity.png)

与其他方法比较以及剪枝对参数分布的改变。

![comparision_prune](./picture/comparision_prune.png)

## Question

- 为什么 retrain 能提高精度？

- 为什么剪枝会使参数发生这样的参数改变？

- 除了 cnn 和 fc , lstm、rnn、transformer 等剪枝后效果怎么样？

- 其他剪枝方式？
