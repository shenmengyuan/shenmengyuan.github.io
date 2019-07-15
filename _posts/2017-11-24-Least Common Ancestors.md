---
layout: post
title: "【算法】最近公共祖先LCA问题"
categories:  编程之美
tags:  算法
keywords: 算法
description: 算法
---

* content
{:toc}

### 问题描述

LCA（Least Common Ancestors），即最近公共祖先，是指这样一个问题：在有根树中，找出某任意两个结点u和v最近的公共祖先（另一种说法，离树根最远的公共祖先）。





### 分析与解法

最近公共祖先简称LCA（Lowest Common Ancestor），所谓LCA，是当给定一个有根树T时，对于任意两个结点u、v，找到一个离根最远的结点x，使得x同时是u和v的祖先，x 便是u、v的最近公共祖先。（参见：<http://en.wikipedia.org/wiki/Lowest_common_ancestor> ）原问题涵盖一般性的有根树，本文为了简化，多使用二叉树来讨论。

举个例子，如针对下图所示的一棵普通的二叉树来讲：

[![img](https://github.com/shenmengyuan/The-Art-Of-Programming-By-July/raw/master/ebook/images/39/39.1.jpg)](https://github.com/shenmengyuan/The-Art-Of-Programming-By-July/blob/master/ebook/images/39/39.1.jpg)

结点3和结点4的最近公共祖先是结点2，即LCA（3 4）=2 。在此，需要注意到当两个结点在同一棵子树上的情况，如结点3和结点2的最近公共祖先为2，即 LCA（3，2）=2。同理：LCA（5，6）=4，LCA（6，10）=1。

直观的做法，可能是针对是否为二叉查找树分情况讨论，这也是一般人最先想到的思路。除此之外，还有几种算法相对高级：Tarjan算法、倍增算法、以及转换为RMQ问题（求某段区间的极值）。

### 参考资料

1. <https://github.com/shenmengyuan/The-Art-Of-Programming-By-July/blob/master/ebook/zh/03.03.md>
2. <http://en.wikipedia.org/wiki/Lowest_common_ancestor>