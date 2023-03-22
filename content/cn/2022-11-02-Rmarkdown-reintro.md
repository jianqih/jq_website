---
title: Rmarkdown再入门——从yaml开始
date: 2022-11-02
author: Jianqi Huang
---

逐渐喜欢从latex转向使用Rmd作为自己主要的文字编译软件。

其主要原因在于可以很好的结合现有的pandoc的markdown编译习惯以及在使用时候能够在对报告中添入的代码进行直接的输出。很好的将代码、图片和文字结合在一起，能够得到更好的展示效果。

当然在之前也一直知道用`.Rmd`，但都是在使用的是`.Rmd`转化为`.html`格式的方式。其中的输出方式为

```yaml
output: html_document
```

在转化为`.pdf`文件时候，`output:pdf_document:default`总是会遇上一些奇怪的报错，在我已经下载好`tineytex`的前提下，后来才慢慢因为一些事情需要和看到别人做的报告，自己试图再去使用这个作为中文输入编译软件。

后来也通过报错的指引找到了谢老大的tineytex 的文档，其中也发现可以通过安装`rtitle`的方式，其中有包括编译中文文档的Rmd模版，因此就迅速转向`.Rmd`

之后的问题就是在对已有的模版下如何自己调试的问题，需要调试就需要知道yaml相关的内核。

### Yet another markup language

什么是标记语言：标记语言是一种注释文本的语言，以便于计算机能够操作文本。大多数是人自然可认的。标记是用于显示或打印文本的指令。

YAML仍然是一个标记语言，YAML的配置文件后缀为`.yml`，在`md`或`.rmd`、`.qmd`等文件中插入

基本语法：

- 大小写敏感
- 使用缩进表示递进关系
- **缩进不允许使用tab，只允许空格**
- 缩机的空格数不重要，只要相同的元素左对齐

- `#`表示的是注释



#### 数据类型

yaml中的数据类型包含三类：

- 对象：字典形式表示
- 数组：一组按次序排列的值，又称为序列/列表
- 纯量：单个的、不可再分的值

对象值对使用冒号结构表示，同时要注意在冒号后加一个空格再输入值。

同时缩进中表示层级关系：

```yaml
key:
	child-key: value1
	child-key: value2
```

较为复杂的结构中，可以使用问号加上一个空格代表一个复杂的key

Yaml数组：以`-`开头的行表示构成一个数组：

```yaml
- A
- B
- C
```

##### 复合结构

数组和对象可以组成一个复合的结构：

```yaml
languages:
	- Ruby
	- Perl
websites: 
	Yaml: yaml.org
	Ruby: ruby-lang.org
	Python: python.org
```



纯量表示的是不可再分的值，包括字符串、布尔值、整数、浮点数、Null、时间等

```yaml
boolean:
	- TRUE
	- FALSE
date:
    - 2018-02-17    #日期必须使用ISO 8601格式，即yyyy-MM-dd
datetime: 
    - 2018-02-17T15:02:31+08:00 #时间使用ISO 8601格式，时间和日期之间使用T连接，最后使用+代表时区
```



### YAML在`Rmd`

yaml在Rmd上的运用实际上是基于Pandoc的使用，Rstudio中已经捆绑了Pandoc，因此我们可以在Rstudio中使用latex、html等不同格式之间自如切换。yaml就是在pandoc中的Metadata block，在开头处添加`---`进行包围。

通过加入一些基本的设置我们可以在对原有的输出进行相应的设置。比如在导出中设置：

```yaml
output:
  rticles::ctex:
    fig_caption: yes
    number_sections: yes
    toc: yes
```

其中`toc`是关于设置输出中是否带有目录

`fig_caption`是关于输出的图像标题的设置；

`number_sections`是关于在已有的缩进下是否添加数字序号。

在其他对象中，我们还可以设置

在一些最基本的设置中包括设置

```yaml
geometry: "left=xxcm,right=xxcm,xxxx"
```

对于字符串是不允许的，因此若需要使用，可以在字符串之前加入`|`或`>`，在新的一行加入所需要的字符串。比如输入一个`abstract`

```yaml
abstract: |
	xxxxxxxx
	xxxxxx
```

还有一些其他更多的设置可以得到探索。





## Resources

- https://en.wikipedia.org/wiki/YAML#Syntax

- https://pandoc.org/MANUAL.html#metadata-blocks