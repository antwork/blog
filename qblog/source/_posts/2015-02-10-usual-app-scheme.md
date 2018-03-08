---
date: 2015-02-10 09:52:12
layout: post
title: 常用app url scheme
categories: 日志
tags: ios
---

微信电话本:  sharecalllog://		

微信: wechat://		

怎么获取app的 url scheme 参考网址:[http://stackoverflow.com/questions/6845693/can-i-extract-the-custom-url-scheme-from-a-ipa-file](http://stackoverflow.com/questions/6845693/can-i-extract-the-custom-url-scheme-from-a-ipa-file)

Yes, this is possible. First, unzip the .ipa file. (you can rename it with .zip to do this). Then, inside the .ipa file, you will find there is a Info.plist file. You can parse that file, look for "CFBundleURLSchemes" and you will see first the app id followed by the Custom URL if one is defined for the app.		
		
翻译:将下载的ipa后缀改为.zip,解压,找到应用中的info.plist,然后找到CFBundleURLSchemes这个key,找到第一个值,如weichat,则url scheme为 wechat://,在手机的safari中尝试下