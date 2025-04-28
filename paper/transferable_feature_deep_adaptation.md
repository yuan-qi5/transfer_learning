# Learning Transferable Features with Deep Adaptation Networks

## Induction



## Related work

motivated by "[How transferable are features in deep neural networks][1]"

[1]:https://github.com/yuan-qi5/transfer_learning/blob/main/paper/transferable_feature.md

对标模型 ：

- DDC
  - 在 deep CNN 上增加了 adaptation layer 和 dataset shift loss 去学习 domain-invariant representation 
  - 只适用于单层网络，导致多层中隐藏特征不可迁移
  - 受概率分布的次优核匹配以及二次计算成本限制



 
## Deep Adaptation Networks (DAN)

core idea : 通过 MK-MMD 使得深度神经网络找到一种抽象特征表示，使得源域和目标域在这种特征表示下变得相似




> true risk（真实风险）：整个真实数据分布下的期望损失，实践中拿不到所有可能数据，故无法直接计算，常用经验风险近似
> 
> empirical risk（经验风险）：在有限训练样本上的平均预测误差，与真实风险相对，用来评估模型
>
> structural risk minimization（结构风险最小化）：在兼顾训练误差（经验风险）最小化的同时，控制模型的复杂度，以防止过拟合。
>
> 领域差异一般分为两种 ：
>   > 边缘分布差异（Marginal Distribution Shift）：源域与目标域的输入特征分布不同。即  $p(x) \neq q(x)$。比如源域是白天的照片，目标域是夜晚的照片
>   >
>   > 条件分布差异（Conditional Distribution Shift）：在同样的输入 x 下，源域和目标域的标签条件概率分布不同。即 $p(y|x) \neq q(y|x)$。比如在源域中一种模糊的动物图片多半是 “狗”；而在目标域中，同样模糊的图片更可能是 “狼”。

 


## question :

- 能不能将源域和目标域中分布解耦成不同子域表示，再分别对齐子域；或者渐进对齐，通过中间域过渡一下？
   




