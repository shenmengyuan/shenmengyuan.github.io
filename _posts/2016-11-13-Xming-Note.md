---
layout: post
title: "Xming图形化显示"
categories: 百宝工具箱
tags:  图形化显示
keywords: Xming
description: 
---

* content
{:toc}


有时候，在使用SSH协议远程登陆服务器时，想要在看看服务器上的图片，但又不想把数据远程拷贝下来。这个需求可以用Xming来完成。





### 安装和使用说明

- 1.下载Xming，默认安装即可，不需要额外的参数设置。
- 2.在自己的安全终端模拟器xshell、putty、SecureCRT上打开X11转移协议。（这是关键步骤，去年在这个步骤磕了一个星期~）

![1](http://o7zaxp1i2.bkt.clouddn.com/c138c5ee-5a14-4529-8f44-aaa327dc2a4d.png)

- 3.打开Xming

![2](http://o7zaxp1i2.bkt.clouddn.com/e7b515ae-c79a-4a4e-acd6-28b2ad384fa3.jpg)

- 4.在模拟终端输入指令

```
firefox  *.html  #查看网页
eog  *.png # 查看图片
gedit   *  #编辑查看文档
```
