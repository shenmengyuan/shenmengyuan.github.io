---
layout: post
title: "anaconda的下载、安装及使用"
categories: 百宝工具箱
tags:  生信
keywords: anaconda
description: 一键安装生信软件
---

* content
{:toc}


第一次使用conada是九月份，那是看了一个公众号的推荐帖子，那时我尝试安装了miniconda，使用和安装软件都非常简单,那会安装的使miniconda，里面的软件相对少些，试用的时候觉得下载速度不行，就没一直用了。今天在学习的过程中用anaconda安装了几个软件，感觉还可以。

> 对于生物专业的人来说，学习生物信息，第一个门槛应该就是Linux，而Linux中最容易出错的就是软件安装了。尤其是不能联网、没有root权限的苦逼状态下。conda像windows下的软件管家、Mac下的APP Store一样，一键安装生信软件。






### 安装和使用
anaconda官网：https://www.continuum.io/downloads#linux
![1](http://o7zaxp1i2.bkt.clouddn.com/f12d7cb6-0506-40b0-a1ab-d043855ae2a2.png)

- 安装ETE
ETE官网：http://etetoolkit.org/download/

```
# Install Minconda  (you can ignore this step if you already have Anaconda/Miniconda)
wget https://repo.continuum.io/archive/Anaconda2-4.2.0-Linux-x86_64.sh
bash Anaconda2-4.2.0-Linux-x86_64.sh
# 将~/anaconda/bin添加到环境变量中
# Install ETE
conda install -c etetoolkit ete3 ete3_external_apps
# Check installation
ete3 version
ete3 build check

# 遇到的问题及解决办法：
# 显示conda error: could not found url
find . -name ".condarc"
vi .condarc # 将里面的内容都删了（是不是太粗暴了，呵呵）。
```

- 安装QIIME
```
conda create -n qiime1 python=2.7 qiime matplotlib=1.4.3 mock nose -c bioconda
source activate qiime1
print_qiime_config.py -t
source activate qiime1
source deactivate
conda remove --name qiime1 --all
```



