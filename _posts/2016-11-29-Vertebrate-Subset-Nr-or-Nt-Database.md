---
layout: post
title: "【软件】软件taxomias—从Nr库中任意提取各分类水平的子库"
categories: 微生物组学
tags:  nt nr 
keywords: 非冗余蛋白库
description: 
---

* content
{:toc}


月初的时候我就在研究这件事，在我坚持不懈的寻找下，终于在github上找到了跟我有一样想法的现成代码啦！但是拥有跟前辈一样的思考思路，我还是挺开心的。从Nr库中任意提取各分类水平的子库，比如蓝藻库啊，真核藻库啊，病毒库啊，细菌库啊~而且还可以进行完整基因组的下载等等~






### 安装

- 下载Taxomias：git clone https://github.com/wegnerce/taxomias.git

- 依赖软件：sqlite3 command-line tool   python 2.7  biopython

- 依赖数据资源：

```
wget -c ftp://ftp.ncbi.nih.gov/pub/taxonomy/taxdmp.zip
wget -c ftp://ftp.ncbi.nih.gov/pub/taxonomy/accession2taxid/prot.accession2taxid.gz
wget -c ftp://ftp.ncbi.nih.gov/genomes/ASSEMBLY_REPORTS/assembly_summary_refseq.txt
unzip taxdmp.zip
gzip -d prot.accession2taxid.gz
```

- 建关联库：ncbi_taxonomy.db
耗时较长，耐心等待~~

```
sqlite3 ncbi_taxonomy.db
create table acc_taxid (accession text, accession_version text, taxid integer, gi integer);
.tables
.mode list
.separator \t
.import prot.accession2taxid acc_taxid # 导入prot.accession2taxid数据
CREATE UNIQUE INDEX accvers_idx_on_accvers_taxid ON acc_taxid(accession_version)
# 唯一索引 使用唯一索引不仅是为了性能，同时也为了数据的完整性。唯一索引不允许任何重复的值插入到表中。
CREATE INDEX taxid_idx_on_accvers_taxid ON acc_taxid(taxid); # 单列索引
# CREATE INDEX语句创建索引，它允许命名索引，指定表及要索引的一列或多列，并指示索引是升序排列还是降序排列。
.exit
```

![1](http://o7zaxp1i2.bkt.clouddn.com/26a9e8d0-79c7-4a1b-b32a-a0d76e7e9ac1.png)
 
在进行下一步之前将assembly_summary_refseq.txt处理成以上格式；

```
python setup_taxomias.py names.dmp nodes.dmp assembly_summary_refseq.txt ncbi_taxonomy.db
```

注：报错信息和解决方法，如下：
![2](http://o7zaxp1i2.bkt.clouddn.com/4930e4ce-b2df-4a0e-8525-b0a70a74c2c8.png)
![3](http://o7zaxp1i2.bkt.clouddn.com/d316241b-6619-4c49-9f79-8e87651f2755.png)
 
- 检查关联库的完整性

```
sqlite3 ncbi_taxonomy.db
SELECT taxid FROM tree WHERE name = "Acidobacterium capsulatum";
.exit
```

检验成功啦~~
![4](http://o7zaxp1i2.bkt.clouddn.com/b548804f-e476-4a0b-9dfd-f8985f092442.png)
 
```
## 查看python安装所在目录
sys has some useful stuff:
[shenmy@localhost taxomias]$ python
Python 2.7.12 |Anaconda 4.2.0 (64-bit)| (default, Jul  2 2016, 17:42:40)
[GCC 4.4.7 20120313 (Red Hat 4.4.7-1)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
Anaconda is brought to you by Continuum Analytics.
Please check out: http://continuum.io/thanks and https://anaconda.org
>>> import sys
>>> sys.executable
'/home/shenmy/anaconda2/bin/python'
>>> sys.exec_prefix
'/home/shenmy/anaconda2'
>>> print '\n'.join(sys.path)
/home/shenmy/anaconda2/lib/python27.zip
/home/shenmy/anaconda2/lib/python2.7
/home/shenmy/anaconda2/lib/python2.7/plat-linux2
/home/shenmy/anaconda2/lib/python2.7/lib-tk
/home/shenmy/anaconda2/lib/python2.7/lib-old
/home/shenmy/anaconda2/lib/python2.7/lib-dynload
/home/shenmy/anaconda2/lib/python2.7/site-packages
/home/shenmy/anaconda2/lib/python2.7/site-packages/Sphinx-1.4.6-py2.7.egg
/home/shenmy/anaconda2/lib/python2.7/site-packages/ete3-3.0.0b36-py3.5.egg
/home/shenmy/anaconda2/lib/python2.7/site-packages/bz2file-0.98-py2.7.egg
/home/shenmy/anaconda2/lib/python2.7/site-packages/screed-0.9-py2.7.egg
/home/shenmy/anaconda2/lib/python2.7/site-packages/khmer-2.0+451.gc114d14-py2.7-linux-x86_64.egg
/home/shenmy/anaconda2/lib/python2.7/site-packages/biopython-1.68-py2.7-linux-x86_64.egg
/home/shenmy/anaconda2/lib/python2.7/site-packages/setuptools-27.2.0-py2.7.egg
>>>
```

```
## 将taxomia链接到python安装目录下，可以让python找到taxomia
[shenmy@localhost taxomias]
ln -s /home/shenmy/biosoft/taxomias /home/shenmy/anaconda2/lib/python2.7
chmod +x setup_taxomias.py taxomias.py
```

### 测试

- 从NR库中分出微囊藻属的非冗余蛋白acc号列表

```
## 下载Nr库
wget ftp://ftp.ncbi.nlm.nih.gov/blast/db/FASTA/nr.gz
gzip -d nr.gz
```

```
# 打开python运行以下代码：
#载入所需要的包
import sqlite3,taxomias
# 看看微囊藻的分类号（taxid）是多少？答案应该是1125。
print taxomias.TaxidByName("Microcystis")
# 把所有属于微囊藻的accession version 号存入一个set，set比list会更快些，因为集合是使用哈希列表。
wanted= set(taxomias.AllAccByTaxid(1125))
len(wanted) # 查看有多少个accession version 号
acc=open('nr_Microcystis_acc_list.txt', 'a')
acc.write('\n'.join(wanted))
```

- 从fasta文件中提取id列表中对应的序列

可以自己编写脚本，我采用现成的工具：

```
wget -c http://hgdownload.cse.ucsc.edu/admin/exe/linux.x86_64/faSomeRecords
chmod +x faSomeRecords
faSomeRecords /home/shenmy/Metavirome/RefSeq/nr nr_Microcystis_acc_list.txt nr_Microcystis.fa
```

```
[shenmy@localhost taxomias]$ cat nr_Microcystis_acc_list_sort.txt |wc -l
180517
[shenmy@localhost taxomias]$ grep ">" nr_Microcystis.fa|wc -l
90165
## 条数不符合哎~
```

- 从nr库中分离Synechocystis sp. PCC 6803的非冗余蛋白

```
import sqlite3, taxomias
taxomias.TaxidByName("Synechocystis sp. PCC 6803")
wanted= set(taxomias.AllAccByTaxid(1148))
# 提取方法1:使用faSomeRecords
acc=open('nnr_Synechocystis_sp._PCC_6803_acc_list.txt', 'a')
acc.write('\n'.join(wanted))
# 提取方法2:使用SeqIO包
from Bio import SeqIO
input_file = "/home/shenmy/Metavirome/RefSeq/nr"
output_file = "nr_Synechocystis_sp._PCC_6803.fasta"
records = (r for r in SeqIO.parse(input_file, "fasta") if r.id.split("\s")[0] in wanted)
count = SeqIO.write(records, output_file, "fasta")
print "Saved %i records from %s to %s" % (count, input_file, output_file)
```

### 全部代码记录

[How_to_use_taxomias.ipynb](https://github.com/shenmengyuan/taxomias/blob/master/How_to_use_taxomias.ipynb)
![5](http://o7zaxp1i2.bkt.clouddn.com/2016-11-30_182134.png)

```
# 下载方法
curl https://github.com/shenmengyuan/taxomias/blob/master/How_to_use_taxomias.ipynb >How_to_use_taxomias.ipynb 
```




