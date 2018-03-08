---
title: iOS状态栏颜色变更
date: 2017-06-25 10:00:00
tags: [swift, UIViewControllerBasedStatusBarAppearance, UIViewControllerBasedStatusBarAppearance, childViewControllerForStatusBarStyle,状态栏]
categories: Swift
---
iOS状态栏颜色变更</b>	
	
1. 怎么改变状态栏颜色				
2. UINavigationController下的状态栏不起作用怎么办					
<!--more-->	

[演示项目下载](/assets/StatusBar.zip)

## 实验:		
**前提1: 没有导航栏的单控制器工程**			
**前提2:	UIViewControllerBasedStatusBarAppearance = false**

实验一:			
条件. 项目Target-General-StatusBarStyle-default		
*结果: ![状态栏黑色](/assets/UIViewControllerBasedStatusBarAppearance1.png)*		

实验二:		
条件: 项目Target-General-StatusBarStyle-lightContent		
*结果: ![状态栏白色](/assets/UIViewControllerBasedStatusBarAppearance2.png)*	
实验三:
条件1: 项目Target-General-StatusBarStyle-lightContent		
条件2: ViewController重写`preferredStatusBarStyle `方法		
		
```
override var preferredStatusBarStyle: UIStatusBarStyle {
    return .default
}

```
*结果:	结果同实验二, 状态栏并没有使用`preferredStatusBarStyle `显示黑色导航栏, 而是显示了白色状态栏*

实验四:		
条件1: 项目Target-General-StatusBarStyle-lightContent		
条件2: 在ViewController的`ViewDidLoad`方法中添加代码
				
```
override func viewDidLoad() {
    super.viewDidLoad()

    UIApplication.shared.setStatusBarStyle(.default, animated: true)
}

```


*结果:	结果同实验一, 显示黑色导航栏*		

**总结一**: UIViewControllerBasedStatusBarAppearance=false时, 影响导航栏颜色的方式有两个:		

1. info.plist中的UIStatusBarStyle(效果同项目Target-General-StatusBarStyle); 		
2. 通过配置UIApplication的setStatusBarStyle方法;

**更改前提条件**		
** 前提1: 没有导航栏的单控制器工程	**		
** 前提2:	UIViewControllerBasedStatusBarAppearance = true **

实验五:		
条件1: ViewController没有重写`preferredStatusBarStyle`方法	
条件2: 项目Target-General-StatusBarStyle-lightContent(项目Target-General-StatusBarStyle-default)

*结果: 状态栏一直为黑色*

实验六:		
条件: 重写ViewController 的`preferredStatusBarStyle `方法
				
```
override var preferredStatusBarStyle: UIStatusBarStyle {
    return .default
}

```
							
		
*结果: 状态栏黑色(设置项目Target-General-StatusBarStyle-lightContent不影响结果)*

实验七:		
条件: 重写ViewController 的`preferredStatusBarStyle `方法
				
```
override var preferredStatusBarStyle: UIStatusBarStyle {
    return .lightContent
}
```
							
	
*结果: 状态栏白色(设置项目Target-General-StatusBarStyle-default不影响结果)*

**结果: UIViewControllerBasedStatusBarAppearance基于控制器的状态栏显示, 实际是由`preferredStatusBarStyle`返回值决定, 默认`default`为黑色文字, `lightContent`显示白色文字**

实验八:	
将ViewController放入UINavigationController中		
*结果: `preferredStatusBarStyle`不起作用, `项目Target-General-StatusBarStyle-lightContent`也不起作用*					
*结果分析: UINavigationController作为容器返回了它的preferredStatusBarStyle导致控制器设置无效*

为了解决这个问题, 引入了一个自定义UINavigtaionController, 将Storyboard中的导航栏class替换为`CustomNavigationController `						

```
import UIKit

class CustomNavigationController : UINavigationController {
    override var preferredStatusBarStyle: UIStatusBarStyle {
        return .lightContent
    }
}
```
							
			
问题解决:
![状态栏白色](/assets/UIViewControllerBasedStatusBarAppearance3.png)

但是又引入新问题了, 如果继承了导航栏, 如果需要变换导航栏风格,就需要经常的变换CustomNavigation的`preferredStatusBarStyle`, 为了解决这个问题, 苹果引入了`childViewControllerForStatusBarStyle `, 将CustomNavigationController更新如下, 则状态栏的会使用栈顶的ViewController的`preferredStatusBarStyle `:		

```
import UIKit

class CustomNavigationController : UINavigationController {
    override var childViewControllerForStatusBarStyle: UIViewController? {
        return self.topViewController
    }
}
```
							
	
官方解释: If your container view controller derives its status bar style from one of its child view controllers, implement this method and return that child view controller. If you return nil or do not override this method, the status bar style for self is used. If the return value from this method changes, call the 
setNeedsStatusBarAppearanceUpdate()
 method.

翻译: 简而言之就是容器控制器需要根据子控制器来决定状态栏颜色, 实现该方法并返回对应的子控制器. 当返回nil或者没有实现该方法则使用默认的, 如果`childViewControllerForStatusBarStyle`的返回值更新了, 需要调用`setNeedsStatusBarAppearanceUpdate`

到此关于状态栏变更的内容就讲完了, 主要分两种情况:		
1.  有导航栏, 并且希望中途修改导航栏颜色, 则自定义一个导航栏, 配置其`childViewControllerForStatusBarStyle`为栈顶控制器, 然后在需要自定义颜色的控制器中重写`preferredStatusBarStyle`方法		
2.  没有导航栏并且希望中途改变导航栏颜色, 则直接重写`preferredStatusBarStyle`方法即可

**备注**		
1. `UIApplication.shared.setStatusBarStyle(.default, animated: true)`方法已过期, 不建议使用, 因此`UIViewControllerBasedStatusBarAppearance=false`也是不被推荐	
2. UIViewControllerBasedStatusBarAppearance默认为true, 所以在info.plist中不需要添加该配置		
3. 总而言之: 忽略UIViewControllerBasedStatusBarAppearance, 使用`childViewControllerForStatusBarStyle`和`preferredStatusBarStyle`来管理状态栏颜色.


参考:		
------
[https://developer.apple.com/documentation/uikit/uiviewcontroller/1621433-childviewcontrollerforstatusbars](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621433-childviewcontrollerforstatusbars)		

[http://www.jianshu.com/p/0d4337b2e18a](http://www.jianshu.com/p/0d4337b2e18a)



