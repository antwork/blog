---
date: 2014-10-26 22:30:12
layout: post
title: "Markdown语法的学习和实践"
description: ""
category: 文档
tags: markdown 
---

本文为[antwork](http://antwork.github.io)原创，转载请注明作者及出处！

##目录
----
&nbsp;&nbsp;&nbsp;&nbsp;[**标题**](#title)    
&nbsp;&nbsp;&nbsp;&nbsp;[**区块元素**](#block)  
&nbsp;&nbsp;&nbsp;&nbsp;[**链接**](#link)  
&nbsp;&nbsp;&nbsp;&nbsp;[**图片链接**](#imagelink)  
&nbsp;&nbsp;&nbsp;&nbsp;[**代码插入**](#code)  
&nbsp;&nbsp;&nbsp;&nbsp;[**参考**](#reference)

<a id='introduce' name='introduce'> </a> 

##标题
----


有两种表示段落的方式:

- 类Setext形式
- Atx形式

**类Setext形式**:只能表示两级,最高阶标题=和第二阶标题-, 例如:    

这是H1标题
====
这是H2标题
---
任何数量的 = 和 - 都可以有效果
效果:

这是H1标题
=

这是H2标题
-

任何数量的 = 和 - 都可以有效果

**\[Warn\]**连续的标题需要中间添加一行空白行

**类 Atx形式:**在行首插入1到6个#，对应到标题1到6阶，例如：  

# 这是 H1

## 这是 H2

###### 这是 H6
效果:  

# 这是 H1

## 这是 H2

###### 这是 H6

**\[Warn\]**第一个标题与顶部需要留空白行

<a id='block' name='block'> </a>

##区块元素

### &nbsp;&nbsp;段落和换行
---

**段落**:由一个或者多个连续的文本组成,它的前后要有一个以上的空格,我的建议是段落的前后都留空行,

比如这样:


我是段落1,我很孤独

我是段落2,我很孤独2



得到的效果图如下:

我是段落1,我很孤独

我是段落2,我很孤独

**换行**:这个有些狗血,在插入处先按入两个以上的空格然后回车,可以得到<br />的效果,两者可以通用,注意我很孤独后面还有两个空白


我是段落1,我很孤独   
我是段落2,我很孤独



得到的效果图如下:

我是段落1,我很孤独   
我是段落2,我很孤独



我是段落1,我很孤独<br />
我是段落2,我很孤独



得到的效果图如下:

我是段落1,我很孤独   
我是段落2,我很孤独

<a href='link' name='link'> </a>

##链接
----

链接文字使用\[方括号\]来标记  
行内式:只要在方括号后面紧接着圆括号并插入网址链接即可,如果你还想要加上链接的 title 文字，只要在网址后面，用双引号把 title 文字包起来即可，例如


This is [an example](http://example.com/ "Title") inline link.

[This link](http://example.net/) has no title attribute.



得到效果图如下:

This is [an example](http://example.com/ "Title") inline link.

[This link](http://example.net/) has no title attribute.

<a href='imagelink' name='imagelink'> </a>

##图片链接
---

格式:!\[方括号\]\(链接\)   
示例:   


垃圾百度![Icon](http://www.baidu.com/img/bdlogo.png)



得到效果图如下:   
垃圾百度![Icon](http://www.baidu.com/img/bdlogo.png)

<a id='code' name='code'> </a>

#代码
---
缩进四个空白\(Tab\)
示例:    


这是一个普通段落：

    这是一个代码区块。



效果:

这是一个普通段落：

    这是一个代码区块。


<a id="reference" name="reference"> </a>

##参考
----

1. 资源网址:[wowubuntu.com](wowubuntu.com/markdown)
2. 学习模板1:[WebFrogs](http://webfrogs.me)
3. 学习模板2:[Yonsm.NET](http://www.yonsm.net)

***

##全文源代码如下:
----



本文为[antwork](http://antwork.github.io)原创，转载请注明作者及出处！

##目录
----
&nbsp;&nbsp;&nbsp;&nbsp;[**标题**](#title)    
&nbsp;&nbsp;&nbsp;&nbsp;[**区块元素**](#block)  
&nbsp;&nbsp;&nbsp;&nbsp;[**链接**](#link)  
&nbsp;&nbsp;&nbsp;&nbsp;[**图片链接**](#imagelink)  
&nbsp;&nbsp;&nbsp;&nbsp;[**代码插入**](#code)  
&nbsp;&nbsp;&nbsp;&nbsp;[**参考**](#reference)

<a id='introduce' name='introduce'> </a> 

##标题
----


有两种表示段落的方式:

- 类Setext形式
- Atx形式

**类Setext形式**:只能表示两级,最高阶标题=和第二阶标题-, 例如:    



这是H1标题
====
这是H2标题
---
任何数量的 = 和 - 都可以有效果

效果:

这是H1标题
=

这是H2标题
-

任何数量的 = 和 - 都可以有效果

**\[Warn\]**连续的标题需要中间添加一行空白行

**类 Atx形式:**在行首插入1到6个#，对应到标题1到6阶，例如：  


# 这是 H1

## 这是 H2

###### 这是 H6

效果:  

# 这是 H1

## 这是 H2

###### 这是 H6

**\[Warn\]**第一个标题与顶部需要留空白行

<a id='block' name='block'> </a>

##区块元素

### &nbsp;&nbsp;段落和换行
---

**段落**:由一个或者多个连续的文本组成,它的前后要有一个以上的空格,我的建议是段落的前后都留空行,

比如这样:


我是段落1,我很孤独

我是段落2,我很孤独2



得到的效果图如下:

我是段落1,我很孤独

我是段落2,我很孤独

**换行**:这个有些狗血,在插入处先按入两个以上的空格然后回车,可以得到<br />的效果,两者可以通用,注意我很孤独后面还有两个空白


我是段落1,我很孤独   
我是段落2,我很孤独



得到的效果图如下:

我是段落1,我很孤独   
我是段落2,我很孤独



我是段落1,我很孤独<br />
我是段落2,我很孤独



得到的效果图如下:

我是段落1,我很孤独   
我是段落2,我很孤独

<a href='link' name='link'> </a>

##链接
----

链接文字使用\[方括号\]来标记  
行内式:只要在方括号后面紧接着圆括号并插入网址链接即可,如果你还想要加上链接的 title 文字，只要在网址后面，用双引号把 title 文字包起来即可，例如


This is [an example](http://example.com/ "Title") inline link.

[This link](http://example.net/) has no title attribute.



得到效果图如下:

This is [an example](http://example.com/ "Title") inline link.

[This link](http://example.net/) has no title attribute.

<a href='imagelink' name='imagelink'> </a>

##图片链接
---

格式:!\[方括号\]\(链接\)   
示例:   


垃圾百度![Icon](http://www.baidu.com/img/bdlogo.png)



得到效果图如下:   
垃圾百度![Icon](http://www.baidu.com/img/bdlogo.png)

<a id='code' name='code'> </a>

#代码
---
缩进四个空白\(Tab\)
示例:    


这是一个普通段落：

    这是一个代码区块。



效果:

这是一个普通段落：

    这是一个代码区块。


<a id="reference" name="reference"> </a>

##参考
----

1. 资源网址:[wowubuntu.com](wowubuntu.com/markdown)
2. 学习模板1:[WebFrogs](http://webfrogs.me)
3. 学习模板2:[Yonsm.NET](http://www.yonsm.net)

