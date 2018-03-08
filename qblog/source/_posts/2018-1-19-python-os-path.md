---
date: 2018-1-19 09:52:12
layout: post
title: python study os.path os path
categories: 日志
tags: python
---

##os.path使用示例

*参考 [python os.path模块常用方法详解](http://blog.51cto.com/wangwei007/1104940)*

### 0. 前置
- import os.path module
- 示例文件路径: /Users/bill/Documents/Study/Python

```
>>> import os.path
```

###1. os.path.abspath获取绝对地址
```
>>> os.path.abspath('readme.txt')
'/Users/bill/Documents/Study/Python/readme.txt'
>>> os.path.abspath('/Users/bill/Documents/Study/Python/readme.txt')
'/Users/bill/Documents/Study/Python/readme.txt'
>>> os.path.abspath(r'../Python/readme.txt')
'/Users/bill/Documents/Study/Python/readme.txt'
```

###2. os.path.split将路径分割为目录和文件名两部分 path = (dir, filename)
*注意: 目录必须以'/'结尾, 否则最后一级会被当成filename*

```
>>> os.path.split('/Users/bill/Documents/Study/Python/readme.txt')
('/Users/bill/Documents/Study/Python', 'readme.txt')
>>> os.path.split('/Users/bill/Documents/Study/Python/')
('/Users/bill/Documents/Study/Python', '')
>>> os.path.split('/Users/bill/Documents/Study/Python')
('/Users/bill/Documents/Study', 'Python')
>>> os.path.split('readme.txt')
('', 'readme.txt')
```

###3. os.path.dirname获取路径中目录部分, 本质是os.path.split的第一部分
``` 
>>> os.path.dirname('readme.txt')
''
>>> os.path.dirname('/Users/bill/Documents/Study/Python/readme.txt')
'/Users/bill/Documents/Study/Python'
>>> os.path.dirname('/Users/bill/Documents/Study/Python/')
'/Users/bill/Documents/Study/Python'
>>> os.path.dirname('/Users/bill/Documents/Study/Python')
'/Users/bill/Documents/Study'
```
### 4. os.path.basename获取路径文件名, 本质是os.path.split的第二部分
**注**: 如果文件夹末尾没有添加'/', 会将文件夹最后一部分当成文件名

```
>>> os.path.basename('/Users/bill/Documents/Study/Python/readme.txt')
'readme.txt'
>>> os.path.basename('/Users/bill/Documents/Study/Python/')
''
>>> os.path.basename('/Users/bill/Documents/Study/Python')
'Python'
```
### 5. os.path.commonprefix获取list中路径共有的最长路径
```
>>> os.path.commonprefix(['/usr/bin/a.txt', '/usr/bin/bin1/b.txt', '/usr/bin/bin2/c.txt'])
'/usr/bin/'
```
### 6. os.path.exists判断文件是否存在
```
>>> os.path.exists('/Users/bill/Documents/Study/Python/readme.txt')
True
>>> os.path.exists('/Users/bill/Documents/Study/Python/nonexist.txt')
False
```
### 7. os.path.isabs判断是否绝对路径
```
>>> os.path.isabs('/Users/bill/Documents/Study/Python/readme.txt')
True
>>> os.path.isabs('./a/b')
False
```

### 8. os.path.isfile判断是否文件
```
>>> os.path.isfile('/Users/bill/Documents/Study/Python/readme.txt')
True
>>> os.path.isfile('/Users/bill/Documents/Study/Python/')
False
```
### 9. os.path.isdir判断是否文件夹

```
>>> os.path.isdir('/Users/bill/Documents/Study/Python/readme.txt')
False
>>> os.path.isdir('/Users/bill/Documents/Study/Python/')
True
>>> os.path.isdir('/Users/bill/Documents/Study/Python')
True
```
### 10. os.path.join将参数拼成完整路径, 第一个绝对参数之前的参数会被忽略
*随便传了个数组参数竟然直接返回了数组*

```
>>> os.path.join(['/usr', 'bin', 'python'])
['/usr', 'bin', 'python']
>>> os.path.join('usr', 'bin', 'python')
'usr/bin/python'
>>> os.path.join('notshow', '/usr', 'bin')
'/usr/bin'
```
### 11. os.path.normcase(path), 在windows平台会将路径中所有字符转换为小写, 并将所有斜杠转为反斜杠, linux/Mac直接返回path
```
# mac平台
>>> os.path.normcase('/Users/lunkr/Documents/Study/Python/readme.txt')
'/Users/lunkr/Documents/Study/Python/readme.txt'
>>> os.path.normcase('/Users/lunkr/Documents/Study/Python\readme.txt')
'/Users/lunkr/Documents/Study/Python\readme.txt'

# windows
>>> os.path.normpath('c://windows\\System32\\../Temp/') 
'c:\\windows\\Temp' 
...
```

### 12. os.path.splitdrive -> tuple:(盘符, 相对路径)
```
>>> os.path.splitdrive('/Users/bill/Documents/Study/Python/readme.txt')
('', '/Users/bill/Documents/Study/Python/readme.txt')
```
### 13. os.path.splitext获取文件名扩展
```
>>> os.path.splitext('/Users/bill/Documents/Study/Python/readme.txt')
('/Users/bill/Documents/Study/Python/readme', '.txt')
>>> os.path.splitext('/Users/bill/Documents/Study/Python/readme')
('/Users/bill/Documents/Study/Python/readme', '')
```
### 14. 获取文件大小
*---- 如果文件不存在, 会报OSError*

```
>>> os.path.getsize('/Users/bill/Documents/Study/Python/readme.txt')
472
>>> os.path.getsize('/Users/bill/Documents/Study/Python/nonexist.txt')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/usr/local/Cellar/python/2.7.9/Frameworks/Python.framework/Versions/2.7/lib/python2.7/genericpath.py", line 49, in getsize
    return os.stat(filename).st_size
OSError: [Errno 2] No such file or directory: '/Users/bill/Documents/Study/Python/nonexist.txt'
```
### 15. os.path.getatime获取文件最后存取时间
*---- 如果文件不存在, 会报OSError*

```
>>> os.path.getatime('/Users/bill/Documents/Study/Python/readme.txt')
1516322694.9506512
>>> os.path.getatime('/Users/bill/Documents/Study/Python/nonexist.txt')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/usr/local/Cellar/python/2.7.9/Frameworks/Python.framework/Versions/2.7/lib/python2.7/genericpath.py", line 59, in getatime
    return os.stat(filename).st_atime
OSError: [Errno 2] No such file or directory: '/Users/bill/Documents/Study/Python/nonexist.txt'
```
### 16. os.path.getmtime获取文件最后修改时间
*---- 如果文件不存在, 会报OSError*

```
>>> os.path.getmtime('/Users/bill/Documents/Study/Python/readme.txt')
1516169147.8499017
```
