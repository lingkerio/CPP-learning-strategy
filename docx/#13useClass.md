# 使用类
[TOC]

<!--$$\int_{-\infty}^{\infty} e^{-x^2} = \sqrt{\pi}$$-->

## 友元函数
> 友元函数的访问权限与类的成员函数一致
### 创建友元
1. 首先将友元函数的原型放在类声明中，原型前要加上friend关键字
2. 然后编写函数定义，此时不需要friend关键字，由于不是成员函数，因此也不需要使用类限定符
3. 友元函数的定义直接写在类声明中会成为内联函数
```c++
//mytime.h
#ifndef MYTIME_H
#define MYTIME_H

class Time
{
private:
    ...
public:
    ...
    friend exampleFunc(parameter_list);
} 
```

### 友元函数的操作数顺序
> 友元函数的操作数按照从左到右一一对应赋值给形参列表

## 运算符重载
> 对于类来说，原本的运算符不能够直接操作他们，需要重载运算符，由于数据一般被封装在类中，则重载运算符需要
### 成员函数重载运算符
> 成员函数重载运算符作为类公有函数
```cpp
//mytime.h
#ifndef MYTIME_H
#define MYTIME_H

class Time
{
private:
    ...
public:
    ...
    Time operator+(parameter_list);
} 
```
> 用这种方式实现运算符重载，必须是对象在操作符前
### 友元函数重载运算符
> 友元函数重载运算符时考虑到实际需要，可以使用引用变量节省开销，但如果有特殊需要也可以按值传递
```cpp
//mytime.h
#ifndef MYTIME_H
#define MYTIME_H

class Time
{
private:
    ...
public:
    ...
    friend operator+(parameter_list);//
} 
```
> 友元函数重载运算符的参数中必须有==类==参数
### 重载限制
1. 重载后的操作符至少有一个操作数为用户定义的类型，以防止用户为标准类型重载运算符
2. 使用运算符不能违反原先的语法规则，如使用一个操作数的操作符即使被重载也只能重载为使用一个操作数的操作符
3. 不能修改运算符优先级
4. 不能创建新运算符
5. 有一部分运算符不可以被重载:
    1. sizeof
    2. .
    3. .*
    4. ::
    5. ?:
    6. typeid
    7. const_cast
    8. dynamic_cast
    9. reinterpret_cast
    10. static_cast
6. 一些运算符只能由成员函数重载
    1. =
    2. ()
    3. []
    4. ->
### 重载运算符的常见应用
> 重载<<运算符以便于输出类，一般来说这需要让重载后运算符的返回类型为ostream&，以便于可以像通常那样连续输出

## 类的自动转换和强制类型转换
### 构造函数
> 使用一个参数的构造函数可以隐式调用，即直接使用赋值运算符来将参数“赋值”给类变量
> C++新增关键字explicit，对构造函数的声明前加上这个关键字可以关闭这个特性以防止意外的类型转换发生并增强代码可读性
> 如果不关闭这个特性，能被隐式转换为该单参数构造函数参数类型的类型都会触发这个特性

### 转换函数
> 将类对象转换为内置类型的函数
> `function_prototype operator typename();`
1. 转换函数必须是类方法
2. 转换函数不能指定返回类型
3. 转换函数不能有参数
4. typename指出了转换的目标类型
5. syntax: `typename(object)`|`(typename)object`
6. 转换函数必须返回转换后的值
#### 自动应用类型转换
> 若只定义了一个转换函数，则可以隐式调用转换函数，若不然，隐式转换则会产生二义性
> 为了防止隐式转换带来的可能的错误，可以使用==explicit==关键字来使得转换函数只可以显式调用
> 另一个方法是定义一个功能相同的非转换函数来使用
#### 转换函数与友元函数 
> 过多的转换函数容易带来二义性
```cpp
double + class;//call friend function
/*
程序不会将double转化为class再调用成员函数完成加法运算，但尽量少造成混淆，以增加程序可读性
*/
```
```cpp title="plus_achieve.cpp"
//1——friend
operator+(const class &, const class &);//double类型构造函数转换为class，再由友元函数实现加法，由于调用构造函数，开销更大
//2——member
class operator+(double)//通过显式匹配参数实现加法，一般执行速度更快
```

