---
title: 重构代码疑问之 as? as as!
date: 2017-04-24 23:00:00
tags: [swift,as,as?,as!,Optional]
categories: Swift
---
重构代码疑问之<b>as? as as!</b>	
	
1. as 使用场景				
2. as! 使用场景		
3. as?		
4. 	as? XXX 和 as! XXX?的区别				
<!--more-->	


#### 1.as使用场景:		
1). 向上转型	

```
class Animal {}
class Cat : Animal {}
let cat = Cat()
let animal = cat as Animal 
```



2). 消除二义性, 数值类型转换		
```
let num1 = 42 as CGFloat
let num2 = 42 as Int
let num3 = 42.5 as Int
let num4 = (42 / 2) as Double
```

3). switch语句中进行模式匹配		
如果不知道一个对象是什么类型, 可以通过Switch语句来检测类型并进行相关处理.
```
class Animal {}
class Cat: Animal {}
class Dog: Animal {} 
let animal = Cat()
switch animal {
case let cat as Cat:
    print("cat class")
case let dog as Dog:
    print("dog class")
default:
    print("")
}
```

#### 2. as!使用场景
向下转型(Downcasting), 转换失败报runtime error
```
let ani2: Animal = Cat()
let cat = ani2 as! Cat
```

#### 3.as?
同as!,但转换失败返回nil, 成功返回Optinal对象	
```
if let cat = animal as? Cat {
    // cat is not nil
} else {
    // cat is nil
}
```
	
#### 4. as? XXX 和 as! XXX?		
```
let dict = NSDictionary()
guard let swiftDict = dict as? [String:Any] else { return }
    
if let tmp = swiftDict["key"] as? String {
    print("\(tmp) is a string")
}
    
if let tmp = swiftDict["key"] as! String? {
    print("\(tmp) is a string")
}

// 编译不能通过, 因为无法确定swiftDict["key"] 向 String转是否是向上转型
/*if let tmp = swiftDict["key"] as String? {
    print("\(tmp) is a string")
}*/
```

两者区别在于 `as? String`会更安全, 当发现`tmp`不是`String`时返回`nil`, 否则返回一个`Optinal<String>	`	
但是 `as! String?` 当 `tmp`不是一个`<Optinal>String`时会运行时崩溃, 因为它使用了`as!`将`swiftDict["key"]`强制解包为一个`<Optional>String`, 但实际对象不为`Optional<String>`, 示例如下:				

```
let dict = NSMutableDictionary()
dict.setValue(NSNumber(value:1), forKey: "key")

guard let swiftDict = dict as? [String:Any] else { return }
    
if let tmp = swiftDict["key"] as! String? {
    print("\(tmp) is a string")
}
    
// Error: Could not cast value of type '__NSCFNumber' (0x1017f3590) to 'NSString' (0x100dffc60).
if let tmp = swiftDict["key"] as! String? {
    print("\(tmp) is a string")
}
```

参考网站:		
[Swift - as、as!、as?三种类型转换操作符使用详解（附样例）](http://www.hangge.com/blog/cache/detail_1089.html)



