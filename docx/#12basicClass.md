# 初识C++类

## 定义类
>
> 定义类由两部分组成：类声明，类方法定义。类声明提供了类的蓝图，类方法提供了实现细节。

### 类声明
>
> 以数据成员的方式描述数据部分，以成员函数的方式描述公有接口

#### 访问控制
>
> 私有属性成员只有类成员或者友元函数可以访问，公有属性成员可以由任何程序访问
>
> 1. 为了实现类的封装的特性，一般将类的数据部分设置为私有属性，将实现公有接口的函数设置为私有属性
> 2. 将用户对类的操作设置为公有接口，接口应该与实现分离

### 实现类成员函数
>
> 一般将成员函数与具体实现分离，实现类成员函数时需要使用作用域解析符标识函数所属的类，例如：

```cpp
void Stock::update (double price)
{
    ...
}
```

> 定义位于类声明中的函数自动成为内联函数，内联函数也可以定义在类声明外，只要加上inline关键字即可，事实上定义在类声明中的函数与紧跟在类声明后的内联函数定义是等价的。最好将内联函数定义在类声明，因为内联函数的所有定义应该是相同的。

#### 成员函数使用的数据
>
> 调用成员函数的时候，成员函数可以直接调用正在调用它的对象的数据成员，因此形参不可以与类声明中的数据成员同名。

#### const成员函数
>
> 在函数头中使用const表明该函数不会修改调用对象

```cpp
function (parameter) const {
    ...
}//考虑到构造函数和析构函数没有返回类型，于是本例没有写返回类型，但这种语法适用于任何类成员函数
```

#### this指针
>
> 类的每个成员函数都有一个this指针，该指针指向调用对象，在函数的括号后面加上const限定符将this指针限定为const使得不能使用this修改对象
> 如果函数返回*this并以引用的形式返回，就可以返回调用对象本身

## 类的构造函数和析构函数

### 构造函数
>
> 与类同名，没有返回类型，需要使用作用域解析符在函数头中

#### 默认构造函数
>
> 如没有为类提供任何构造函数，则编译器会提供一个默认构造函数，这个函数可能什么行为都没有
> 自定义默认构造函数的方式有两种
>
> 1. 给已有构造函数的所有参数提供默认值
> 2. 通过函数重载来提供一个没有参数的构造函数
>
不要同时使用这两种方法，因为构造函数只可以有一个
> 设计构造函数时通常应该提供一个对所有类成员做隐式初始化的默认构造函数

#### 构造函数的参数
>
> 构造函数的参数不应该与类的数据成员同名，因为这样会使编译器混淆，如果一定要使用，可以用this指针与->运算符来向编译器表明类的数据成员（或许类比一下Java的this关键字（捂脸））

#### 构造函数的使用
>
> 1. 显式调用构造函数：Class object = Class (parameter list);
> 2. 隐式调用构造函数：Class object (parameter list);
> 3. new动态分配内存时：Class * pointer = new Class (parameter list);
>
每次创建类对象时，C++都将调用构造函数，即使是使用new运算符时
> 接受一个参数的构造函数允许用赋值语法把对象初始化为一个值

### 析构函数
>
> 函数名为~+类名，没有返回类型，需要使用作用域解析符在函数头中
> 通常当构造函数使用了new，就必须提供一个使用delete的析构函数
> 如果构造函数没有使用new，那么析构函数实际上没有什么必须完成的事情，可以不提供，由编译器提供，程序员不提供析构函数的话，编译器会隐式提供一个析构函数，并在发现导致对象删除的代码后提供这个析构函数的定义

### 列表初始化
>
> C++11允许使用与某个构造函数的参数列表匹配的列表初始化

## 静态存储类对象
>
> 在C++中，静态存储类对象是指用static关键字修饰的类成员变量或函数。它们有以下特点：
>
> - 静态成员变量是类的所有对象共享的，它的值可以被所有对象访问和修改。
> - 静态成员函数不需要this指针，只能访问静态成员变量，不能访问非静态成员变量。
> - 非const静态成员必须在类内声明，在类外初始化。
> - const的静态成员变量既可以在类内初始化也可以在类外初始化
>
> 声明静态存储类对象的语法如下：
>

```c
// 在类内声明
class 类名 {
    static 类型名 变量名; // 静态成员变量
    static 返回类型 函数名(参数列表); // 静态成员函数
};

// 在类外初始化
类型名 类名::变量名 = 初始值; // 静态成员变量
返回类型 类名::函数名(参数列表) {
    // 函数体
} // 静态成员函数
```

例如：

```c
// 在类内声明
class MyClass {
public:
    static int count; // 静态成员变量
    static void show(); // 静态成员函数
};

// 在类外初始化
int MyClass::count = 0; // 静态成员变量
void MyClass::show() {
    cout << "count = " << count << endl;
} // 静态成员函数
```

## 对象数组

### 对象数组的定义
>
> 类名 数组名 [元素个数];

### 对象数组的初始化
>
> 1. 如没有显式调用任何构造函数初始化数组，对象数组将会自动调用默认构造函数
> 2. 可以用构造函数来初始化数组元素，可以只对部分元素显式调用构造函数，未显式调用构造函数的元素会自动调用默认构造函数
> 3. 初始化对象数组的方案实际上是：首先用默认构造函数创建数组元素，然后花括号中的构造函数创建临时对象，然后将临时对象的内容复制到对应的元素中。因此，要创建类对象数组，则该类必须有默认构造函数。

## 类作用域

### 作用域为类的常量
>
> 1. 在类中声明一个枚举，该枚举只是为了创建一个符号常量，不创建枚举变量，不用提供枚举名，任何对象也不会包含这个枚举
> 2. 使用关键字static和const创建一个const类型的静态类成员

### 作用域内枚举（C++11）
>
> C++11提供了一种作用域为类的新枚举

```cpp
enum class egg {...};//struct可以替换class
enum class nood {...};
egg varible1 = egg::con_var;//con_var是一个枚举常量
nood varible2 = nood::con_var;
```

> 作用域内枚举不可以隐式地转化为整型，提高了类型安全，如有需要，可以显式转化

#### 作用域内枚举的底层整数类型
>
> 默认为int
> 提供了一种语法可用于不同的选择

```cpp
enum class : short pizza {...};//: short将底层类型指定为short
```

## 抽象数据类型（ADT）
>
> OOP非常适合用于描述ADT方法，公有函数接口提供了ADT描述的服务，类的私有部分和类方法的代码提供了实现，这些实现对类的客户隐藏
