---
title: Swift语言基础
copyright: true
date: 2018-03-12 22:04:48
tags:
- swfit
- 基础
- 苹果
- iOS
---


## Swift基础

### 注释
```swift
// 单行注释

/*
 * 多行注释
 *
 * 注释一行
 * 注释二行
 */

```


### 输出
```swift
print("Hello World")	// Hello World
print("Hello", "World", separator: " ", terminator: ".") //Hello Wrold."

```
### Swift的语法特点      
> 1. 语句行末不要分号. 单行多语句, 使用分号分隔(**不推荐**)
> 2. if不需要括号, 多条件使用逗号(,)分隔

```siwft
print("Hello") 

// 单行多语句:

// 错误方式: error: consecutive statements on a line must be separated by ';' print("Hello") print("World")
print("Hello") print("World")

// 正确方式
print("Hello"); print("World")

if "a" == "a", true {}
```

### 变量、常量
> 使用关键词```var```定义变量    
> 使用关键词```let```定义常量	
> 语法:```[let|var] name:type = value```	

```swift
var variable:String = "I'm variable value"	

let constVariable:String = "I'm constant value"
```

> *备注: 通过字面量初始化变量(常量), 编译器可以通过值推断出变量(常量)类型, 所以上面代码可以简写为:*

```swift
var variable = "I'm variable value"	

let constVariable = "I'm constant value"
```

### 数值
```swift
// 布尔值
let trueValue:Bool = true
let falseValue:Bool = false

// 有符号整数
let int8Max:Int8 = Int8.max     // 127        = 2^7
let int16Max:Int16 = Int16.max  // 32767      = 2^15
let int32Max:Int32 = Int32.max  // 2147483647 = 2^31
let int64Max:Int64 = Int64.max  // 9223372036854775807  = 2^63
let intMas:Int = Int.max        // 在32位机器值范围等同Int32, 64位机器值范围等同Int64

// 无符号整数
let uInt8Max:UInt8 = UInt8.max      // 256  = 2^8
let uInt16Max:UInt16 = UInt16.max   // 65535 = 2^16
let uInt32Max:UInt32 = UInt32.max   // 4294967295 = 2^32
let uInt64Max:UInt64 = UInt64.max   // 18446744073709551615 = 2^64
let uIntMax:UInt = UInt.max         // 在32位机器值范围等同UInt32, 64位机器值范围等同UInt64

// 浮点型
let floatValue:Float = 12.3
let doubleValue:Double = 12.3

// 类型转换
var int8:Int8 = 1

// 错误方法:
var int16_:Int16 = int8 // err: cannot convert value of type 'Int8' to specified type 'Int16'

// 正确方法:
var int16:Int16 = Int16(int8)
```

