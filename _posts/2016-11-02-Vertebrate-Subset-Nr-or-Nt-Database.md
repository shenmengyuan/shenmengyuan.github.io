---
layout: post
title: "【数据库】如何nt/nt库中分离出细菌和古细菌数据"
categories: 微生物组学
tags:  nt nr 
keywords: 非冗余蛋白库
description: 
---

* content
{:toc}


对微生物宏基因组做物种分类或者基因功能注释中会采用基于比对的方法，将未知的序列比对到已知的参考库（nt/nr库）中。为什么想要从nt/nr库中分离细菌和古细菌呢，因为解压缩后的nt/nr库实在是太大了，里面包含了所有生物的已知基因。如果研究的对象仅仅使细菌或者使古细菌，那么将这些未知物种的基因组拿到庞大的参考库中比对，是非常耗费时间的。（NCBI上有病毒单独的参考基因库，师兄说以前细菌也是单独有的。）






### 根据gi号进行分离

- 1:了解物种分类号码：

Taxonomy IDs
Microsporidia 6029  txid6029[ORGN]
Archaea 2157  txid2157[ORGN]
Bacteria 2  txid2[ORGN]
Eukaryota 2759  txid2759[ORGN]
Viruses 10239  txid10239[ORGN]
Streptococci 1301  txid1301[ORGN]

- 2:在NCBI第一个搜索框中选中蛋白质，第二个搜索框中，添加你要的分类ID，如下：

![1](http://o7zaxp1i2.bkt.clouddn.com/b780c19f-deca-45e2-8f1d-4cc79d27192b.png)


- 3:点击查询，将搜索到的结果选择输出格式为：GI list，具体如下：

![2](http://o7zaxp1i2.bkt.clouddn.com/1f00b368-9240-4539-8bdb-577cee6d5e0d.png)

- 4:将输出的GI list文件：命名为gi_list.txt

- 5:根据gi list文件将数据分离出来

blastdb_aliastool -gilist gi_list.txt -db nr -out nr_bac -title nr_bact
（blastdb_aliastool 为新版blast+ 的一部分）

### 根据acc号进行分离

NCBI中的gi号逐渐被acc号取缔了，具体细节和原因没怎么研究。就我所知我近期所下载的nr库header行中的编号已经从原来的gi号改成了acc号。由于blastdb_aliastool只能提取gi号，acc列表还不能接受，只能等NCBI更新了。我目前的想法是前两个步骤一样，第三个步骤输出acc列表（accession list）。第四个步骤改名后，使用faSomeRecords进行数据分离。

```
---> faSomeRecords
faSomeRecords - Extract multiple fa records
usage:
   faSomeRecords in.fa listFile out.fa
options:
   -exclude - output sequences not in the list file.
```

### 思考
- acc列表提取的完整性，是否存在更好的方法，如果是从NCBI上下载的文件中提取出列表的话，我才觉得比较可靠。

- 了解ftp://ftp.ncbi.nih.gov/pub/taxonomy中的文件意义；

![3](http://o7zaxp1i2.bkt.clouddn.com/c6e46894-cfd6-4bc7-9a36-ee72a7517750.png)
![4](http://o7zaxp1i2.bkt.clouddn.com/54e83766-ff4a-409c-8024-1d8179658147.png)


- 数据分离正确性还未验证。




