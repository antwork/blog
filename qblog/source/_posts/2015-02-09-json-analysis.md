---
date: 2015-02-09 09:46:12
layout: post
title: json基础及解析
categories: 日志
tags: json
---

json格式解析
-----------		

1. 格式2. 	
	* json两种构建方法:键值对组,通俗的说就是字典		
	* 有序的值组,通俗的说就是数组	
2. 元素构成3. 		 
	2.1 object(字典),以一个 { 开始,以 } 结束, 每组子元素以字符串为key:value形式由,分隔开来
	![](http://www.json.org/object.gif)	
	示例:```{"name":"xuqiang","gender":"男"}```	
	2.2 array(数组),以一个 [ 开始, 以 ] 结束,每组value由, 分隔   
	![](http://www.json.org/array.gif)  
	示例:```["张三","李四", "王五"]```	
	2.3 value(值), 可以是通过""包裹的字符串,可以是数字,可以是bool值(true,false),或者null,或者一个object(2.1),或者一个value(2.2),结构可以嵌套
	![](http://www.json.org/value.gif)	
	2.4 string(字符串),通过双引号包裹,如果中间需要加入引号,则需要使用\进行转移,如 ```"\""```,表示有一个引号,下图列出了需要转义的字符	
	![](http://www.json.org/string.gif)
	2.5 number(数字),一般使用十进制,不进行详细说明
	![](http://www.json.org/number.gif)
3. 在线解析辅助	 
	[www.bejson.com](http://json.parser.online.fr)    
	[http://json.parser.online.fr](http://json.parser.online.fr)
4. 使用示例:
5. iOS解析JSON

