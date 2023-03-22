---
title: "Using Jupyter translated into other format"
date: 2022-10-21
author: Jianqi Huang
---
# Using Jupyter translated into other format

based on `#｜` in the normal compile and the necessity of translating into other format，It will be as an annotation in Jupyter complier, And be considered as a setting in Quarto,which could input some basic infomation and format in chunk about output.

```
#| label: fig-polar

#| fig-cap: "A line plot on a polar axis"
```

## A test for Quarto

For a demonstration of a line plot on a polar axis, see @fig-scatter.


```python
x = np.arange(0,1,0.01)
y_mins = 0 
y_maxs = 5
y = y_mins+np.random.randn(100)
```


```python
#| label: fig-scatter
#| fig-cap: "A scatter plot random"
plt.scatter(x,y)
plt.show()
plt.savefig("/Users/a182501/Desktop/Programming/hello_file/hello_6_0.png")
```


![hello_6_0](https://cheinchi.oss-cn-hangzhou.aliyuncs.com/img/hello_6_0.png) 
    



we use the label when we markdown `@`

exam: we can see the normal distribution @fig-nordis


```python
#| fig-cap: "the normal distribution"
#| label: fig-nordis
import seaborn as sns
random3=np.random.randn(10000)
sns.set_palette("hls")
sns.displot(random3,color='r',bins=1000,kde=True)
plt.show()
plt.savefig("/Users/a182501/Desktop/Programming/hello_file/hello_9_0.png")
```


![]("media/hello_9_0.png")


```
quarto render hello.ipynb --to html    
quarto render hello.ipynb --to markdown
```