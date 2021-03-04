# Go - 类型转换

> Go 不支持隐式转换类型

转换格式：

```go
float32(17) // type_name(expression)
```

## strconv 包

strconv包提供了字符串与简单数据类型之间的类型转换功能。可以将简单类型转换为字符串，也可以将字符串转换为其它简单类型。

这个包里提供了很多函数，大概分为几类：

- 字符串转 int：Atoi()
- int 转字符串: Itoa()
- ParseTP 类函数将 string 转换为 TP 类型：ParseBool()、ParseFloat()、ParseInt()、ParseUint()。因为 string 转其它类型可能会失败，所以这些函数都有第二个返回值表示是否转换成功
- FormatTP 类函数将其它类型转string：FormatBool()、FormatFloat()、FormatInt()、FormatUint()
- AppendTP 类函数用于将TP转换成字符串后 append 到一个 slice 中：AppendBool()、AppendFloat()、AppendInt()、AppendUint()