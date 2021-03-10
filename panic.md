# Go - panic, recover

## panic 和 recover 的关系

panic 和 recover 的组合有如下特性：

- 有 panic 没 recover，程序宕机。
- 有 panic 也有 recover，程序不会宕机，执行完对应的 defer 后，从宕机点退出当前函数后继续执行。

## panic

Go语言的类型系统会在编译时捕获很多错误，但有些错误只能在运行时检查，如数组访问越界、空指针引用等，这些运行时错误会引起宕机。

宕机不是一件很好的事情，可能造成体验停止、服务中断，就像没有人希望在取钱时遇到 ATM 机蓝屏一样，但是，如果在损失发生时，程序没有因为宕机而停止，那么用户将会付出更大的代价，这种代价可以是金钱、时间甚至生命，因此，宕机有时也是一种合理的止损方法。

一般而言，当宕机发生时，程序会中断运行，并立即执行在该 goroutine（可以先理解成线程）中被延迟的函数（defer 机制），随后，程序崩溃并输出日志信息，日志信息包括 panic value 和函数调用的堆栈跟踪信息，panic value 通常是某种错误信息。

### 手动触发宕机

```go
panic("panic here")
```

### 运行时宕机

运行时发生的错误，例如数组越界等。

### 宕机时触发延迟执行语句

```go
func main() {
  defer fmt.Println("宕机了，我写一下日志")
  panic("panic here")
}
```

## recover

Recover 是一个Go语言的内建函数，可以让进入宕机流程中的 goroutine 恢复过来，recover 仅在延迟函数 defer 中有效，在正常的执行过程中，调用 recover 会返回 nil 并且没有其他任何效果，如果当前的 goroutine 陷入恐慌，调用 recover 可以捕获到 panic 的输入值，并且恢复正常的执行。

```go
package main
import (
    "fmt"
    "runtime"
)
// 崩溃时需要传递的上下文信息
type panicContext struct {
    function string // 所在函数
}
// 保护方式允许一个函数
func ProtectRun(entry func()) {
    // 延迟处理的函数
    defer func() {
        // 发生宕机时，获取panic传递的上下文并打印
        err := recover()
        switch err.(type) {
        case runtime.Error: // 运行时错误
            fmt.Println("runtime error:", err)
        default: // 非运行时错误
            fmt.Println("error:", err)
        }
    }()
    entry()
}

func main() {
    fmt.Println("运行前")
    // 允许一段手动触发的错误
    ProtectRun(func() {
        fmt.Println("手动宕机前")
        // 使用panic传递上下文
        panic(&panicContext{
            "手动触发panic",
        })
        fmt.Println("手动宕机后")
    })
    // 故意造成空指针访问错误
    ProtectRun(func() {
        fmt.Println("赋值宕机前")
        var a *int
        *a = 1
        fmt.Println("赋值宕机后")
    })
    fmt.Println("运行后")
}
```

