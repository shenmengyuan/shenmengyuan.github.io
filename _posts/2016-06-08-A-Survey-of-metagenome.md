---
layout: post
title: "【笔记】宏基因组学之初识"
categories: 微生物组学
tags: 宏基因组 
keywords: metagenome 宏基因组
description: 宏基因组学之初识
---

* content
{:toc}

![1](http://o7zaxp1i2.bkt.clouddn.com/1.jpg)

上图是我第一次看见二师兄用R做出来的图，当时的感觉就好漂亮，当时在场的李老师给解释了半天，说每个Group是个颜色等等。其实我当时是挺好奇的是这个图到底是怎么画出来的呢。(当时的我刚进实验室，大概只会用Excel绘制一些柱状图和饼图这些简单的统计图形。)



     
### 1 宏基因组学的基本概念梳理

宏基因组学(也称元基因组学)，是环境样品中所有微生物基因组集合的研究技术和方法。全部宏基因组测序以环
境样品中的微生物群体基因组为研究对象，直接从环境样品中提取全部微生物的DNA，构建宏基因组文库，利用高通量测序技术分析环境样品所包含的全部微生物的群体基因组成及功能和参与的代谢通路，解读微生物群体的多样性与丰度，探求微生物与环境，微生物与宿主之间的关系，发掘和研究新的、具有特定功能的基因。（我们实验室研究湖泊环境中是菌藻共生关系，因此我们在采样的时候把其他原生动物过滤掉了。）另外16S/18S 
rDNA测序则是以细菌16S rRNA 或者真菌18S rRNA 基因测序为主,
核心是研究样品中的物种分类、物种丰度以及系统进化。

![2](http://o7zaxp1i2.bkt.clouddn.com/process_of_metagenomics.jpg)

### 2 宏基因组学研究的内容
    1 Who is there? 
    2 What are they doing? 
    3 Who is doing what? 
    4 How do they interact with their environments?(Integration with metadata) 
    就是通过宏基因组学测序可以知道一个环境群体里的到底有谁在？它们每天的工作是什么？它们是如何工作的？
	
![3](http://o7zaxp1i2.bkt.clouddn.com/mg.jpg)

- Integration with metadata:
Combining biogeochemical data with organism abundace makes habitat preferences apparent.(Walsh *Science* 2009)
![4](http://o7zaxp1i2.bkt.clouddn.com/11.jpg)

### 3 宏基因组学的分析流程

宏基因组学大数据分析的各个环节都需要运用信息学和生物信息学技术(下图)。首先是大数据的存储，包括环境样品的采集(采集地点、样本类型、地理环境、气候季节等)和处理信息(实验条件、处理时间等)， 样品的地球物理化学参数， 测序信息(测序反应条件、测序仪器、测序深度等)和大量的序列数据；经过分类和整理之后的数据，需要进入标准化的数据库进行保存，以备后续分析使用。其次是大数据的前处理，即海量序列的基础分析，包括序列质量控制、序列拼接、序列的物种分类学分析、序列功能的预测和相对定量分析。大数据的前处理是宏基因组学研究的基础，其速度和准确性都将对实验进度和最终结论产生很大影响。最后，经过基础分析的数据需要进一步进行信息分析、比对与提炼，进而分析微生物的群落组成与多样性、群落功能与遗传变异、群落结构与物种间的相互关联、群落与环境的相互作用，最终为环境变化的预测和治理提供理论依据。

- 环境微生物宏基因组学研究中的生物信息学方法（邓晔 *微生物学通报* 2015）

![5](http://o7zaxp1i2.bkt.clouddn.com/9.jpg)
![6](http://o7zaxp1i2.bkt.clouddn.com/8.jpg)
- Recovering complete and draft population genomes from metagenome datasets (Sangwan et al. *microbiome * 2016)

总体上说宏基因组学分析工具正在不断地进步，优秀的分析工具也越来越多，但是there is no clear winner that suits all situations。并且在不久的将来，群体转录组、蛋白质组和代谢组数据的整合分析成为可能。也许最重要的多组学整合分析是建立预测模型来识别不同物种之间独有的代谢交流。

![7](http://o7zaxp1i2.bkt.clouddn.com/6.png)
![8](http://o7zaxp1i2.bkt.clouddn.com/12.png)
![9](http://o7zaxp1i2.bkt.clouddn.com/13.png)

- Metagenomics：Tools and Insights for Analyzing Next-Generation Sequencing Data Derived from Biodiversity Studies（Anastasis oulas *Bioinformatics and biology insights* 2015）
单细胞测序技术的发展，可以使用单细胞基因组协同辅助宏基因组分析，已到达更精确区分每个物种的基因组。
误差会由许多不一致的因子产生，例如DNA提取的方法、引物和扩增区域、测序平台、使用的软件等。正因为误差的存在，通过两个群落宏基因组之间的比较很难取得可信的结果。
![10](http://o7zaxp1i2.bkt.clouddn.com/7.png)

补充软件：
Assembly:
Minia/HiPmer/ALE/SoAPdenovo2/sPAdes V3/iMetAMOS/MeGArge/GAM-NGS/Ray/minimus-2/MeGA-Merge/CAP3/
Bining:
MetaBAT/MaxBin/ABAWACA/CONCOCT/GroopM/
Annotation:
MetaPhlAn 2.0(在nature method上发表的)
![11](http://o7zaxp1i2.bkt.clouddn.com/2.png)
Functional metagenomics of extreme environments（Salvador Mirete *ScienceDirect* 2016）
![12](http://o7zaxp1i2.bkt.clouddn.com/4.jpg)
Mitochondrial metagenomics:letting the genes out of the bottle(Crampton-Platt et al. *GigaScience* 2016)
质粒宏基因组
![13](http://o7zaxp1i2.bkt.clouddn.com/f701907d-fa0d-49e6-a216-7941916c0722.png)

### 4 群体分析面临的挑战

#### 4.1 技术障碍

- 大量的数据但覆盖度低   
- 拼接和注释对计算的需求高  
- 拼接、注释、分箱的质量不确定

#### 4.2 概念障碍

复杂的数据在噪音识别困难
数据拥有固有的多维，每一段序列属于某个生物并且具有功能；

### 5 其他概念摘要

#### 5.1 预测编码基因

目前发现编码基因的方法有两种。一种是基于BLAST比对的方法，这种方法通过比对已有的数据库，可以发现宏基因组数据中有哪些已知基因的同源基因的存在，但缺陷是找不到那些和已经基因没有同源关系的新基因。第二方法是重新预测基因的方法，这些方法大部分是基于有指导学习和统计模式识别的方法，包括隐马尔科夫模型。GeneMark.hmm就是基于单密码子频率的非均一马尔科夫模型来预测基因的软件，当这些软件用到宏基因组数据上时，这些软件通常无法确定部分的ORF,即使这些 ORF是真实基因的一部分。

#### 5.2 衡量样本中物种的多样性

     为了估算测序的物种的比例，通常用rarefaction curse来表示。

#### 5.3 菌群间差异分析

有几种基于序列特征的比较，包括样品间GC含量的比较，微生物基因组大小的比较，系统发育关系树的比较和功能组分的比较。许多比较分析都用到了关联统计学的方法，通常假设有几种元数据影响观测到的宏基因组群体的组分。主成分分析（PCA）和非度量多维标度（NM-MDS）用来图形化展示数据并揭示有哪些因素最影响数据。有几种进行宏基因组比较分析的软件：第一个是MEGAN， 可以比较两个或几个标准化后的样品的GC含量；第二种是MG-RAST，提供了一种比较功能和基于序列的分析来上传样本；第三种是CAMERA，提供了BLAST接口让客户可以比对40多种现有的宏基因组数据。

#### 5.4 宏基因组做De Novo拼接

由于宏基因组测序的覆盖率通常是不完全的，所以组装所需要的序列并不是很完整。并且组装的时候，可能会把来自不同分类单元（OTU）的序列组装在一起，产生嵌合体基因组。Phrap,Forge,Arachne,JAZZ和Celera Assembler等可用来组装由sanger法产生的宏基因组序列。这些算法大部分都利用mate-pair信息来参与组装。这些算法用顶点来代表每条read,互相重叠的read之间用边连起来，它们的组装问题可以转换成“哈密尔顿路径”搜索问题，即找到一条路径走过所有顶点，且每个顶点只走一次。

#### 5.5 估计宏基因组样本中的物种组成及丰度

宏基因组中的物种分类，一般用OTU (operational taxonomic unit), 即可操作物种单元，来表示。在典型情况下，原核生物的OUT使用16S rDNA来衡量，真核生物的OUT使用18s rDNA来衡量。但选择16S/18S rDNA鉴定物种，存在以下几个问题：1）rDNA之间的平行转移来干扰rDNA鉴定的可靠性。2）在单个细菌中，16r DNA可能存在序列不同的几个拷贝，干扰估计OTU数目的准确性。所以，其他备选的标记基因，比如单拷贝的看家基因被推荐用来作为菌种鉴定的标记。

#### 5.6 代谢通路

代谢通路分析是为了研究某一个环境中各种代谢途径的富集程度。一般需要根据统计检验方法（如P-value）来筛选。常用的代谢通路数据库有KEGG、Reactome、BioCyc、 RegulonDB、 WikiPathwans等。

### 写在最后

随着相关软件的开发及测序技术的发展，宏基因组的研究会不断地向前发展。我觉得地球环境宏基因组计划、人类微生物宏基组计划等等，他们所做的工作都非常的有趣，有意义。尤其是最后将研究结果应用到实际生活中，建立地球环境变化预测模型、指导人类日常生活都激发了我对该学科的研究兴趣。希望未来我也能够做出有价值的研究。