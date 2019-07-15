---

layout: post

title: "【R】《R for Data Science》学习笔记-读书总结"

categories:  编程之美

tags:  R语言 数据科学

keywords: R语言  数据分析

description: R语言  数据分析

---

* content
{:toc}
今天大致看完了hadley大神的[《R for Data Science》](http://r4ds.had.co.nz/)：<http://r4ds.had.co.nz/>，前面三部分认真看了，后面模型和交流部分简单翻阅了下，就跟看《R语言实战一样》那么飞速。作为一个总结狂，不写点学习总结感觉少了点什么，下面我简单写几点总结，作为这本书学习暂时结束的一个结束：








### 1：写了四篇学习笔记

> 在学习刚开始写了几篇笔记（做的很粗糙，都是摘录性的），从时间上看，大概看了三个星期左右。后面就没有继续写了，不太习惯做读书笔记，个人喜欢写那种带着问题的探索性笔记。

- [【R】《R for Data Science》学习笔记-先导篇](http://shemy.site/2017/11/19/R-for-Data-Science-introduction/)：<http://shemy.site/2017/11/19/R-for-Data-Science-introduction/>

- [【R】《R for Data Science》学习笔记-数据探索篇]( http://shemy.site/2017/11/23/R-for-Data-Science-data-explore/)：<http://shemy.site/2017/11/23/R-for-Data-Science-data-explore/>

- [【R】《R for Data Science》学习笔记-程序篇](http://shemy.site/2017/11/25/R-for-Data-Science-data-program/)：<http://shemy.site/2017/11/25/R-for-Data-Science-data-program/>

- [【R】Project Euler通关打怪兽](http://shemy.site/2017/11/20/The-projecteuler-practice/)：<http://shemy.site/2017/11/20/The-projecteuler-practice/>

在先导篇是铺垫性的内容，为后面的数据探索篇、Wrangle(不懂中文啥意思)、程序篇、模型篇、交流篇做一个整体性的介绍。

### 2：体会最深的知识

> 在看完《R语言实战》后，这是我看的第二本关于R语言书籍，其他都是粗粗扫过，不算数（像R cook、ggplot2）。在这本书里，hadley大神写了很多用R做数据分析的技巧。下面我写下我体会最深的知识点：

- **数据类型**认识更为深刻了，第一次把R中的向量、矩阵、数组、数据框、列表捣鼓明白，此外我还看了[R语言教程](https://www.w3cschool.cn/r/)和[Advanced R](https://adv-r.hadley.nz/)。

|      | Homogeneous   | Heterogeneous |
| ---- | ------------- | ------------- |
| 1d   | Atomic vector | List          |
| 2d   | Matrix        | Data frame    |
| nd   | Array         |               |

- 高级数据整形包的学习：
  - 使用`tibble`来替代`data.frame`；（优点很多，生成的数据框数据每列可以保持原来的数据格式，不会被强制性改变；查看数据时，像`head()`时不再会一行显示不下，多行显示得非常丑；数据操作速度会更快了；）
  - `dplyr`和`tidyr`结合对数据进行tidy，超级有用的函数：选取部分数据`filter()`、`select()`、创造新的变量`mutate()`、排序`arrange()`、`summarise()`和`group_by()`结合使用来进行数据描述性统计；此外`gather()`、`spread()`、`separate()`、`unite()`用来高效对表格进行操作；还有就是`left_join()`、`full_join()`等关系型数据的合并函数，`intersect()`、`union()`、`setdiff()`取数据的交并集函数都是第一次接触；
```txt
# √ ggplot2 2.2.1     √ purrr   0.2.4
# √ tibble  1.3.4     √ dplyr   0.7.4
# √ tidyr   0.7.2     √ stringr 1.2.0
# √ readr   1.1.1     √ forcats 0.2.0
```

- 用R处理数据的规范：要新建project，学会写注释，用pipeline`%>%`写简洁的代码，函数的书写；
- 将数据整理好才能绘图，数据可视化作为数据挖掘的强有力工具；所以画图要有假设、目的性地画。

### 3：写在最后

看完这本书后，在以后用R进行数据分析绘图会更加高效了，对数据整形、数据可视化在数据挖掘中的重要性有了深刻的认识，当然模型也很重要（_我不是没认真看嘛_）。对R的编程语法更加熟悉了，毕竟中间刷了7道编程题（_代码惨不忍睹_）。总之，对于R语言又有更新的认识，更上一层楼的感觉（R的学习曲线还是比较陡峭的，一些高手的技巧在一定阶段是看不懂的，需要跟着时间慢慢沉淀。不要灰心，俺觉得R还是挺好学的一门语言，比Perl好学）。

![刷题](https://projecteuler.net/profile/shenmy.png)

![](http://o7zaxp1i2.bkt.clouddn.com/LearningCurve2.png)