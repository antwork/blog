---
title: hexo,travis,gitub搭建博客总结
date: 2018-03-08 22:26:52
tags: hexo
---


> 前言: 买了个1g的腾讯云, 想着随便折腾着点什么, 思来想去最简单的就是博客, 就先倒腾博客上去吧. 问题来了, 之前使用github pages写的, 换台电脑之后只记得将文章拷贝过来, 怎么使用都忘光了, 折腾了两天, 终于有点小成果. - -!!

### GitHub
😶在我准备倒腾博客时发现我的antwork.github.io只剩下个光棍master, 里面也只发布内容, 源码什么的都没有, 我本地倒是有, 不过都是没提交的记录, 也不记得是我从电脑拷贝过来就没管了, 还是一直是这个状态. 总之我要先解决源码存储问题.
方案有两种:		

1. 使用两个仓库, 一个用于存储源码, 一个用于存储静态网站
2. 一个仓库, 使用不同分支

综合对比, 方案2怎么都比方案1清爽, 花了点时间调研下, 最终的步骤:

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
	
5. 接下来就是clone项目到本地了, 后续就进入hexo环节

### Hexo使用
> [中文官网: https://hexo.io/zh-cn/](https://hexo.io/zh-cn/)     
> 😔, 看了半天的英文, 还是挺抓鸡的.   
> [指令速达](https://hexo.io/zh-cn/docs/commands.html)

常用指令:

```shell
hexo init [folder] # 新建一个网站, 如果没有设置 folder ，Hexo 默认在目前的文件夹建立网站。

hexo g # 生成静态网站

hexo s # 启动服务, 默认通过localhost:4000可以访问静态网站

hexo new [layout] title # 生成新文章, 默认layout为post, 还可以是draft

hexo clean # 删除静态网站, 然后再次调用`hexo g` 

hexo d # 部署

hexo s --debug # 启动服务, 调试模式, 可以查看日志

hexo s -p 5000 # 启动服务, 端口=5000
```

### Travis使用

... 挖坑
