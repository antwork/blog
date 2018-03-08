---
date: 2014-1-27 12:48:12
layout: post
title: "Linux基本使用"
description: "介绍Linux的一些常用使用备忘"
category: 文档
tags: Linux 
---


Control+d 退出
Control+l 清屏

###命令行		
* 创建文件夹 mkdir aFolder
* 删除文件: rm aFile	
* 删除文件夹:rm -r AFolder/ 
* 查看某个命令行使用: man rm
* 退出查看某个命令行: q
* 下一处 Enter键	

###文件系统树	
Linux只有一个系统树	
Linux的分区为挂载点	
挂载点:对应到系统树的某个层级范围	

根目录:Root Directory 	/
当前工作目录:用户当前所站立的文件点,使用```pwd```来显示当前的文件夹	
绝对路径:	
采用/开始,如 /Desktop	
	
相对路径:
一般采用 . ..开始
.表示当前目录: 如 ./abc 表示当前目录中的abc文件	
.. 表示父目录  如 ../abc 表示父文件夹的abc文件	

cd:Change directory

###操作文件和目录
#### * 常用命令
copy	

```
$ cp file1 file2	
$ cp -r dir1 dir2	
```
move
	
```
$ mv file ..
$ mv file dir/
```

rename
	
```
$ mv file1 file2 #如果file2存在,则将file2的内容替换为file1,然后删除file1
$ mv dir1 dir2 #dir2存在,则为移动操作
```

remove
	
```
$ rm file
$ rm -r dir
```

创建文件:	
	
```	
$ touch a.txt
$ >a.txt
```

```
#查看文件    
$ cat a.txt

#查看文件类型 
$ file a.txt

#查看隐藏文件
$ ls -a

#压缩
zip:   $: zip -r xxx.zip  directory/
unzip: $: unzip xxx.zip

tar.gz:   
$:tar zxvf aa.tar.gz
$:tar zcvf  aaa.tar.gz abc/

.tar.bz2
$:tar jxvf aa.tar.gz
$:tar jcvf  aaa.tar.gz abc/

备注:file命令查看结果是POSIX tar archive格式，使用命令	
	
$tar xvf xxx.tar
	
```

####文件:三种文件	
* stdin : 0,
* stdout: 1, 直接显示在屏幕上
* stderr: 2, 直接显示在屏幕上(报错信息)

#####输出重定向stdin >
$ cat file1 > file       (将file1赋值给file)
$ cat file1 file2 > file (两个文件合并为新文件)

#####重定向错误输出 2>
$ ls xsdfsd 2> output.txt

######管道线: |

####权限
三种权限:	

* Read   :r	
* Write  :w	
* Excute :x	
	
查看文件权限		

```
#文件
apple@ubuntu:~/Desktop$ ls -l out.txt
-rw-rw-r-- 1 apple apple 0 Nov 27 06:33 out.txt
	
#目录
apple@ubuntu:~/Desktop$ ls -ld dir1
drwxrwxr-x 2 apple apple 4096 Nov 26 21:12 dir1

$ chmod +w .
$ chmod 666 a.txt #6 = 110 代表read, write

# 三种用户,Owner,group world


$ chomod u+x a.txt (Owner)
$ chomod a-w a.txt (group)
$ chomod o-x a.txt (world)

```
#### 进程 PID(process id)

复制文本: Control Shift  c
黏贴: Control Shift  v	
	
#### 查找
locate	:(从数据库中读取信息,有延迟)
find	
grep	

sudo updatedb:强制更新文件数据库
find . -type f
f 代表文件
d 代表目录

#### 安装软件	
* 下载安装包
* Deb
* apt-get



编译三步骤:
1. .configure
2. .make
3. .make install

deb包	
包含:程序本身,配置文件,安装位置, 依赖关系

安装deb包:	
sudo dpkg -i xxx.deb	
	
软件仓库
apt-get

Unbuntu安装GO([参考网址](http://blog.chinaunix.net/uid-20718384-id-3338012.html))

1. 下载源码go1.3.3.linux-amd64.tar
2. 解压缩  $: tar xvf go1.3.3.linux-amd64.tar
3. 复制到根目录中 $:cp -r go ~
4. 打开根目录中的rrc $: cd ~/go/src
5. 安装 ./all.bash







