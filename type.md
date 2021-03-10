# Go - 类型

## type 用法

### 定义结构体

```go
type person struct {
  name string
  age int
}
```

### 定义接口

```go
type IPerson interface {
  Run()
  Name() string
}
```

### 定义函数类型

函数类型还可以再定义方法

```go
type handler func(name string) int
func (h handler) add(name string) int {
  return h(name) + 10
}
```

### 类型等价定义，相当于类型重命名

还可以为新类型定义方法

```go
type name string
func (n name) len() int {
  return len(n)
}
```

### 定义类型别名

别名只会存在于代码中，编译完成后，不会再存在。不能为别名定义方法，编译会报错。

```go
package main
import (
    "fmt"
)
// 将NewInt定义为int类型
type NewInt int
// 将int取一个别名叫IntAlias
type IntAlias = int
func main() {
    // 将a声明为NewInt类型
    var a NewInt
    // 查看a的类型名
    fmt.Printf("a type: %T\n", a)
    // 将a2声明为IntAlias类型
    var a2 IntAlias
    // 查看a2的类型名
    fmt.Printf("a2 type: %T\n", a2)
}
// 输出结果
// a type: main.NewInt
// a2 type: int
```

## 类型分类

### Basic type

Numbers, strings, and booleans

### Aggregate Type

Array and structs

### Reference type

Pointers, slices, maps, functions, and channels

### Interface type

interface

## 不能比较的类型

slice/map/function, 不能使用 == 来比较，不能作为 map 的 key

## 值类型和引用类型 

### 值类型

变量直接存储值，内存通常在栈中分配

int、float、bool、string、array、struct

### 引用类型

变量存储的是一个地址，这个地址对应的空间里才是真正存储的值，内存通常在堆中分配

pointer、slice、channel、interface、map、function