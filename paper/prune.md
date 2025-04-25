# Learning both Weights and Connections for Efficient Neural Network

(NIPS 2015 , 8785 citation on Google Scholar by 2025/04/25)

## Background

神经网络即是计算密集型，也是内存密集型，使其很难在嵌入式系统上部署，希望能在不影响精度的前提下减少内存与计算开销。

为解决该问题，考虑通过学习网络中重要连接，将不重要连接删掉以减少冗余。使用三步方法修剪冗余连接，先训练网络以确定重要连接，再删除不重要连接，最后重新训练网络微调剩余连接权重。

## Method

![prune_method](./pictures/prune_method.png)

prune connections 通过删去低于阈值的权重，来将密集网络变为稀疏网络。

接着介绍不同组件对 prune 影响

### Re


## Experiment




