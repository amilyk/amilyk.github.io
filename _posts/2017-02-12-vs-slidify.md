---
layout:     post
title:      "[slidify]slidify的安装及使用"
date:       2017-02-12
author:     "xunkang"
header-img: "img/post-bg-js-version.jpg"
tags:
    - 可视化

---

### 1 slidify安装

+ 首先安装devtools.

+ 导入devtools，然后安装slidify
  {% highlight ruby %}
  install.packages("devtools")	
  library(devtools)	
  install_github('slidify','ramnathv')	
  install_github('slidifyLibraries','ramnathv')
  {% endhighlight %}

+ 加载slidify
  {% highlight ruby %}
  library("slidify")	
  {% endhighlight %}

### 2 slidify使用

#### 2.1 slidify运行
​	{% highlight ruby %}
​	Sys.setlocale("LC_CTYPE","English_United States.1252")
​	author("demo") 
​	slidify("index.Rmd")
​	{% endhighlight %}

​	在当前R工作目录下建立一个命名demo的slidify目录,并建立index.Rmd,点击目录下的index.html可看到运行效果。

#### 2.2 slidify用法及参数设置

​	幻灯片页面间使用 --- 划分。

​	幻灯片的各页面内容可以使用markdown语法编写。


| 参数             | 说明                                       |
| :------------- | :--------------------------------------- |
| framework      | slidifyLibraries引入的h5模板：(io2012/deckjs/revealjs/shower/...)  【用好一个模板即可】 |
| highlighter    | slidifyLibraries引入代码高亮插件：(highlight.js/prettify) |
| hightheme      | 代码高亮的主题                                  |
| widget         | slidifyLibraries引入的数学工具mathjax(数学公式)/quiz(互动：单选多选框) |
| mode           | 插件调用的模式，本地方式、网络方式                        |
| ex_widget      | slidify以外的插件，如rcharts                    |
| --- .class #id | 在页首部能自定义页面格式，.后面定义全局，#后面定义局部。如--- .class #id bg:black该页面背景黑色 |

### 3 解决slidify中文乱码问题

> 如果你的操作系统为中文，使用slidify可能出现乱码现象。

​	方法1

+ `slidify`函数出错是因为R的环境语言的设置问题造成的，运行一段设置R语言环境的代码就可以完成这个工作:
  {% highlight ruby %}
  Sys.setlocale("LC_CTYPE", "English_United States.1252")#设置R语言环境<br/>
  slidify("index.Rmd")  
  {% endhighlight %}

+ 麻烦：每次打开R都要重新运行一遍这个代码，因为R语言环境重新回到简体中文形式。

​	方法2

+ 安装slidify中文优化包【亲测有效】
  {% highlight ruby %}
  install_github("lchiffon/slidify")
  {% endhighlight %}

![rtools](/img/demo.png) 

### 3 参考

+ [雪晴数据网-slidify+rCharts+ECharts制作炫酷HTML5 之如何使用slidify](http://www.xueqing.tv/lesson/142)




















