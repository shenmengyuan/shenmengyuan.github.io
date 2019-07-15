---
layout: post
title:  "【笔记】韦恩图的简单绘制"
categories: 编程之美 
tags: 韦恩图   
keywords: R 韦恩图
description: 用R绘制韦恩图
---

* content
{:toc}

![1](http://o7zaxp1i2.bkt.clouddn.com/five.png)





### 1 写在前面：
 VennDiagram，简称文氏图，又称为韦恩图，是一种非常常用的图示手段，主要用于显示组与组之间重叠的程度
 。R中提供了多个可用于绘制韦恩图的软件包，本文主要是介绍的是VennDiagram包.函数venn.diagram是利用集
 合作为参数绘制韦恩图的，但是有时候我们并不知道各个集合都包含什么元素，而只知道集合及相互之间交集的
 大小，这个时候如何绘制韦恩图呢？包VennDiagram还给我们提供了另外几个函数：绘制两个集合的韦恩图的dra
 w.pairwise.venn，三个集合的draw.triple.venn，四个、五个集合的draw.quad.venn、draw.quintuple.venn。
 (此处有个疑问我要画超过五个的韦恩图怎么办呢？二师兄说存在第三方软件包，可以达到这个目的，事实上不
 用到画那么多五个集合的韦恩图。
 后来我查了似乎 Vennerable 这个包可以，最多可画9个集合。)
[软件链接](https://github.com/js229/Vennerable)

### 2 一个例子
2.1 现有已有叶/茎/叶三个基因列表，绘制韦恩图。

自己创建集合时，要注意文件里面不要加入空白行。

2.2 网页版的韦恩图绘制工具

【1】[http://bioinformatics.psb.ugent.be/cgi-bin/liste/Venn/calculate_venn.htpl](http://bioinformatics.psb.ugent.be/cgi-bin/liste/Venn/calculate_venn.htpl)

【2】[http://www.pangloss.com/seidel/Protocols/venn.cgi](http://www.pangloss.com/seidel/Protocols/venn.cgi)

2.3 使用R包VennDiagram，绘制韦恩图

```
leaf<-unlist(read.table("Leaf_gene.txt"))
stem<-unlist(read.table("Stem_gene.txt"))
root<-unlist(read.table("Root_gene.txt"))
library(VennDiagram)
venn.plot<-venn.diagram(list(leaf=leaf,root=root,stem=stem),col = "transparent",
fill = c("red", "green", "yellow"),alpha =c(0.5,0.5,0.5),
scaled = TRUE,ext.text = TRUE,ext.line.lwd = 2,ext.dist = -0.15,ext.length = 0.9,ext.pos = -4,
inverted = TRUE,cex = 2.5,cat.cex = 2.5,filename = "venn.tiff",main = "Venn Diagram",
sub = "Leaf_Root_Stem",main.cex = 2,sub.cex = 1)
```

![2](http://o7zaxp1i2.bkt.clouddn.com/example.png)

### 3 写在最后

具体的[代码和文件](http://pan.baidu.com/s/1hrINnd6)存放在百度云里，可以下载练习一下。

