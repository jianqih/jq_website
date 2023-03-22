---
title: "如何使用quarto创建beamer"
author: JianqiHuang
date: 2022-10-29
---



首先需要安装一个quarto

其次在点开quarto document 创建文档

在`.qmd`文档中，其基本的语言仍然是基于pandoc中的markdown语法。

通常使用二级标题`##`进行分割两个幻灯片。

同样也可使用一级标题创建一个只有一个一个标题的一页，往往是作为一个部分的标题。

在每一次render的时候，都会生成一个本地的html网站，可以通过浏览器打开，随着render的更新，html文件也会跟着更新。

同样可以使用的是`---`来对一些没有标题的slides进行分割

```markdown
---
- why are you so smart
- because work hard
---
- why you work so hard
- because need to live
```

同时这个是不会一次性全部出现的，也就是在多个分段中逐次出现。对于一些不能增加标题的来说，可能就需要使用这样的方式。

但若想要同样有标题以及逐次出现的类似动画的效果（因为一般而言，slides包含标题下是同时显示的）因此就需要使用在YAML中的format设定`incremantal: true`的方式。本质上就是生成多页的slides，而每一页都是逐次增加行内容的方式。

```yaml
title: "My Presentation"
format:
  beamer:
    incremental: true   
```

之后如同输出定理一般：在slides中添加

```markdown
::: {.incremental}

- Eat spaghetti
- Drink wine

:::
```

之后就会逐次出现的方式实现slides的播放。

既然有incremental增加式，自然也会有`non-incremental`方式

只需要在`:::{}`中修改为`::: {.nonincremental}` 实际上和不加`:::{.}:::`这个环境没太大区别。

同样是在这个基础上，如何生成多列来输出：

```markdown
::::{.columns}
:::{.column width="40%"}
writing some words in column 1
:::
:::{.column width="60%"}
just write in column 2
:::
::::
```

这里的环境又发生了变化在外面先嵌套了一层`::::{.columns}`这里有四个`:`





### 插入数学公式及定理

数学公式的插入这个功能基本上同其他的markdown类似，但可以更多的是插入对公式的编号`\tag{}`

```
$$
y = f(x)
\tag{*}
$$
```



更多具体的beamer设置可以参考下面的介绍以及beamer官方指导文章和cosx中R markdown的beamer详细介绍

- https://mirrors.sustech.edu.cn/CTAN/macros/latex/contrib/beamer/doc/beameruserguide.pdf

- https://quarto.org/docs/reference/formats/presentations/beamer.html#slides

- https://cosx.org/2022/08/beamer-not-down/