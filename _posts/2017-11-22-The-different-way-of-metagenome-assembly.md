---
layout: post
title: "宏基因组要不要混着拼呀？"
categories:  微生物组学
tags:  宏基因组 拼接 
keywords: 宏基因组 拼接 分箱
description: 宏基因组 拼接 分箱
---

* content
{:toc}
**许多人跟我交流，自己的宏基因组和宏转录组要不要拼接？然后拼接要不要混这拼？对于这些问题，其实我没有很多的实战经验跟大家分享，所以以前跟大家交流的都是在文献中看到的内容。**









### 分箱的基础知识

- 分箱的定义 
  分箱（binning）指从微生物群体序列中将不同个体的序列(reads或contigs等)分离开来的过程。其扩展定义为，从群体序列中重新构建群体成员个体基因组的过程。但也有人将分箱定义为将微生物群体序列与产生这些序列的物种（或者更高一级生物分类单元）关联起来的过程，准确来说，该定义的分箱是一种特殊形式（taxonomic binning/profiling/assignment），多了个体的生物分类信息。
- 分箱的对象 
  分箱的对象可以是reads、contigs、scaffolds、基因四个特征单元的任意一个，但一般情况下很少对基因进行分箱，对contigs和scaffolds的分箱不加以区别。因此，分箱按照分箱对象的不同可以分为两类，一种是直接对环境样品测序产生的reads进行分箱的方法，另一种则是对环境样品序列的拼接结果进行分析分箱的方法。前者可以避免拼接过程中出现的错误拼接序列（misassembly）或者嵌合体序列(chimeric)的产生，但二代测序的短读长会直接导致序列比对过程中出现歧义。
- 分箱的原理 
  与已知物种信息序列的相似性；群体序列的组成成分的相似性；群体序列的测序覆盖度。

> 以上摘自二师兄的毕业论文。

我虽然对分箱抱有怀疑的态度（_但是大家都发表了许多宏基因组重构基因组的文章，而且质量还看起来挺好_的）：

第一，几乎所有的分箱方法都是在拼接以后的（_现在很少有人去拿reads去分箱了吧，这个我觉得更不准哦_），拼接的错误率我觉得是很高的；

第二，然后现在许多分箱是需要人眼配合去对Bin进行筛选优化的，就不说你这属于劳动密集型工作吧（_人眼不小心看差了手一抖_）；

第三，宏基因组拼接的结果肯定不会太完整的（_以前说在Genome Bin找不到16sRNA的说的就是这个问题是很正常的，不要想拼全啦~_）然后就是[物种的变异](http://www.biorxiv.org/content/early/2017/07/03/155358) ，当处理那种高深度的测序数据时，需要在宏基因组拼接的时候考虑到。



###  比较Tara海洋宏基因组数据集的两种不同分箱方法的结果

> 为什么我比较关注Tara，因为我是做湖泊宏基因组的，借鉴学习海洋的宏基因组分析是最好的啦~当然人呀，猪呀，老鼠的我也看的。

Tara 海洋的数据集 ([Sunagawa S, Coelho L P, Chaffron S, et al. Ocean plankton. Structure and function of the global ocean microbiome[J]. Science, 2015, 348(6237):1261359.](https://www.ncbi.nlm.nih.gov/pubmed/25999513))

> 来点摘要：
>
> Microbes are dominant drivers of biogeochemical processes, yet drawing a global picture of functional diversity, microbial community structure, and their ecological determinants remains a grand challenge. We analyzed **7.2 terabases** of metagenomic data from **243 Tara Oceans samples** from **68 locations **in epipelagic and mesopelagic waters across the globe to generate an ocean microbial reference gene catalog with**>40 million nonredundant**, mostly novel sequences from viruses, prokaryotes, and picoeukaryotes. Using **139** prokaryote-enriched samples, containing **>35,000 species**, we show vertical stratification with epipelagic community composition mostly driven by temperature rather than other environmental factors or geography. We identify ocean microbial core functionality and reveal that >73% of its abundance is shared with the human gut microbiome despite the physicochemical differences between these two ecosystems

现在有人来挖掘Tara项目数据，比如把他们重新拼一拼进行分箱，文章发表在bioRxiv 上[Tully et al., 2017](http://www.biorxiv.org/content/early/2017/07/13/162503) and [Delmont et al., 2017](http://www.biorxiv.org/content/early/2017/04/23/129791). 我们就把它们叫做 **Tully**和**Delmont**。

####  Tully的分析方法

Tully et al. produced 2631 genomes, and estimated that 1491 were more than 70% complete and 603 were more than 90% complete. (Wow!)

The process used was (roughly) as follows --

1. Assemble each of 234 samples with MEGAHIT, yielding 562m contigs.
2. After length filtering the contigs at 2kb, use CD-HIT to eliminate contigs that are more than 99% similar.
3. Co-assemble contigs from each of the 61 stations (geographical locations) with MINIMUS2, yielding 7.2m contigs.
4. Apply BinSanity to cluster these contigs into genome bins, and use CheckM to evaluate completeness.

#### Delmont的分析方法

Delmont et al. produced 957 genomes from 93 samples (presumably a subset of the 234 samples above?), using this [very well documented approach](http://merenlab.org/data/2017_Delmont_et_al_HBDs/) - briefly,（就是那个anvi'o软件作者嘛）

1. Co-assemble samples from 12 geographical regions with MEGAHIT.
2. Bin results with CONCOCT.
3. Manually refine CONCOCT results using a'n'vio'.
4. Extract bins with > 70% completion or 2 Mbp of contigs into 1077 genome bins.
5. Collapse redundant genomes from across the different regions into 957 bins based on average nucleotide identity (> 98% ANI).

#### 主要区别

拼接方法：

Tully是先把234个样品先单独拼MEGAHIT（快就是好，这个是De Bruijn 图算法呢），然后在分解不同地理区域按区域（61个点一起）使用MINMUS2混拼（把长的contig拼在一起咯，那个啥overlap算法的）；

Delmont是这样子的，他的样品少一点，只用了93个样品，把它们分为12个区域（肯定是按照海域啥来分的咯），然后同样是用MEGAHIT来拼（很受欢迎嘛，我也用它）所有样品按区域混拼咯。

分箱方法：

Tully用BinSanity（17年刚出来的，我没有顺利运行，不评价）；Delmont用CONCOCT（比较老的分箱软件，看别人说比较准）

分箱评定：

Tully用的是CheckM啦，Delmont用的是自己的anvi'o啦，用的方法都是几十个核心基因来判断的，我看anvi'o用的数据集大些。

> 然后就没啥然后了，我看有人把这两个分箱完成的genome bins拿去做比较（_用的好像是_[sourmash](https://sourmash.readthedocs.io/en/latest/tutorials.html)），但是肯定结果是不好的。两个进行数据挖掘，采用的样本大小是不一样的。在我看来如果要比较两种拼接方法哪种好，至少要其他分析步骤都一样嘞。