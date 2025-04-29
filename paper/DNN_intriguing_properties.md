# Intriguing properties of neural networks

## Induction

这篇论文介绍了 DNN 的两个反直觉性质 ：

- 通过不同方式的单元分析，作者发现 individual high level units 和 random linear combinations of high level units 没有区别，即在神经网络的高层包含语义信息的是空间，而不是单个单元

  - 先前工作通过找到最能激活给定单元的输入集来分析各种单元的语义，但这暗含了高层神经元构成了一个 “极好的基底” (distinguished basis)，能够很好地提取语义信息

- 作者发现 DNN 学习的 input-output mappings 在很大程度上是不连续的，可在图像通过最大化网络预测误差进行扰动，来使网络对图像进行错误分类，且相同的扰动会导致在同一数据集的不同子集上训练的不同网络对相同的输入进行错误分类

  - 将通过优化输入以最大化预测误差找到的扰动样本称为 “对抗性样本” (adversarial examples)

## Framework





## Conclusion
