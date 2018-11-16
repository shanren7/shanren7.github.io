
# 2018-11-16 [Neural Architecture Search: A Survey](https://arxiv.org/abs/1808.05377)阅读笔记

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
  + 一种优化meta-architecture的方式是层次搜索空间(hierarchical search space)，论文待看[Hierarchical Representations for Efficient Architecture Search, Liu et al. 2018](https://arxiv.org/abs/1711.00436)
  
## 2. Search Strategy
2.1 search strategy 有以下几类：random search，Bayesian optimization，evolutionary methods，reinforcement learning
和gradient-based methods

2.2 一种基于RL的NAS方法为将其看做sequential decision process：state为当前结构，reward为performance，action为修改结构。

2.3 还有一种为neuro-evolutionary方法，采用进化算法来优化模型结构。在NAS任务中，突变为局部operations，比如增减层、选择层的超参数、增减跳跃链接
以及选择训练超参数等。进化算法的差异在于：1)sample parents;2)update populations;3)generate offsprings

2.4 [Regularized Evolution for Image Classifier Architecture Search, Real et al,2018](https://arxiv.org/abs/1802.01548)做了一个RL，evolution和random search在NAS任务中的比较，可以了解下。

2.5 贝叶斯方法主要基于几个方面：1)基于高斯过程，看作低维连续优化问题；2）基于tree-based，比如随机森林等，高维空间最优搜索。

2.6 还有一些基于层次搜索的方法：1）基于蒙特卡洛树搜索树结构；2）基于hill climbing算法，发现最优结构。

2.7 还有采用gradient based optimization方式进行搜索。

```diff
+ 感想：NAS可以看做一个大网络剪枝优化的过程。
```

## 3. Performance Estimation Strategy

3.1 效果评测主要是考虑到计算量：1）减少训练次数 2) 在子集中训练和验证 3) 用低分辨率图片训练 3) 减少filter数量 

3.2 另外一种是通过学习曲线来判断模型效果，不用训练到最终收敛。

3.3 还可以```训练另外一个网络```来评判模型效果，可以参见[Progressive Neural Architecture Search,Liu et al. 2018a](https://arxiv.org/abs/1712.00559)

3.4 还有一种加速效果测评的方法是基于已训练的模型参数来初始化新的模型

3.5 还有one-shot architecture search也是一种有效加速的方法，即将所有的结构看做一个超级大图的不同的子图（sub graph），有相同边界的子图共享权重。因此，只有一个子图需要训练[Understanding and Simplifying One-Shot Architecture Search,Bender et al.2018](Understanding and Simplifying One-Shot Architecture Search)。这类方法的问题是会严重低估模型性能。One-shot architecture NAS方法的差异是one-shot 模型的训练方法。 one-shot NAS的局限在于supergraph。

# 4. 一些方向

4.1 当前NAS主要集中于优化图像分类模型，目前效果已经很不错了，但是在其它任务上，比如```分割、目标检测、多任务问题、多目标问题、生成对抗网络模型、NLP相关任务、语音相关任务、模型压缩相关任务[N2N Learning: Network to Network Compression via Policy Gradient Reinforcement Learning,Ashok et al.2018](https://arxiv.org/abs/1709.06030)```

4.2 NAS中的一些变量需要考虑：1) search space 2) 计算量 3) 数据增强 4) 训练过程 5) 正则化等。

4.3 同时，当前NAS没有一个统一的好的benchmark


