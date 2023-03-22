---
date: 2022-11-11
author: Jianqi Huang
title: "stata与python交互使用"
---

### 在python中使用Stata

在stata17之后，Stata支持使用Python作为接口来调用stata命令。

我们可使用python在ipynb文件中。

首先一步是导入包：

```python
import stata_setup
stata_setup.config("se")
```

其中的`se`表示的是版本号。

```text
from pystata import stata
```

```python
stata.run('sysuse auto, clear')

stata.run('''
summarize
reg mpg price i.foreign
ereturn list
''')
```

在**jupyter**中，我们可以使用魔法命令`%%stata`方式进行调用。

同样也可实现在python中安装stata包绘图等命令。

```stata
ssc intsall sum2docx
```

<img src="https://cheinchi.oss-cn-hangzhou.aliyuncs.com/img/Screen%20Shot%202022-11-11%20at%2014.26.24.png" alt="plot" style="zoom:50%;" />



同样也可在安装`IPyStata`实现在jupyter中直接使用stata。

```
pip install IPyStata
```





### 在Stata中使用python

在stata16中输入：

```
set python_exec python位置及版本
```

只需要直接在`do.`文件中或是命令行中输入python即可直接打开python命令行。

- 若需要退出python环境，输入`end`即可





### 总结

而实际上在不同的编程语言中使用其他的编程语言，主要考虑的是在不同编程语言下的优势，能够为目前的工作所用。





### Source

https://blog.stata.com/author/chuber/