---
date: 2015-03-11 16:06:12
layout: post
title: iOS 应用的图标和启动图尺寸
categories: 日志
tags: ios, Icon, 启动图, Default
---

官网数据:
[https://developer.apple.com/library/prerelease/ios/documentation/UserExperience/Conceptual/MobileHIG/IconMatrix.html#//apple_ref/doc/uid/TP40006556-CH27-SW1](https://developer.apple.com/library/prerelease/ios/documentation/UserExperience/Conceptual/MobileHIG/IconMatrix.html#//apple_ref/doc/uid/TP40006556-CH27-SW1)

#Icon
* iPhone icon size	

|  尺寸 | 图片名称 | 备注 |
| ------------- | ------------ |------------ |
| 57 x 57  | Icon.png | iOS 5, 6 |
| 114 x 114  | Icon@2x.png | iOS 5, 6 |
| 120 x 120  | Icon-60@2x.png | iOS 7, 8
| 29 x 29  | Icon-Small.png | Spotlight -iOS5,6 Settings-iOS 5-8|
| 58 x 58  | Icon-Small@2x.png | Spotlight -iOS5,6 Settings-iOS 5-6|
| 80 x 80  | Icon-Small-40@2x.png | Spotlight -iOS57,8|

* iPad	

|  尺寸 | 图片名称 | 备注 |
| ------------- | ------------ |------------ |
| 72 x 72  | Icon-72.png | iOS 5, 6 |
| 144 x 144  | Icon-72@2x.png | iOS 5, 6 |
| 180 x 180  | Icon-60@3x.png | iOS 7, 8
| 29 x 29  | Icon-Small.png | Settings -iOS5,8 |
| 58 x 58  | Icon-Small@2x.png | Settings -iOS5,8 |
| 50 x 50  | Icon-Small-50.png | Spotlight -iOS5,6 |
| 100 x 100  | Icon-Small-50@2x.png | Spotlight -iOS5,6|
| 80 x 80  | Icon-Small-40@2x.png | Spotlight -iOS7,8|


###启动图

| 设备 | 尺寸 | 图片名称 |
| ------------ | ------------- | ------------ |
| iphone 3 | 320 x 480  | Default.png |
| iphone 4 | 640 x 960  | Default@2x.png |
| iphone 5 | 640 x 1136  | Default-568h@2x.png |
| iphone 6 | 750 x 1334  | Default-667h@2x.png |
| iphone 6p | 1242 x 2208  | Default-736h@3x.png |