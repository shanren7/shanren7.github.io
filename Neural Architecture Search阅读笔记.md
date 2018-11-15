# NAS阅读笔记
- 三个方面：search space、search strategy、performance estimation strategy

## 1. Search Space
1.1 简单的chain-structured neural networks的搜索层面有三个：
  - 网络层数
  - operation 类型，比如卷积，池化，depthwise卷积，孔洞卷积
  - operation的超参数，比如filter数量，stride，kernel size等

1.2 复杂的还需要加入skip connections,residual network
1.3 一些采用搜索模组比如 cells 或者blocks的方式，而不是搜索全部网络结构有几个优点：
  + 搜索空间急剧减少
  + cells可以通过简单的增加重复模组的数量来迁移到其它数据集
1.4 搜索模组的方式会产生新的问题，即meta-architecture应该怎样构成？
  + 一种优化meta-architecture的方式是层次搜索空间(hierarchical search space)，论文待看[Liu et al. 2018](??)
  
## 2. Search Strategy
2.1 search strategy 有以下几类：random search，Bayesian optimization，evolutionary methods，reinforcement learning
和gradient-based methods

2.2 一种基于RL的NAS方法为将其看做sequential decision process：state为当前结构，reward为performance，action为修改结构。

2.3 还有一种为neuro-evolutionary方法，采用进化算法来优化模型结构。在NAS任务中，突变为局部operations，比如增减层、选择层的超参数、增减跳跃链接
以及选择训练超参数等。进化算法的差异在于：1)sample parents;2)update populations;3)generate offsprings

2.4 [Real et al,2018]()做了一个RL，evolution和random search在NAS任务中的比较，可以了解下。

2.5 贝叶斯方法主要基于几个方面：
