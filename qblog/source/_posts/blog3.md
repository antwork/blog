---
title: 心酸心爽博客-Hexo生成博客网站
date: 2018-03-09 22:52:01
tags:
- travis
- ci
- blog
- hexo
- github
- ssh
---

> 仓库准备好了，就等文章到碗里来了，这里选用hexo, 想着原来就用过，上手会挺快。😔，实际做着高大上， 默认是英文界面，看了半天的英文才发现有中文版。
> [Hexo中文官网](https://hexo.io/zh-cn/)    
> [docs/commands.html](https://hexo.io/zh-cn/docs/commands.html)

*官网的文档已经很简略了，我就不重复，自己去看文档，这里就做点代码注释吧。*

### 常用指令:

```shell
hexo init [folder] # 新建一个网站, 如果没有设置 folder ，Hexo 默认在目前的文件夹建立网站。没看文档吃亏了，搞了个子文件夹，后面各种不舒适。

hexo g # 生成静态网站

hexo s # 启动服务, 默认通过localhost:4000可以访问静态网站

hexo new [layout] title # 生成新文章, 默认layout为post, 还可以是draft

hexo clean # 删除静态网站, 然后再次调用`hexo g` 

hexo d # 部署

hexo s --debug # 启动服务, 调试模式, 可以查看日志

hexo s -p 5000 # 启动服务, 端口=5000
```

### 关于主题：

1. 以前老想着抠人家的css, 各种复杂，hexo提供了近200个主题可供选择：[https://hexo.io/themes/](https://hexo.io/themes/)   
2. 找到满意的主题，然后找到对应的github网址(*基本所有主题都会在网页最底端提供链接指向主题网址*), 类似如下：
![主题源码](/blog/assets/theme_snap.png)		
3. 单个主题文件夹如下图所示，原理很简单, 将主题文件夹如landscape拷贝到themes文件夹下（网上方法为gitclone，原理一样），编辑**项目的_config.yml(不是主题里文件夹里的_config.yml,不是主题里文件夹里的_config.yml,不是主题里文件夹里的_config.yml)**,找到`theme: [主题文件夹名称]`, 将[主题文件夹名称]换成你新加的主题文件夹名称；修改了项目的_config.yml要重启服务才生效。

4. 你可以到主题的_config.yml里配置是否需要显示about等特殊定制，具体见使用的主题。

### 本地搜索
[参考博客]：

* [实现Hexo next 主题博客本地站内搜索 - True Me](https://zty.js.org/post/2016/07/08/hexo-localsearch.html)

* [Hexo博客添加搜索功能](http://www.itfanr.cc/2017/10/27/add-search-function-to-hexo-blog/)

基本原理都是使用`hexo-generator-searchdb`, 我的问题是我装完了，但还看不到搜索框， 原因是因为主题里没有开启`enable: false`

```
# Local search
# Dependencies: https://github.com/flashlab/hexo-generator-search
local_search:
  enable: true
  # if auto, trigger search by changing input
  # if manual, trigger search by pressing enter key or search button
  trigger: auto
  # show top n results per article, show all results by setting to -1
  top_n_per_article: 1
```

博客建完，并且部署到Github了，进入下一篇[自动化部署-Travis](/blog/2018/03/09/blog4/)

---
心酸心爽博客系列

* [博客存储-使用GitHub存储博客](/blog/2018/03/09/blog2/)
* [博客生成-Hexo生成博客网站](/blog/2018/03/09/blog3/)
* [自动化部署-Travis](/blog/2018/03/09/blog4/)