---
title: "Rmarkdown 的html输出格式"
date: 2022-11-24
author: Jianqi Huang
---

## 引言

rmarkdown对于文学性编程有很好的支持，因此用rmarkdown是一个很好的作为一个日常的作业以及日常的记录方式的工具。

## 附加内容设置

对于html的输出主要是在Yaml中的`output`下的`html_document`中对一些参数的设置：

- 设置目录： `toc=true`和进一步可设置目录的深度`toc_depth:`

- `toc_float=true`会使得目录在侧边悬浮

  - 进一步可以改变其中的动画效果：`smooth_scroll`在页面滚动的时候

  

## 对文本内容修饰

`number_sections=true`:可使得在每一个`##...`中以级别附上其标题序号。默认下为`false`

但有时候会与之前提到的`toc`发生冲突，可能是与所使用的模版相关。在最原始的`html_document`并不会冲突。



### 使用标签页

只需要在对应的标题后加入`{.tabset}`

会使得在其子标题分别生成对应的标签页。



### 代码

- 高亮：`hightlight: kate`
  - 还有一些其他可选的内容包括`tango`、`pygments`、`monchrome`等
- 代码折叠：`code_folding: hide`，使用这个命令之后会默认开启`html`一侧的`code`这个的选项，若使用`code_folding: show`也会和原先一样，不过是多了一个展开折叠的选项

- 为控制输出的页面长度，很多时候一些代码并没有完全的传递有效的信息，因此可选择一些滚动的来筛选有效信息。在代码块中插入`class.output="scroll-100"`限制输出的代码像素为100。
- 对于数据也是如上，通过在yaml中设置`df_print: paged`使得输出的数据框支持行列的分页。





## 附加数据

在一些情况下需要在rmarkdown中所展示的效果有限或对其他的附加内容的要求，可以使用`xfun::embed_files(source_file)`进行附加各种的文件，若是多个会被打包为一个zip可解压文件。





## Source

- https://bookdown.org/qiushi/rmarkdown-guide/html-document.html#%E7%9B%AE%E5%BD%95%E5%92%8C%E6%A0%87%E9%A2%98