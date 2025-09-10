# variable

## 标准声明

```
声明格式:
var 变量名 变量类型

var name string
var age int
var isOk bool
```

## 批量声明
```
var (
    name string
    age int
    isOk bool
)
```

## 变量初始化
```
初始化格式:
var 变量名 变量类型 = 表达式

var name string = "mike"
var age int = 18
var isOk bool = true
```

## 类型推导
```
var name = "mike"
var age = 18
var isOk = true
```

## 简短声明
> 必须定义在函数内部
```
name := "mike"
age := 18
isOk := true
```