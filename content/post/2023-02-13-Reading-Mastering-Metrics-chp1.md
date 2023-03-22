---
title: "Reading Mastering Metrics(Chapter 1)"
date: "2023-02-13"
katex: true
---

### The chapter 1 randomized Trials

We want to solve a causal questions.*random assignment*

bg: elderly Americans are covered by a federal program call Medicare.

> The ceteris paribus question in this context contrasts the health of someone with insurance coverage to the health of the same person were they without insurance.

The conundrum is that we could only observe one outcome of one person.

- treatment group: with insurance

- The comparison or control group: without insurance 



comparisons outcome: the difference between with insurance and without insurance.

But we intuitively want the characteristics of others should be equal or indifferent.

In the table we find that those with health insurance are better educated, have higher income.

![Screen Shot 2023-02-13 at 23.01.29](https://cheinchi.oss-cn-hangzhou.aliyuncs.com/img/Screen%20Shot%202023-02-13%20at%2023.01.29.png)





### Contruct model

$Y$ shorthand for health, the outcome variable of interest.

And $Y_i$ stands for the health of oindividual $i$

Further more, to identify individual whether having insurance, $Y_{0i}$ without health insurance and $Y_{1i}$ with health insurance for person $i$

So parantly, the causal effect is the difference between $Y_{1i}$ and $Y_{0i}$

In a group of $n$ people, average causal effects are written $Avg_n[Y_{1i}-Y_{0i}]$
$$
Avg_n[Y_{1i}-Y_{0i}]=\frac1n\sum_{i=1}[Y_{1i}-Y_{0i}]\\=\frac1n\sum_{i=1}Y_{1i}-\frac1n\sum_{i=1}Y_{0i}
$$
And writing  $Avg_n[Y_i|D_i=1]$ for the average among the insured and $Avg_n[Y_i|D_i=0]$ for the average among the uninsured.

Recall the $Y_{1i}$ and $Y_{0i}$ take the roads with insurance ends and without insurance, perspectively.

![Screen Shot 2023-02-13 at 23.24.32](https://cheinchi.oss-cn-hangzhou.aliyuncs.com/img/Screen%20Shot%202023-02-13%20at%2023.24.32.png)



And consider the causal effect we would like to estimate $Y_{1i}-Y_{0i}=\kappa$

- $\kappa$ is both the individual and average causal effect of insurance on health.

Take the equation $Y_{1i}-Y_{0i}=\kappa$ into Difference in group means, we have

![Screen Shot 2023-02-13 at 23.34.00](https://cheinchi.oss-cn-hangzhou.aliyuncs.com/img/Screen%20Shot%202023-02-13%20at%2023.34.00.png)

we usually call the second term selection bias.

![Screen Shot 2023-02-13 at 23.35.12](https://cheinchi.oss-cn-hangzhou.aliyuncs.com/img/Screen%20Shot%202023-02-13%20at%2023.35.12.png)

The selection bias is defined as the difference in average $Y_{0i}$ between the group being compared.



#### eliminate selection bias

The seclection bias that arises from such unobserved differences.

The Experimental random assignment is the most frequent way.

Random assignment makes this comparison *ceteris paribus*: groups insured and uninsured by random assignment differ only in their insurance status and any consequences that follow from it.

LLN:  sampled subjects are randomly divided into treatment and control groups, they come from the same underlying population.

when $D_i$ is randomly assigned, $E[Y_{0i}|D_i=1]=E[Y_{0i}|D_i=0]$

so the difference in expectations by treatment status captures the causal effect of treatment.

![Screen Shot 2023-02-13 at 23.46.47](https://cheinchi.oss-cn-hangzhou.aliyuncs.com/img/Screen%20Shot%202023-02-13%20at%2023.46.47.png)





So the random assignment firstly we need to compare the groups for balance. Actually, in reality we couldn’t find the absolutely identical objects in other characteristics. we use the statistical tool to solve this problem, like the p-value check.













