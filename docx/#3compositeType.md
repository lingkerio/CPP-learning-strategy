## 数组（C++11特性）
1. 初始化数组可省略等号
2. 可以不在大括号内包含任何东西，这把所有元素置零
3. 列表初始化禁止缩窄转换
## cin的输入函数

1. cin.getline(destination,size)
   - 读取一整行的输入，最多读取size个字符，如果读到换行符，会读取换行符并抛弃它然后终止读取
   - destination必须是数组，该函数返回一个cin对象，故可以连续调用（具体参见代码）
   - 若是一行输入超过getline的最大读取数，无法读取的字符会被留在输入队列，并且getline会设置失效位，关闭后面的输入，但是cin.clear()可以恢复输入
2. cin.get(destination,size)
   - 读取一整行的输入，最多读取size个字符，如果读到换行符，不读取它并终止读取
   - 由于不读取换行符导致输入队列留下一个换行符，会阻拦接下来get函数的读取，故需要使用无参数的cin.get()函数读取走换行符，若是让带参数的cin.get()函数读取这个换行符，get读取空行后将设置失效位，这意味着阻断接下来的输入，但是cin.clear()可以恢复输入
   - 若是一行输入超过get的最大读取数，无法读取的字符会被留在输入队列，
   - destination必须是数组，该函数返回一个cin对象，故可以连续调用（具体参见代码）
```cpp
#include <iostream>
using namespace std;
int main()
{
    char mov[190] = "hello world";
    cin.getline(mov,25).getline(mov,25);
    cin.get(mov,25).get(mov,25);
    cin.get();
    cin.clear();
    return 0;
}
```
## 初识string类
string类位于std名称空间
### 初步

1. 可以使用C-风格字符串来初始化string对象
2. 可以使用cin来将键盘输入存储到string对象
3. 可以使用cout来显示string对象
4. 可以使用数组表示法来访问存储在string对象中的字符
### C++11字符串初始化
列表初始化被C++11允许用于C-风格字符串和string对象
```cpp
char first_date[] = {"hello"};
char second_date[] {"hello"};
string third_date = {"hello"};
string fourth_date {"hello"};
```
### string类的赋值、拼接和附加

1. string对象之间可以互相赋值，违背初始化的string对象长度自动置零
2. 运算符+可以将string对象与C-字符串或string对象拼接在一起
```cpp
string mov {"hello"};
string mev {"hello"};
char men[] {"hello"};
mov += mev;
mov += men;
```
### string类的其他操作

- string类具有自动调整大小的功能
- string类包含一个成员函数size，其返回值为string类对象包含的字符数
- 非istream的成员函数的getline函数可以做到对string类的行输入，getline(cin,string);
## 特殊字符串字面值种类

- 前缀L表示wchar_t类型字符串
- 前缀u表示char16_t类型字符串
- 前缀U表示char32_t类型字符串
- 前缀u8表示UTF-8类型字符串
- 前缀为R，以"+自定义+( 和 )+自定义+" 作为定位符的字符串是原始字符串，无需\来将特殊字符转义。前缀R可以与其他字符串前缀结合使用，以标识其他类型的原始字符串，结合顺序无要求
## 结构
### C++11结构初始化

1. 支持列表初始化
2. 大括号内未包含任何东西，则将所有结构成员置零
3. 不允许缩窄转换
### 结构属性

1. 允许将string类作为结构成员
2. 结构变量之间可以互相赋值，即成员赋值（memberwise assignment)
3. 可以同时完成定义结构和创建结构变量以及初始化结构变量的工作
4. 定义一种结构可以匿名，创建这种结构变量必须在定义时完成
5. C++结构可以有成员函数
6. C++结构使用时可以不加struct标记
```cpp
struct perks
{
	int key_number;
	char car[12];
} mr_glitz =
{
	7,
"Packard"
};

struct
{
	int x;
	int y;
} position;
```
### 结构数组初始化
初始化结构数组可以结合使用初始化数组和初始化结构的规则
```cpp
struct inflatable
{
	char name[20];
	float volume;
	double price;
};

inflatable gifts[200] =
{
    {"Bambi",0.5,21.99},
	{"Godzilla",2000,565.99}
}
```
### 结构中的位字段

1. 字段类型为整型或枚举
2. 可以使用没有名称的字段来提供间距
3. 通常用于低级编程，可以用整型和按位运算符代替



## 共用体

1. 共用体长度为最大成员的长度
2. 匿名共用体没有名称，其成员将成为位于相同地址处的变量，可以直接使用成员的名称访问成员
3. 共用体常用于（但并非只用于）节省内存，还常用于操作系统数据结构或硬件数据结构

## 枚举

1. enum 工具类似于struct创建结构来创建枚举
2. 枚举只定义了赋值运算符
3. 枚举量可以自动转换为整型，单证行不可以自动转换为枚举
### 设置枚举量的值

1. 若完全不显式设置，则默认为从0开始递增赋值
2. 若有显式设置，则其之后未被显式设置的变量从该值+1递增赋值
3. 可以创建多个值相同的枚举量
### 枚举的取值范围
上限为大于最大值的、最小的2的幂-1
下限为：当最小值不小于0，则为0；否则为小于这个最小值的、最大的负的2的幂
在这个取值范围内，可以将未在声明中出现的整型值通过强制类型转换赋给枚举

## 动态数组与自由存储空间
### new|delete 操作符

1. 为一个数据对象获取并分配内存：
2. 释放一个数据对象得自于new的内存:
3. delete后跟的指针只需要是指向new分配的内存的指针即可
```cpp
typeName* pointer_name = new typeName;
delete pointer_name;
```

4. 为一个动态数组获取并分配内存：
5. 释放一个动态数组得自于new的内存：
```cpp
type_name* pointer_name = new type_name [n];
delete [] pointer_name;
```

6. 不要使用delete释放不是new分配的内存
7. 不要使用delete释放同一个内存块两次
8. 对空指针应用delete是安全的
### 指针算术

1. 指针+1，值变为原值+指向类型所占的字节数，同时指针指向原内存位置的下一块内存
2. 数组名被解释为数组中第一个元素的地址
3. 可以修改指针的值，但数组名的值不可以修改
4. 对数组名使用sizeof得到的是数组的长度，对指针使用sizeof得到的是指针的长度
5. 创建指向数组的指针：
```cpp
type_name (*pointer_name)[number];

//int ts[20];
//&ts被解释为数组ts的地址
//ts被解释为数组ts的第一个元素的地址
```
## 指针与字符串

1. char*类型的指针会被cout识别为字符串，从其所指的字节开始，一直输出到空字符
2. 用指针表示字符串时，应将指针设定为const以防止错误地通过指针修改了所指的字符串字面量，字符串字面量被视为常量，如果对其修改，在运行时会出现段错误或写入位置错误
3. 获取字符串字面量的可写的指针副本：
```cpp
char* str = new char[strlen("hello")+1];
strcpy(str,"hello");
```
## 动态结构

1. 声明想要的结构类型
2. 通过指针的方式和new操作符创建这个结构
3. 指针通过->或(*pointer_name)通过句点操作符访问结构成员
## 动态联编的优越性

- 当需要储存一千个字符串，最大的字符串长度为79
- 若使用静态联编，需要一千个长度为80的char数组，这一行为会浪费巨大的内存资源
- 若使用动态联编，可以创建一个包含一千个指向字符串的指针的数组，用new为每个字符串分配合适的空间，者能够节省巨大的内存资源，但是要记得程序结束前delete所有申请过的内存
## 存储类型

1. 自动存储：在函数内部定义的变量，作用域为包含它的代码块，储存在栈中
2. 静态存储：两种方式使得变量成为静态，一是在函数外面定义变量，二是在声明变量时使用关键字static，存在于程序的整个生命周期
3. 动态存储：new和delete运算符提供。存在于自由存储空间，堆。数据的生命周期不完全受程序或函数的生存时间控制。但占用的堆区的内存可能不连续。
4. 堆区的内存空间被分配后没有得到释放会造成内存泄露。
## 数组替代品
### 模板类vector

1. 这是一种动态数组
2. 它会自动调用new和delete管理内存
3. 使用它需要头文件vector，以及vector包含在名称空间std中
4. 声明一个vector对象：
```cpp
vector<typeName> vt(n_elem);
//n_elem表明存储几个元素，它可以是整型常量，也可以是整型变量
//可以使用列表初始化
```
### 模板类array（C++）

1. array对象的长度是固定的，存储在栈中
2. 效率和数组一样 更方便、安全
3. 使用它需要头文件array，以及array包含在名称空间std中
4. 声明一个array对象：
5. 可以将array对象赋给另一个array对象
```cpp
array<typeName, n_elem> arr;
//n_elem不能是变量
//可以使用列表初始化
```
### 数组、vector、array的对比

1. 数组和array对象都存储在栈中，vector存储在堆中
2. 数组、vector、array都可以使用 [索引] 的方式访问元素，但是索引可以向下越界，即为负数，编译器不检查这种错误
3. vector和array的成员函数at()可以捕获非法索引，程序将默认中断，额外检查的代价是运行时间变长
4. vector和array包含成员函数begin()和end()，以此可以确定数组边界








## 