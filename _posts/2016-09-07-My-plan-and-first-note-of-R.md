---
layout: post
title:  "【R】我的R学习计划"
categories: 编程之美
tags: 生信 R语言 
---

* content
{:toc}

这几天实验室服务器瘫痪了，今天上午瞄了几眼python，后来想想自己perl学得不怎么样，还有shell脚本、sed、awk都没好好学习呢，还是算了，了解了解就行了。还有去年9月份看了1个月的R语言，右脚还在门外。想想就好伤心，一年了竟然什么都不精通。从今天开始都要有计划、系统得学习生信，同时结合手上两个宏基因组的项目，好好学习！！！先从R语言开始，今天下午和晚上倒腾了一下，做了一些学习摘记和初步计划。





### 遇到的小问题
- windows下Rstudio控制台中文乱码如何解决：
在R中设定 Locale
      \> Sys.setlocale("LC_ALL","Chinese") 
- 如何安装bioconductor上的包：
source("https://bioconductor.org/biocLite.R")
biocLite("XXXXX")

*** 

### RNA-seq数据基因水平表达差异分析
学习了一下糗世界博主的文章[RNA-seq数据基因水平表达差异分析](http://blog.qiubio.com:8080/archives/3777)，下面是我看得懂的部分做了一些摘记。

- 介绍Bioconductor中三种包（edgeR, DESeq2以及voom）对RNA-seq数据进行分析；

- 获取基因水平表达差异结果主要分三步：记数(counts) -> 质量控制(diagnostics) -> 统计分析(statistics)；

- 如果只是RPKM或者FPKM值的话，可以使用anova来处理。现在没有软件直接处理这种数据的；

- 无论多么复杂的设计，都可以按照其说明书来进行操作。在设计matrix的时候，你可以参考limma的说明文档；

- 样品内标准化的概念是由microarray带来的。一般而言，基因芯片因为染色不均和杂交不均，所以同一芯片内不同区间需要进行标准化。而这种技术上的障碍并不存在于RNA-seq上，所以在RNA-seq的结果比较中，不讨论样品内标准化的问题。使用RPKM并不是很好的选择。RPKM的标准化方法是在library size的基因上再对基因长度做了标准化，以达到不同基因间也可以相互比较的目的。但是，它的false positive rate会不如TMM以及DESeq2的好。

### 学习计划
今天时间比较晚了，暂时先粗略写了几点简单的安排，后续再添加。

- R基础和绘图的巩固、练习（14天）
- R进阶和统计基础的学习、练习（14天）
- Bioconductor包的学习、练习（14天）


![1](http://o7zaxp1i2.bkt.clouddn.com/5a5290c1-3dcb-4c62-821f-6a5fae39d980.png)