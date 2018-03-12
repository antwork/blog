---
title: swiftstring
copyright: true
date: 2018-03-12 22:14:03
tags:
- swift
- ios
- apple
- 苹果
---

## 字符串

1. 使用字面量创建字符串

```swifit
let str = "Hello World"
```

2. 使用String对象创建字符串	

```swift
let strA = String("Hello My World")
```

3. 创建多行字符串
> 方式1: 通过```"\n"```和```+```拼接
>
> 方式2: 使用三引号```"""字符串"""```

4. 常用方法 	
 
```swift
// 获取字符串长度
str.count   // 11

// 拼接字符串
let str3 = str + str2 // Hello World多行文本...

// String和NSString转换
let nsStr:NSString = str as NSString

// 判断:开头
str3.hasPrefix(str)      // true

// 判断:结尾
str3.hasSuffix(str2)    // true

// 判断:包含
str3.contains(str)      // true

// 查找子序列: 找到返回范围, 未找到返回nil
str3.range(of: str2)

// 字符串替换
str3.replacingOccurrences(of: "第一行", with: "第三行")

// 字符串分隔
str3.split(separator: "\n")

// 数组合并为字符串
let arr = ["1", "2", "3"]
arr.joined(separator: "_")  // 1_2_3

// 大小写转换
let abc = "aBc"
let upper = abc.uppercased() // ABC
let lower = abc.lowercased() // abc

// 格式化输出
String.init(format: "%ld %f %@", 123, 0.5, "hello") // "123 0.500000 hello"

// 浮点数保留小数点位数
String.init(format: "%.2f", 12.3)   // 12.30

// 整数前加0
String.init(format: "%05ld", 1)     // 00001

// 字符串翻转
String(str.reversed())

// slice vs String
// 参考 [https://stackoverflow.com/questions/39677330/how-does-string-substring-work-in-swift](https://stackoverflow.com/questions/39677330/how-does-string-substring-work-in-swift)
var sli1 = str3.prefix(5)   // Hello
// 等同于
var index = str3.index(str3.startIndex, offsetBy: 5)
let sli11 = str3.prefix(upTo: index)

let sli2 = str3.suffix(5)   // 文本第二行
// 等同于
let index2 = str3.index(str3.endIndex, offsetBy: -5)
let sli22 = str3.suffix(from: index2)

let start = str3.index(str3.startIndex, offsetBy: 1)
let end = str3.index(str3.startIndex, offsetBy: 7)
let range = start..<end
let sli3 = str3[range] // ello W

// slice to String
let sli22Str = String(sli22)

// 错误用法
//let sli22Str:String = sli22 // error: cannot convert value of type 'String.SubSequence' (aka 'Substring') to specified type 'String'

// utf-8Data String
let strForUTF8 = "Hello utf-8"
if let convertToUtf8Data = strForUTF8.data(using: .utf8) {
    let convertBackToStr = String(data: convertToUtf8Data, encoding: .utf8)
    print(convertBackToStr ?? "")
}

// base64
let originText = "Hello base64"
if let based = originText.data(using: .utf8)?.base64EncodedString(),
    let decodeData = Data.init(base64Encoded: based) {
    let decodeStr = String(data: decodeData, encoding: .utf8)
    print(decodeStr ?? "")
}
```
