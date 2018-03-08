---
title: resizableImage的疑问
date: 2017-03-22 09:40:53
tags: [UIImage,resizableImage的疑问]
categories: 计算机
---
resizableImage拉伸图片时以下两种情况具体怎么处理的?	
	
1. 边缘怎么拉伸的		
2. 中间怎么填充的		
<!--more-->

>今日在跟踪一个问题的时候看到了这个方法, 想了下图片是怎么填充的, 然后记得中间的规则, 然后发现对四边的规则有些懵, 于是就写了个demo来尝试下

#### 介绍:

1. 原图(资源见尾部): 100*100 	
2. 中间方框:30 * 30
3. 理论上下左右35, 但是实际是上36, 底部34



#### 使用方法:

```
self.imgView.image = UIImage(named: "WechatIMG1")?.resizableImage(withCapInsets:UIEdgeInsetsMake(36.5, 35, 34.5, 35))

```


#### 结论:
如图1所示, 虽然传的参数是个inset, 但是实际上它如图3 所示整个图切成了9分, 1,3,7,9固定不变, 2\8水平填充,4\6垂直填充, 5中间填充

**Q**: 水平怎么拉伸的?			
**A**: 原图inset取出四角后四边剩余部分做成萝卜章, 水平\垂直看到空白就盖(*填充区域内有效*)

**Q**: 中间怎么填充的			
**A**: 将原图inset中间部分取出做成萝卜章, 然后看到空白就盖萝卜章(*填充区域内有效*)

**脑洞**: 如果ImageView比图片还小会怎样呢?
**A**: 如图2所示, 中间会显示很小, 四角会有覆盖的情况

#### 鸣谢:
感谢木木鱼提供的图片

#### 图片资源:

原图:		
![原图](/assets/resizableImage1.png)

图1		
![大拉伸图](/assets/resizableImage2.png) 

图2		
![缩小图](/assets/resizableImage3.png) 

图3		
![缩小图](/assets/resizableImage4.png)
