---
title: 心酸心爽博客-使用GitHub存储博客
date: 2018-03-09 22:51:55
tags:
- travis
- ci
- blog
- hexo
- github
- ssh
---

### 为什么选择Github：
1. 方便；有了仓库，可以随便换电脑写博文；有版本管理，可以很好的迭代；
2. 公开；我的博文没啥私密文章，所以随便啦；
3. 强大；通过GitHub Pages即使没有域名和服务器，也能生成静态网站。

### 怎么用：
😶在我准备倒腾博客时发现我的antwork.github.io只剩下个光棍master, 里面也只发布内容, 源码什么的都没有, 我本地倒是有, 不过都是没提交的记录, 也不记得是我从电脑拷贝过来就没管了, 还是一直是这个状态. 总之我要先解决源码存储问题.
网上调研了下方案有两种:		

1. 使用两个仓库, 一个用于存储源码, 一个用于存储静态网站
2. 一个仓库, 使用不同分支

综合对比, 方案2怎么都比方案1清爽, 花了点时间研究了下, 最终的方案如下：

```
* blog-source  # 存储源码（包括后面的hexo\markdown文章等）
  master       # 存储静态网站（有源码得到的静态网站，部署前基本是个空文件夹）
```
> 由于不了解hexo的部署，此处卡壳了下。不要想太多将master留空就好了，作者专注于blog-source分支写博文，部署。

具体步骤如下:

1. 新建仓库
2. 随便commit点内容, master分支存储静态网站 (*第一次发现空仓库连master分支都没有*)
2. 新建分支 blog-source 用于存储源码
3. 设置 blog-source 为默认分支, 步骤如下 
   > 设置默认分支为非master原因: 1) master存储静态网站, 不需关注; 2) 远程默认分支为blog-resoure, 有助于提交代码; 

	![操作步骤](/blog/assets/Snip20180308_1.png)
	
	step1: 切换到项目主页, 如https://github.com/antwork/blog
	
	step2: 找到设置(Settings)
	
	step3: 找到分支(Branchs)
	
	step4: 切换分支到blog-source, 单击"Update"
	
4. 开启Github pages
   > 目的: 通过链接 https://antwork.github.io/blog/ 就可以像访问普通网站一样访问我的博客了, 而https://github.com/antwork/blog 访问的是代码页面
	
	步骤同3, Settings-Options-Github Pages, 默认选中none, 选中Master分支, 然后Save  
	
5. 接下来就是clone项目到本地了, 后续就进入【[博客生成-Hexo生成博客网站](/blog/2018/03/09/blog3/)】

*下一篇：* [博客生成-Hexo生成博客网站](/blog/2018/03/09/blog3/)

---
心酸心爽博客系列

* [博客存储-使用GitHub存储博客](/blog/2018/03/09/blog2/)
* [博客生成-Hexo生成博客网站](/blog/2018/03/09/blog3/)
* [自动化部署-Travis](/blog/2018/03/09/blog4/)