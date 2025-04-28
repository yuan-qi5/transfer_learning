# Deep Neural Networks are Easily Fooled: High Confidence Predictions for Unrecognizable Images

## Induction 

**question** : 鉴于 DNN 在视觉分类上已经实现了人类水平性能，那计算机域人类视觉之间还存在哪些差异？

**related work** : [Intriguing properties of neural networks][1] 可以通过一种人类无法察觉的方式改变图像从而使 DNN 将图像标记为其他东西。

**author related result** : 很容易产生人类完全无法识别的图像，但可以使 DNN 相信其是 99.99% 的可识别图像。


**main result** :

- 可通过进化算法或梯度下降生成卷积网络给出高预测分数但人类无法识别的图像

- 对于 MNIST DNNs，通过重训练 DNNs 失其能将 fooling images 分类为 negative examples ，也可以产生一批新的 fooling images 来欺骗这些新网络 

- 引发了一个问题：DNN 在面对不同于训练和测试时用的图像时，整体表现如何？

> fooling images :  人眼无法识别，但 DNNs 几乎肯定地认为是熟悉物体的图像

![fool_images](./picture/fool_images.png)

[1]:https://github.com/yuan-qi5/transfer_learning/blob/main/paper/DNN_intriguing_properties.md

##



## Question

- fooling images 是否可无限迭代？

- 基于此工作有没有人尝试开发新的 benchmark？

