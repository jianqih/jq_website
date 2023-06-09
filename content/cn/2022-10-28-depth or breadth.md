---
title: "深度优先or广度优先"
date: 2022-10-28
author: Jianqi Huang
---

在算法上有两种有名的算法，深度优先算法和广度优先算法，这两种算法的最终目的都是为了实现搜索的最终目标。对于一件事情的选择也是如此。对于一件事情，总是会考虑这个事情的两个维度：深度和广度，如何在衡量深度还是广度，很多人会认为这个是并非是一个非此即彼的问题，是需要在不断权衡中进行的，达到一个既要深度也有广度的状态。现实果真如此？

## 信息检索

举一个生活中的例子，之前在使用搜索引擎的时候，mac系统的搜索引擎都是使用的是百度的搜索引擎，之后虽然了解到chrome的一些方便，主要在插件以及自由度上（实际上的使用体验没有较大的差异）但在更换为bing搜索引擎之后，自己的dock中的浏览器就只保存了chrome。必应搜索引擎的好处在于在国际版的搜索选项，比如在正常情况下百度下的搜索一个关键词无论中文还是英文最终呈现的结果类似：

<img src="https://cheinchi.oss-cn-hangzhou.aliyuncs.com/img/Screen%20Shot%202022-10-28%20at%2001.25.06.png" alt="Screen Shot 2022-10-28 at 01.125.06" style="zoom:40%;" />

<img src="https://cheinchi.oss-cn-hangzhou.aliyuncs.com/img/Screen%20Shot%202022-10-28%20at%2001.25.33.png" alt="Screen Shot 2022-10-28 at 101.25.33" style="zoom:40%;" />

再换到bing：国内版可以看到对“bayes inference”的一个显示结果大概类似，唯二的区别在于bing中有进一步的探索和右侧的维基百科的支持(需要翻墙)

当转换到国际版之后，不一样的东西就出现了：可能是根据我的选择偏好，很快就发现了Bayes inference 的slides（第一个是计算机名校的课程slides，第二个是美国Top30的Rice 的课程slides）

![Screen Shot 2022-10-28 at 01.29.04](https://cheinchi.oss-cn-hangzhou.aliyuncs.com/img/Screen%20Shot%202022-10-28%20at%2001.29.04.png)

当我再搜索引擎中再附上关键词“pdf”对于结果上出现更多相关的大学课程slides。

不仅仅于此，信息的进一步探索：比如我在上述的CMU找到了Chapter 12 Bayes Inference点击进去，得到网站链接[https://www.stat.cmu.edu/~larry/=sml/Bayes.pdf](https://www.stat.cmu.edu/~larry/=sml/Bayes.pdf)

可以进一步的得到链接：将url后面几个路径名删去（显然larry是一个人名）得到[https://www.stat.cmu.edu/~larry/](https://www.stat.cmu.edu/~larry/)

点击进去，发现是一个Prof的个人网站，再看下网站内容下的相关链接：原来他（中文名L沃塞曼）是“All of Statistics”（已经被翻译为中文：统计学完全教程）这本书的作者！同时还能看到他其余的课程以及相关的介绍。

就这样一个简单的信息检索过程结束，对比之下，百度仅仅停留下第一个搜索过程，并没有检索深入的过程。

### 深度

进一步来说，对于这些所检索到的信息该如何处理，对于一个人在利用搜索引擎上，有可能会患有“信息饥渴症”：不停的检索、持续不断的进行收藏等分类工作，但实质性的工作并没有进行下去，也就是落入另外一头——广度。但深度的同等重要性，甚至有些时候高于广度，因为在某种程度上，深度会自然带动广度。

笔者认为在面对信息的饥渴，其本身对于信息的认识上出现偏差，信息也可以视为一种产品，当其使用量增加时也会产生边际收益递减的情况。因此可以自行的设定一个标准，给自我的信息“减枝”。比如在上述情况下，可以选择U of Rice的slides或者CMU的slides，但在信息的检索下，发现slides也是“all of statistics“作者本人，就更愿意相信larry的slides可以提供的帮助更大。也就大概率选择停止检索相关信息。

### 广度

但另一个角度来说，若你拥有你所在的领域的较高质量的信息，完全并不需要搜索引擎的改变来改善个人的信息，换句话说，信息检索只是一个提供自身信息补充的工具，但自己已经有足够高质量的信息或者目前的信息无法完全吸纳的时候，需要好好的深入下去才是更好的选择。

在一些时候，正如我之前所利用搜索引擎所提到的，搜索引擎实际上在一开始并没有认识到其对于我个人的信息获取的差异。仅仅就在一转变的瞬间，将自己的信息检索框架完全发生了转变。也就是说，信息检索工具的充分信息尽管我有所了解（之前也知道bing的搜索引擎，现在也知道一些其他的搜索引擎）但仍然会停驻于此，只是有某个偶然的契机让我实际的体验之后才得以进行更深入的判断。**在生活中这样的问题比比皆是，仅仅不过想要停驻于当下，不愿踏出半步，未曾想在多出的半步却是一片广阔的天地。**

