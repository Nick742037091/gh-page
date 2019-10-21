---
title: Go 的一些技巧
date: 2019-10-18 10:17:46
categories:
  - Go
tags:
  - 技巧
---

收集 GO 语言的一些技巧。

### 输出

println 可用于一般的输出
fmt.Println 可用于包括数组、解构体等的格式化输出
fmt.Sprint 可用于组合字符串并返回值

### 交换值

```go
// 普通变量
a, b = b, a

// 数组
list := []int{1,3}
list[0], list[1] = list[1], list[0]
```

### init 函数

- 每个 go 文件都有一个 init 函数，用于实现初始化，会在 main 函数之前自动调用，不可人为调用。
- 格式化按照包的依赖关系顺序执行。

### 枚举利用 iota 的自动初始化为 0 和自增

```go
type BitFlag int
const (
	Active BitFlag = 1 << iota // 1 << 0 == 1
	Send // 1 << 1 == 2
	Receive // 1 << 2 == 4
)

flag := Active | Send // == 3
```

### 使用位左移与 iota 计数配合可优雅地实现存储单位的常量枚举

```go
type ByteSize float64
const (
	_ = iota // 通过赋值给空白标识符来忽略值
	KB ByteSize = 1<<(10*iota)
	MB
	GB
	TB
	PB
	EB
	ZB
	YB
)
```

### 自增和自减不能用于表达式

### 数组和结构体属于值类型，赋值时是值拷贝

### 习惯用法：result,err := fun() 的方式构造和使用函数，优先判断错误，有错误直接返回。如下所示：

```go
func fun() type,error{
  result,err := f()
  if err != nil{
    return nil,errors.New("error")
  }
  // 不出错则执行以下操作
  // ...
  // return ...
}
```
