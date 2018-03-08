---
date: 2015-03-20 16:06:12
layout: post
title: Python Flask使用备忘
categories: 日志
tags: python, flask, alchemy
---

备忘:		

1. 处理请求参数:通过request.args.get可以获取get的参数和将参数放入header的post请求,如果需要处理将form-data的数据,需要使用request.form['key']获取

示例:		
```
method = request.method
if method == 'POST':
	username = request.form['username']
	password = request.form['password']
elif method == 'GET':
	username = request.args.get('username')
	password = request.args.get('password')
```
	
2. one-to-many的模型数据查询中,对于多的那一方查询,比如 person.posts,得到的时一个sql查询,需要使用person.posts.all()才能获取到数据		

3. 处理 @app.route('/xxx'), 如果是post请求记得,要添加methods=['POST']	



