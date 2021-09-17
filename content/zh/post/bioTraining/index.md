---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "生物信息最佳入门实践路线图"
subtitle: "生信是一门交叉学科，要学习的东西非常多。如何快速入门是个问题，本文提供了一些入门的路线图。"
summary: "生信是一门交叉学科，要学习的东西非常多。如何快速入门是个问题，本文提供了一些入门的路线图。"
authors: [风不止]
tags: ["生信","生物信息","入门","教程","路线图","实践"]
categories: [生信]
date: 2020-10-10T09:23:30+08:00
lastmod: 2020-10-10T09:23:30+08:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: "生信入门路线图"
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---



{{% toc %}}

# 生物信息最佳入门实践路线图

### 介绍

　　生信是一门交叉学科，要学习的东西非常多。本人至2011年开始学习，深知生信的博大精深。因此，给大家推荐一些学习资料。由于我是一位喜欢阅读多过视听学习的人，所以书籍都是亲自阅读过的，但是视频并没有认真看过。

　　下面这张图展示了生信学习的路线图。一开始可能就是学习一门编程语言，首选R语言，然后是python。其次如果你要处理大量测序数据，你得学习linux操作系统。接着最重要的一步是：利用项目进行实践。最后是利用你的生物学知识来解释你的分析结果。

　　其实生信这一领域或者说计算机这一领域最重要的一个能力就是**学习**。学习怎么搜索问题和答案并亲自去尝试。得学会怎么高效搜索，可以google, bing, QQ群，论坛（如[stackoverflow](https://stackoverflow.com)），老师和同学等。大部分问题都可以在网上得到解决，你肯定不是第一个碰到问题的人。然后是在QQ或论坛去请教，当然如果你身边有学生信的人请教可以节省大量时间。

　　所有资料我都尽量用开源免费的，这样省掉很多学习成本。另外有一些收集的pdf书籍放在百度云上，[链接](https://pan.baidu.com/s/1RyV2Mlm1fuUEroJAIzeXsw)，提取码：bioT。如果失效了请在最下方的评论区提醒一下。

![](https://raw.githubusercontent.com/Feng-Zhang/figures/master/blog/生物信息数据分析.png)

### R语言

如果你想快速入门深信，请**必学**R语言。这是一门开源的编程语言，主要优势在于统计和绘图，以及极其丰富的软件包。

#### R语言资料

- 如果你是一位喜欢视听学习这种方式的，请参考[生信技能树的生信人应该这样学R语言](https://www.bilibili.com/video/av25643438)。

- 如果你是一位喜欢阅读学习这种方式，请参考**R for beginners**和**R现代统计图形**。如果你有余力还可以学习**R语言实战**及**ggplot2:数据分析与图形艺术**等深入内容。

- 最后进行这[20个R语言习题](http://www.bio-info-trainee.com/3409.html)进行实践，加深印象。如果你没有时间，而且入门资料都能看得懂，也可以跳过这步，在项目实践阶段结合自己课题进行练习。



### linux

如果要对上机后的原始数据进行分析的话，你一定得学会Linux。如果你不用处理多组学数据的原始序列，那么这个可以跳过。

- 入门视频：https://www.bilibili.com/video/av28813815

- 书籍：**鸟哥的linux私房菜**。

- linux 实践：http://www.bio-info-trainee.com/2900.html



### python

python是一门胶水语言，基本上什么都干，尤其是在机器学习方面。目前很多机器学习和神经网络的开源项目都是用python写的，如果你有兴趣往这方面发展。python是非学不可的。

- 编辑入门：[笨办法学 Python](https://wizardforcel.gitbooks.io/lpthw/content/)
- 机器学习入门：python机器学习基础教程（Andreas C.Muller and Sarah Guido著， 张亮译）
- 神经网络入门：[Python深度学习（Francois Chollet 著， 张亮译）



### 项目实践

目前没找到好的开源项目进行实践，这个跟课题组的研究内容相关。不过下面列出一些组学的内容可以用来实践。

- 转录组：https://www.bilibili.com/video/av28453557
- 单细胞组：https://www.bilibili.com/video/av38741055

本人目前在做肿瘤免疫的生信分析，分享一些文献进行具体实战。链接：https://pan.baidu.com/s/10nUWgVR4SRT83Qwmwuy0pg 
提取码：qapd 


