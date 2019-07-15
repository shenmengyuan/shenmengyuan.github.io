---
layout: post
title: "【笔记】宏基因组学之向前一步"
categories: 微生物组学
tags: 宏基因组
keywords: metagenome 宏基因组
description: 宏基因组学之向前一步
---

* content
{:toc}

紧接着上个星期学习初步认识了宏基因组学的基本概念、了解的宏基因组数据分析方面的软件。我继续深入学习，这里是学习TGAC宏基因组教程的学习笔记。[TGAC Metagenomics 2015教程](https://github.com/TGAC/361Division/tree/master/Metagenomics%202015)




### 内容

#### 组学项目研究成本

     随着测序技术的发展，测序成本会逐渐下降，在未来下游的生物信息数据分析将成为整个组学实验项目中的最高成本因素，也是最为重要的一个因素。

![1](http://o7zaxp1i2.bkt.clouddn.com/2016-6-15-1.png)

#### 宏基因组研究基本流程

![2](http://o7zaxp1i2.bkt.clouddn.com/2016-6-15-2.jpg)
![3](http://o7zaxp1i2.bkt.clouddn.com/2016-6-15-3.jpg)

Morgan XC, Huttenhower C (2012) PLoS Comput Biol 8(12): e1002808. 

#### 宏基因组数据处理典型流程

![4](http://o7zaxp1i2.bkt.clouddn.com/2016-6-15-4.jpg)

#### 三个基本数据处理问题

- 有什么？
- 干什么？
- 有啥不一样？

![5](http://o7zaxp1i2.bkt.clouddn.com/2016-6-15-5.jpg)

#### MEGAN-MEtaGenome ANalyzer

     MEGAN不仅可以处理宏基因组数据还可以处理宏转录组、宏蛋白质组以及扩增子测序产生的数据。序列比较是整个一个计算瓶颈。

![6](http://o7zaxp1i2.bkt.clouddn.com/2016-6-15-6.jpg)

#### 比较宏基因组学

- 1 想要了解微生物群体结构随着时间和地理环境的变化，以及通过比较不同个体、不同时间点、不同药物作用时微生物的变化与疾病的相关性，因此比较基因组学是一个很好的研究工具。
![7](http://o7zaxp1i2.bkt.clouddn.com/2016-6-15-7.png)
- 2 宏基因组并不是呈现树状进化的。
![8](http://o7zaxp1i2.bkt.clouddn.com/2016-6-15-8.png)
- 3 相关性分析
![9](http://o7zaxp1i2.bkt.clouddn.com/2016-6-15-9.png)
![10](http://o7zaxp1i2.bkt.clouddn.com/2016-6-15-10.jpg)

#### 比对到NCBI-NR蛋白参考库，更快更好的软件
     已经有的工具：BLASTX、RAPSearch2，2015年nature methods上发布了一款新的比对软件DIAMOND，据说更快更灵敏。一般宏基因组拼接完后进行blast，造成数据减少；现在可以通过DIAMOND比对后再进行拼接。并且还可以进行核心基因的拼接：将每个基因拼接到一起，然后使用DIAMOND比对到蛋白序列，最后将比对到的基因拼接到一起。
     
![11](http://o7zaxp1i2.bkt.clouddn.com/2016-6-15-11.png)

### 写在最后
     生物信息的学习重在实战，我在专业领域基础知识的同时也开始了数据模仿处理的项目实战（奶酪宏基因组），并且已经拼接完成。在此感谢提供学习资料的生信菜鸟团群主健明师兄以及李琪师兄和杨耀华师兄的指点。
     
