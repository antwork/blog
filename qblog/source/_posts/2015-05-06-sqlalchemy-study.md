---
date: 2015-05-06 16:49:12
layout: post
title: SQLAlchemy学习备份
categories: 日志
tags: flask, sqlalchemy
---

参考资料来源:
http://docs.sqlalchemy.org/en/rel_1_0/orm/tutorial.html

case1:
查询数据库中某些字段

session.query(User.name, User.fullname)

case2:
更换数据库返回的key
for row in session.query(User.name.label('name_label')).all();
	print(row.name_label)

case3:
偏移
for u in session.query(User).order_by(User.id)[1:3]:
	print u

意思为limit2 offset 1,即偏移1位,取2个值

case4:
filter_by(),使用关键词为key
	session.query(User.name).fitler_by(fullname="Ed jone") #这里是单等号

fitler()
	session.query(User.name).filter(User.fullname=="Ed jone") #这里是双等号

多重filter意味着条件与AND
	session.query(User.name).filter(User.name=="Ed jone").\
							 filter(User.fullname=="abc")


条件判断
等:
	query.filter(User.name == 'ed')

不等:
	query.filter(User.name != 'ed')

like:
	query.filter(User.name.like('%ed%%'))

IN:
	query.filter(User.name.in_(['ed','wendy','jack']))

	# 潜逃
	query.filter(User.name.in_(
		session.query(User.name).filter(User.name.like('%ed%'))
		))

NOT IN:
	query.filter(~User.name.in_(['ed','ab']))

IS Null:
	query.filter(User.name == None)

IS NOT NULL:
	query.filter(User.name != None)

AND:
	#方法1 使用and_
	from sqlalchemy import and_
	query.filter(and_(User.name=='ed', User.fullname=='ab'))

	#方法2 使用多表达式
	query.filter(User.name == 'ed', User.fullname=='bc')

	#方法3 串表达式
	query.filter(User.name=='ed').fiter(User.fullname=='bc')

OR:
	from sqlachemy import or_
	query.filter(or_(User.name=='ed', User.name=='wendy'))

MATCH:
	query.filter(User.name.match('wendy'))

使用字面sql
	# 使用局部的sql条件
	from sqlalchemy import text
	from user in session.query(User).\
				filter(text("id<224")).\
				order_by(text("id")).all():
		print user.name

	关联参数,可以使用params()方法
	session.query(User).filter(text("id<:value and name=:name")).\
			params(value=224, name='fred').order_by(User.id).one()

	全string的sql语句查询
	session.query(User).from_statement(
			text("SELECT * FROM users where name=:name")).\
			params(name='ed').all()

计数:
	session.query(User).filter(User.name.like('%ed')).count()


数据库关系:
one to many:
	在子表中添加foreignkey, 在父表中添加关系

	class Parent(Base):
		__tablename__ = 'parent'
		id = Column(Integer, primary_key=True)
		children = relationship('Child')

	class Child(Base):
		__tablename__ = 'child'
		id = Column(Integer, primary_key=True)
		parent_id = Column(Integer, ForeignKey('parent.id'))

	# 双向关系 bidirectional relationship 使用backref选项
	class Parent(Base):
		__tablename__ = 'parent'
		id = Column(Integer, primary_key=True)
		children = relationship("Child", backref="parent")

	class Child(Base):
		__tablename = 'child'
		id = Column(Integer, primary_key=True)
		parent_id = Column(Integer, ForeignKey('parent.id'))

Many to one:
	class Parent(Base):
		__tablename__ = 'parent'
		id = Column(Integer, primary_key = True)
		child_id = Column(Integer, ForeignKey('child.id'))
		child = relationship('Child', backref="parents")

	class Child(Base):
		__tablename__ = 'child'
		id = Column(Integer, primary_key=True)

One to one:
	方式一:
	class Parent(Base):
		__talbename__ = 'parent'
		id = Column(Integer, primary_key=True)
		child = relationship('Child', uselist=False, backref='parent')

	class Child(Base):
		__tablename__ = 'child'
		id = Column(Integer, primary_key=True)
		parent_id = Column(Integer, ForeignKey('parent.id'))

	方式二: 

	class Parent(Base):
	    __tablename__ = 'parent'
	    id = Column(Integer, primary_key=True)
	    child_id = Column(Integer, ForeignKey('child.id'))
	    child = relationship("Child", backref=backref("parent", uselist=False))

	class Child(Base):
		    __tablename__ = 'child'
		    id = Column(Integer, primary_key=True)

Many-to-many:
	association_table = Table('association', Base.metadata,
		Column('left_id', Integer, ForeignKey('left.id')),
		Column('right_id', Integer, ForeignKey('right.id'))
	)

	class Parent(Base):
		__tablename__ = 'left'
		id = Column(Integer, primary_key=True)
		children = relationship('Child', secondary =association_table)

	class Child(Base):
		__tablename__ = 'right'
		id = Column(Integer, primary_key=True)

	# 双向关系
	association_table = Table('association', Base.metadata,
	    Column('left_id', Integer, ForeignKey('left.id')),
	    Column('right_id', Integer, ForeignKey('right.id'))
	)

	class Parent(Base):
	    __tablename__ = 'left'
	    id = Column(Integer, primary_key=True)
	    children = relationship("Child",
	                    secondary=association_table,
	                    backref="parents")

	class Child(Base):
	    __tablename__ = 'right'
	    id = Column(Integer, primary_key=True)


	    


Bind parameters can be specified with string-based SQL, using a colon. To specify the values, use the params() method:
	>>> session.query(User).filter(text("id<:value and name=:name")).\
	...     params(value=224, name='fred').order_by(User.id).one() 
