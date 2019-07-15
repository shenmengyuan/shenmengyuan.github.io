---
layout: post
title: "【笔记】宏基因组论文《Assembling the microbial dark matter》阅读笔记"
categories: 微生物组学
tags:  宏基因组 
keywords: 宏基因组
description: 
---

* content
{:toc}


《Assembling the microbial dark matter》是比勒费尔德大学一位博士的毕业论文，该博士论文主要利用单细胞测序技术、宏基因组和宏转录组学技术来研究biogas反应器中的微生物群体，结合多种组学技术来对不能培养的微生物进行基因组拼接及代谢通路分析。




![1](http://o7zaxp1i2.bkt.clouddn.com/IMG_2949.JPG)

### 前言

近来对于微生物的研究，比较重视抗生素耐药性，却忽视了对新的抗生素的开发与探索。几乎现存所有的抗生素来源于海洋、土壤中的放线菌门。将宏基因组、宏转录组、宏蛋白质组以及单细胞数据进行整合分析具有极大的价值。

### 可重复性

心理学和癌症领域发表的研究可重复率分别为39%、11%，非常低。在生物信息工作中，在不同的服务器，使用不同的软件版本，甚至一切都相同的条件下多次运行相同的命令都会出现不同的结果。因此，在生信工作中，应当详尽地记录所采用的工作平台参数、软件版本及具体参数命令。
![1](http://o7zaxp1i2.bkt.clouddn.com/0f6eea52-4a68-4cc1-ab29-316562a328c9.png)

### 单细胞基因组

在宏基因组中，基因组的覆盖度取决于其丰度。宏基因组和单细胞基因组结合，互相补充完善拼接。
![2](http://o7zaxp1i2.bkt.clouddn.com/493f2d36-d533-47ed-8ad2-3f1828c605b9.png)

### 宏基因组拼接和分箱技术

- 挑战：（拼接高质量的基因组是很难的）宏基因组数据量大；每个物种的覆盖度不一致；基因组范围的复制体（例如rRNA基因）会比一般的reads长并且很难解决（去重复？）

- 接近完整的基因组，可以用来研究代谢。但是，尽管使用了表征结果做好的工具来完成工作了，也还是要仔细检查每一个contigs的分类、可视化不同的覆盖度信息或使用自动化工具来评估宏基因组的拼接质量。

### 例子1：宏基因组和宏转录组的分析

- 可使用Picard工具来估计插入片段的大小；

- 读长155~160bp左右，使用IDBA-UD,MEGAHIT,Ray Meta进行拼接，k-mer值从12-61，间隔10。最后选择Ray Meta（k-mer 31的结果）

这里的问题是，我查阅的资料建议k-mer的设置在1/2~2/3的reads长度最佳，因为设置太短，拼接完成后的短序列会太多，设置太长的话则结果的就都是长contigs偏多。**但是人家肯定也是经验值，肯定不会乱设置的。**

- 将过滤后的数据reads比对至拼接好的contigs,从而计算比对率。工具：Bowtie2和SAMtools。

- 基因预测采用的是Metaprodigal，接着比对到KEGG数据库（这个要钱的）e值是10-6（经验值）。每个基因可能会比对到好多个KO号，选取打分最高的。

- 使用BEDTools计算每个基因的reads数（基因丰度），计算宏基因组和宏转录组的在不同甲烷类型的代谢通路上的基因的RPKM值，绘制下图分布图。

![3](http://o7zaxp1i2.bkt.clouddn.com/a5268978-62c6-47bf-bc5e-6b5d14910062.jpg)

- 使用MetaBAT对宏基因组进行分箱，再使用checkM对重构的基因组bin完整度和杂合度评估。根据经验，只选取完整度大于90%、杂合度低于10%的组。

- 宏基因组样品测了27X\19X，宏转录组测了230X。宏基因组拼接可以用来提高对群体宏蛋白质和宏代谢的研究。

- 使用Mash软件进行群体结构何相似性分析，两两比对。

- 将所有的数据放在一起进行拼接了（混合拼接）（Ray Meta k-mer 31），接着将每个样品的reads比对到大于1000bp的contigs上计算覆盖度。

![4](http://o7zaxp1i2.bkt.clouddn.com/943b7d78-4a7f-48c7-b8c0-39d02b936922.jpg)
![5](http://o7zaxp1i2.bkt.clouddn.com/11e09eff-96e5-434f-adb0-7d83263ede1d.jpg) 

- 分箱软件
![6](http://o7zaxp1i2.bkt.clouddn.com/f5c92962-031a-4143-ab80-4a46e7fadd08.png)

尝试了三种分箱软件，GroopM失败了，可能是数据集太大了。对分箱结果进行交互可视化，如下，作者说看起来不太对~~说CONCOCT的覆盖度没有比好。MetaBAT却没有这样的图表征。所以凭直觉作者选择MetaBAT的分箱结果，尽管只有22%的contigs被分箱了，其他78%被丢弃了。但这22%的contigs被分成532个bins包含了62.6%拼接？然后用CheckM进行分箱评估。

![7](http://o7zaxp1i2.bkt.clouddn.com/8ade84e5-1eea-4b8c-bbcf-1675acb1135d.jpg) 

- 分类

根据16S扩增子测序数据进行分类丰度（为什么不直接用宏基因组的数据，而是再一次进行16S扩增？）

![8](http://o7zaxp1i2.bkt.clouddn.com/ccd86046-9615-44d5-bae6-90e686ae1dbe.png)
 
其次就是鉴定分箱后的每个bin的分类鉴定，一种方法是使用DIAMOND BLASTP与非冗余蛋白库进行比对，导入MEGAN5进行分类；另一种方法就是根据序列的相似性来判断进化关系使用taxator-tk's BLASTN的方法进行分类注释，直接在每个contigs后面加上分类标签。以上两种方法都很一致。

![9](http://o7zaxp1i2.bkt.clouddn.com/bff8d814-0150-4074-bab2-a88f9dbeef3a.png)

120_Cloacimonetes的杂合度水平高，可能是因为菌株的异质性，例如同一物种的不同的菌株混到一起了。 


- 宏基因组的适用性和可靠性

糖利用通路，使用宏基因组拼全的206_Thermotogae bin被归到是Defluviitoga tunisiensis L3，该物种已经有参考基因组了，但是把参考基因组和分箱拼全的基因组一比，206_Thermotogae bin包含了几乎多有的糖利用通路模块，只有13个模块缺失。

![9](http://o7zaxp1i2.bkt.clouddn.com/f529ce03-e462-48cc-9c15-073ceeb38b3c.jpg)

**说明利用宏基因组几乎可以拼全一个基因组，但总归还是没有拼全。**

 
### 展望未来

- 宏基因组和宏转录组的覆盖度相关图，可以看出啥呢？？

![10](http://o7zaxp1i2.bkt.clouddn.com/50b097a9-36ea-45fb-bfea-2e578d1bf9b8.jpg)

- 平均每个样品60G的数据量。

![11](http://o7zaxp1i2.bkt.clouddn.com/176fd79c-8b88-47b5-9f1c-95a023d80530.png)

- 单细胞测序和宏基因组数据结合，验证宏基因组的拼接结果，此外宏基因组和宏蛋白组的整合，使蛋白分类率显著提升，可以更清晰地阐述代谢活动。

- 古细菌关注点

使用Prokka和BlastKOALA进行基因组和甲烷代谢通路的研究。古细菌群体基因组水平的代谢通路重建。

### 问题
该论文把所用的软件和数据都集成放在[docker容器](https://hub.docker.com/r/metagenomics/2015-biogas-cebitec/)里了，但是在运行的时候总是掉网，重新连起来后，容器attach不上。不想安装软件~~Ray meta安装不上~


```
docker pull metagenomics/2015-biogas-cebitec
docker run -v /home/shenmy:/home/biogas/data metagenomics/2015-biogas-cebitec
```
