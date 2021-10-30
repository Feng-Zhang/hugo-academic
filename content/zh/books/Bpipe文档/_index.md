---
# Course title, summary, and position.
linktitle: Bpipe
summary: Bpipe中文文档，翻译于Simon P. Sadedin 网站"http://docs.bpipe.org"。
weight: 1

# Page metadata.
title: Bpipe 文档
date: "2021-10-28T00:00:00Z"
lastmod: "2021-10-30T00:00:00Z"
draft: false  # Is this a draft? true/false
toc: true  # Show table of contents? true/false
type: book # Do not modify.

---

## 关键英文翻译
英文 | 中文
--- | ---
stage | 阶段
pipeline | 流程
job | 任务
reference | 引用
evaluation | 取值


## 欢迎来到Bpipe世界

Bpipe提供了一个运行大型生物信息学分析的平台，该工作平台由一系列处理阶段（也就是常说的“流程”）组成。

- 2021年9月-Bpipe 0.9.11版本发布了！
- 下载[最新的](http://download.bpipe.org/versions/bpipe-0.9.9.9.tar.gz)或[其它的](http://download.bpipe.org/)版本。
- [英文文档说明](http://docs.bpipe.org/)
- [邮件列表](https://groups.google.com/forum/#!forum/bpipe-discuss)（Google网络论坛）

此外，Bpipe已在[Bioinfomatics](http://bioinformatics.oxfordjournals.org/content/early/2012/04/11/bioinformatics.bts167.abstract)中发表！如果您使用Bpipe，请引用：

*Sadedin S, Pope B & Oshlack A, Bpipe: A Tool for Running and Managing Bioinformatics Pipelines, Bioinformatics*

## 为什么选择Bpipe？

很多从事生物信息学数据分析的人最终都会将流程写成shell程序脚本运行。尽管这使它们易于运行，但有很多限制存在。比如，脚本中途失败时，通常很辨别它们在哪里或为什么失败，甚至修复问题后从失败的地方接着运行脚本也很困难，需要把前面的代码注释掉。没有自动记录已执行的命令或自动捕获控制台的输出记录，以确保后面可以查看运行情况。有时脚本会在中途失败，这些失败的文件可能会与已经成功的文件混淆。而修改脚本也很耗时且容易出错，需要在多个位置进行添加或删除步骤，比如文件名。这意味着更改文件名太容易了，很容易导致后面的命令失败或对不是你需要的文件上进行分析。Bpipe试图解决所有这些问题（还有更多问题！），同时尽可能地不修改Shell脚本。事实上，您的Bpipe脚本通常看起来与您最初使用的原始Shell脚本非常相似。

通过将您的shell脚本转换为Bpipe脚本，您可以获得以下一些功能：

- **对运行的任务进行简单的定义**：Bpipe几乎与原始的shell命令相同，且无需额外的编程基础。
- **简单方便的任务管理系统**：失败命令时结果文件会被清理，日志文件会保留，并彻底中止脚本运行。
- **不同管道的自动连接**：Bpipe 会以系统的方式管理每个阶段的输入和输出的文件名。删除或添加新阶段仅仅是增加或删除一个模块而已，不会干扰到整个流程。
- **轻松重启整个流程**：当脚本失败时，可以从故障点干净地重新启动整个流程。
- **轻松并行**：通过Bpipe，可以轻松地将任务拆分为多个部分，并在群集中或本地计算机上并行运行。
- **进程跟踪**：Bpipe准确记录执行了哪些命令以及它们的输入和输出是什么，并保存到日志文件中。
- **集成了集群的资源调度系统**：如果您使用Torque PBS，Oracle Grid Engine或Platform LSF，Bpipe允许您轻松地在集群上运行，而不用修改本地的Bpipe脚本。
- **电子邮件，即时消息，消息队列系统进行通知**：Bpipe可以向您发送消息告知您管道何时完成，甚至是每一个阶段的完成情况。
- 了解Bpipe与[同类工具](http://docs.bpipe.org/Overview/ComparisonToWorkflowTools/)的比较

最后建议查看[简介](http://docs.bpipe.org/Overview/Introduction/)以了解Bpipe的大概特性，通过[基本教程](http://docs.bpipe.org/Tutorials/Hello%2CWorld/)对Bpipe进行初步了解，也可以学习制作好的[Bpipe流程例子](http://docs.bpipe.org/Examples/PairedEndAlignment/)，或者查看[语法内容](http://docs.bpipe.org/Language/About/)。