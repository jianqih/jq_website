---
title: "混合高斯，EM算法与K均值聚类"
author: Jianqi Huang
date: 2022-11-25
---

# GMM

GMM混合高斯模型是将多个不同的高斯分布进行混合而得到的一个概率分布模型。因此可用于表示一个总体的分布中含有K个子分布的模型。
$$
p(x|\Theta)=\sum_{i=1}^c\alpha_ip_i(x|\mu_i,\Sigma_i)
$$
`$\Sigma_i$`表示的是参数

其中的参数空间：
$$
\Theta=\{\alpha_1,\alpha_2,\cdots,\alpha_c,\mu_1,\mu_2,\cdots,\Sigma_1,\Sigma_2,\cdots,\Sigma_c\}
$$
直接使用MLE求解参数：
$$
l(\Theta)=\prod_{j=1}^N\sum_{i=1}^c\alpha_ip_i(x|\mu,\Sigma_i)\\
\ln \left[l(\Theta)\right]=\sum_{j=1}^N\ln\left[\sum_{i=1}^c\alpha_ip_i(x|\mu,\Sigma_i)\right]
$$
对上式求导得到：
$$
\frac{\partial \ln \left[l(\Theta)\right]}{\partial \mu_k}=\sum_{i=1}^N\frac{\alpha_ip_i(x|\mu,\Sigma_k)}{\sum_{j=1}^c\alpha_jp(x_i|\mu_j,\Sigma_j)}\Sigma_k^{-1}(x_i-\mu_k)=0
$$
进一步得到
$$
\mu_k=\frac{\Sigma_{i=1}^NP(w_k|x_i,\mu_k,\Sigma_k)x_i}{\Sigma_{i=1}^NP(w_k|x_i,\mu_k,\Sigma_k)}
$$
同样的方法对于`$\Sigma_k$`会得到
$$
\sigma_k=\frac{\Sigma_{i=1}^NP(w_k|x_i,\mu_k,\Sigma_k)(x_i-\mu_k)(x_i-\mu_k)^T}{\Sigma_{i=1}^NP(w_k|x_i,\mu_k,\Sigma_k)}
$$




# EM算法

EM(expectation-Maximum)算法也称为期望最大化算法。其实际上就是使用迭代的方式来对最大似然估计进行求解的算法。EM算法受缺失思想的影响，对于数据缺失或似然的解析求解较为困难的时候较为有效。

基本思路是根据已有的观测数据，估计参数值，同时根据估计出的缺失的数据再加上之前的观测到的数据重新进行估计，反复迭代直到收敛。

而我们想要进行已有的数据估计参数值，需要对原有对数据进行扩张，也就是将缺失数据显性表示，令其中的隐变量数据为`$x$`，构建`$z=(y,x)$`。其中的`$y$`为观测数据。最终使得扩张后的后验分布为`$\pi(\theta|z)=\pi(\theta|y,x)$`



## 计算步骤

假设有`$p(x|y,\hat \theta)$`是在给定`$y,\hat\theta$`下`$X$`的预测分布。`$\hat{\theta_i}$`为第i次迭代的`$\theta$`的估计值。基本的步骤为

- 计算`$x^{(i)}=E[X|y,\hat\theta^{(i)}]$`
- 扩张观测数据`$y$`为`$(y,x^{(i)})$`，最大化概率`$\pi(\theta|y,x^{(i)})$`，记录最大值`$\theta^{(i+1)}$`

- 用上述得到的`$\theta^{(i+1)}$`和第一步的`$x^{(i)}=E[X|y,\hat\theta^{(i)}]$`计算下一个`$x^{(i+1)}$`，再同样带入（2）如此重复得到收敛的结果。
  - 收敛常常用一个$||\theta_{i+1}-\theta_i||<\varepsilon$来表示

### 证明其收敛性

注意到`$\pi(\theta|y)=\pi(\theta,x|y)/p(x|y,\theta)$`，有
$$
\ln\pi(\theta|y)=\ln\pi(\theta,x|y)-\ln p(x|y,\theta)
$$
同时对两侧`$X|y,\theta^{(i)}$`取期望得到：

$$\ln\pi(\theta|y)=\int\ln\pi(\theta,x|y)p(x|y,\hat\theta^{(i)})dx-\int\ln p(x|y,\theta)p(x|y,\hat\theta^{(i)})dx\\
=Q(\theta,\hat{\theta}^{(i)})-H(\theta,\hat{\theta}^{(i)})$$

- E-step：计算`$Q(\theta,\hat{\theta}^{(i)})$`

- M-step：对`$\theta$`最大化得到`$Q(\theta,\hat{\theta}^{(i)})$`以获得`$Q(\theta^{(i+1)},\hat{\theta}^{(i)})$`

即
$$
Q(\theta^{(i+1)},\hat{\theta}^{(i)})=\max_\theta Q(\theta,\hat{\theta}^{(i)})
$$
注意到
$$
\ln \pi(\hat\theta^{(i+1)}|y)-\ln \pi(\hat\theta^{(i)}|y)
=\{Q(\hat\theta^{(i+1)},\hat\theta^{(i)})-Q(\hat\theta^{(i)},\hat\theta^{(i)})\}-\{H(\hat\theta^{(i+1)},\hat\theta^{(i)})-H(\hat\theta^{(i)},\hat\theta^{(i)})\}
$$
同时我们又可根据期望的表达式：
$$
H(\theta,\hat\theta^{(i)})-H(\hat\theta^{(i)},\hat\theta^{(i)})\\
=\int\ln p(x|y,\theta)p(x|y,\hat\theta^{(i)})dx-\int\ln p(x|y,\theta)p(x|y,\hat\theta^{(i)})dx\\
=\int\ln \frac{p(x|y,\theta)}{p(x|y,\hat\theta^{(i)})}p(x|y,\hat\theta^{(i)})dx\le 0
$$
因此可看到
$$
H(\hat\theta^{(i+1)},\hat\theta^{(i)})\le H(\hat\theta^{(i)},\hat\theta^{(i)})
$$
可看出对于任意的`$i$`，都有：
$$
\ln\pi(\hat\theta^{(i+1)}|y)\ge \ln\pi(\hat\theta^{(i)}|y)
$$
同时根据之前的任意性，可知从任何一个初值出发都可以得到一个最大值。

## 算法缺点

**缺点**：对初始值敏感：EM算法需要初始化参数，而参数的选择直接影响收敛效率以及能否得到全局最优解。





# K-means与GMM

Kmeans所使用的算法的核心思想也是通过EM求解迭代得到最终的簇，为克服EM算法中的塌陷到局部最小值，K-means在每次都随机选择新的点作为中心，由此不断的迭代计算。也因此，对于Kmeans需要指定一个k值的大小，也就是指定将其聚为哪几类。而这个的确定需要通过一些计算方法实现：

- 较为常见的是Elbow method，x轴为k大小，即聚类数，y轴为WSS(within cluster sum of squares )，显然这个的约束是K的个数，因此在这个权衡下找到那个下降的拐点即可。（在图中k=3最佳）

![k-means](https://cheinchi.oss-cn-hangzhou.aliyuncs.com/img/k-means.jpg)



#### kmeans算法衡量指标

- SSE误差平方和
- 轮廓系数`$\in [-1,1]$`，轮廓系数接近于1时表示样本远离相邻聚类，0表示在两个边界十分接近，-1表示分配到错误的地方。

GMM不同于Kmeans方法：在kmeans中一个数据点，不是0就是1，而对于GMM，能够从概率的角度对该数据点的类别进行刻画。

通常我们并不能直接得到高斯混合模型的参数，而是观察到了一系列的数据点，给出一个类别的数量K后，希望求得最佳的K个高斯分模型。因此，高斯 混合模型的计算，便成了最佳的均值`$\mu$`，方差`$\Sigma$`、权重`$\pi$`的寻找，这类问题通常通过最大似然估计来求解。

正如上述1所说，一些情况下的参数求解并非完全是有解的，同样可以借鉴于EM算法的思路，对原有的最大似然函数的求解通过迭代的方法得到。



### Source

- https://zhuanlan.zhihu.com/p/40991784
- https://www.cnblogs.com/jerrylead/archive/2011/04/06/2006936.html

- https://zhuanlan.zhihu.com/p/30483076

- https://scikit-learn.org/stable/auto_examples/cluster/plot_kmeans_silhouette_analysis.html