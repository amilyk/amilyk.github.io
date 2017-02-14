---
layout:     post
title:      "python开发简单爬虫(2)"
date:       2017-02-14
author:     "xunkang"
header-img: "img/post-bg-version.jpg"
catalog: true
tags:
    - 爬虫
---


> 续接 [python开发简单爬虫 (1)]()

### 6 网页下载器

#### 6.1 网页下载器

​	网页下载器会将网页下载到本地。

+ 以html形式下载到本地
+ 保存成本地文件

  python 网页下载器的**种类**：

+ urllib2【官方】 
+ requests【第三方包，强大】

#### 6.2 urllib2下载网页的方法

I. url传递给函数urllib2.urlopen(url)

{% highlight python %}
# -*- coding: utf-8 -*-
##加utf格式就能支持中文注释

import urllib2
#直接请求
response = urllib2.urlopen('http://baidu.com')
##获取状态码，如果是200，表明获取成功
print response.getcode()
# 读取内容
cont = response.read()
{% endhighlight %}

II. 添加data、http header，和url一起形成Request对象

{% highlight python %}
import urllib2
#创建Request对象
request = urllib2.Request(url)
#添加数据
request.add_data('a','1')
#添加http的header，将浏览器伪装成Mozilla的浏览器
request.add_header('User-Agent','Mozilla/5.0')
#发送请求获取结果
response = urllib2.urlopen(request)
{% endhighlight %}

III. 有的网页需要登陆、代理、或者https协议加密访问、URL存在相互自动跳转关系，将添加的handler放到builder_opener,创建opener对象，将url install_opener(opener)，就拥有这些场景的处理能力。


{% highlight python %}
import urllib2
import cookielib
#创建cookie容器
cj = cookielib.CookieJar()
#创建opener
opener = urllib2.build_opener(urllib2.HTTPCookieProcessor(cj))
#给urllib2安装opener
urllib2.install_opener(opener)
#带cookie的urllib2访问网页
response = urllib2.urlopen('http://www.baidu.com')
print response1.read()
print cj
print response1.getcode()
{% endhighlight %}

### 7 网页解析器

#### 7.1 网页解析器

+ 正则表达式，模糊匹配
+ html.parser【python自带】
+ Beauttiful Soup：【第三方插件】，能使用lxml或html.parser作为解析器
+ lxml【第三方插件】，(解析xml网页)

> 除了正则表达式，其他解析方式为**结构化解析**。网页文档下载为**DOM**【Document Object Model文档对象模型】树，树形结构，**上下级元素遍历**，从根结点到子元素或属性，没有子元素或属性就为文本。

#### 7.2 Beautiful Soap安装及使用

#### 安装

​	检查是否已经安装过，在python环境中输入以下代码：

{% highlight python %}
import bs4
print bs4
{% endhighlight %}

​	运行结果：

​	<module 'bs4' from 'D:\python\Anaconda2\lib\site-packages\bs4\__init__.py'>，表明已安装过。

​	实际上：安装Anaconda2最新版，里面会安装好Beautiful Soap插件。若是安装Anaconda2，却没有该插件。可利用conda在cmd中安装。安装参考[教程](http://www.jianshu.com/p/d2e15200ee9b)

#### 语法

​	根据下载好的html网页，创建Beautiful Soap对象后，即已经将网页转变为DOM树。然后用搜索结点'find_all'、 'find'方法,搜索参数为结点名称、属性和文字。

![](/img/soup.png)

1. 创建Beautiful Soap对象

{% highlight python %}
# -*- coding: utf-8 -*-
# 加utf格式就能支持中文注释

from bs4 import BeautifulSoup
#根据HTML网页字符串，创建BeautifulSoap对象
soup = BeautifulSoup(
    html_doc ,#html文档字符串
    'html.paser' #解析器
    from_encoding='utf_8'#html文档编码，需与python脚本编码一致，不然乱码
)
{% endhighlight %}

2. 搜索结点，'find'与'find_all'函数的参数都是相同的，但是find_all方法可以找到所有满足条件的结点，find方法只会找出满足条件的第一个结点。以'find_all'为例

   find_all(name,attr,string)	#参数分别为名称、属性和文字，同时三个参数都用正则表达式来表示。

![](/img/find.png)

​	**注意**：这里class_加了下划线，为了与python里class关键字区分。

#### 访问节点信息

{% highlight python %}
node.name#获取节点名称
node['href']#获取href属性
node.get_text#获取节点文字
{% endhighlight %}

#### 实例

{% highlight python %}
from bs4 import BeautifulSoup
import re
#根据HTML网页字符串，创建BeautifulSoap对象
soup = BeautifulSoup(
    html_doc,#html文档字符串
    'html.parser', #解析器
    from_encoding='utf_8'#html文档编码，需与python脚本编码一致，不然乱码
)
print '获取所有的链接，其名称、属性及文字'
node = soup.find_all('a')
for link in node:
    print link.name,link['href'],link.get_text()

print '正则匹配'
link1 = soup.find('a',href=re.compile(r"ill"))
print link1.name,link1['href'],link1.get_text()
{% endhighlight %}

### 8 爬虫实例

#### 8.1分析目标

#### 理论

+ 哪个网站哪些网页的数据。**这里，爬取百度百科python及python相关数据**
+ 爬取的策略。URL格式【确定范围】、数据格式【数据所在标签的格式】、网页编码
+ 编写代码
+ 执行爬虫

#### 实践

+ 查看URL，先进入百度百科，搜索python，得到搜索栏中的URL格式。
+ 查看页面上其他链接，鼠标放在链接上，右击审查元素或检查，得到其他URL格式。
+ 查看标题：选中标题，右键审查元素或检查。h1
+ 查看简介：选中简介，右键审查元素或检查。div class=
+ 查看网页编码：在网页空白处，右键审查元素或检查，打开head标签，找到meta charset。

![](/img/example.png)

#### 8.2 实例

​	问题：爬取百度百科前1000个python相关网页。

​	解决：**完整代码及使用说明**点击我的[github](https://github.com/amilyk/spider)

### 参考


[慕课网 python开发简单爬虫](http://www.imooc.com/learn/563)

