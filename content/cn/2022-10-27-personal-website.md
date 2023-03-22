---
date: 2022-10-27
author: Jianqi Huang
title: 个人网站——基于hugo的使用
toc: true
---
## Hugo安装

Hugo是一个较好的用Go语言编写的静态网站生成器。被称为世界上最快的网站生成器。[^1]

首先需要先安装Hugo，对于macOS来说，可以使用Homebrew来快速在terminal实现：

```bash
brew install hugo
```



> 这个方式同样适用于Linux系统。





Mac同样可以使用Macport实现：

```bash
port install hugo
```

因为比较少使用Windows这里就不介绍相关内容，具体可以在Hugo[^2]官网查看。

一个通用的方法是通过git将文件从Github中获取：

```bash
mkdir $HOME/src
cd $HOME/src
git clone https://github.com/gohugoio/hugo.git
cd hugo
go install --tags extended
```



## Hugo初始化

```bash
hugo --theme=hugo-eureka --baseUrl="https://cheinchi.github.io/" --buildDrafts
cd public
git add .
git status
git commit -m "add blog post"
git push  
```

1. `--buildDrafts`
2. `  —-buildExpired `
3. `– – buildFuture`

toml为site的顶层配置文件，直接在文件内部进行修改。
## 添加一篇文章

`hugo new posts/my-first-post.md`

同时在进一步地在进行修改基础属性

`hugo server -D`即可显示网站

hugo的目录结构

```
├── archetypes #内容模版文件，包括预配置的首选项，可以用自定义的预配置前端字段创建新的原形
├── assets (not created by default) 存储所有的文件，默认不创建这个目录
├── config.toml  #可作为默认网站的配置文件
├── content#放文本
├── data#生成网站时候用到
├── layouts#以.html的文件形式存储模版
├── static  #存储所有静态内容
└── themes#选择的hugo主题
```

- 不能直接编辑文件

**git init** 命令用于在目录中创建新的 Git 仓库。

在目录中执行 **git init** 就可以创建一个 Git 仓库了

`$ rm -rf  .git  #删除`



## 版本库(Repository)

工作区中的隐藏目录`.git`，就是Git的版本库。



## 个人习惯

笔者的一大习惯是使用Rstudio中的blogdown的功能来实现。这个要求你对于R语言有一个基本的了解，之后再安装相关的包。

```R
install.packages('blogdown')
blogdown::install_hugo() #在R中可以通过blogdown直接下载hugo
```

之后需要在新建一个Project，新建文件中包括了一个Website using blogdown 这个项目类型。同时还可直接选择Hugo theme，这里默认的是使用Yihui/hugo-lithium主题。

![Screen Shot 2022-10-27 at 23.51.06](https://cheinchi.oss-cn-hangzhou.aliyuncs.com/img/Screen%20Shot%202022-10-27%20at%2023.51.06.png)

之后若需要生成上传文档只需要使用Rstudio中自带的Git功能。笔者习惯的方式是通过Github的桌面软件对本地仓库的访问再连接到git中的仓库，有变更的时候直接进行意见commit-git。这样就基本上将一个网站建好了，同时之后的new post只需要通过addins中的`New Post`选项，可以生成`Rmd`、`md`等格式的post。比之前需要进行的流程省了大量步骤。

![Screen Shot 2022-10-27 at 23.58.03](https://cheinchi.oss-cn-hangzhou.aliyuncs.com/img/Screen%20Shot%202022-10-27%20at%2023.58.03.png)





## reference

[^1]:[Hugo相关介绍](https://zh.wikipedia.org/zh-cn/Hugo_(%E8%BB%9F%E4%BB%B6))
[^2]: [Hugo官网](https://gohugo.io/getting-started/installing/)
[^3]: 这里有blogdown的更为详细的介绍：https://bookdown.org/yihui/blogdown/
[^4]:  blogdown 的作者对于为何使用hugo的介绍 https://yihui.org/en/2017/12/blogdown-book/
