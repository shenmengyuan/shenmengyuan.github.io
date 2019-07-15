---
layout: post
title:  "【每日一生信】用perl统计碱基计数及GC含量"
categories: 编程之美
tags: 碱基计数 GC含量 perl
keywords: 碱基计数 GC含量 perl
description: 用perl统计碱基计数及GC含量
---

* content
{:toc}

**统计clean.fa文件的碱基个数和GC%,在此之前我利用别人的代码看了一下clean.fa文件基本信息如下：**





```
#计算其有多少条序列
$ cat clean.fa |grep ">"|wc -l
30515834
#下面的代码是查看fasta文件读段平均读长、最大读长、最短读长（别人写的- -）
$ perl -ne 'BEGIN{$min=1e10;$max=0;}next if ($.%2);chomp;$read_count++;$cur_length=length($_);$total_length+=$cur_length;$min=$min>$cur_length?$cur_length:$min;$max=$max<$cur_length?$cur_length:$max;END{print qq{Totally $read_count reads\nMAX length is $max bp\nMIN length is $min bp \nMean length is },$total_length/$read_count,qq{ bp\n}}' clean.fa
Totally 30515834 reads
MAX length is 96 bp
MIN length is 25 bp
Mean length is 94.2260904289884 bp
real    0m37.245s
user    0m35.819s
sys    0m1.421s
```

## 方法

### 方法一

```
#! /usr/bin/perl
use strict;
open INPUT,"../4_Removehost/clean.fa";
my($GC,$count_A,$count_C,$count_G,$count_T,$total);
while(<INPUT>){
while ($_=~/A/ig){$count_A++} 
while ($_=~/C/ig){$count_C++} 
while ($_=~/G/ig){$count_G++} 
while ($_=~/T/ig){$count_T++}
}
$total=$count_A+$count_T+$count_G+$count_C;
$GC=($count_G+$count_C)/$total*;
print "total count is $total \nGC is $GC";

#total count is 2875363107
#GC is 0.430857696888437
#real   13m52.721s
#user   13m51.099s
#sys    0m1.520s
```

### 方法二

```
#! /usr/bin/perl
use strict;
open INPUT,"../4_Removehost/clean.fa";
my($GC,$count_A,$count_C,$count_G,$count_T,$total);
while(<INPUT>){
$count_A=$count_A+($_=~tr/A//); 
$count_T=$count_T+($_=~tr/T//); 
$count_G=$count_G+($_=~tr/G//); 
$count_C=$count_C+($_=~tr/C//);
}
$total=$count_A+$count_T+$count_G+$count_C;
$GC=($count_G+$count_C)/$total;
print "total count is $total \nGC is $GC";
 
#这个结果比4_2_Remocehost_count.pl快多了。
#total count is 2875363107
#GC is 0.430857696888437
#real   1m3.280s
#user   1m1.762s
#sys    0m1.509s
```

### 方法三

```
#! /usr/bin/perl
use strict;
open INPUT,"../4_Removehost/clean.fa";
my($GC,$count_A,$count_C,$count_G,$count_T,$total);
while(<INPUT>){
$count_A=$count_A+($_=~s/A//ig); 
$count_T=$count_T+($_=~s/T//ig); 
$count_G=$count_G+($_=~s/G//ig); 
$count_C=$count_C+($_=~s/C//ig);
}
$total=$count_A+$count_T+$count_G+$count_C;
$GC=($count_G+$count_C)/$total;
print "total count is $total \nGC is $GC";

#total count is 2875363107
#GC is 0.430857696888437
#real   10m23.054s
#user   10m21.412s
#sys    0m1.564s
```

### 方法四

将上面最快的方法二写成一行perl代码，方便使用。

```
perl -ne  '{$count_A=$count_A+($_=~tr/A//);$count_T=$count_T+($_=~tr/T//);$count_G=$count_G+($_=~tr/G//);$count_C=$count_C+($_=~tr/C//)};END{print qq{total count is },$count_A+$count_T+$count_G+$count_C, qq{\nGC:},($count_G+$count_C)/($count_A+$count_T+$count_G+$count_C),qq{\n} }'  ../4_Removehost/clean.fa
#total count is 2875363107
#GC:0.430857696888437
 #real    1m16.111s
#user    1m14.730s
#sys    0m1.371s
```

## 写在最后

这是昨天做的小题目，最终还是比较好得完成了任务，不知道怎么写还能再快一些？







