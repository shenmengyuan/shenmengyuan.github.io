---
layout: post
title:  "【笔记】基因组的拼接原理"
categories: 组学原理
tags: 拼接原理
---

* content
{:toc}

 最近学习了一下基因组的拼接原理，以下是我的学习笔记和一些思考。基因组的拼接原理是高通量测序技术的基础知识吧，我个人认为即使不做基
 因组拼接工作，也可以学习一下几个主流拼接软件的算法和原理。我主要是学习了两个网上教程，其教程出处为[https://github.com/
 TGAC/361Division/tree/master/de_novo_2016](https://github.com/TGAC/361Division/tree/master/de_novo_2016)和[https://github.com/
 lexnederbragt/INF-BIO9120_fall2013_de_novo_assembly/tree/master/presentations](https://github.com/lexnederbragt/INF-
 BIO9120_fall2013_de_novo_assembly/tree/master/presentations)。






![1](http://o7zaxp1i2.bkt.clouddn.com/374990fb-8212-4fc4-b5ec-5cc0da1f35d2.png)
![2](http://o7zaxp1i2.bkt.clouddn.com/778cee53-ac5d-41cf-a9d1-b3ae010ae8f1.png)

### 拼接是个啥？
A hierarchical data structure that maps the sequence data to a putative reconstruction of the target.(Miller et al 2010,Genomics
 95(6):315-327)
基因组拼接可以类比成一本书被碎纸机碎个稀巴烂，然后用胶水把他们一片片给拼回去的过程。
![3](http://o7zaxp1i2.bkt.clouddn.com/56e304b2-6f8c-4114-9b10-a166991a8b15.jpg)
![4](http://o7zaxp1i2.bkt.clouddn.com/b63deb18-bd51-4717-8067-18bb69917d5a.png)

- 拼接的过程就像一个黑箱处理过程，reads序列输入，经过拼接黑盒，输出就是基因组拼接好的结果。正确的拼接应该是The right motifs,the 
correct number of times,in correct order and position。我个人认为是尽可能得还原真实的基因组是拼接的终极目的。

- 另外，拼接的算法分为试探型和穷举型两种，一般都用试探型算法，因为它更好更快更简单（在绝大多数时候）。穷举型算法局限性强、运行速度
慢、召回率低，并且数据类型不尽相同，因此没有很好的模型适合全部的数据类型。

- 在拼接之前，我们确保输入的数据是去除接头、污染等的good 
data，并且要大概知道拼接的原理。最后完成拼接后，要检查拼接结果的可靠性和完整性。
![5](http://o7zaxp1i2.bkt.clouddn.com/8b936af1-756a-4db0-942b-ca118a22479e.jpg)

### 测序技术
测序长度越长，覆盖度越高，带来的拼接结果也会越好。并且根据研究目的的不同，我们使用不同测序技术，产生不同类型的数据，得到不同的测序
信息。
![6](http://o7zaxp1i2.bkt.clouddn.com/27bf1fe6-1bf3-4f7a-9dc9-e3efbe90f5ff.png)

### 拼接算法
**None of which is assessed by length stats.**   

- Overlap Layout Consensus
找到重叠区域并且定义他们是key。layout有点难度。这种方法tracks每一条read。Consensus是由reads构建而成的。
![7](http://o7zaxp1i2.bkt.clouddn.com/e1b85e2e-e4c9-4b53-97f4-bc44e78a8c3b.jpg)

- De Bruijn Graphs
![8](http://o7zaxp1i2.bkt.clouddn.com/8e943760-826e-4ae1-9da3-6e05455e30b9.png)

- OLC VS DE bruijn
![9](http://o7zaxp1i2.bkt.clouddn.com/a054ef5b-88ea-43d0-ba19-34b420cd5fcb.png)
![10](http://o7zaxp1i2.bkt.clouddn.com/ea1ed047-348a-4e85-8559-ee1aefae3535.png)

### 拼接实验前

- 有时候一次测序拼接结果可能很难达到预设的拼接目标，可能需要多次补测样品来完善拼接结果。我们在测序拼接前，需要知道所研究对象的基因
组的大小、倍型、杂合性、GC含量、是否有污染物/
共生者、数据集的类型、是否线粒体还是叶绿体的细胞器基因组。其实这些内容在测序之前就需要考虑了，下面一些点进行进行较为详细的介绍
：

（1）基因组大小的获取关系到对以后组装结果的大小的正确与否判断；基因组太大（>10Gb），可能会超出了目前denovo组装基因组软件的对机器存
的要求，从客观条件上讲是无法实现组装的。一般物种的基因组大小可以从公共数据库查到。如果没有搜录，需要考虑通过实验（流式细胞仪福尔根
染色/定量pcr/）或Kmer估计法来获得基因组大小。

（2）杂合度对基因组组装的影响主要体现在不能合并姊妹染色体，杂合度高的区域，会把两条姊妹染色单体都组装出来，从而造成组装的基因组偏
大于实际的基因组大小。一般是通过SSR在测序亲本的子代中检查SSR的多态性。杂合度如果高于0.5%，则认为组装有一定难度。杂合度高于1%则很难
组装出来。杂和度估计一般通过kmer分析来做，降低杂合度可以通过很多代近交来实现。杂合度高，并不是说组装不出来，而是说，装出来的序列不
适用于后续的生物学分析。比如拷贝数、基因完整结构。

（3）随着测序对质量要求越来越高和相关技术的逐渐成熟，遗传图谱也快成了denovo基因组的必须组成。

（4）实验设计需要考虑的问题：1.明确我们的生物学问题;2.设计数据处理方案；3.设置实验条件和生物/技术重复数；4.选择测序平台和覆盖度。

![11](http://o7zaxp1i2.bkt.clouddn.com/abe45cd0-1b4d-4b07-adfb-198b66e9ee9f.jpg)
![12](http://o7zaxp1i2.bkt.clouddn.com/3dc186b3-b3f4-45fa-9e9f-5aef1df4bc70.png)
![13](http://o7zaxp1i2.bkt.clouddn.com/1843d9ca-dc46-4190-82eb-bab4be2987a4.jpg)
![14](http://o7zaxp1i2.bkt.clouddn.com/eb139f08-e40d-461c-aad7-a0266082c0f9.png)
![15](http://o7zaxp1i2.bkt.clouddn.com/8d0be417-9112-4302-be64-3b28185fab60.png)

### 为啥拼接挺难的
- 重复序列
- 二倍体
- 多倍性
- 可供选择的软件多
![16](http://o7zaxp1i2.bkt.clouddn.com/56405729-685e-4f68-af2c-da812d90596c.jpg)

### 两个拼接软件
- A modern assembler-SOAPdenovo2
![17](http://o7zaxp1i2.bkt.clouddn.com/9015bf04-f6fc-499e-b650-f69d303be401.jpg)
- Trinity运行的原理和过程
1 Trinity 如何运作
 a. 序列延伸 (inchworm) ——虫子
 将 reads切为 k-mers (k bp长度的短片段)   拆分K-mer的目的：节省内存，降低测序错误对拼接的影响；利用Overlap关系对k-mers进行延伸 (
 贪婪算法)；输出所有的序列 (“ contigs”)。
b. 构建 de Bruijn graph (chrysalis)—— 成蛹
聚类所有相似区域大于1kbp的 contigs；构图 (区分不同的 “components”)； 将reads比对回 components，进行验证
c. 解图，列举转录本 (butterfly)——化蝶
拆分graph 为线性序列；使用reads以及 pairs关系消除错误序列。
2 组装质量评估与去冗余
d. 组装质量：  组装完整性、组装准确性、后续定量准确性、组装冗余度
 N50长度，可以初步评估组装质量；但并非越长越好，应该参照相关的研究（同物种或近缘种）；通过统计Unigene对近缘种编码基因的覆盖度分，
 也可以从整体评估组装质量。
3 注释与其他

### 组装评估
(1)  kmer spectra，可用软件KAT、CEGMA；
![18](http://o7zaxp1i2.bkt.clouddn.com/45f4b610-fd96-4cde-bb18-da4da1ed612f.jpg)
(2)使用生物学知识去进行评估验证
- Direct experimental evidence: the reads、Genome size、ploidy、GC content、Symbionts、Plastids、ESTs、cDNAs、peptides、genome
 walking
- Indirect experimental evidence: genomes in general（Genes! （They have structure，Repeats），Chromosome macrostructure
，(circular?, number, telomeres, …)）、other species（Close relatives: proteins, transcripts, genomes； Distant relatives: single-copy genes, phylogeny, HGT）

### 误差和质控
样本的准备和建库：样品未纯化，PCR偏差（没有化学反应是perfect、complete的）
![19](http://o7zaxp1i2.bkt.clouddn.com/8f395d22-1c19-468e-aba7-71c717cba90b.png)
![20](http://o7zaxp1i2.bkt.clouddn.com/055c40cf-9340-4756-9f7b-baaceb219cb8.png)
![21](http://o7zaxp1i2.bkt.clouddn.com/589c3d30-9b63-4bc0-b32a-a26b8d0273d2.png)

N50并不是那么可靠、敏感，我们要注意。
![22](http://o7zaxp1i2.bkt.clouddn.com/834d4d11-59ad-4c18-88c4-101f4f169a56.png)
![23](http://o7zaxp1i2.bkt.clouddn.com/c0e709b7-de7c-4278-bb48-c40b2e834634.png)

### 其他参考资料
[https://www.cbcb.umd.edu/research/assembly_primer](https://www.cbcb.umd.edu/research/assembly_primer)