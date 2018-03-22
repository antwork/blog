---
title: rbenv使用备忘
copyright: true
date: 2018-03-22 16:27:06
tags: rbenv,ruby,gem,fastlane
---

**官网网站**：[https://github.com/rbenv/rbenv](https://github.com/rbenv/rbenv)

**用途**：管理ruby版本，类似rvm, 支持场景化配合ruby

**通过Homebrew安装rbenv**：

```shell
$ brew install rbenv
$ rbenv init
# 按照提示将 eval "$(rbenv init -)" 放到~/.bash_profile里
$ vim ~/.bash_profile
# 按i键，将光标移到最尾，黏贴$(rbenv init -)，按Esc键，输入:wq 
# 关闭terminal，打开terminal

# 检查是否安装正常
$ -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash
Checking for `rbenv' in PATH: /usr/local/bin/rbenv
Checking for rbenv shims in PATH: OK
Checking `rbenv install' support: /usr/local/bin/rbenv-install (ruby-build 20180224)
Counting installed Ruby versions: none
  There aren't any Ruby versions installed under `/Users/xuq/.rbenv/versions'.
  You can install Ruby versions like so: rbenv install 2.2.4
Checking RubyGems settings: OK
Auditing installed plugins: OK

# 更新
$ brew upgrade rbenv ruby-build
```

**操作ruby**

```shell
# 列出所有 ruby 版本
$ rbenv install -l 

# 安装Ruby版本
$ rbenv install 2.5.0

# 常用打开方式
# 1. 切换到要使用指定Ruby版本的文件夹
# 2. 切换版本：rbenv local 2.5.0
# 3. 继续调用相关指令
$ cd /Documents/Projects/Test
$ rbenv local 2.5.0
$ gem install fastlane -NV
# 查看输出，发现已经采用了新装的ruby2.5.0
# /Users/xuq/.rbenv/versions/2.5.0/lib/ruby/gems/2.5.0/gems/rouge-2.0.7/lib/rouge/lexers/tap.rb

# 重置当前文件夹Ruby版本
$ rbenv local --unset

# 设置shell指定Ruby版本，发现仅仅作用当前Shell
$ rbenv shell 2.5.0
$ rbenv shell --unset

# 列出所有版本
$ rbenv versions
# * system (set by /Users/xuq/.rbenv/version) # 当前版本
#   2.5.0

# 列出当前版本
$ rbenv version
# system (set by /Users/xuq/.rbenv/version)
```



