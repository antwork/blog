---
title: python字符串常用函数用法
copyright: true
date: 2018-04-12 00:22:18
tags: [python, python3, string]
categories: python
---

## python字符串常用函数用法

主要介绍内容如下: 1) 存在判断	2) 字符串格式化	3) 字符串拼接 4) 其他





### 1) 字符串存在判断:

* `a.startswith(b)` a是否以b开始, 返回布尔值
*  `a.endswith(b)` a是否以b结束, 返回布尔值
* `a in b` : 字符串a是否在字符串b内,  True包含, False不包含
* 使用`a.find(b)`找到返回位置, 找不到返回-1
* `re`正则匹配(以及忽略大小写写法)

```python
>>> s = 'hello world'
>>> s.startswith('hello')
True
>>> s.startswith('world')
False
>>> s.endswith('hello')
False
>>> s.endswith('world')
True
>>> 'ello' in s
True
>>> 'xx' in s
False

>>> 'hello'.find('l')
2
>>> 'hello'.find('z')
-1

>>> import re
>>> bool(re.search('[许小]路', '许小路'))
True
>>> bool(re.search('[许小]路', '小路'))
True
>>> bool(re.search('[许小]路', ' 许路))
True
>>> bool(re.search('[许小]路', '杨路'))
False
# 忽略大小写
>>> bool(re.search('hello', 'HELLO WORLD', re.I))
True
>>> bool(re.search('hello', 'HELLO WORLD'))
False
```



### 2) 字符串格式化

* 方法1: 使用 %

  > 单个值直接使用 % value `"abc %s" % 'value'`
  >
  > 多个值使用Tuple

* 方法2: 使用format格式化字符串

  > 注意: key不需要使用引号, 多个值使用逗号`,`隔开

* 方法3: 使用format格式化对象

```python
>>> "hello %s" % '许路'
'hello 许路'
>>> "hello %s %s" % ("许", "路")
'hello 许 路'

>>> "hello {name}".format(name="许路")
'hello 许路'
>>> "hello {f_name}{l_name}".format(f_name='许', l_name='强')
'hello 许强'
>>> "hello {f_name}{l_name}".format(f_name='许', 'l_name'='强')
  File "<stdin>", line 1
SyntaxError: keyword can't be an expression

# 格式化对象
>>> class M(object):
...     def __init__(self, f_name, l_name):
...             self.f_name = f_name
...             self.l_name = l_name
...
>>> m = M('许', '路')
>>> "{obj.f_name} {obj.l_name}".format(obj=m)
'许 路'
```



### 3) 字符串拼接

```python
>>> "许" + "路"
'许路'

# 在print中使用逗号分隔多个字符串
>>> print('hello', 'world', 'yeah')
hello world yeah
```



### 4) 其他

```python
# 长度
>>> len("中国")
2

# 字符串分割
>>> 'xizhipian.com'.split('.')
['xizhipian', 'com']

# 字符串数组合并
>>> '.'.join(['xizhipian', 'com'])
'xizhipian.com'

# 大小写
>>> "hello".upper()
'HELLO'
>>> "Hello".lower()
'hello'

# 替换
>>> "hello world".replace('world', 'qxu')
'hello qxu'
>>> "hello world world world".replace('world', 'qxu')
'hello qxu qxu qxu'
# 指定替换次数
>>> "hello world world world".replace('world', 'qxu', 1)
'hello qxu world world'

# 截取字符串
>>> str = "0123456789"
>>> str[0:3]
'012'
>>> str[:]
'0123456789'
>>> str[:-3]
'0123456'
>>> str[-3:]
'789'
```





参考链接:

[python re官网说明: https://docs.python.org/2/library/re.html](https://docs.python.org/2/library/re.html)