---
title: "制作slides的方法（N）"
date: 2022-12-15
---



在pandoc中，`aspectratio`表示的是对屏幕比例的调整

`43`就是4:3的屏幕比例；`169`就是16:9比例、`141`是14:9比例等等。

Institute: 添加机构

`logo`：slides中的logo

`navigation`控制导航栏的形式，是水平的还是纵向的。

`section-titles`用于每一个新的title pages

`documentclass`：能够用于控制输出。



#### 前言

`thanks`





### BibLaTeX Bibliographies

These variables function when using BibLaTeX for [citation rendering](https://pandoc.org/MANUAL.html#citation-rendering-1).

- `biblatexoptions`

  list of options for biblatex

- `biblio-style`

  bibliography style, when used with [`--natbib`](https://pandoc.org/MANUAL.html#option--natbib) and [`--biblatex`](https://pandoc.org/MANUAL.html#option--biblatex)

- `biblio-title`

  bibliography title, when used with [`--natbib`](https://pandoc.org/MANUAL.html#option--natbib) and [`--biblatex`](https://pandoc.org/MANUAL.html#option--biblatex)

- `bibliography`

  bibliography to use for resolving references

- `natbiboptions`

  list of options for natbib





### 文本内容设置

`fontsize`：对于主体文本的

`headertext`和`footertext`

`toc`：设置目录

进一步还可以`toc-depth=NUMBER`来设置目录深度。





### note

演讲人可通过一下的代码来添加注释：

```
::: notes

This is my note.

- It can contain Markdown
- like this list

:::
```



### 设置左右分割



```yaml
:::::::::::::: {.columns}
::: {.column width="40%"}
contents...
:::
::: {.column width="60%"}
contents...
:::
::::::::::::::
```



```
:::::::::::::: {.columns align=center totalwidth=8em}
::: {.column width="40%"}
contents...
:::
::: {.column width="60%" align=bottom}
contents...
:::
::::::::::::::
```

### 设置可滚动

```
::: incremental

- Eat spaghetti
- Drink wine

:::
```



输出slides

```R
rmarkdown::beamer_presentation()
```







### Source

https://pandoc.org/MANUAL.html#metadata-variables

