---
title: 创建博客-Hexo生成博客网站
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

### 打开方式
> 注：以下脚本中#之后为注释，不需要键入
> 打开终端

```shell
$ cd myblog   # 打开博客文件夹(可键入cd 然后将博客文件夹拖入终端)
$ mkdir temp  # 创建临时文件夹(原因最后解释）
$ cd temp	  # 打开临时文件夹
$ hexo init   # 初始hexo
...			  # 一堆信息， 最后提示Start blogging with Hexo!
$ cd ..		  # 切回父文件夹
$ mv temp/* . # 将temp里的内容移到父文件夹
$ ls 		  # 通过ls命令检查是否移动成功
_config.yml		package.json		temp
node_modules		scaffolds		themes
package-lock.json	source
$ rm -rf temp	 # 移除temp文件夹
$ ls 			 # 通过ls命令检查是否删除temp成功
_config.yml		package.json		themes
node_modules		scaffolds
package-lock.json	source
$ hexo g	# 生成静态网站
$ hexo s	# 开启本机服务，用于本地预览静态网站
INFO  Start processing
INFO  Hexo is running at http://localhost:5000/. Press Ctrl+C to stop.
```
打开浏览器，输入 localhost:4000，见到下图表示你成功了🎉🎉🎉。
![hexo本地服务启动成功](/blog/assets/githubblog/Snip20180311_18.png)

#### 写文章

```shell
$ hexo new 你好hexo # 使用hexo new 创建博文
INFO  Created: ~/Documents/GitHub/myblog/source/_posts/你好hexo.md # 提示成功，并告知文件地址。
$ hexo clean    # 清除public等已生成静态网站
$ hexo g		# 重新生成静态网站
$ hexo s 		# 开启本地预览服务
```
如下图所示，新写的你好hexo.md已经成功上屏了。
![hexo本地服务启动成功](/blog/assets/githubblog/Snip20180311_20.png)

### 草稿-发布模式
```shell
$ hexo new draft hello2 # 创建草稿
$ hexo g				# 生成网站
$ hexo s --draft		# 开启本地服务-草稿模式，否则看不到草稿
$ hexo publish hello2   # 发布hello2
$ hexo s			    # 开启本地服务
```
草稿模式（成功发布）后如下图所示：
![hexo本地服务启动成功](/blog/assets/githubblog/Snip20180311_22.png)

## FAQ

**Q1**: 如果hexo s提示错误： Port 4000 has been used. Try other port instead.   
**A1**: 使用 hexo s -p 5000 将端口指定为5000

**Q2**: 为啥要创建临时文件夹，不直接在blog目录调用hexo init, 官网文档，如果init后面没有文件夹，则在当前文件夹初始    
**A2**: 原因为当前文件夹已存在文件，并且因为是git仓库，肯定会有.git文件夹，这里通过创建临时文件夹避开这个错误

```
FATAL ~/Documents/GitHub/myblog not empty, please run `hexo init` on an empty folder and then copy your files into it
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
```

博客建完，你可能注意到我们并没有使用hexo的部署功能，因为我们准备使用travis自动化部署，进入下一篇[创建博客-自动化部署Traviss](/blog/2018/03/09/blog4/)




*补充内容*

---

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

---
心酸心爽博客系列

* [创建博客-使用GitHub存储博客](/blog/2018/03/09/blog2/)
* [创建博客-Hexo生成博客网站](/blog/2018/03/09/blog3/)
* [创建博客-自动化部署Travis](/blog/2018/03/09/blog4/)