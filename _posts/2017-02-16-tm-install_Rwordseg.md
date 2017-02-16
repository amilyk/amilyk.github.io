---
layout:     post
title:      "Rwordseg 安装"
date:       2017-02-16
author:     "xunkang"
header-img: "img/post-bg-version.jpg"
tags:
    - 文本挖掘
---


> Rwordseg的安装依赖rJava包，但是rJava包安装前需要本地安装java、jdk环境

​	**I**.安装java及jdk

+ [java安装链接](http://www.java.com/zh_CN/)	
+ [jdk安装链接](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
+ **安装注意事项**,先安装java，然后安装jdk。如java安装目录为D:/software_install/R/Java。可将jdk安装目录设置在Java目录下，如D:/software_install/R/Java/jdk。其中，安装jdk时会跳出安装jre，jre安装可在Java目录下，不与jdk同一文件夹。如：D:/software_install/R/Java/jdk/jre。安装都是不断执行下一步。



​	**II**.配置Java环境变量

​	右击【我的电脑】---【属性】-----【高级】---【环境变量】

​	(1) 新建系统变量，名为JAVA_HOME，其值为jdk安装路径D:/software_install/R/Java/jdk

​	(2) 在“系统变量”选项区域中查看PATH变量，如果不存在，则新建变量 PATH，否则选中该变量，单击“编辑”按钮，在“变量值”文本框的起始位置添加“%JAVA_HOME%/bin;%JAVA_HOME%/jre/bin;”，若前一个路径没有;,需要加上; ，再添加路径。

​	(3) 在“系统变量”选项区域中查看CLASSPATH 变量，如果不存在，则新建变量CLASSPATH，否则选中该变量，单击“编辑”按钮，在“变量值”文本框的起始位置添加“.;%JAVA_HOME%/lib/dt.jar;%JAVA_HOME%/lib/tools.jar;”【注意】路径最前的 .不要忘记。

​	(4) 配置完成后，若是在命令行中输入java、javac均有帮助信息，即配置正确,jdk、jre、java安装成功。	

​	(5)为了运行rJava，假设R包的安装目录为D:/software_install/R/R-3.3.2/library，jre安装在D:/software_install/R/Java/jdk/jre。另外，需要将以下路径添加至path环境变量中。

+ D:/software_install/R/Java/jdk/jre/bin
+ D:/software_install/R/Java/jdk/jre/bin/server
+ D:/software_install/R/R-3.3.2/library/rJava/jri


​	**III**.下载安装rJava包及Rwordseg包
{% highlight ruby %}
install.packages("rJava")
install.packages("Rwordseg", repos="http://R-Forge.R-project.org")
{% endhighlight %}

​	因为Rwordseg包不在CRAN上，所以安装时需要设置repos。

#### 	若是网速不好

+ [R-Forge下载Rwordseg包](http://R-Forge.R-project.org/src/contrib/Rwordseg_0.2-1.tar.gz)，本地安装。


+ [github下载Rwordseg包](https://github.com/lijian13/Rwordseg)，本地安装。
+ github上获得Rwordseg的[git地址](https://github.com/lijian13/Rwordseg.git)，用git bash的git clone命令。然后打包文件为zip，本地安装。


​	**IV**.导入R包，并运行demo
{% highlight ruby %}
library(rJava)
library(Rwordseg)
##导入Rwordseg安装目录下的demo，并运行
source('Rwordseg/demo/demo.R')
##简单分词
segmentCN("hello word!")
{% endhighlight %}

