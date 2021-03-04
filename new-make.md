# Go - new, make

## 定义

```go
  func new(Type) *Type
  func make(t Type, size ...IntegerType) Type
```

## 区别

new 函数分配内存，make 函数初始化

### 返回值

从定义中可以看出，new 为每个新的类型 Type 分配一片内存，初始化为 0 并且返回类型为 *Type 的内存地址。 返回一个类型为 Type 的初始值。

### 入参

new 只有一个 Type 参数，Type 可以是值类型如数组和结构体，它相当于 &Type{}。 make 可以有多个参数，其中第一个参数与 new 的参数相同，但是只能是 slice，map，或者 chan 中的一种。

- 对于slice，第一个size表示长度，第二个size表示容量，且容量不能小于长度。如果省略第二个size，默认容量等于长度。
- 对于map，会根据size大小分配资源，以足够存储size个元素。如果省略size，会默认分配一个小的起始size。
- 对于chan，size表示缓冲区容量。如果省略size，channel为无缓冲channel。

