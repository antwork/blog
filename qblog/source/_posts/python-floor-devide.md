---
title: Python floor devide用法(符号://)
copyright: true
date: 2018-04-20 10:20:09
tags:
- python
- python3
- floordevide
- devide
---

### 前言:

前两天被同事问了下//这个和/有啥区别, 有点懵, 了解了下:

### 结论

````python
result = a // b 等价于 floor(a/b)

# floor函数:
# floor(x)，也写做Floor(x)，其功能是“向下取整”，或者说“向下舍入”，即取不大于x的最大整数（与“四舍五入”不同，下取整是直接取按照数轴上最接近要求值的左边值，即不大于要求值的最大的那个值）。
````

>floor函数有点意思, 对结果floor后总返回的是比结果更小的整数
>
>`10 // 3`  # 结果 3  == floor(3.333…) == 3
>
>`10 // -3` #结果 -4  == floor(-3.33...) == -4



关于除法备注:

> python2整数除法返回整数
>
> python3整数除法返回浮点数
>
> 所以在python2中检验 // 没啥效果

```python
Python2: 
int / int = int

示例:
Python 2.7.10 (default, Oct  6 2017, 22:29:07)
[GCC 4.2.1 Compatible Apple LLVM 9.0.0 (clang-900.0.31)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 1 / 2
0

Python3:
int / int = float

示例:
Python 3.6.4 (v3.6.4:d48ecebad5, Dec 18 2017, 21:07:28)
[GCC 4.2.1 (Apple Inc. build 5666) (dot 3)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 1 / 2
0.5
```



### 参考:

[floor函数说明](https://baike.baidu.com/item/floor函数/1344448?fr=aladdin)