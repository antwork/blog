---
title: 创建博客-自动化部署Travis
date: 2018-03-09 22:52:07
tags: 
- travis
- ci
- blog
- hexo
- github
- ssh
---

travis的使用其实挺简单，简略步骤：

1. 使用github账号登录官网[https://travis-ci.org](https://travis-ci.org)
2. 找到项目，打开自动测试开关，添加Github个人token用于Travis推送到github
3. 项目中添加.travis.yml配置文件
4. 提交代码github
5. Traivis.ci开始自动部署

### 1. 获取Github personal accesstoken步骤
> 方便travis免密推送内容到Github

1. 打开github, 单击头像 - 设置
![github设置](/blog/assets/githubblog/github_token0.png)
2. 左边找到 Developers settings
![Developer settings](/blog/assets/githubblog/github_token1.png)
3. 选择"Personal access token" - "Generate new token" - 勾选"Repo" - "Generate"
![](/blog/assets/githubblog/github_token2.png)
![](/blog/assets/githubblog/github_token3.png)
![](/blog/assets/githubblog/github_token4.png)
4. 复制生成的Token（因为后期再也看不到，建议另外存储）
![](/blog/assets/githubblog/github_token5.png)

### 配置travis
1. 打开travis官网 - 单击头像 - 找到博客仓库 - 单击开关开启自动测试
![](/blog/assets/githubblog/travis_0.png)
*开启成功显示绿色箭头*
![](/blog/assets/githubblog/travis1.png)
2. travis中单击项目博客仓库名称进入配置项，选择"More options" - "Settings" - 在"General"中勾选"Build if only .travis.yml is present"
3. 在Environmen Variables中填入GH_TOKEN, 黏贴github personal accesstoken, 单击Add(*不要勾Display values in build log， 会暴露该值)*
> 注意底部 Cron Jobs中勾选分支是否为blog-source，这里应该选择了github默认分支
![](/blog/assets/githubblog/travis_setting.png)

4. 打开博客本地仓库目录，添加.travis.yml文件，输入以下内容

> [...]为替换内容

```
language: node_js
node_js: stable
install:
- npm install
script:
- hexo clean
- hexo g
- cd ./public
- git init
- git config user.name "[你的名称]"
- git config user.email "[github邮箱账号]"
- git add .
- git commit -m "Travis CI Auto Builder"
- git push --force --quiet "https://${GH_TOKEN}@${GH_REF}" master:master
branches:
  only:
  - blog-source
env:
  global:
  - GH_REF: [博客代码仓库地址]

```
5. 提交本地内容到Github

```
$ git add .
$ git commit -m "init project"
$ git push origin blog-source
```
6. 检测效果
	打开Github Pages链接，地址为: https://[你的github账号].github.io/myblog/ , 检查页面是否正常
	Github Pages配置方法参照[创建博客-使用GitHub存储博客](/blog/2018/03/09/blog2/)
	 
*我的.travis.yml, 仅供参考*

```
language: node_js
node_js: stable
install:
- npm install
script:
- hexo clean
- hexo g
- cd ./public
- git init
- git config user.name "antwork"
- git config user.email "antwork@126.com"
- git add .
- git commit -m "Travis CI Auto Builder"
- git push --force --quiet "https://${GH_TOKEN}@${GH_REF}" master:master
branches:
  only:
  - blog-source
env:
  global:
  - GH_REF: github.com/antwork/myblog.git
```

### 部署到自己的服务器
目前为止，Travis已经能够检测到Github blog-source分支变化，下一步是推送静态网站到自己的服务器。

原理：travis ssh登录到远程服务器，执行pull操作更新服务器中静态网站，因为travis都是自动化，所以不能有任何人为参与，这里就需要使用到ssh passphase登录模式。

相关步骤参照： [Travis CI 系列：自动化部署博客](https://segmentfault.com/a/1190000011218410)

补充几点：

1. addons: 必须使用原文, 不能使用${ENV_VAR}，travis中定义的环境变量， 预计是addon太早引入了，环境变量还未初始化或这里根本就没处理环境变量。所以只能是如下形式：

```
addons:
  ssh_known_hosts: 118.24.152.130
```
	
2. ssh正确打开方式： `ssh username@hostip "commands"`，我犯的错误是以为travis能够顺序执行，所以代码都写在.travis.yml中，如

```
after_success:
- ssh username@hostip
- cd myblog
- pull xxx
```

正确打开方式为，在服务端写一个执行脚本(如pullblog), 然后ssh部分改为

```
after_success:
  - ssh root@118.24.152.130 "./pullblog"
```
>将服务端的命令打包为一个shell脚本, 对外隐藏了具体内容, 可以保护隐私内容。

*我的pullblog脚本如下：*

```
echo "run begin"
cd /home/www/blog # 打开git文件夹
git config user.name "antwork" # 修改name
git config user.email "antwork@126.com" # 修改email
git fetch --all
git reset --hard origin/master
git pull
echo "run end"
```
> * 注意我已经拉取博客仓库代码到服务器文件夹/home/www/blog中，所以travis只要执行pull就可以了	
> * 因为静态网站变化挺多的，所以合并时使用服务器版本。

到此博客就算搭完了😊，后续博文只要写好后推送到github仓库，travis就会自动生成静态网站，然后推送回github，并且触发服务端的脚本来服务器的静态网站。写完三篇都累屎了，完结撒花~

---
创建博客系列

* [创建博客-使用GitHub存储博客](/blog/2018/03/09/blog2/)
* [创建博客-Hexo生成博客网站](/blog/2018/03/09/blog3/)
* [创建博客-自动化部署Travis](/blog/2018/03/09/blog4/)