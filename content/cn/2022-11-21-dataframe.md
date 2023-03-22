---
title: pandas数据框提取子集与R比较
date: "2022-11-21"
author: Jianqi Huang
format:
    html:
        code-fold: true
---
最初R首先使用数据框的这一理念，之后又发展出了`tibble`的方法来对数据框进行更精细的设计。python也紧跟其后，在pandas中引入了数据框，在具体的使用中仍然能够看出两者的不同。


在R中我们可以直接使用`df[x,y]`其中若选择提取行，就可令`x=c(row_num/row_name)`，`y`为空；同理也可以反过来提取列值，或在`c()`中变量前填入减号：`-`，就可筛去不想要加入的变量或数据。或者使用`subset(dataframe,condition)`在`condition`输入逻辑判断、`which`和`%in%`等命令得到数据框的子集。

在python中较为常用的方式是使用`iloc`,`loc`和`ix`

`iloc`通过行号和列号进行数据筛选。将`i`理解为`integer`。即选择一个整数进行提取。


```python
import pandas as pd
import numpy as np
```


```python
df = pd.DataFrame({'name':['张三','李四','王二','丁一','李五'],

'gender':['男','女','女','女','男'],

'age':[25,26,22,29,27]},columns = ['name','gender','age'])
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>gender</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>张三</td>
      <td>男</td>
      <td>25</td>
    </tr>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>女</td>
      <td>26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王二</td>
      <td>女</td>
      <td>22</td>
    </tr>
    <tr>
      <th>3</th>
      <td>丁一</td>
      <td>女</td>
      <td>29</td>
    </tr>
    <tr>
      <th>4</th>
      <td>李五</td>
      <td>男</td>
      <td>27</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.iloc[1:4,:]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>gender</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>女</td>
      <td>26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王二</td>
      <td>女</td>
      <td>22</td>
    </tr>
    <tr>
      <th>3</th>
      <td>丁一</td>
      <td>女</td>
      <td>29</td>
    </tr>
  </tbody>
</table>
</div>



设置标签`df=df.set_index()`


```python
df2=df.set_index("name")
```


```python
df2.loc["张三",]
```




    gender     男
    age       25
    Name: 张三, dtype: object




```python
df.iloc[0, ]
```




    name      张三
    gender     男
    age       25
    Name: 0, dtype: object




```python
df.loc[1:4,['name','age']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>name</th>
      <th>age</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>李四</td>
      <td>26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>王二</td>
      <td>22</td>
    </tr>
    <tr>
      <th>3</th>
      <td>丁一</td>
      <td>29</td>
    </tr>
    <tr>
      <th>4</th>
      <td>李五</td>
      <td>27</td>
    </tr>
  </tbody>
</table>
</div>


