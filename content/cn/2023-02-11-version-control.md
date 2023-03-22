---
title: "Git版本控制(version control)"
date: "2023-02-11"
---

#### 什么是版本控制

版本控制系统(VCSs)是一类用于追踪源代码改动的工具。能够帮助我们找到以前的改动历史。最简单的一个应用是在word软件中Review板块下的Track Changes。不仅于此，VCS在一个分布式系统下，能够帮助不同的工作者协同工作。VCS通过快照来将某个文件夹及其内容保存起来，每个快照都包含了文件或文件夹的完整状态。



#### 为何要进行版本控制？

> It allows you to revert selected files back to a previous state, revert the entire project back to a previous state, compare changes over time, see who last modified something that might be causing a problem, who introduced an issue and when, and more. Using a VCS also generally means that if you screw things up or lose files, you can easily recover. In addition, you get all this for very little overhead.

对于一个写作者或创作者来说，在不同的状态下有不同的作品，因此需要在时间前后进行综合比较得到最终的版本。使用VCS可帮助恢复丢失的文件，同时只需要付出非常小的成本就可以得到。

通常人们会选择在本地进行版本控制，非常简单的进行复制，再用一个可识别的方式来标记版本。

但对于多任务处理时候，很容易会将这些问题忘记，比如在文件保存时候，随手会点击ctrl+s直接在原文件进行保存，这样就并没有区分上一个版本和下一个版本。同时我们还需要在不同合作者之间管理版本，用Git来管理版本就可以得到很好的控制。

> 本文假设你已经知道和安装了git。

### Git基本概念

- 工作区：在电脑中能看到的目录
- 暂存区：一般存放在`.git`目录下的index文件中，也称暂存区为索引
- 版本库：工作区有一个隐藏目录`.git`，并不算工作区，而是Git的版本库。

其中之间的关系就是要通过`git`命令来实现连接。

- 对工作区的修改文件执行`git add`命令时候，暂存区的目录会更新，同时工作区的文件内容写到对象库中的一个新的对象中，而该对象的ID被记录在暂存区的文件索引中。
- 当执行`git commit`时候，暂存区的目录树会写到版本库，master分支会做出相应的更新。

- `git checkout .`或者`git checkout --<file>`命令时候，会使用暂存区全部或指定的文件替换工作区的文件。

```shell
git commit -m [message]
```

`-m`为提交信息，`[message]`是一些备注信息。

`git commit -a`其中的`-a`是修改文件后不想要执行`git add`命令，直接提交。

`git commit --amend`可以修改我们上次提交的`message`。



#### 关联方式
- HTTP方式：这种方式要求project在创建的时候只能选择“Public”公开状态，Private和Internal私有模式下不能使用http方式进行连接，如果考虑到安全性必须进行安全设置。
- SSH方式：这是一种相对安全的方式，本地git仓库和远端gitlab仓库之间的传输是通过SSH加密，SSH方式在三种project模式下都可以使用。


#### 快照

Git将顶级目录中的文件和文件夹作为集合，通过一系列的快照来管理历史记录。在Git术语中，文件呗称为Blob对象（数据对象），也即是一组数据。目录被称为“树“。快照则是被追踪的最顶层的树。





### Git获取仓库

获取仓库(**respority**)的方法通常有两种，一种是从其他人的那clone一个过来，另一个是我们主要操作的将一些尚未进行版本控制的本地目录转化为Git仓库。

#### 初始化

在不同系统中都是先使用`shell`命令

```shell
cd project_direction
```

之后再执行

```
git init
```

取消git

```
rm -rf .git
```

这之后会在创建一个`.git`的子目录，这个子目录含有你初始化的 Git 仓库中所有的必须文件，这些文件是 Git 仓库的骨干。 

但这时候并没有对现有的文件内进行跟踪，因此需要在之后进行版本控制，需要追踪这些文件，可以通过`git add`来到指定文件追踪。

`git add .`可以追踪项目文件夹中的所有文件。

在完成初始化之后，在工作目录下的文件都可以分为两个状态：已追踪和未追踪。已追踪文件就是Git已经知道的文件。

我们可以通过`git status`来查看目前哪些文件处于何种状态。

```shell
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean
```



#### 配置

在你的远程仓库，你首先需要建立两岸之间的联系，也就是对本地仓库进行配置。配置是使用`git config`命令。

```shell
git config --list
```

编辑git配置文件

```shell
git config -e
```

或者：

```shell
git config -e --global
```

设置提交新文件时候对用户信息

```shell
git config --global usr.name "xxx"
git config --global user.email xxx@xxx.com
```

若去除`--global`参数只对当前的仓库有效。为此，我们就可以设置不同的仓库与不同的github账号。



#### 跟踪新文件

git的工作原理是将创建和保存的项目的快照与之后的快照进行对比。

```shell
# 添加文件到暂时存放区域
git add
# 查看仓库当前的状态，显示有变更的文件。
git status
# 比较不同的文件，即暂存区与工作区的不同
git diff <filename>
# 显示某个文件两个版本之间的差异
git diff <revision> <filename>
# 提交暂存区到本地仓库
git commit
# 退回版本
git reset
# 从暂存和工作区删除
git rm
# 移动或重命名工作区文件
git mv
```



#### 查看日志

```shell
git log # 查看历史提交记录
git blame <file> # 以列表形式查看指定文件的历史修改记录
git bisect # 通过二分查找搜索历史记录
```



#### 远程库信息查看命令

```shell
# 远程仓库操作
git remote
git remote -v
git branch -r, git branch -a
git remote add origin 
```



#### 获取和提交

```shell
# 从远程获取代码库
git fetch
# 下载远程代码并合并
git pull
# 上传远程代码并合并
git push
```

- `git pull`的作用是将远程主机 origin 的 master 分支拉取过来，与本地的 brantest 分支合并。
- 如果远程分支是与当前分支合并，则冒号后面的部分可以省略。








#### 分支交互命令

分支意味着每一种的版本控制系统能够以某种形式来支持分支，一个分支代表一条独立的开发线。

使用分支意味着可以从开发主线上分离开，同时不影响主线的继续工作。

当你在`git init`的时候，git就自动帮你创建了一个master分支。若我们要再创建一个分支，就可以通过执行`git branch (branchname)`来实现。

创建分支：

```shell
git branch (branchname)
```

切换分支命令:

```shell
git checkout (branchname)
```

合并分支：

```shell
git merge 
```

删除分支

```
git branch -d (branchname)
```



- `origin`是clone时候托管在github上代码库时候，git为你默认创建的标签。origin指向的是这个仓库，`master`知识这个的一个分支。
- 若对branch改名了，之后再对其进行push的时候需要注意使用`git push origin branch_name`





#### Git标签

为使得我们的git操作更容易辨识，我们可以对修改提交打上标签。

```shell
git tag -a v1.0
```

`-a`表示的是创建一个带有注解的标签。





## 实例

利用terminal建立一个文件夹，之后进行`git init`初始化一下。

```shell
mkdir <filename>
```

新建一个readme文件，其中的filename是文件名。

```
touch README
```

之后需要进行`git remote`来链接上我们的github。注意这里要使用上github在2021年的修改之后的token，先在setting中获得一个，注意保存，只有显示一次。

```
git remote set-url origin https://<your_token>@github.com/<USERNAME>/<REPO>.git
```

之后就可以进行`git pull`和`git push`等操作了。

我们在先把想要提交的放在缓存区：

```shell
git commit -m "deliever_time"
```

之后`git push`

若创建了多个分支，就需要在对不同的分支进行切换：

```
git checkout(branch)
```

之后的commit和提交都是在这个分支之下实现。注意，当你切换分支的时候，Git 会用该分支的最后提交的快照替换你的工作目录的内容， 所以多个分支不需要多个目录。

也就是在我们之前所说的那样，在拍照片，分支管理就像用不同的相机拍下不同的照片，比较的还是这个镜头时间前后的差异。









### 重新关联
注意：现在的github的默认分支为main：在提交的时候使用`git push origin main`实现。

之前发现一直会报错，后来发现是因为关联github仓库的时候出错。

`github remote -v`来查看远程仓库信息，仓库名称、关联地址。

```shell
git remote remove orign #可删除orign仓库（比如名称错误）

git remote add origin #仓库地址：重新添加远程仓库地址

gti push -u origin master： #提交到远程仓库的master主干
```

---

一个讨巧便捷的方法是下载github官方应用，直接进行点点点操作即可完成一整套的流程。不过，在使用这些便捷操作之前，还是需要掌握一些github背后的一些原理。


## Resources

- https://www.runoob.com/git/git-branch.html
- https://missing-semester-cn.github.io/2020/version-control/

- https://blog.csdn.net/yjw123456/article/details/119696726

- https://www.freecodecamp.org/chinese/news/git-and-github-for-beginners/
