---
date: 2015-03-24 10:06:12
layout: post
title: Flask database使用
categories: 日志
tags: python, flask, sqlalchemy, database
---
### Flask-SQLAlchemy的使用	

1. 初始化	
	* 安装sqlalchemy 		

	```(venv) $ pip install flask-sqlalchemy```		
	* 初始化:		

	```		
	# 导入包
	from flask.ext.sqlalchemy import SQLAlcheymy
	basedir = os.path.abspath(os.path.dirname(__file__))

	app = Flask(__name__)

	# 配置数据库路径
	app.config['SQLALCHEMY_DATABASE_URI'] =\
		'sqlite:///'+os.path.join(basedir,'data.sqlite')
	app.config(['SQLALCHEMY_COMMIT_ON_TEARDOWN']) = True

	# 初始
	db = SQLAlchemy(app) 
	```

2. 模型管理	

* 建立模型		

```		
class Role(db.Model):
	__tablename__ = 'roles'  # 自定义表名
	id = db.Column(db.Integer, primary_key=True)  # primary_key 主键
	name = db.Column(db.String(64), unique=True)  # unique 唯一
	def __repr__(self):
		return '<Role %r>' % self.name

class User(db.Model):= 'users'
	id = db.Column(db.Integer, primary_key=True)
	username = db.Column(db.String(64), unique=True, index=True) # index索引,有助于数据查询
	def __repr__(self):
		return '<User % __tablename__ r>' % self.username
```		
		
* 关系示例		

one-to-many示例:
```		
class Role(db.Model):
	# ...
	users = db.relationship('User', backref='role')

class User(db.Model):= 'users'
	# ..
	role_id = db.Column(db.Integer, db.ForeignKey('roles.id'))
```	

one-to-one示例:		

```		
class Role(db.Model):
	# ...
	user = db.relationship('User', backref='role', uselist=Flase) # 添加uselist为False

class User(db.Model):= 'users'
	# ..
	role_id = db.Column(db.Integer, db.ForeignKey('roles.id'))
```	

many-to-many示例:		

```		
# 关系定义需要先于model		
registrations = db.Table('registrations',
	db.Column('student_id', db.Integer, db.ForeignKey('students.id')),
	db.Column('class_id',db.Integer, db.ForeignKey('classes.id')))

class Student(db.Model):
	id = db.Column(db.Integer, primary_key=True)
	name = db.Column(db.String)
	classes = db.relationship('Class',
								secondary=registrations,
								backref=db.backref('students',lazy='dynamic'),
								lazy='dynamic')

class Class(db.Model):
	id = db.Column(db.Integer, primary_key=True)
	name = db.Column(db.String)

```

self many-to-many示例:		

```			
class Follow(db.Model):
	__tablename__ = 'follows'
	follower_id = db.Column(db.Integer, db.ForeignKey('users.id'),
                            primary_key=True)
    followed_id = db.Column(db.Integer, db.ForeignKey('users.id'),
                            primary_key=True)
    timestamp = db.Column(db.DateTime, default=datetime.utcnow)

class User(UserMixin, db.Model): 
	# ...
    followed = db.relationship('Follow',
                               foreign_keys=[Follow.follower_id],
                               backref=db.backref('follower', lazy='joined'),
                               lazy='dynamic',
                               cascade='all, delete-orphan')
    followers = db.relationship('Follow',
                                foreign_keys=[Follow.followed_id],
                                backref=db.backref('followed', lazy='joined'),
                                lazy='dynamic',
                                cascade='all, delete-orphan')


```	

UserMixin是什么鬼

[![](/assets/flask_sqlalchemy1.png)](/assets/flask_sqlalchemy1.png)   
[![](/assets/flask_sqlalchemy2.png)](/assets/flask_sqlalchemy2.png)   
[![](/assets/flask_sqlalchemy3.png)](/assets/flask_sqlalchemy3.png)    
[![](/assets/flask_sqlalchemy4.png)](/assets/flask_sqlalchemy4.png)    


