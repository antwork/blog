---
date: 2015-04-18 07:44:12
layout: post
title: Flask和SQLAlchemy
categories: 日志
tags: flask, 怎么使用virtualenv
---

### Flask和SQLAlchemy

#### 安装

怎么使用virtualenv

1. 安装virtualenv
$ sudo easy_install virtualenv
或者 $ sudo pip install virtualenv

2. 添加virtualenv到文件夹
$ virtualenv venv

3. 激活virtual环境
$ . venv/bin/activate

4. 安装python

5. 安装flask到虚拟环境,如果全局使用 $ sudo pip install Flask
$  pip install Flask

6. 安装 SQLAlchemy
$ pip install flask-sqlalchemy
学习网站: http://pythonhosted.org/Flask-SQLAlchemy/quickstart.html

7. 操作数据库前需要先创建

8. 安装依赖
	------------------------------------------
	将当前的依赖包放入requrements.txt中
	(venv) $ pip freeze >requirements.txt

	------------------------------------------
	安装依赖包
	(venv) $ pip install -r requirements.txt
