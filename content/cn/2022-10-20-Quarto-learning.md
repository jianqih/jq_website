---
title: Quarto 简单入门
author: Jianqi Huang
date: 2022-10-20
---


Quarto 是一个基于Pandoc的开源出版系统。支持基于`R`、``python`及`Julia`等动态内容创作。

### 安装

通过`.tar.gz`文件安装

通过`.deb`文件安装



### 对于行内的代码

为了包括可执行的表达式，通过`r code`来实现。

```markdown
There are `r nrow(mpg)` observations in our data. 
```

就可以实现结果的显示。

``#| echo: FALSE`放入代码块中就可以实现代码的隐藏。但传统的`{}`代码块中也可以实现。



若代码中需要大量的运算，同样可以让yaml中设置缓冲的方式来减少每次运算所耗费的性能和时间。

```yaml
execute:
	cache: true
```

或者就像上面的一样直接在chunk中加入

```R
#| cache: true
```

直接对于需要进行缓存的代码块进行指定。





### 格式选择

在`File>New File>Quato Document`选择生成一个新的Quardo document文件

### 快捷键

对于文本的一些变换操作在visual能够通过快捷键的方式。

| Command      | Keyboard Shortcut | Markdown Shortcut |
| ------------ | :---------------: | :---------------: |
| Bold         |        ⌘ B        |    `**bold**`     |
| Italic       |        ⌘ I        |    `*italic*`     |
| Code         |        ⌘ D        |     ``code``      |
| Link         |        ⌘ K        |     `<href>`      |
| Heading 1    |       ⌥⌘ 1        |        `#`        |
| Heading 2    |       ⌥⌘ 2        |       `##`        |
| Heading 3    |       ⌥⌘ 3        |       `###`       |
| R Code Chunk |       ⌥⌘ I        |     ````{r}`      |





## 输入

### 数学公式

可以将RStudio从Source转到Visual 模式，输入`/`或者`Cmd+/`可以自由的输入想要输入的东西。



### 引用

同样和上面一样的逻辑：引用`/ci`就可以调出内置的文件库数据。内置支持Zotero和PubMed等多种库数据。也可支持输入doi来进行插入引用。同样也是支持用`@ciation`语法进行常规的引用。

目前来看对于中文的支持较差，需要在后期进行一定的优化。

同时若这个ciation被第一次引用，会被导入到references.bib之内。



### 交叉引用

在原先的rmd中的交叉引用的方式是较为复杂的，在这里只需要直接通过`@ref`实现。

在visual下`/ref`会打开所有的可调用的引用方程等。







### Callouts

Callouts是一个很好的帮助用于注释需要注意的地方。

visual 下的语法为`/cal`

![Screen Shot 2022-10-20 at 16.39.12](https://cheinchi.oss-cn-hangzhou.aliyuncs.com/img/Screen%20Shot%202022-10-20%20at%2016.39.12.png)







### 文章格式





### 发布

`quarto::quarto_publish_doc()`



```R
quarto::quarto_publish_doc(
  "authoring.qmd", 
  server = "rpubs.com"
  )
```



## Beamer

生成幻灯片

在markdown中，幻灯片通过标题来描绘出来。

```yaml
---
title: "Habits"
author: "John Doe"
format: beamer
---

## Getting up

- Turn off alarm
- Get out of bed

## Going to sleep

- Get in bed
- Count sheep
```

同样可用可分的幻灯片进入不同的section。



### 增加列表

默认情况下，数字和项目号列表在幻灯片中是一次出现的。可以通过`incremental`选项来设置非同时出现

也可以在局部实现：

```R
::: {.incremental}

- Eat spaghetti
- Drink wine

:::
```







## Books

书结构

```yaml
book:
  title: "mybook"
  author: "Jianqi"
  date: "5/9/2021"
  chapters:
    - index.qmd
    - intro.qmd
    - summary.qmd
    - references.qmd
```
基本的原理与bookdown类似，只需要进行`render`即可实现编译。若需要新加一些`.qmd`文档，可以在`yaml`文件中进行调试，只需要生成的文档名加入对应需要添加的位置即可。


`reference.qmd`会包括所有的引用文献。

