---
title: "特征选择"
date: 2022-11-02
author: Jianqi
---

### 特征选择

对于一个数据集来说，其特征是可能是庞大的，同时又存在样本数N，若选择所有的特征作为样本数据进行训练，最终的运算会极大的降低。因此需要对特征进行选择来降低特征量。因此对于特征选择方式：

- 过滤式Filter：直接衡量单个特征，常用的筛选指标有：
  - 相关性：对于特征（属性）之间所表现的相关程度的衡量，常常使用pearson相关系数，或者用spearman相关系数。
  - 稳定性：对于最终的模型构建是否稳定，不仅仅体现在方差的大小（数据稳定性），还包括计算稳定性、性能稳定性等，对于特征稳定性来说可以使用群体稳定性指标(population stability index,PSI)来衡量
  - 有效性：有效性是一个相对的概念，比如在一个线性无偏估计中，OLS具有最小方差。
- 嵌入式Embedded：通过模型得到特征的重要性
- 封装式Wrapper：根据目标，每次选择或排除若干特征



### 特征重要性

#### Permutation importance

Permutation importance 适用于表格型数据，对特征值的重要性评判取决于该特征值被随机重排序之后，模型表现评分下降的程度。

- 输入数据集D
- 模型m在数据集D上的性能评分s
- 对于数据集D的每一个特征j
  - 对于重复K次实验中的每一次迭代`$k$`，随机重排特征`$j$`，构造一个被污染（加入噪音）数据集`$D_{C_{k,j}}$`
  - 特征`$j$`的重要性分数`$i_j$`可以记作


$$
i_j=s-1/K\sum_{k=1}^Ks_{k,j}
$$

#### Boruta

核心思路为将特征矩阵进行shuffle，再将shuffle的特征(shadow features)与原特征(real features)拼接为新特征。判断打乱以后的重要性和原特征之间的差异。若差距越大该特征越显著。

这里还用上z- score特征缩放的方法，将shadow features中最大的为`$Z_{max}$`，标记为重要，相反，不重要的自然是远低于`$Z_{max}$`的值，从特征集合中剔除。

删除之前合并的shadow features，接着重复，直到所有特征被标记。



### 特征缩放方法

1. Min-Max method :
$$x_{norm}=\frac{x-\min(x)}{\max(x)-\min(x)}\in[0,1]$$
2. Scale to [-1,1] 
$$x_{norm}=\frac{x-mean(x)}{\max(x)-\min(x)}$$
3. Z-score: 
$$x_{norm}=\frac{x-mean(x)}{std(x)}\sim N(0,1)$$
4. Log-based 
$$x_{log}=\log(1+x)$$
5. L2 normalize 
$$x_{norm}=\frac{x}{||x||_2}$$

6. Gauss Rank : transfer to guass distribution and get the rank.



