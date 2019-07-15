---
layout: post
title: "【笔记】原核生物CRISPR分子机制"
categories: 生物基础
tags:  CRISPR 
keywords: CRISPR
description: 
---

* content
{:toc}


CRISPR基因编辑技术在生物研究领域已成热门，无论是否使用该技术，如果不了解就是落伍了。今天学习的内容主要是CRISPR-Cas系统的前世今生和功能实现。





### 先来看视频

这位小哥讲得非常生动、清楚，我反反复复看得五六遍。

<video width="320" height="240" controls>
   	<source src="http://o7zaxp1i2.bkt.clouddn.com/What%20is%20CRISPR.mp4" type="video/mp4">
   </video>

### 什么是CRISPR-Cas系统?

- 全名：Clustered Regularly Interspaced Short Palindromic Repeats 成簇的、规律间隔的、短回文、重复序列(CRISPR)& CRISPR-associated genes (Cas)

- CRISPR-Cas系统： 是在细菌(>50%)和古菌(>90%)中广泛存在的对外源病毒和质粒具有特异性抗性的、 获得性免疫系统。CRISPR 由短的高度保守的重复序列(repeat)和各不相同的间隔序列(spacer)组成 。Repeat多具有回文结构。Spacer与外源DNA（ 如质粒或病毒） 同源。由CRISPR转录加工形成的crRNA,可通过与Cas功能蛋白形成复合物，特异识别和消除入侵细胞的外源质粒或病毒。 
![0](http://o7zaxp1i2.bkt.clouddn.com/d99e2932-9dd5-4f67-b08f-8346f4fbe1f3.png)
![1](http://o7zaxp1i2.bkt.clouddn.com/32cad66d-d001-4965-a357-a838ea20df84.jpg)
![2](http://o7zaxp1i2.bkt.clouddn.com/8a29c491-89a4-4198-9b9a-7e50196703c8.jpg)


上图是最新的CRSPR-Cas分类系统，共六类。

### CRISPR-Cas发现之旅

以下图片来自中科院微生物所向华老师的《古菌遗传与分子生物学》课程课件。就像课件里所说的，了解一个领域的科学史，理解每个突破性发现的背景，对于启迪科学研究具有重要意义。从以下几张片子里我不光对CRISPR-Cas的研究历史有了清晰地了解，而且更大的收获是严谨的科学态度，假如我从事一个领域的研究，也应当像这位老师一样对自己领域的前世今生有着透彻地认知。
![3](http://o7zaxp1i2.bkt.clouddn.com/5a7ee53d-8e38-4a7d-bf13-af8b1f730e3a.jpg)
![4](http://o7zaxp1i2.bkt.clouddn.com/2016-12-03_205936.png)
![5](http://o7zaxp1i2.bkt.clouddn.com/2016-12-03_183225.png)

### CRISPR功能实现的三个阶段

用学过的抗原抗体免疫通俗的比喻CRISPR系统：

![15](http://o7zaxp1i2.bkt.clouddn.com/6a3c8fd5-92e7-4c8a-be6d-352ff54926f6.jpg)

外源DNA就是坏蛋，而抓住坏蛋特征这一最核心的步骤之一则是--靠的Cas复合体将片段特征proto-spacer制作成spacer，整合进CRISPR序列中，形成记忆。于是接下来的2次免疫中，spacer便可以快速bingding到proto-spacer上。完成这一target的精确打击过程。干掉入侵者。

![16](http://o7zaxp1i2.bkt.clouddn.com/7c1c4209-9463-4781-ace4-204be2a94188.jpg)

#### 第一个阶段：外源性DNA的采集（Foreign DNA Acquisition）

当噬菌体病毒侵入宿主细菌后，病毒dsDNA被注入细胞中。此时，Cas1/2蛋白可识别外源DNA原间隔序列临近基序（PAM，通常由NGG三个碱基构成，N为任意碱基），并将原间隔序列（protospacer）剪切下来。之后Protospacer可插入到CRISPR序列前导区的下游中，完成外源DNA的捕获。

#### 第二阶段：crRNA的合成（crRNA biogenesis）
在I型和III型系统中，初始CRISPR转录产物（Pre-crRNA）会被CRISPR特异性核酸内切酶（Cas6 / Cas5d）在重复序列位点内切割形成成熟的crRNA。在II型系统中，Pre-crRNA可通过重复序列与其互补序列transacting RNA（trancrRNA）反式结合，然后在Cas9存在的情况下被RNaseIII加工融合成一个sgRNA。目前，II型系统是最成熟也是应用最广的类型，而Cas9已经变成了在多种细胞类型和组织中靶向基因编辑的强大工具。

#### 第三阶段：靶向干扰（Target interference）

I型和II型系统均可靶向含有与PAM和protospacer互补序列的dsDNA底物。不同的是，在I型系统中，通过含有多个亚型的复合物结合到dsDNA，并招募反式核酸酶Cas3对DNA进行靶向干扰。在II型系统中，则通过Cas9蛋白的HNH酶活性剪切crRNA互补的DNA链及其RuvC活性位点剪切非互补链，促使dsDNA断裂。类似于I型系统，III型系统也同样依赖于具有核酸酶活性的多亚基复合物对靶向DNA进行干扰，但不同于I型和II型系统，III型系统不依赖于PAM进行靶标位点的识别，而是通过碱基互补配对来识别靶序列并进行DNA的裂解。

#### Closing the Loop

In type I systems, target binding by the surveillance complex results in Cas3-mediated target degradation (direct interference直接干预) or primed acquisition, which involves crRNAguided recruitment of Cas3, Cas1, and Cas2 to foreign DNA and results in rapid acquisition of new spacers into the CRISPR (Datsenko et al., 2012; Sorek et al., 2013). While primed acquisition has not yet been observed in type II systems, Cas9 is required for proper protospacer selection, suggesting a functional link between the target interference and foreign DNA acquisition (Heler et al., 2015; Wei et al., 2015). Recently, diverse viral-encoded genes that produce proteins known as anti-CRISPRs have been shown to subvert CRISPR systems by interfering with each of the different stages (Bondy-Denomy et al., 2015).

**以上三个步骤具体细节我还不太理解，但是大体的作用机制已经了解了。**

### 再来看视频

这里还有个视频，感兴趣的再看看，我是看了好多次。

<video  width="320" height="240" controls>
   	<source src="http://o7zaxp1i2.bkt.clouddn.com/Genome%20Editing%20with%20CRISPR-Cas9.mp4" type="video/mp4">
   </video>

### 参考链接

[What is CRISPR?](https://www.youtube.com/watch?v=MnYppmstxIs)

[SnapShot: CRISPR-RNA-Guided Adaptive Immune Systems](http://www.cell.com/cell/pdf/S0092-8674(15)01131-9.pdf)

[Biology and Applications of CRISPR Systems:Harnessing Nature’s Toolbox for Genome Engineering](http://www.cell.com/cell/pdf/S0092-8674(15)01699-2.pdf)

[CRISPR Cas](https://felixfan.gitbooks.io/pm/content/chapter%2015.html)

[云生信:你真的了解CRISPR吗？](http://mp.weixin.qq.com/s?__biz=MzAwNjE0MDY3MQ==&mid=2650694339&idx=1&sn=ba4c655993fd01954be56c091203fa68&chksm=831b2553b46cac4546ca1781d2a0c0c0fcc129b2c3b7ef93ef62bd1672e980a8da6a62545585&mpshare=1&scene=23&srcid=1203BowYfom0iNREqefhOQRa#rd)

