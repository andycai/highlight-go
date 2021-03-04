# Go - 类型

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