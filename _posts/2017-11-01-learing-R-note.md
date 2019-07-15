---
layout: post
title: "【R】R极简教程学习笔记"
categories: 编程之美
tags: 生信 R
keywords: R 教程
description: R极简教程学习笔记
---

* content
{:toc}

昨天晚上师兄发给我这么一篇文章[《Shiny和Plotly实现可交互DNA甲基化分析包ChAMP》](http://blog.csdn.net/joshua_hit/article/details/54982018)，让看着学习如何用Shiny和Plotly开发一个R包。看完以后我觉得这个作者写得实在太好了，就好像是Jimmy师兄写得一样。我就去翻该作者后面的博文，发现有个R极简教程写得也是非常好，不知不觉就看到了凌晨一点钟。今天接着学，并且做了点笔记。







### [1数据分析前景](http://blog.csdn.net/joshua_hit/article/details/73740996)

>1: 科研学术界从古至今都是数据分析的最大提供方和需求方。尤其到了当代，数据分析的需求简直可以用“饥渴”来形容。计算生物学、计算化学、计算物理学、计算社会学、计算天文学……这些学科，其实全部都是基于那些领域的数据分析工作。而且难度一点都不小。
>
>2：数据分析搞的厉害真的很难，需要常年的积累和不断地学习。现在有太多人搞一些很粗浅的数据分析，然后就自称数据分析师了。哎……我博士都快毕业了，都不敢称，因为我统计说不上大师。
>
>3：现在数据分析真的应该更多地被人重视。经济学新闻的那些数据分析统计，很多都是错的，或者隐瞒了很多问题。雄安新区规划发布了，有没有人研究一下，上海浦东20年发展的状况呢？
>
>4: 数据分析是非常非常依赖分析员本身的，我也觉得目前还不存在被AI替代的可能性。因为分析什么、用什么分析、分析的结果是怎样的，这些都是问题，而这些问题都需要分析员本身去解决，可以这么说，分析这个行业没有什么具体的规范：咨询师可以成为分析师、博士后也是分析师……高下是很难判断的。

生信的数据分析并不是大家想的写写胶水性代码，跑跑流程那么简单。每一步的数据转换后面都有很多的统计学原理，所以既会数据处理也要懂统计学才能真正挖掘出真正有用的。对了，还有生物学问题。做好生信，在IT和统计界应该也是高手。

url：[http://blog.csdn.net/joshua_hit/article/details/73740996](http://blog.csdn.net/joshua_hit/article/details/73740996)



### [2常用挖掘工具介绍](http://blog.csdn.net/joshua_hit/article/details/73741034)

>简而言之，我推荐R语言作为“分析语言”（R语言的优势：免费、算法实现容易、数据可视化、交互平台做的好；R语言的劣势：IDE太少、R包质量不一定高、受到内存限制），Python可以作为“全能工具”语言，另外需要学习一门建站语言。除此以外，最好学会Markdown，git(svn)，linux bash. 此外，鉴于现在数据量越来越大，感觉最好学一学Scala和Spark集群。

作者推荐R语言作为生信数据分析的主要工具，这跟jimmy师兄教给大家一样。**学生信先学R语言就好**。后面的Python我不会，但是正在学习中......Markdown,git,Linux，这些我都会。Scala没有听说过，但是Spark倒是经常在一些大数据文章里可以看到。

url：[http://blog.csdn.net/joshua_hit/article/details/73741034](http://blog.csdn.net/joshua_hit/article/details/73741034)



### [3R及RStudio的安装](http://blog.csdn.net/joshua_hit/article/details/73741139)

记得在Window下面安装好R后，把它添加到环境变量；这样子就可以在cmd命令行界面运行R了，并可以运行Rscript脚本，就跟Perl、Python一样，是用R语言写的程序啦~

url：[http://blog.csdn.net/joshua_hit/article/details/73741139](http://blog.csdn.net/joshua_hit/article/details/73741139)



### [4R语言工作空间](http://blog.csdn.net/joshua_hit/article/details/73741206)

>**查看源代码：**R语言可以很方便地让你查看每一个函数的源代码，其实严格来说，其原因是每一个函数都是一系列复制给了一个变量，你只不过是查看了这个变量而已。不过这确实让人们可以很轻易地查看R里的函数源代码。比如说，我们想要查看lm这个函数的源代码，只需要直接输入lm，不加括号就可以实现。
>
>**运行脚本：**再很多时候，你不想每一次跑程序都很重新些，也不想要复制粘贴。所以可以写成R脚本的形式，然后直接运行。R脚本就是普通的文件，只需要再命名文件的时候，结尾用.R来结尾就行了。运行R脚本的方式有很多，不过最常用的大概有两种，一个与交互框有关——通过source()命令运行，另一种是直接再bash命令中调用Rscript运行。

查看源代码、source()的方法来运行R脚本，从来没有看到过。还有上周末学习的Rdata、Rproject，说明R语言还有好多我没有学习过的。

url：[http://blog.csdn.net/joshua_hit/article/details/73741206](http://blog.csdn.net/joshua_hit/article/details/73741206)



### [5包](http://blog.csdn.net/joshua_hit/article/details/73741362)

讲解如何修改维护一个R包。文章里面用pheatmap包为例，讲解如何在这个包中添加一个boxplot函数。上周听Y叔直播，说写R包是一件很自然的事情，水平到了，就像写作文写博客一样。但并不是每一个人写作文写得都很好，包自然也有好坏之分。_很多包是很多科研工作者为了发表文章而写的，用起来不是特别好用。_导师不太指导我的工作，也没有很好的数据可以用来分析，到现在宏基因组方面还没有跑过完完整整的流程，还是半吊子在那里。还好跟jimmy师兄学习转录组入门，准备先精通它再说，各种组学分析概念都是一样的。

url：[http://blog.csdn.net/joshua_hit/article/details/73741362](http://blog.csdn.net/joshua_hit/article/details/73741362)



### [6基本语法](http://blog.csdn.net/joshua_hit/article/details/73741410)

> 写R语言最重要的一点就是，脑子里一定要有向量、矩阵、列表这样的概念。
>
> ”判断一个人聪不聪明，就是看他有没有能力把复杂的问题拆散成小部分，然后逐个去完成，最后把整个问题综合起来解决。这句话很适合编程，无论需要写多大的程序，你都只需要把那个问题分散出来，分成一个部分，一个循环，一个判断，一个读取，一个输出……然后一步一步，像乐高积木一样去解决这个问题。“
>
> R语言中的数据结构，主要有Vector, List, matrix, DataFrame, Array, Facter。**其中最常用的有DaraFrame, matrix, list, vecter。**
>
> 有时候，人们会分不清矩阵和DataFrame，感觉用起来差不多，但实际上DataFrame应该用来存储数据，而Matrix更适合单纯的运算分析。**换言之，最好矩阵中的所有数值，都是一类的元素。不要列与列之间是不同的东西。**

一定要掌握[R语言中的apply函数族：http://blog.fens.me/r-apply/](http://blog.fens.me/r-apply/)，进阶还是做师兄出的编程实战题来提升自己。

url：[http://blog.csdn.net/joshua_hit/article/details/73741410](http://blog.csdn.net/joshua_hit/article/details/73741410)



### [7读取数据](http://blog.csdn.net/joshua_hit/article/details/73741516)

> 读取数据往往是进行数据分析的第一步，数据读取的方式很多，就R语言而言，常见的有几种：**Load已经存好的RData，读取文本文件，读取excel文件，读取数据库文件，抓取网络数据。**
>
> 个人觉得读取Excel文件最理想的办法，不就是把它存储成csv文件，然后直接用read.csv()读取吗？不过[有很多很多其他的直接从Excel读取数据的方法：https://www.r-bloggers.com/a-million-ways-to-connect-r-and-excel/](https://www.r-bloggers.com/a-million-ways-to-connect-r-and-excel/)。比如`gdata`包就是不错的选择。
>
> 用R语言链接数据库是非常方便的，直接从数据库读取，写入数据，畅快淋漓。而且连接方法很简单很简单，这使得R语言再生产环境下有了一大功能，就是直接对接上数据库进行操作。**R语言对接数据库的步骤就散步：1. 载入函数包，2：连接数据库，3：进行数据操作。**
>
> 网络爬虫就是一种可以抓取网络数据的方法，抓去完毕以后，就可以进行一些字符串处理等等。另外，抓取过程可以开并行运算加速，有些时候页面过不去，可以用tryCatch来防止错误阻断程序等等……**总而言之，再复杂的爬虫程序，其实也是通过小脚本慢慢搭建起来的。**

关于用读取数据，用的最多的就是`read.table()`和`read.csv`，数据库和网络爬虫接触过，通过KEGG这些数据库的API查询收集数据应该也算爬虫吧。

url：[http://blog.csdn.net/joshua_hit/article/details/73741516](http://blog.csdn.net/joshua_hit/article/details/73741516)

### [8缺失值与异常值](http://blog.csdn.net/joshua_hit/article/details/73741593)

> 识别缺失数据的数目、分布和模式有两个目的：分析生成缺失数据的潜在机制，评价缺失数据对回答实质性问题的影响。我们需要弄清楚以下几个问题：
>
> 缺失数据的比例多大？ 缺失数据是否集中在少数几个变量上，或者广泛存在？ 缺失是随机产生的吗？ 缺失数据间的相关性或与可观测数据间的相关性，是否可以表明产生缺失值的机制？
>
> 缺失值处理是一个比较需要经验的问题，一般来说我的处理办法是，如果样本数据很多，比如列有上百个，那就先对列做缺失值比例计算，将缺失达到10%的样本直接删除。然后再剩下的数据中，按行做缺失值比例调查，将比例高达一定阈值（比如20%）的删掉，然后对剩下的数据做impute过程。
>
> impute（补足）过程可以使用`impute`R包，其中的`impute.knn()`函数很好用。
>
> ---
>
> **异常值**顾名思义就是偏离了“寻常值”的数据。但是多“异常”的值才能成为异常值，这就得看研究项目而定了。有些时候，异常值才是一个科研项目中应该去研究的问题。**一般来说，有一个想对通用的检测异常值的标准，就是均值±三倍标准差。**这个很好理解，你的均值是数据大部分“寻常值”的所在位置，标准差是其差异程度。那么3倍标准差很明显就说明一个数据严重地偏离了均值了。
>
> 有一个特别简单找出异常值的办法，就是使用boxplot函数。直接将boxplot存储成为一个变量tmp，tmp中的out子元素就是异常值。
>
> 对于异常值的处理也是花样繁多，有的人就直接把所有异常值设置成为NA，然后就回到了上边的缺失值部分。也有人保留他们，总之这方面算法很多，不一而足。异常值产生的原因很多，**有很多时候，异常值其实不仅有意义，而且很重要：**
>
> 比如，探查人流涌动，就是通过异常值来看那些地方突然人数激增？探查宇宙射线一类的科研，最关注的东西永远都是异常值。再**大数定律**横行其道的今天，几乎各种数据都是需要量化来达到规律总结的，这恰好令了“天鹅”一类事件越来越难以估计。所以对于异常值的处理和解读，其实正是数据分析人员的水平高下所在。

目前还没有接触过缺失值和异常值，先记下来，说是判断数据质量的好坏的两个指标。

url：[http://blog.csdn.net/joshua_hit/article/details/73741593](http://blog.csdn.net/joshua_hit/article/details/73741593)

### [9描述性统计分析](http://blog.csdn.net/joshua_hit/article/details/73741688)

> **拿到一批数据，判断一下它离散程度最好办法，就是直接一个boxplot画出来。**

这个作者很喜欢pheatmap和boxplot呀，哈哈。

url：[http://blog.csdn.net/joshua_hit/article/details/73741688](http://blog.csdn.net/joshua_hit/article/details/73741688)

### [10R语言绘图基础](http://blog.csdn.net/joshua_hit/article/details/73742264)

>R语言的原生绘图系统已经非常强大了，根本不需要其他东西的辅助，就可以绘制非常炫目的图片，**需要的仅仅是耐心。**另外R语言还有一系列的绘图辅助R包，比如著名的`ggplot2`，我经常用的`plotly`都是很好的工具。
>
>`Shiny`框架，可以用R语言快速写成一个网页，这简直不能更方便。**R已经能做分布式大数据了RSpark，建站还会远吗？**
>
>[RColorBrewer](https://cran.r-project.org/package=RColorBrewer)，这个包的功能主要就是提供一些自己已经配好色的R颜色，另外提供一系列颜色的分配，比如你想要从正黄色到正蓝色直接过度10个颜色，就可以用这个包
>
> 构图函数：首先就是，如果你想在一张图上绘制多个图形怎么办？使用`par(mfrow=c(2,3))`命令可以完成**比较规则的**构图，其中参数中，前一个代表行，后一个代表列，我这里的意思就是，把图片分成两行三列。还有另外一种更为厉害的分屏：`layout(matrix(c(1,1,2,3), 2, 2, byrow = TRUE))`其中的设置都是在layout里边的matrix，里边你可以无限多地设置函数，每一张图可以通过数字连起来，这样就可以做出各种形状的组合图形。

我也经常用plotly配合ggplot2画图哦，像以前用它来找进化树每个节点的数值，不知道他们不用plotly包，是怎么看的。之前有段时间想要用python学习建站搭建数据库平台，上个月国庆数据库看了几天，接下来就没有看了，不知道我学啥没有继续了。想想，好像说是等着我实验室同级小伙伴搭建好了以后，在她的基础上直接改。也想让熊猫弟弟帮忙做，我来负责数据库那部分内容，然后就没有然后了。

小伙伴最近又不搭建了，熊猫弟弟忙着找工作，所以呢凡事都要靠自己。我做数据库平台的目的是凑博士工作量，并不是想发表。最近看到一篇文章开发了一个整合了26个人类肠道宏基因组数据集，加起来有5716个样本，它就把原始数据和相关的metadata下载下来，整合分析后，做了点可视化，可以通过调用函数下载原始数据，自己比较分析啥的。_**原来R包也可以写类似数据库的功能呀！**_

![R包](http://o7zaxp1i2.bkt.clouddn.com/f072a86a-e33e-4b93-955b-1952c8de495c.jpg)

url：[http://blog.csdn.net/joshua_hit/article/details/73742264](http://blog.csdn.net/joshua_hit/article/details/73742264)

### [11高级绘图函数](http://blog.csdn.net/joshua_hit/article/details/73743932)

> boxplot函数中将`notch`参数设置为TRUE，这样的boxplot会展现出更多细节。boxplot的前几个参数有很多种写法，可以输入一个matrix，这样boxplot会自动提取每一列做一个boxplot，也可以输入单个的一个个vector，无限多的输入。另外，也可以先输入一个长长的vector，然后用`~`符号跟一个分割vector，意思也就是，前一个vector根据后一个vector进行分割，其中每一个部分，都绘制一个boxplot。
>
> 散点图矩阵是散点图的高维扩展，它从一定程度上克服了在平面上展示高维数据的困难，在展示多维数据的两两关系时有着不可替代的作用。负责这方面工作的函数是`pairs()`函数。**散点图矩阵的意思就是，针对一个矩阵中的不同的列，每两列做一个散点图，直接看出是否有两个列之间是显著相关的，这在你的数据有很多维度，你想要确定分析那两个维度的时候尤其有用。**详见[不同版本的散点图矩阵：https://cosx.org/2009/03/scatterplot-matrix-visualization](https://cosx.org/2009/03/scatterplot-matrix-visualization)

用plotly画美丽的[气泡图：https://plot.ly/r/bubble-charts/](https://plot.ly/r/bubble-charts/)。Circular plot，就是圈圈图，我一直认为这种图很难读懂，但是大家就是那么喜欢，据说表现几个变量之间的关系是非常好的。

url：[http://blog.csdn.net/joshua_hit/article/details/73743932](http://blog.csdn.net/joshua_hit/article/details/73743932)

### [12交互式绘图](http://blog.csdn.net/joshua_hit/article/details/73744018)

目前绘制R语言交互图的主要Rchart，Highchart和plotly，我用过plotly，但还是停留在对ggplot构造的对象进行交互式而已，就是`ggploty(p)`就可以对本来的ggplot画的图变成可交互的了。

url：[http://blog.csdn.net/joshua_hit/article/details/73744018](http://blog.csdn.net/joshua_hit/article/details/73744018)

### [13交互式网站Shiny框架](http://blog.csdn.net/joshua_hit/article/details/73744064)

> 所以Shiny的模式基本上就是，从前段接受参数，传到到后端，后端处理完的图片，直接传递到前段。写代码的时候，要有前后端的概念。

具体特点暂时没有体会，但是Shiny用户界面可以用纯R语言构建，也可以直接用HTML、CSS和JavaScript来写，对于我没学过前端的小白，可以很快写成一个小应用，上次数据，展示数据，调调参数，可以重新画个图呀，下载绘制的图片。现在很多用shiny开发web工具箱，上半年的时候倒腾过一段时间。由于没有想好用Shiny来做比较实际的事情（可以用来发文章，现在愁啊~）。手头上的数据不太好呀，想要开发软件凑文章。Jimmy师兄推荐我用R包来写软件。不管咋样，先学起来再说，好好学，好好想，至少不能写个辣鸡软件。

![开发软件](http://o7zaxp1i2.bkt.clouddn.com/%E5%A6%82%E4%BD%95%E5%BC%80%E5%8F%91%E7%94%9F%E4%BF%A1%E8%BD%AF%E4%BB%B6-%E6%B2%88%E6%A2%A6%E5%9C%86.png)

url：[http://blog.csdn.net/joshua_hit/article/details/73744064](http://blog.csdn.net/joshua_hit/article/details/73744064)

### 其他学习资源

[R语言资源汇总：http://guoshipeng.com/2017/10/17/01_R_resource/](http://guoshipeng.com/2017/10/17/01_R_resource/)

果子师兄收集的资料，除了用R学习统计以外，用R编程处理数据也要跟上了!