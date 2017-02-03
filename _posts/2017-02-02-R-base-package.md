---
layout:     post
title:      "[基础]R包安装及卸载"
date:       2017-02-02 11:00:00
author:     "XunKang"
header-img: "img/post-bg-js-version.jpg"
tags:
    - R
---


## 1. 安装R包

###	install.packages("car",lib = "D:/software_install/Rpackage",dependencies = TRUE)

### 	lib参数不填，会按照默认路径安装。dependences参数默认为False，True安装该包的依赖包。若出现包安装完毕，但是无法require，可以改dependences为True试试。



## 2. 卸载R包

###	remove.packages("car",lib = "D:/software_install/Rpackage")

## 3. require与library区别

###	在一个函数中，如果一个包不存在，执行到library将会停止执行，require则会继续执行。require将会根据包的存在与否返回true或者false。

## 4. 包安装问题

###	包library以后可能出现某个包不存在导致library失败。即使在安装时加了dependencies = TRUE，安装了依赖包。但是有时候根据错误提示，安装缺少的包，先library缺少的包，再library该包。

+ ## 例如

  ###library(car,lib.loc = "D:/software_install/Rpackage")

> Error in loadNamespace(j <- i[[1L]], c(lib.loc, .libPaths()), versionCheck = vI[[j]]) :   不存在叫‘minqa’这个名字的程辑包Error: ‘car’程辑包或名字空间载入失败，

### 	install.package("minqa",lib = "D:/software_install/Rpackage")

> package ‘minqa’ successfully unpacked and MD5 sums checked

### 	library(minqa,lib.loc = "D:/software_install/Rpackage")

### 	library(car,lib.loc = "D:/software_install/Rpackage")