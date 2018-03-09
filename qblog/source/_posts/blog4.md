---
title: 心酸心爽博客-Travis
date: 2018-03-09 22:52:07
tags: 
- travis
- ci
- blog
- hexo
- github
- ssh
---

...挖坑挖坑

1. addons: 必须使用原文, 不能使用${ENV_VAR}
2. ssh后不能继续- 命令了, 而应该在接下来的使用`ssh name@ip "cmd"` 将服务端的命令打包为一个shell脚本, 既对外隐藏了具体内容, 起到保护作用
3. shh方法

参考:
[Travis CI 系列：自动化部署博客](https://segmentfault.com/a/1190000011218410)

---
心酸心爽博客系列

* [博客存储-使用GitHub存储博客](/blog/2018/03/09/blog2/)
* [博客生成-Hexo生成博客网站](/blog/2018/03/09/blog3/)
* [自动化部署-Travis](/blog/2018/03/09/blog4/)