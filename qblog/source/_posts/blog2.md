---
title: 创建博客-使用GitHub存储博客
date: 2018-03-09 22:51:55
tags:
- travis
- ci
- blog
- hexo
- github
- ssh
---






### 为什么选择Github？：
1. 方便；有了仓库，可以随便换电脑写博文；有版本管理，可以很好的迭代；
2. 公开；我的博文没啥私密文章，所以随便啦；
3. 强大；通过GitHub Pages即使没有域名和服务器，也能生成静态网站。

### 使用步骤（清爽版）
1. 新建仓库
> 添加README，有提交记录才会有master分支(*第一次发现空仓库连master分支都没有*)

2. 创建新分支`blog-source`
3. 将分支blog-source设置为默认分支
> 设置默认分支为非master原因: 1) master存储静态网站, 不需关注; 2) 远程默认分支为blog-resoure, 有助于提交代码; 	

	操作步骤：
	
	step1: 切换到项目主页, 如https://github.com/antwork/myblog
	
	step2: 找到设置(Settings)
	
	step3: 找到分支(Branchs)
	
	step4: 找到 `Default Branch`, 将`master`更新为`blog-source`, 单击`Update`, 单击`i understand ...`

	
4. 开启Github pages
   > 目的: 通过链接 https://antwork.github.io/blog/ 就可以像访问普通网站一样访问我的博客了, 而https://github.com/antwork/blog 访问的是代码页面
	
	步骤同3, Settings - Options - Github Pages, 默认为none, 选中Master分支, 然后Save.

5. 克隆项目到本地


### 使用步骤（截图版）

#### 1. 创建新仓库	
打开主页https://github.com; 选择右上角加号，选中“New repository"
![创建新仓库](/blog/assets/githubblog/github_blog0.png)
![创建新仓库](/blog/assets/githubblog/github_blog1.png)

#### 2. 创建blog-source分支	
   1) 单击"Branch:master"，输入分支名blog-source, 回车(截图为后补图，原理一样，当发现分支不存在时会创建分支) 
![test](/blog/assets/githubblog/github_blog2.png)
	2） 分支创建完效果图 
![test](/blog/assets/githubblog/github_blog3.png)

#### 3. 设置默认分支
			
1) 步骤："Settings" - "Branches" - "Default branch" - 单击"master" - 选择 "blog-source" - 单击 "update" - 单击 "I understand ..."	
![test](/blog/assets/githubblog/github_blog4.png)	
![test](/blog/assets/githubblog/github_blog5.png)
2) 更改默认分支后效果图：
![test](/blog/assets/githubblog/github_blog6.png)

#### 4. 开启Github Pages
> 目的: 通过链接 https://antwork.github.io/blog/ 就可以像访问普通网站一样访问我的博客了, 而https://github.com/antwork/blog 访问的是代码页面

类似步骤3，操作顺序：Settings - Options - Github Pages, 默认选中了`none`, 选中`Master`分支, 然后Save

#### 5. 克隆代码仓到本地		
1）打开项目页面
2）"Code" - "Clone or download" - 单击“复制按钮”（或自己复制地址）
![test](/blog/assets/githubblog/github_blog7.png)
3）本地打开终端（我用的是iterm)
4) 打开博客准备存储文件夹, 输入指令`git clone [你的仓库地址]`
5）使用cd打开blog文件夹
6）通过git branch检测当前分支为blog-source

```
qiangdeMBP:GitHub xuq$ git clone https://github.com/antwork/myblog.git
Cloning into 'myblog'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.

qiangdeMBP:GitHub xuq$ cd myblog

qiangdeMBP:myblog xuq$ git branch
* blog-source
```

### 关于仓库使用方案的确定：
网上调研了下，方案基本有两种:
		
* 使用两个仓库, 一个用于存储源码, 一个用于存储静态网站	
* 一个仓库, 使用不同分支	

综合对比, 方案2怎么都比方案1清爽, 花了点时间研究了下, 最终的方案如下：

```
* blog-source  # 存储源码（包括后面的hexo\markdown文章等）
  master       # 存储静态网站（有源码得到的静态网站，部署前基本是个空文件夹）
```
> 由于不了解hexo的部署，此处卡壳了下，不要想太多将master留空就好了。


*下一篇：* [创建博客-Hexo生成博客网站](/blog/2018/03/09/blog3/)

---
创建博客系列

* [创建博客-使用GitHub存储博客](/blog/2018/03/09/blog2/)
* [创建博客-Hexo生成博客网站](/blog/2018/03/09/blog3/)
* [创建博客-自动化部署Travis](/blog/2018/03/09/blog4/)