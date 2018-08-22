---
title: Swift Error
copyright: true
date: 2018-08-22 21:23:09
tags:
- swift
- error
- oc
---

## Swift Error

> 本来想自己写一篇日志, 最后折腾了半天, 发现官网的的介绍已经很完整了, 所以干脆将官网的说明翻译一下, 最后补充个Demo和与说明下oc的交互.

### 错误协议
表示可以抛出的错误值类型。

---

### 概观
声明符合Error协议的任何类型都可在Swift中当成错误类型。由于Error协议没有自己的要求，因此您创建的任何自定义类型都能当做Error。

### 使用枚举作为错误
Swift的枚举非常适合表示简单的错误。创建符合Error协议的枚举，并为每个可能的错误添加一种类型。如果错误需要其他信息, 可以通过关联的值来包含该信息。

以下示例显示了一个IntParsingError枚举，它捕获从字符串解析整数时可能发生的两种不同类型的错误：1) 字符串表示的值超出整数表示范围后的溢出; 2) 输入非数字字符的无效输入。

```
enum IntParsingError: Error {
    case overflow
    case invalidInput(String)
}
```

invalidInput类型包含引发错误的无效字符。

下一段代码展示了一个Int类型扩展, 实现从字符串型初始Int类型，初始出错抛出错误。

```
extension Int {
    init(validating input: String) throws {
        // ...
        if !_isValid(s) {
            throw IntParsingError.invalidInput(s)
        }
        // ...
    }
}
```

通过do catch语法, 你可以catch设定的错误类型, 并且访问其关联值, 如下例所示。

```
do {
    let price = try Int(validating: "$100")
} catch IntParsingError.invalidInput(let invalid) {
    print("Invalid character: '\(invalid)'")
} catch IntParsingError.overflow {
    print("Overflow error")
} catch {
    print("Other error")
}
// Prints "Invalid character: '$'"
```

### 在错误中包含更多数据
有时，虽然包含相同的公共数据, 但是你可能希望使用不同的错误状态，如文件中的位置或某些应用程序的状态。此时你可以使用结构来表示这种错误。以下示例在解析XML文档时使用结构体来表示错误，包括发生错误的行号和列号：

```
struct XMLParsingError: Error {
    enum ErrorKind {
        case invalidCharacter
        case mismatchedTag
        case internalError
    }

    let line: Int
    let column: Int
    let kind: ErrorKind
}

func parse(_ source: String) throws -> XMLDoc {
    // ...
    throw XMLParsingError(line: 19, column: 5, kind: .mismatchedTag)
    // ...
}
```
再一次，使用模式匹配来有条件地捕获错误。以下是如何捕获函数抛出的任何错误：XMLParsingErrorparse(_:)

```
do {
    let xmlDoc = try parse(myXMLData)
} catch let e as XMLParsingError {
    print("Parsing error: \(e.kind) [\(e.line):\(e.column)]")
} catch {
    print("Other error: \(error)")
}
// Prints "Parsing error: mismatchedTag [19:5]"

```
    
   
    

--

#### 补充1: 当前不处理错误, 直接向上抛出
方法: 移除do{}, 方法添加throws, 在抛出错误方法前添加try

```
@objc class PasswordHP: NSObject {

    func throwFunc1() throws {
        try throwFunc2()
    }
    
    func throwFunc2() throws {
        let str = "abc"
        let len = str.count
        if len < PASSWORD_MIN_LEN {
            throw ClassError.init(code: ClassError.PASSWORD_TOO_SHORT, userInfo: ["msg":"密码不得少于\(PASSWORD_MIN_LEN)"])
        }
        
        throw ClassError.init(code: StructError.PASSWORD_NOT_ALPHA, userInfo: ["msg":"包含不合法字符"])
    }
}

``` 

#### 补充2: 通过`try?`忽略错误
说明: 如果有返回值, 则结果转化为Optional类型, 抛出错误时返回nil
```
func ignoreError() {
        let password = "123"
        try? password.passwordValidate()
    }
```

#### 补充3: 在OC中使用Swift定义的Error
步骤1: 定义enum Error

步骤2: 实现CustomNSError

步骤3: 在oc中调用


```
enum PasswordError: Error {
    case lessThan6
    ...
    
    var errorMessage:String {
        switch self {
        case .lessThan6:
            return "密码不得超过\(PASSWORD_MAX_LEN)位"
        ....
    }
    
    var code:String {
        switch self {
        case .lessThan6:
            return "FA_LESS_THAN_6"
        ....
    }
}

extension PasswordError: CustomNSError {
    /// The domain of the error.
    public static var errorDomain: String { return "Lunkr" }
    
    /// The error code within the given domain.
    public var errorCode: Int { return -1 }
    
    /// The user-info dictionary.
    public var errorUserInfo: [String : Any] {
        return ["code":code, "message": errorMessage]
    }
}

@objc class PasswordHP: NSObject {
    @objc class func validate(password:String) throws {
        try password.passwordValidateInClass()
    }
}



// 在oc中调用
+ (void)test {
    NSString *password = @"1";
    
    NSError *error;
    [PasswordHP validateWithPassword:password error:&error];
    NSLog(@"error:%@", error.userInfo);
}

```

#### 参考:
[https://developer.apple.com/documentation/swift/error](https://developer.apple.com/documentation/swift/error)