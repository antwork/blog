---
date: 2015-03-19 16:06:12
layout: post
title: iOS in-house发布
categories: 日志
tags: ios, ad-hoc, 企业发布 ,发布, In house, 
---

几个备忘:		

1. plist的链接必须是https开头的,貌似第三方存储平台没啥用,还是考虑怎么在服务器端搞定吧
2. 新版不会自动生成plist,所以需要手动的去弄
3. https://xx./xx.plist这里对于长度没要求,不一定必须放入根目录中,(不知道谁好像说过,反正这个是没要求的)
4. 生成证书的参考这里 [http://blog.csdn.net/abbottsuccess/article/details/4445160](http://blog.csdn.net/abbottsuccess/article/details/4445160), 需要在keychain的偏好设置--证书--OCSP关闭, CRL关闭再请求
5. ssl申请网站 [沃通](https://www.wosign.com)

参考网址:			
[http://blog.csdn.net/pang040328/article/details/40924737](http://blog.csdn.net/pang040328/article/details/40924737)		


[空白模板](/assets/AppName.plist)