# 内存管理

[TOC]

## keyword

### storage class specifier
>
> 1. auto
> 2. register
> 3. static
> 4. extern
> 5. thread_local
> 6. mutable
>
> > auto & register 已经不再具有存储说明符的作用  
> > static & extern 用于修饰静态 和 引用声明  
> > thread_local 为并发程序设计的内容  
> > mutable 表明即使 结构 or 类 被const修饰，其被mutable修饰的成员依然可以被修改  

### cv-qualifier
>
> 1. const
> 2. volatile
>
> > const 全局变量的链接性是内部的，extern 可以覆盖默认的内部链接属性，重新变为外部链接
> > volatile 用于告诉编辑器，该变量有可能以未知方式变动，不要对其实现代码优化

## function link
>
> 函数默认为外部链接，但如果被static 修饰，则变为内部链接，静态函数将覆盖外部定义
> 内联函数不需要遵守单定义规则，但同一个内联函数的所有内联定义都必须相同

## language link
>
> 在函数原型中可以显式指定名称修饰规范

```cpp
extern "C" void spiff(int);//explicit
extern void spoff(int);//default
extern "C++" void spaff(int);//explicit
```

## dynamic allocate

### 使用*new*运算符初始化
>
> 初始化内置标量类型，可使用（）初始化，也可以列表初始化
> 初始化结构、数组，则列表初始化

### *new* 失败时
>
> 引发异常 std::bad_alloc

### *new*运算符、函数、替换函数
>
> 1. *new* 运算符将会调用函数来分配内存，初始化等，delete也会调用相应的函数
> 2. 这些函数是可替换的，可以自己编写一个这样的函数取而代之

### 定位*new*算符
>
> 1. 使用这种*new*运算符需要包含头文件 *new*
> 2. *new*运算符分配的内存只取决于传给它的地址，两次对同一个地址使用定位 *new* 运算符将只是两次分配这一块地址，因此，需要程序员自己管理内存（传给 *new* 运算符的参数）
> 3. 定位 *new* 运算符分配的内存不可以delete释放，delete只能用于heap内存
> 4. 定位 *new* 运算符返回的是 void* 指针，以便可以赋值给任意指针类型
> 5. 定位 *new* 运算符允许重载
>
```cpp
int * p1 = new int;
int * p2 = new (buffer) int;
int * p3 = new (buffer) int[40];
```
