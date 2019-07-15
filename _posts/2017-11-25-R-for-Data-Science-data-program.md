---
layout: post
title: "【R】《R for Data Science》学习笔记-程序篇"
categories:  编程之美
tags:  R语言 数据科学
keywords: R语言  数据分析
description: R语言  数据分析
---

* content
{:toc}
写呀写呀写代码，写成一个程序，你真棒！









### Functions

> 写函数好处多多，使你的代码变得通俗易懂，容易维护，减少出错率。所以一定要学会写函数。

- 不使用`return`，最后代码不赋值即可作为返回值；

- **do not repeat yourself**(DRY) principle

- 为什么要写函数的例子

  ```R
  df <- tibble::tibble(
    a = rnorm(10),
    b = rnorm(10),
    c = rnorm(10),
    d = rnorm(10)
  )

  ## 最不好的做法
  df$a <- (df$a - min(df$a, na.rm = TRUE)) / 
    (max(df$a, na.rm = TRUE) - min(df$a, na.rm = TRUE))
  df$b <- (df$b - min(df$b, na.rm = TRUE)) / 
    (max(df$b, na.rm = TRUE) - min(df$a, na.rm = TRUE))
  df$c <- (df$c - min(df$c, na.rm = TRUE)) / 
    (max(df$c, na.rm = TRUE) - min(df$c, na.rm = TRUE))
  df$d <- (df$d - min(df$d, na.rm = TRUE)) / 
    (max(df$d, na.rm = TRUE) - min(df$d, na.rm = TRUE))

  ## 改善了一点
  x <- df$a
  (x - min(x, na.rm = TRUE)) / (max(x, na.rm = TRUE) - min(x, na.rm = TRUE))
  rng <- range(x, na.rm = TRUE)
  (x - rng[1]) / (rng[2] - rng[1])

  ## 写函数
  rescale <- function(x){
   # 处理Inf和-Inf
   for (i in length(x)) {
    if(x[i] == -Inf){
     x[i] <- 0
    }else if(x[i] == Inf){
     x[i] <- 1
    }
   }
    
   rng <- range(x,na.rm = T)
   (x - rng[1])/(rng[2]-rng[1])

  }

  ## 使用函数
  rescale(c(1:10,Inf))
  ## 使用apply对df的每列进行循环处理
  apply(df,2,rescale)
  ```

- <https://nicercode.github.io/intro/writing-functions.html>
  ```R
  standard.error <- function(x) {
      v <- var(x)
      n <- length(x)
      sqrt(v/n)
  }

  variance <- function(x) {
      n <- length(x)
      m <- mean(x)
      (1/(n - 1)) * sum((x - m)^2)
  }
  ## variance等同于var，真的么？
  skewness <- function(x) {
      n <- length(x)
      v <- var(x)
      m <- mean(x)
      third.moment <- (1/(n - 2)) * sum((x - m)^3)
      third.moment/(var(x)^(3/2))
  }
  ```

- 函数名最好前缀写一样，这样使用Tab可以在函数家族中找

- 注释`#`, to explain the “why” of your code,avoid comments that explain the “what” or the “how”

- `Ctrl + Shift + R`可以用了生成下面格式的注释
  ```R
  # Load data --------------------------------------

  # Plot data --------------------------------------
  ```

- `||` (or) and `&&` (and) to combine multiple logical expressions;never use `|` or `&` in an `if` statement;`any()` or `all()` to collapse it to a single value （操作符的区别，不要在`if`语句中使用`|`或者`&`）

- 注意，`x == NA` doesn’t do anything useful!

- 如果写了太多的`if`语句，则需要考虑使用`switch()` 语句，还有个`cut()`（适用于离散型变量）

- `ifelse(test, yes, no)`

- 问候函数编写（要点是字符串的切割）

  ```R
  greet <- function(){
    # lubridate::now()好像也可以返回当前时间
    sys_time <- as.character(Sys.time())
    split_time <- unlist(strsplit(sys_time,split = " |:"))
    hour <- as.numeric(split_time[2])
    if(hour<12 && hour >=6){
    return("good morning")
    }else if(hour >= 12 && hour <18){
    return("good afternoon")
    }else {
    return("good evening")
    }
  }

  greet()
  ```

  ​

- 函数的两个变量的长度，NA值进行判断，程序会中止接着，报错、提醒：`stopifnot()`

- special argument: `...` (pronounced dot-dot-dot)

- <http://adv-r.had.co.nz/Functions.html#lazy-evaluation>

- 如果可以尽早设置返回值

- Writing pipeable functions:

  ```R
  mtcars %>% 
  show_missings() %>% 
  mutate(mpg = ifelse(mpg < 20, NA, mpg)) %>% 
  show_missings() 
  ```

- 环境

  ```R
  `+` <- function(x, y) {
    if (runif(1) < 0.1) {
      sum(x, y)
    } else {
      sum(x, y) * 1.1
    }
  }
  table(replicate(1000, 1 + 2))
  #> 
  #>   3 3.3 
  #> 100 900
  rm(`+`)
  ```

  ​


