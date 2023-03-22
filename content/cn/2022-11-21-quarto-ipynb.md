---
title: 如何使用Quarto转换ipynb文件
author: Package Build
date: '2022-11-21'
slug: quarto-ipynb
categories: []
tags:
  - 编程
toc: true
---

Quarto作为整个集成的形式，能够将所有的转换方法集成在其终端。

但对于`markdown`的转换其效果并不好，这里推荐使用hongtao编写的[hupyter](https://hongtaoh.com/en/2022/08/28/hupyter/)，命令：
```python
python hupyter.py notebook_directory post_direction
```
Quarto在转换其余格式上还是值得使用的，尤其是在转换为`.html`格式，能够使用`quarto`特定的格式，包括在其中使用`yaml`，因此也就可以在如`rmd`一般在yaml中设置`format`
```
format: 
  html:
    code-fold: true
jupyter: python3
```
同样在`.ipynb`文件中，可对输出的表格图片等进行设置：在code首行，加入

```python
#| label: xxxx
#| fig-cap: the caption of the figure
```


实现转换的命令为：
```
quarto render notebook.ipynb
```
上述的转换是根据`yaml`中设置的`format`，同样也可以指定输出的文件类型：
```
quarto render notebook.ipynb --to docx
```

最终这个显示的效果[dataframe.html](www.jianqihuang.com/cn/posts/dataframe.html)

