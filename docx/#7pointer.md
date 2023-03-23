## const与指针

[TOC]

### 两类const修饰的指针

#### 指向const的指针

1. 这样的指针被认为指向一个const变量
2. 但实际指对于这个指针来说，指向的值不能改变
3. 即指针指向的这块内存存储的值不可以通过指针解引用来改变，但可以直接通过变量名等其他方式改变

```cpp
int age = 30;
const int* pt = &age;
```

#### 指针自身为const变量的指针

1. 这样的指针自身的值不可改变，即其指向的内存地址不可改变
2. 但内存地址上存储的数据可以被改变

```cpp
int solv = 3;
int* const pointer = &solv;
```

#### const变量的地址能够赋给的指针

1. const变量的地址可以赋给指向const变量的指针
2. 但不可以被赋给常规指针，否则const的修饰显得很荒谬
3. 如果非要这样做，可以使用强制类型转换来突破限制
4. C++不允许将int**转换成const int**（因此不允许将常规指针的地址赋给const指针），也不允许将const指针赋给非const指针

## 函数的指针

### 基础知识

1. 获取函数的地址：函数名即是函数的地址
2. 声明函数指针：

```cpp
typeName (*pointer_name)(parameter list);
```

3. 使用函数指针调用函数：
   - 通过间接运算符*，(*pointer_name)即可视作函数名使用
   - C++允许直接把函数指针当作函数名使用

### 深研函数指针

1. 不同形式的函数原型

```cpp
const double * f1(const double ar[], int n);
const double * f2(const double [], int);
const double * f3(const double *, int);
```

2. 声明对应的函数指针，只需要把函数名换成**_(*pointer_name)_**即可
3. 或者使用auto工具，自动推导类型
4. 而声明一个函数指针数组，**_[]_** 添加方式为---**_（*pointer_name[])_**
5. 若想得到指向函数指针数组的指针，最方便的方式是使用auto工具
6. 若想自己声明指向函数指针数组的指针可以声明为：

```cpp
const double *(*(*pd)[3])(const double *, int) = &pa;
```

7. 若想简化声明，也可以使用**_typedef_**工具，防止使用auto时，赋予的初值类型错误
